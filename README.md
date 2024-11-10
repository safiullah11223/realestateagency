<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Real Estate Agency</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Navigation -->
  <nav>
    <h1>Real Estate Agency</h1>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#properties">Properties</a></li>
      <li><a href="#mortgage">Mortgage Calculator</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- Home Section -->
  <section id="home">
    <h2>Welcome to Our Real Estate Agency</h2>
    <p>Your dream home is just a click away!</p>
  </section>

  <!-- Properties Section -->
  <section id="properties">
    <h2>Available Properties</h2>
    <div class="property-card">
      <img src="property1.jpg" alt="Property 1">
      <p>Modern Apartment in City Center</p>
    </div>
    <div class="property-card">
      <img src="property2.jpg" alt="Property 2">
      <p>Spacious Family Home in Suburbs</p>
    </div>
  </section>

  <!-- Mortgage Calculator -->
  <section id="mortgage">
    <h2>Mortgage Calculator</h2>
    <form id="mortgage-form">
      <label for="loanAmount">Loan Amount:</label>
      <input type="number" id="loanAmount" required>
      <label for="interestRate">Interest Rate (%):</label>
      <input type="number" id="interestRate" step="0.01" required>
      <label for="loanTerm">Loan Term (Years):</label>
      <input type="number" id="loanTerm" required>
      <button type="button" onclick="calculateMortgage()">Calculate</button>
    </form>
    <p id="mortgageResult"></p>
  </section>

  <!-- Contact Form -->
  <section id="contact">
    <h2>Contact Us</h2>
    <form id="contact-form">
      <label for="name">Name:</label>
      <input type="text" id="name" required>
      <label for="email">Email:</label>
      <input type="email" id="email" required>
      <label for="message">Message:</label>
      <textarea id="message" required></textarea>
      <button type="submit">Send Message</button>
    </form>
  </section>

  <script src="script.js"></script>
</body>
</html>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

nav {
  display: flex;
  justify-content: space-between;
  padding: 1rem;
  background-color: #333;
  color: #fff;
}

nav ul {
  list-style: none;
  display: flex;
}

nav ul li {
  margin: 0 10px;
}

nav ul li a {
  color: #fff;
  text-decoration: none;
}

section {
  padding: 2rem;
}

.property-card {
  display: inline-block;
  margin: 1rem;
  text-align: center;
}

.property-card img {
  width: 100%;
  max-width: 300px;
}

#mortgage-form, #contact-form {
  max-width: 400px;
  margin: 1rem auto;
}

button {
  padding: 0.5rem 1rem;
  cursor: pointer;
}

#mortgageResult {
  font-size: 1.2rem;
  margin-top: 1rem;
}

/* Animations */
.property-card, #mortgage-form, #contact-form {
  opacity: 0;
  transition: opacity 1s ease-out;
}

.property-card.show, #mortgage-form.show, #contact-form.show {
  opacity: 1;
}

// Scroll animations
const elements = document.querySelectorAll('.property-card, #mortgage-form, #contact-form');
window.addEventListener('scroll', () => {
  elements.forEach(element => {
    const position = element.getBoundingClientRect().top;
    const windowHeight = window.innerHeight;
    if (position < windowHeight - 100) {
      element.classList.add('show');
    }
  });
});

// Mortgage Calculator
function calculateMortgage() {
  const loanAmount = parseFloat(document.getElementById('loanAmount').value);
  const interestRate = parseFloat(document.getElementById('interestRate').value) / 100 / 12;
  const loanTerm = parseFloat(document.getElementById('loanTerm').value) * 12;
  const mortgageResult = document.getElementById('mortgageResult');

  if (loanAmount && interestRate && loanTerm) {
    const monthlyPayment = (loanAmount * interestRate) / (1 - Math.pow(1 + interestRate, -loanTerm));
    mortgageResult.textContent = `Estimated Monthly Payment: $${monthlyPayment.toFixed(2)}`;
  } else {
    mortgageResult.textContent = "Please enter all fields.";
  }
}

// Contact Form Submission (using EmailJS for example)
document.getElementById('contact-form').addEventListener('submit', function(event) {
  event.preventDefault();
  // Integrate with EmailJS or other email service
  alert('Message sent! Thank you for contacting us.');
});
