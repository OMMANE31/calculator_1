# calculator_1
import React, { Component } from 'react';
import './styles.css';
class Calculator extends Component {
constructor(props) {
super(props);
this.state = {
displayValue: '0',
operator: null,
prevValue: null,
waitingForOperand: false,
};
}
inputDigit = (digit) => {
const { displayValue, waitingForOperand } = this.state;
if (waitingForOperand) {
this.setState({
displayValue: String(digit),
waitingForOperand: false,
});
} else {
this.setState({
displayValue: displayValue === '0' ? String(digit) :

displayValue + digit,
});
}
};

inputDecimal = () => {
const { displayValue, waitingForOperand } = this.state;
if (waitingForOperand) {
this.setState({
displayValue: '0.',
waitingForOperand: false,

});
} else if (displayValue.indexOf('.') === -1) {
this.setState({
displayValue: displayValue + '.',
waitingForOperand: false,
});
}
};
clearDisplay = () => {
this.setState({
displayValue: '0',
});
};
handleOperator = (nextOperator) => {
const { displayValue, operator, prevValue } = this.state;
const inputValue = parseFloat(displayValue);
if (prevValue == null) {
this.setState({
prevValue: inputValue,
waitingForOperand: true,
operator: nextOperator,
});
} else if (operator) {
const result = this.calculate(prevValue, inputValue,
operator);
this.setState({
displayValue: String(result),
prevValue: result,
waitingForOperand: true,
operator: nextOperator,
});
}
};

calculate = (prevValue, nextValue, operator) => {
switch (operator) {
case '+':
return prevValue + nextValue;
case '-':
return prevValue - nextValue;
case '*':
return prevValue * nextValue;
case '/':
return prevValue / nextValue;
default:
return nextValue;
}
};
render() {
const { displayValue } = this.state;
return (
<div className="calculator">
<div className="display">{displayValue}</div>
<div className="keypad">
<button onClick={() => this.clearDisplay()}>C</button>
<button onClick={() => this.inputDigit(7)}>7</button>
<button onClick={() => this.inputDigit(8)}>8</button>
<button onClick={() => this.inputDigit(9)}>9</button>
<button onClick={() =>
this.handleOperator('+')}>+</button>

<button onClick={() => this.inputDigit(4)}>4</button>
<button onClick={() => this.inputDigit(5)}>5</button>
<button onClick={() => this.inputDigit(6)}>6</button>
<button onClick={() => this.handleOperator('-')}>-

</button>

<button onClick={() => this.inputDigit(1)}>1</button>
<button onClick={() => this.inputDigit(2)}>2</button>
<button onClick={() => this.inputDigit(3)}>3</button>
<button onClick={() =>
this.handleOperator('*')}>*</button>

.calculator {
width: 250px;
margin: 0 auto;
padding: 20px;
background-color: #f4f4f4;
border: 2px solid #ccc;
border-radius: 5px;
box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

.display {
font-size: 24px;
text-align: right;
margin-bottom: 10px;
padding: 5px;
background-color: #fff;
border: 1px solid #ccc;
border-radius: 3px;
}

.keypad button {
width: 50px;
CSS CODE FOR THE ABOVE

<button onClick={() => this.inputDigit(0)}>0</button>
<button onClick={() => this.inputDecimal()}>.</button>
<button onClick={() =>
this.handleOperator('/')}>/</button>
<button onClick={() =>
this.handleOperator('=')}>=</button>

</div>
</div>
);
}
}
export default Calculator;

height: 50px;
font-size: 20px;
margin: 2px;
padding: 0;
border: 1px solid #ccc;
border-radius: 3px;
background-color: #fff;
cursor: pointer;
}
.keypad button:hover {
background-color: #e0e0e0;
}
