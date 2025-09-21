# ApexPlanet_Task5
#html file
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chinni's All-in-One Web Project</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Header -->
    <header>
        <h1>Chinni's Web Project</h1>
        <nav>
            <a href="#about">About</a>
            <a href="#todo">To-Do</a>
            <a href="#interactive">Interactive</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <!-- About Section -->
    <section id="about">
        <h2>About Me</h2>
        <p>Hello! I'm Chinni, a B.Tech CSE student passionate about Web Development.</p>
        <img src="images/profile.jpg" alt="My Photo" loading="lazy">
    </section>

    <!-- To-Do Section -->
    <section id="todo">
        <h2>To-Do List</h2>
        <input type="text" id="taskInput" placeholder="Enter a task">
        <button onclick="addTask()">Add Task</button>
        <ul id="taskList"></ul>
    </section>

    <!-- Interactive Section (API Example) -->
    <section id="interactive">
        <h2>Joke Generator</h2>
        <button onclick="getJoke()">Get a Joke</button>
        <p id="joke"></p>
    </section>

    <!-- Contact Form Section -->
    <section id="contact">
        <h2>Contact Me</h2>
        <form id="contactForm">
            <input type="text" id="name" placeholder="Name" required>
            <input type="email" id="email" placeholder="Email" required>
            <textarea id="message" placeholder="Message" required></textarea>
            <button type="submit">Send</button>
        </form>
    </section>

    <!-- Footer -->
    <footer>
        <p>© 2025 Chinni. All rights reserved.</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>

#css file
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

header {
    background-color: #333;
    color: white;
    text-align: center;
    padding: 15px 0;
}

nav a {
    color: white;
    margin: 0 15px;
    text-decoration: none;
}

section {
    padding: 40px 20px;
    max-width: 900px;
    margin: auto;
}

section img {
    max-width: 200px;
    border-radius: 50%;
}

#todo input {
    padding: 10px;
    width: 70%;
    margin-right: 10px;
}

#todo button {
    padding: 10px 20px;
}

ul#taskList {
    list-style-type: disc;
    margin-top: 20px;
}

form input, form textarea {
    display: block;
    width: 100%;
    margin: 10px 0;
    padding: 10px;
}

form button {
    padding: 10px 20px;
    cursor: pointer;
}

footer {
    text-align: center;
    background-color: #333;
    color: white;
    padding: 15px 0;
    margin-top: 20px;
}

/* Responsive */
@media(max-width: 768px){
    nav {
        display: flex;
        flex-direction: column;
    }
    #todo input {
        width: 100%;
        margin-bottom: 10px;
    }
}

#js file
// Contact Form Validation
document.getElementById("contactForm").addEventListener("submit", function(e){
    e.preventDefault();
    let name = document.getElementById("name").value;
    let email = document.getElementById("email").value;
    let message = document.getElementById("message").value;

    if(name && email && message){
        alert("Thank you, " + name + "! Your message has been sent.");
        document.getElementById("contactForm").reset();
    } else {
        alert("Please fill all fields.");
    }
});

// To-Do App
let taskList = JSON.parse(localStorage.getItem("tasks")) || [];
const ul = document.getElementById("taskList");

function renderTasks(){
    ul.innerHTML = "";
    taskList.forEach((task, index)=>{
        let li = document.createElement("li");
        li.textContent = task;
        li.onclick = ()=>{ removeTask(index) };
        ul.appendChild(li);
    });
}
function addTask(){
    let taskInput = document.getElementById("taskInput");
    if(taskInput.value.trim() !== ""){
        taskList.push(taskInput.value.trim());
        localStorage.setItem("tasks", JSON.stringify(taskList));
        taskInput.value = "";
        renderTasks();
    }
}
function removeTask(index){
    taskList.splice(index, 1);
    localStorage.setItem("tasks", JSON.stringify(taskList));
    renderTasks();
}
renderTasks();

// Joke API Example
function getJoke(){
    fetch('https://api.chucknorris.io/jokes/random')
    .then(res => res.json())
    .then(data => {
        document.getElementById("joke").innerText = data.value;
    })
    .catch(err => console.error(err));
}
