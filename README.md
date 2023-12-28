# Responsive-Calculator
<!DOCTYPE html>
<html>
<head>
<title> Resposive Web Calculator</title>
<link rel = "stylesheet" href = "style.css"/> 

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,400;1,500;1,600;1,700&family=Montserrat+Alternates:ital,wght@0,500;0,600;0,800;0,900;1,500;1,600;1,700;1,800&family=Poppins:wght@700&display=swap" rel="stylesheet">
<script src = "app.js"> </script>
<meta name="viewport" content="width=device-width, initial-scale=1.0">




</head>



<body>
<section class = "calcContainer">
    <div class = "display">
        <h1>0</h1>
    </div>
    <div class = "btnContainer"></div>

    <div class = "btnRow smRow">
        <button onclick = "handleInteraction()" class = "btn"><p>(</p></button>
        <button onclick = "handleInteraction()" class = "btn"><p>)</p></button>
        <button onclick = "handleInteraction('%')" class = "btn"><p>%</p></button>
        <button onclick = "handleReset()" class = "btn"><p>AC</p></button>
         </div>
    

     <div class = "btnRow">
        <button onclick = "handleInteraction(7)" class = "btn">7</button>
        <button onclick = "handleInteraction(8)" class= "btn">8</button>
        <button onclick = "handleInteraction(9)" class = "btn">9</button>
        <button onclick = "handleInteraction('/')" class = "btn">/</button>
         </div>

         
    <div class = "btnRow">
    <button  onlick  = "handleInteraction(4)" class  = "btn">4</button>
     <button onlick  = "handleInteraction(5)" class  = "btn">5</button>
    <button  onlick  = "handleInteraction(6)" class  = "btn">6</button>
    <button  onlick  = "handleInteraction('*')" class  = "btn">*</button>
     </div>

     <div class = "btnRow">
        <button onlick = "handleInteraction(1)" class = "btn">1</button>
        <button onlick = "handleInteraction(2)" class = "btn">2</button>
        <button onlick = "handleInteraction(3)" class = "btn">3</button>
        <button onlick = "handleInteraction('-')" class = "btn">-</button>
         </div>

    <div class = "btnRow">
    <button  onlick = "handleInteraction(8)"class = "btn">8</button>
    <button  onlick = "handleInteraction('.')"class = "btn">.</button>
    <button  onlick = "handleEvaluate()"class = "btn">=</button>
     <button onlick = "handleInteraction('+')"class = "btn">+</button>
    </div>

    <style>
        *{
  margin: 0;
  padding:0;
  box-sizing: border-box;
  font-family:'Jetbrains Mono',monospace;
  user-select: none;
}

body{
  background: var(--bg-color);
  color:var(--text-color);
  padding:14px;
  background:lightblue;
  min-height: 100vh;
  display:flex;
  flex-direction: column;

}

:root{
  --bg-color: black;
  --text-color:#c5cbed;
  --background-light: black;
  --accent-color:lightblue;

  
}
.calcContainer{
  background:white;
  flex:1;
  border-radius:14px;
  padding:14px;
  display:flex;
  flex-direction:column;
  gap:14px;

}

.display{
  background-color: var(--bg-light);
  padding:14px;
  border-radius: 8px;
  border:2px solid var(--text-color);
  flex:1;
  display:flex;
  align-items: center;
  justify-content: end;
  font-size: 1.6em;
  line-height: 1rem;

}

.display h1{
 white-space:nowrap;
 text-align:end;
 font-family:'Montserrat', sans-serif;
 font-weight: bold;
}

.btnContainer{
  display:flex;
  flex-direction:column;
  gap:14px;
  flex:8;
  
}

.btnRow{
  display:grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap:14px;
  flex:5;


}

.smRow{
  flex: 4!important;

}

  .smRow > button:nth-child(1),
  .smRow > button:nth-child(2){
    background:white;
    color:black;
  }

  .btn{
    background-color: var(--bg-color);
    color: var(--text-color);
    border: 7px solid(--text--color);
    border-radius:8px;
    diplay:grid;
    place-items: center;
    cursor:pointer;
    transition-duration: 200ms;

  }


  .btn:hover{
    opacity:0.8;
  }

  .btn p{
    font-size:1.2rem;

  }

  .btnRow:last-child > .btn:nth-child(3) {
    border-color: var(--bg-color);
    background: white;

    @media (max-width: 600px) {
  .btn {
    font-size: 1em;
  }
}
}

<script>

const displayInput = document.getElementById('inputValue');

// Variables
const operators = ['-', '+', '%', '*', '/'];
let operations = [];
let currValue = '';

// Functions and Operations

function handleInteraction(value) {
  if (operators.includes(value)) {
    console.log('Clicked an operator:', value);
    handleOperatorInput(value);
  } else {
    console.log('Clicked a numeric value', value);
    handleNumericInput(value);
  }
  updateUI();
}

function handleNumericInput(value) {
  if(value === '.' && currValue.includes('.') {return})
  currValue += value;
  console.log('NEW VALUE:', currValue);
}

function handleOperatorInput(value) {
  if (!currValue) {
    return;
  }

  operations.push(currValue);
  operations.push(value);
  currValue = '';
}

function handleEvaluate() {
  if (operations.length === 0) {
    return;
  }

  let finalAmount = parseFloat(operations[0]); // Convert to a number
  let prevOperator = null;

  if (!currValue) {
    operations.pop();
  } else {
    operations.push(currValue);
    currValue = '';
  }

  for (let i = 1; i < operations.length; i += 2) {
    const operator = operations[i];
    const operand = parseFloat(operations[i + 1]);

    switch (operator) {
      case '+':
        finalAmount += operand;
        break;
      case '-':
        finalAmount -= operand;
        break;
      case '*':
        finalAmount *= operand;
        break;
      case '/':
        finalAmount /= operand;
        break;
      case '%':
        finalAmount %= operand;
        break;
      default:
        break;
    }
  }

  operations = [];
  currValue = finalAmount.toString(); // Convert back to a string
  updateUI();
}

function handleReset() {
  currValue = '';
  operations = [];
  updateUI();
}

function updateUI() {
  console.log(operations);
  const displayString = operations.join('');
  displayInput.innerText = displayString.trim() ? displayString : '0';
}





</script>






        </style>
        
