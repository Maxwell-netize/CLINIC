<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Doctor's Dashboard</title>
    <link rel="stylesheet" href="styles.css">
    <form method="post" action='symtops.html'></form>
</head>
<body>
    <header>
        <h1>Doctor's Dashboard</h1>
        <nav>
            <ul>
                <li><a href="#patient-info">Patient Information</a></li>
                <li><a href="#appointments">Appointments</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <section id="patient-info">
            <h2>Patient Information</h2>
            <form id="patient-form">
                <label for="patient-name">Patient Name:</label>
                <input type="text" id="patient-name" placeholder="Enter patient's name" required>

                <label for="patient-age">Age:</label>
                <input type="number" id="patient-age" placeholder="Enter patient's age" min="0" required>

                <label for="patient-condition">Condition:</label>
                <textarea id="patient-condition" placeholder="Describe the patient's condition" rows="4" required></textarea>

                <button type=submit>Submit Patient Info</button>
                <form method="post" action=''></form>
            </form>
        </section>

        <section id="appointments">
            <h2>Appointments</h2>
            <form id="appointment-form">
                <label for="appointment-date">Date:</label>
                <input type="date" id="appointment-date" required>

                <label for="appointment-time">Time:</label>
                <input type="time" id="appointment-time" required>

                <label for="appointment-patient">Patient Name:</label>
                <input type="text" id="appointment-patient" placeholder="Enter patient's name" required>

                <button type="submit">Schedule Appointment</button>
            </form>
        </section>

        <section id="contact">
            <h2>Contact</h2>
            <form id="contact-form">
                <label for="contact-name">Your Name:</label>
                <input type="text" id="contact-name" placeholder="Enter your name" required>

                <label for="contact-email">Your Email:</label>
                <input type="email" id="contact-email" placeholder="Enter your email" required>

                <label for="contact-message">Message:</label>
                <textarea id="contact-message" placeholder="Enter your message" rows="4" required></textarea>

                <button type="submit">Send Message</button>
            </form>
        </section>
    </main>

    <footer>
        <p>&copy; GCTU Hospital Management System. All rights reserved.</p>
    </footer>
</body>
</html>
//JS.js
 express = require('express');
const constbodyParser = require('body-parser');
const fs = require('fs');
const path = require('path');

const app = express();
const PORT = 3000;

// Middleware
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(express.static('public')); // Serve static files from the 'public' directory

// Endpoint to save patient info
app.post('/submit-patient-info', (req, res) => {
    const patientInfo = req.body;
    const data = `Patient Name: ${patientInfo.name}, Age: ${patientInfo.age}, Condition: ${patientInfo.condition}\n`;
    fs.appendFile(path.join(__dirname, 'data.txt'), data, (err) => {
        if (err) {
            return res.status(500).send('Error saving patient info');
        }
        res.send('Patient info saved successfully!');
    });
});

// Endpoint to save appointment
app.post('/schedule-appointment', (req, res) => {
    const appointmentInfo = req.body;
    const data = `Appointment - Patient Name: ${appointmentInfo.patientName}, Date: ${appointmentInfo.date}, Time: ${appointmentInfo.time}\n`;
    fs.appendFile(path.join(__dirname, 'data.txt'), data, (err) => {
        if (err) {
            return res.status(500).send('Error scheduling appointment');
        }
        res.send('Appointment scheduled successfully!');
    });
});

// Endpoint to send message
app.post('/send-message', (req, res) => {
    const messageInfo = req.body;
    const data = `Message from ${messageInfo.name} (${messageInfo.email}): ${messageInfo.message}\n`;
    fs.appendFile(path.join(__dirname, 'data.txt'), data, (err) => {
        if (err) {
            return res.status(500).send('Error sending message');
        }
        res.send('Message sent successfully!');
    });
});

// Endpoint to save the HTML dashboard
app.post('/save-dashboard', (req, res) => {
    const htmlContent = req.body.htmlContent;
    const filePath = 'C:\\Users\\BOXO_MAX\\Desktop\\GCTU.HTML\\mmm.html'; // Specify the path

    fs.writeFile(filePath, htmlContent, (err) => {
        if (err) {
            return res.status(500).send('Error saving dashboard');
        }
        res.send('Dashboard saved successfully!');
    });
});

// Start the server
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});


body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin
