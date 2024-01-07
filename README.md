/*Q1. Write a program to find all pairs of an integer array whose sum is equal to a given number?*/
function findPairsWithSum(arr, targetSum) {
    let pairs = [];

    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] + arr[j] === targetSum) {
                pairs.push([arr[i], arr[j]]);
            }
        }
    }

    return pairs;
}

// Example usage:
let arrayQ1 = [1, 2, 3, 4, 5, 6];
let targetSumQ1 = 7;
let resultQ1 = findPairsWithSum(arrayQ1, targetSumQ1);
console.log(resultQ1);



/*Q2. Write a program to reverse an array in place? In place means you cannot create a new array. You have to update the original array.*/
function reverseArrayInPlace(arr) {
    let start = 0;
    let end = arr.length - 1;

    while (start < end) {
        // Swap elements at start and end indices
        let temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;

        // Move towards the center
        start++;
        end--;
    }
}

// Example usage:
let arrayQ2 = [1, 2, 3, 4, 5];
reverseArrayInPlace(arrayQ2);
console.log(arrayQ2);


/*Q3. Write a program to check if two strings are a rotation of each other?*/
function areStringsRotations(str1, str2) {
    if (str1.length !== str2.length) {
        return false;
    }

    let concatenated = str1 + str1;
    return concatenated.includes(str2);
}

// Example usage:
let string1Q3 = "abcd";
let string2Q3 = "cdab";
let resultQ3 = areStringsRotations(string1Q3, string2Q3);
console.log(resultQ3);


/*Q4. Write a program to print the first non-repeated character from a string?*/
function firstNonRepeatedChar(str) {
    let charCount = {};

    for (let char of str) {
        charCount[char] = (charCount[char] || 0) + 1;
    }

    for (let char of str) {
        if (charCount[char] === 1) {
            return char;
        }
    }

    return null; // If there is no non-repeated character
}

// Example usage:
let inputStringQ4 = "aabbccde";
let resultQ4 = firstNonRepeatedChar(inputStringQ4);
console.log(resultQ4);


/*Q5. Read about the Tower of Hanoi algorithm. Write a program to implement it.*/
function towerOfHanoi(n, source, auxiliary, destination) {
    if (n === 1) {
        console.log(`Move disk 1 from ${source} to ${destination}`);
        return;
    }

    towerOfHanoi(n - 1, source, destination, auxiliary);
    console.log(`Move disk ${n} from ${source} to ${destination}`);
    towerOfHanoi(n - 1, auxiliary, source, destination);
}

// Example usage:
towerOfHanoi(3, 'A', 'B', 'C');


/*Q6. Read about infix, prefix, and postfix expressions. Write a program to convert postfix to prefix expression.*/
function postfixToPrefix(postfixExpression) {
    let stack = [];

    for (let token of postfixExpression) {
        if (/[a-zA-Z0-9]/.test(token)) {
            stack.push(token);
        } else {
            let operand2 = stack.pop();
            let operand1 = stack.pop();
            stack.push(token + operand1 + operand2);
        }
    }

    return stack.pop();
}

// Example usage:
let postfixExpressionQ6 = "ABC/-AK/L-*";
let resultQ6 = postfixToPrefix(postfixExpressionQ6);
console.log(resultQ6);


/*Q7. Write a program to convert prefix expression to infix expression.*/
function prefixToInfix(prefixExpression) {
    let stack = [];

    for (let i = prefixExpression.length - 1; i >= 0; i--) {
        let token = prefixExpression[i];

        if (/[a-zA-Z0-9]/.test(token)) {
            stack.push(token);
        } else {
            let operand1 = stack.pop();
            let operand2 = stack.pop();
            stack.push(`(${operand1}${token}${operand2})`);
        }
    }

    return stack.pop();
}

// Example usage:
let prefixExpressionQ7 = "*-A/BC-/AKL";
let resultQ7 = prefixToInfix(prefixExpressionQ7);
console.log(resultQ7);


/*Q8. Write a program to check if all the brackets are closed in a given code snippet.*/
function areBracketsClosed(codeSnippet) {
    let stack = [];

    for (let char of codeSnippet) {
        if (char === '(' || char === '{' || char === '[') {
            stack.push(char);
        } else if (char === ')' && stack.pop() !== '(') {
            return false;
        } else if (char === '}' && stack.pop() !== '{') {
            return false;
        } else if (char === ']' && stack.pop() !== '[') {
            return false;
        }
    }

    return stack.length === 0;
}

// Example usage:
let codeSnippetQ8 = "(a + b) * (c - d)";
let resultQ8 = areBracketsClosed(codeSnippetQ8);
console.log(resultQ8);


/*Q9. Write a program to reverse a stack.*/
class Stack {
    constructor() {
        this.items = [];
    }

    push(element) {
        this.items.push(element);
    }

    pop() {
        if (this.items.length === 0) {
            return null;
        }
        return this.items.pop();
    }

    isEmpty() {
        return this.items.length === 0;
    }

    size() {
        return this.items.length;
    }
}

function reverseStack(stack) {
    let reversedStack = new Stack();

    while (!stack.isEmpty()) {
        reversedStack.push(stack.pop());
    }

    return reversedStack;
}

// Example usage:
let stackQ9 = new Stack();
stackQ9.push(1);
stackQ9.push(2);
stackQ9.push(3);
let reversedStackQ9 = reverseStack(stackQ9);
console.log(reversedStackQ9.items);


/*Q10. Write a program to find the smallest number using a stack*/
class MinStack {
    constructor() {
        this.stack = [];
        this.minStack = [];
    }

    push(value) {
        this.stack.push(value);
        if (this.minStack.length === 0 || value <= this.minStack[this.minStack.length - 1]) {
            this.minStack.push(value);
        }
    }

    pop() {
        if (this.stack.length === 0) {
            return null;
        }
        let poppedValue = this.stack.pop();
        if (poppedValue === this.minStack[this.minStack.length - 1]) {
            this.minStack.pop();
        }
        return poppedValue;
    }

    getMin() {
        if (this.minStack.length === 0) {
            return null;
        }
        return this.minStack[this.minStack.length - 1];
    }
}

// Example usage:
let minStackQ10 = new MinStack();
minStackQ10.push(3);
minStackQ10.push(5);
minStackQ10.push(2);
minStackQ10.push(1);
console.log(minStackQ10.getMin()); // Output: 1
minStackQ10.pop();
console.log(minStackQ10.getMin()); // Output: 2
