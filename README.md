<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PhotoSell - Sell Your Photos Online</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <div class="logo">PhotoSell</div>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#gallery">Gallery</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <section id="home" class="hero">
        <h1>Welcome to PhotoSell</h1>
        <p>Your destination for high-quality photos</p>
        <a href="#gallery" class="btn">Explore Gallery</a>
    </section>

    <section id="gallery" class="gallery">
        <h2>Gallery</h2>
        <div class="photo-grid">
            <div class="photo-item">
                <img src="photo1.jpg" alt="Photo 1">
                <p>Photo 1 - $20</p>
                <button class="btn">Buy Now</button>
            </div>
            <div class="photo-item">
                <img src="photo2.jpg" alt="Photo 2">
                <p>Photo 2 - $25</p>
                <button class="btn">Buy Now</button>
            </div>
            <!-- Add more photo items here -->
        </div>
    </section>

    <section id="about" class="about">
        <h2>About Us</h2>
        <p>We are a team of passionate photographers dedicated to bringing you the best photos from around the world.</p>
    </section>

    <section id="contact" class="contact">
        <h2>Contact Us</h2>
        <form>
            <input type="text" placeholder="Your Name" required>
            <input type="email" placeholder="Your Email" required>
            <textarea placeholder="Your Message" required></textarea>
            <button type="submit" class="btn">Send Message</button>
        </form>
    </section>

    <footer>
        <p>&copy; 2023 PhotoSell. All rights reserved.</p>
    </footer>

    <script src="scripts.js"></script>
</body>
</html>

/* styles.css */
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background-color: #333;
    color: #fff;
}

header .logo {
    font-size: 1.5rem;
    font-weight: bold;
}

header nav ul {
    list-style: none;
    display: flex;
    gap: 1rem;
}

header nav ul li a {
    color: #fff;
    text-decoration: none;
}

.hero {
    background: url('hero-bg.jpg') no-repeat center center/cover;
    color: #fff;
    text-align: center;
    padding: 5rem 1rem;
}

.hero h1 {
    font-size: 3rem;
}

.hero p {
    font-size: 1.5rem;
}

.btn {
    background-color: #ff6f61;
    color: #fff;
    padding: 0.5rem 1rem;
    text-decoration: none;
    border-radius: 5px;
    display: inline-block;
    margin-top: 1rem;
}

.gallery {
    padding: 2rem;
    text-align: center;
}

.photo-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
}

.photo-item {
    border: 1px solid #ddd;
    padding: 1rem;
    border-radius: 5px;
}

.photo-item img {
    max-width: 100%;
    border-radius: 5px;
}

.about, .contact {
    padding: 2rem;
    text-align: center;
}

.contact form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 400px;
    margin: 0 auto;
}

.contact form input, .contact form textarea {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 5px;
}

footer {
    background-color: #333;
    color: #fff;
    text-align: center;
    padding: 1rem;
    margin-top: 2rem;
}

// scripts.js
document.addEventListener('DOMContentLoaded', function() {
    const buyButtons = document.querySelectorAll('.photo-item .btn');
    
    buyButtons.forEach(button => {
        button.addEventListener('click', function() {
            alert('Thank you for your purchase!');
        });
    });
});

// server.js
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const port = 3000;

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.get('/', (req, res) => {
    res.sendFile(__dirname + '/index.html');
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});

// Install Stripe package: npm install stripe
const stripe = require('stripe')('your_stripe_secret_key');

app.post('/create-payment-intent', async (req, res) => {
    const { amount } = req.body;

    const paymentIntent = await stripe.paymentIntents.create({
        amount,
        currency: 'usd',
    });

    res.send({
        clientSecret: paymentIntent.client_secret,
    });
});
