# todo-list-app
I made created little to do list 
HTML 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To do list</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="todo-app">
            <h2>To-Do list<img src="images/icon.png" alt=""></h2> 
            <div class="row">
                <input type="text" id="input-box" placeholder="hedefini yaz">
                <button onclick="AddTask()">Add</button>
            </div> 
            <ul id="list-container">
               <!-- <li class="checked">task 1</li>
                <li>task 2</li>
                <li>task 3</li> -->
            </ul>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
CSS
*{
    margin: 0;
    padding: 0;
    font-family: 'Poppins',sans-serif;
    box-sizing: border-box;
}
.container{
    width: 100%;
    min-height: 100vh;
    background: linear-gradient(135deg, #ac5f92,#1f1561);
    padding: 10px;
}
.todo-app{
    width: 100%;
    max-width: 540px;
    background: #fff;
    margin: 100px auto 20px;
    padding: 40px 30px 70px;
    border-radius: 10px;
}
.todo-app h2{
    color:#1f5461;
    display:flex;
    align-items: center;
    margin-bottom: 20px;
}
.todo-app h2 img{
    width: 30px;
    margin-left: 10px;
}
.row{
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #c7b4c1;
    border-radius: 30px;
    padding-left: 20px;
    margin-bottom: 25px;
}
input{
    flex: 1;
    border: none;
    outline: none;
    background: transparent;
    padding: 10px;
    font-weight: 14px;
}
button{
    border: none;
    outline: none;
    padding: 16px 50px;
    background: #ac5f92;
    color:#fff;
    font-size: 16px;
    cursor: pointer;
    border-radius: 40px;
}
ul li{
    list-style: none;
    font-size: 17px;
    padding: 12px 8px 12px 50px;
    user-select: none;
    cursor: pointer;
    position: relative;
}
ul li::before{
    content: '';
    position: absolute;
    height: 28px;
    width:28px;
    border-radius: 50%;
    background-image: url(images/unchecked.png);
    background-size: cover;
    background-position: center;
    top: 12px;
    left: 8px;
}
ul li.checked{
    color: #555;
    text-decoration: line-through;
}
ul li.checked::before{
    background-image: url(images/checked.png);
}
ul li span {
    position: absolute;
    right: 0;
    top:5px;
    width: 40px;
    height: 40px;
    font-size: 22px;
    color: #555;
    line-height: 40px;
    text-align: center;
    border-radius: 50%;
}
ul li span:hover{
    background: #1f1561;
}
part of JavaScript
const inputBox = document.getElementById("input-box");
const listContainer = document.getElementById("list-container");
function AddTask(){
    if(inputBox.value === ''){
        alert("bir şeyler yazmalısınız");
    }
    else{
        let li = document.createElement("li");
        li.innerHTML = inputBox.value;
        listContainer.appendChild(li);
        let span = document.createElement(span);
        span.innerHTML = "\u00d7";
        li.appendChild(span);
    }
    inputBox.value = "";
    saveData();

}

listContainer.addEventListener("click",function(e){
    if(e.target.tagName === "LI"){
        e.target.classList.toggle("checked");
        saveData();
    }
    else if(e.target.tagName === "SPAN"){
        e.target.parentElement.remove();
    }

},false);

function saveData(){
    localStorage.setItem("data",listContainer.innerHTML);
}
function showTask(){
    listContainer.innerHTML = localStorage.getItem("data");
}
showTask();
