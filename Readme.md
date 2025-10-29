# Ex06 BMI Calculator
## Date:29.10.2025

## AIM
To create a BMI calculator using React Router 

## ALGORITHM
### STEP 1 State Initialization
Manage the current page (Home or Calculator) using React Router.

### STEP 2 User Input
Accept weight and height inputs from the user.

### STEP 3 BMI Calculation
Calculate the BMI based on user input.

### STEP 4 Categorization
Classify the BMI result into categories (Underweight, Normal weight, Overweight, Obesity).

### STEP 5 Navigation
Navigate between pages using React Router.

## PROGRAM

### App.jsx
```
import React from "react";
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import Home from "./components/Home";
import Calculator from "./components/Calculator";

export default function App() {
  return (
    <BrowserRouter>
      <div className="app">
        <h1 className="title">BMI Calculator</h1>

        <nav className="nav">
          <Link to="/" className="link">Home</Link>
          <Link to="/calculator" className="link">Calculator</Link>
        </nav>

        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/calculator" element={<Calculator />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

```

### Home.jsx
```
import React from "react";
import { Link } from "react-router-dom";

export default function Home() {
  return (
    <div className="page">
      <h2>Welcome!</h2>
      <p>This app helps you calculate your Body Mass Index (BMI) easily.</p>
      <p>
        Click below to go to the calculator page and find your BMI.
      </p>
      <Link to="/calculator" className="button">Go to Calculator</Link>
    </div>
  );
}

```

### Calculator.jsx

```
import { useState } from "react";

export default function Calculator() {
  const [weight, setWeight] = useState("");
  const [height, setHeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");

  const calculateBMI = () => {
    if (!weight || !height) {
      alert("Please enter valid weight and height");
      return;
    }

    const bmiValue = (weight / (height * height)).toFixed(2);
    setBmi(bmiValue);

    if (bmiValue < 18.5) setCategory("Underweight");
    else if (bmiValue < 25) setCategory("Normal weight");
    else if (bmiValue < 30) setCategory("Overweight");
    else setCategory("Obesity");
  };

  return (
    <div className="page">
      <h2>BMI Calculator</h2>

      <input
        type="number"
        placeholder="Weight (kg)"
        value={weight}
        onChange={(e) => setWeight(e.target.value)}
        className="input"
      />
      <input
        type="number"
        placeholder="Height (m)"
        value={height}
        onChange={(e) => setHeight(e.target.value)}
        className="input"
      />

      <button onClick={calculateBMI} className="btn">Calculate</button>

      {bmi && (
        <div className="result">
          <h3>Your BMI: {bmi}</h3>
          <h4>Category: {category}</h4>
        </div>
      )}
    </div>
  );
}

```

### index.css
```
/* 🌑 Dark Modern Theme */

body {
  margin: 0;
  font-family: "Poppins", sans-serif;
  background: radial-gradient(circle at top, #0f172a, #000);
  color: #f1f5f9;
  text-align: center;
  min-height: 100vh;
}

.app {
  padding: 30px;
}

.title {
  font-size: 2.2rem;
  font-weight: 700;
  color: #38bdf8;
  text-shadow: 0 0 10px rgba(56, 189, 248, 0.5);
  margin-bottom: 20px;
}

/* Navigation Bar */
.nav {
  margin-bottom: 40px;
  display: flex;
  justify-content: center;
  gap: 20px;
}

.link {
  color: #94a3b8;
  font-weight: 500;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 8px;
  transition: all 0.3s ease;
  border: 1px solid transparent;
}

.link:hover {
  color: #38bdf8;
  border-color: #38bdf8;
  background-color: rgba(56, 189, 248, 0.1);
  box-shadow: 0 0 10px rgba(56, 189, 248, 0.3);
}

/* Card Container */
.page {
  max-width: 420px;
  margin: 0 auto;
  background: rgba(30, 41, 59, 0.75);
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 4px 25px rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(148, 163, 184, 0.2);
}

.form {
  display: flex;
  flex-direction: column;
  gap: 18px;
  text-align: left;
}

/* Inputs */
label {
  display: flex;
  flex-direction: column;
  font-size: 14px;
  font-weight: 500;
  color: #cbd5e1;
}

input {
  padding: 10px;
  margin-top: 6px;
  border: 1px solid rgba(148, 163, 184, 0.3);
  border-radius: 8px;
  outline: none;
  font-size: 15px;
  color: #f1f5f9;
  background-color: rgba(51, 65, 85, 0.8);
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

input:focus {
  border-color: #38bdf8;
  box-shadow: 0 0 10px rgba(56, 189, 248, 0.3);
}

/* Buttons */
.btn-group {
  display: flex;
  justify-content: space-between;
  margin-top: 15px;
}

button {
  background-color: #38bdf8;
  color: #0f172a;
  border: none;
  padding: 10px 20px;
  border-radius: 10px;
  font-weight: 600;
  letter-spacing: 0.5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:hover {
  background-color: #0ea5e9;
  color: #fff;
  box-shadow: 0 0 12px rgba(56, 189, 248, 0.5);
}

/* Result Section */
.result {
  margin-top: 25px;
  background: rgba(56, 189, 248, 0.08);
  border-left: 4px solid #38bdf8;
  padding: 15px;
  border-radius: 10px;
  color: #f8fafc;
  animation: fadeIn 0.4s ease;
}

/* Buttons and Links (shared style for CTA) */
.button {
  background-color: #38bdf8;
  color: #0f172a;
  padding: 10px 22px;
  border-radius: 10px;
  text-decoration: none;
  font-weight: 600;
  transition: 0.3s;
  display: inline-block;
}

.button:hover {
  background-color: #0ea5e9;
  color: #fff;
  box-shadow: 0 0 15px rgba(56, 189, 248, 0.5);
}


@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

```
## OUTPUT
### Home page
<img width="1905" height="1094" alt="image" src="https://github.com/user-attachments/assets/d56c5865-89d4-4d2b-a565-87636264d9ce" />
### Calculator page
<img width="1914" height="1093" alt="image" src="https://github.com/user-attachments/assets/6e08415e-271f-4191-a391-5509ab813dbf" />


## RESULT
The program for creating BMI Calculator using React Router is executed successfully.
