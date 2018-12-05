# js-advance--closure-prototype, IIFE -etc
Advance ES5 - Closure, Prototype, IIFE etc

...................................................................................................................................

Here is some advance ES5 syntex with a proper example.

/*********************
 * Function Contructor
 *  */

// var john = {
//     name : 'John',
//     yearOfBirth : 1990,
//     job : 'techer'
// };

/**********************
 *  simple function constructor
    var Person = function (name, yearOfBirth, job) {
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
    this.calculateAge = function () {
        console.log(2018 - this.yearOfBirth);
    }
}
 */
/*
var Person = function (name, yearOfBirth, job) {
    this.name = name;
    this.yearOfBirth = yearOfBirth;
    this.job = job;
    // this.calculateAge = function () {
    //     console.log(2018 - this.yearOfBirth);
    // }
}
// here is inheritence used with prototype -- using method
Person.prototype.calculateAge = function () {
    console.log(2018 - this.yearOfBirth);
};

// here is inheritence used with prototype -- using properties
Person.prototype.lastName = 'Smith';


var john = new Person('john', 1990, 'teacher');
var jane = new Person('jane', 1985, 'Model');
var mark = new Person('Mark', 1969, 'Designer');
john.calculateAge();
jane.calculateAge();
mark.calculateAge();
console.log(john.lastName);
console.log(jane.lastName);
console.log(mark.lastName);
*/



/*******************
 *  Object.create
 */
/*

var personProto = {
    calculateAge : function () {
        console.log(2018 - this.yearOfBirth);
    }
}
var john = Object.create(personProto);
john.name = 'John';
john.yearOfBirth = 1990;
john.job = 'teacher';

var jane = Object.create(personProto, 
    {
        name : {value : 'Jane'},
        yearOfBirth : {value : 1992},
        job : { value : 'Designer'},
    });

*/
/*****************************
 * Primitives vs Objects
 */
/*
 //premitives
var a = 26;
var b = a;
a = 46;
console.log(a);
console.log(b);

//objects

var obj1 = {
    name : 'john',
    age : 26
}
var obj2 = obj1;
obj1.age =30;
console.log(obj1.age);
console.log(obj2.age);

//Functions
var age = 30;
var obj = {
    name : 'Raj',
    city : 'Bengluru'
}
function change(a, b) {
 a =25;
 b.city = 'Delhi';
}
change(age, obj);
console.log(age);
console.log(obj.city);
*/

/***************************
 * Lecture : passing functions as an arguments
 */
/*
var year = [1990, 1985, 1960, 2002, 1996];

function arrayCalc(arr, fn) {
    var arrResult = [];
    for (var i = 0; i < arr.length; i++) {
        arrResult.push(fn(arr[i]));
    }
    return arrResult;
}

function calculateAge(elem) {
    return 2018 - elem;
}

function isFullAge(elem) {
    return elem >= 18;
}

function maxHeartRate(elem) {

    if (elem >= 18 && elem <= 81) {
        return Math.round(206.9 - (0.67 * elem));
    } else {
        return -1;
    }

}
var ages = arrayCalc(year, calculateAge); // calculate age

var fullAges = arrayCalc(ages, isFullAge); // calculate adult or not

var rates = arrayCalc(ages, maxHeartRate); // calculatin heart rate

console.log(ages);
console.log(fullAges);
console.log(rates);

*/
/*****************************
 *  Functions returning functions
 */
/*
function interviewQuestion (job) {
    if (job === 'designer') {
        return function (name) {
            console.log(name + ', can you please explain me what UX design is?');
        }
    } else if (job === 'teacher') {
        return function (name) {
            console.log('Hello ' + name + ', what subject do you teach ?');
        } 
    } else   {
        return function (name) {
            console.log('Hello ' + name + ', What do you do?');
        }
    }
}

var teacherQuestion = interviewQuestion('teacher');
var designerQuestion = interviewQuestion('designer');
var driverQuestion = interviewQuestion('driver');
designerQuestion('Mark');
teacherQuestion('John');
driverQuestion('Rahul');

interviewQuestion('designer')('Sourav'); // another way to call
*/
/*****************
 * IIFE : immediately Invoked Function Expression
 */
/*
// let if we have to create a game in which it will generate a random num between 1 to 9 and if 
// num is greater then 5 then wins the game or loose. we have keep the score hidden and private
//treditional way to do this

// function game() {
//     var score = Math.random() * 10;
//     console.log(score >= 5);
// }
// game();

//using IIFE

(function () {
    var score = Math.random() * 10;
    console.log(score >= 5);
}) ();

// passing the parameters in IIFE

(function (goodluck) {
    var score = Math.random() * 10;
    console.log(score >= 5 - goodluck);
}) (4);
*/

/*****************************
 * Closures
 * An inner function has always access to the variables and parameters of its outer function , 
 * even after outer function has returned.
 */
/*
function retirement(retirementAge) {
    var a = ' year left until retirement.';
    return function (yearOfBirth) {
        var age = 2018 - yearOfBirth;
        console.log((retirementAge - age) + a)
    }
}

var retirementUS = retirement(66);
var retirementGermany = retirement(65);
var retirementIceland = retirement(67);
retirementUS(1990);
retirementGermany(1990);
retirementIceland(1990);
*/
// retirement(66)(1991); another sore way to calling above functions
//rewrite interview function using clouser

/*
// normal function
function interviewQuestion (job) {
    if (job === 'designer') {
        return function (name) {
            console.log(name + ', can you please explain me what UX design is?');
        }
    } else if (job === 'teacher') {
        return function (name) {
            console.log('Hello ' + name + ', what subject do you teach ?');
        } 
    } else   {
        return function (name) {
            console.log('Hello ' + name + ', What do you do?');
        }
    }
}
*/
/*
// using clouser

// my way
// function interviewQuestion (name) {
//     var a = name + ' , can you please explain what UX design is?'
//     var b = ' hello ' + name + ', what subject do you teach?'
//     var c= 'Hello' + name + ', What do you do?'
//     return function (job) {
//         if (job === 'designer') {
//             console.log(a);
//         } else if (job === 'teacher') {
//             console.log(b);
//         } else {
//             console.log(c);
//         }
//     }
// }


// var interviewName = interviewQuestion('John');
// interviewName('designer');

// instructor way 
function interviewQuestion(job) {
    return function (name) {
        if (job === 'designer') {
            console.log(name + ', can you please explain me what UX design is?');
        } else if (job === 'teacher') {
            console.log('Hello ' + name + ', what subject do you teach ?');
        } else {
            console.log('Hello ' + name + ', What do you do?');
        }
    }
}
interviewQuestion('designer')('john');
*/

/************************
 * Bind, Call, and apply
 */
/*
var john = {
    name: 'John',
    age: 26,
    job: 'designer',
    presentation: function (style, timeOfDay) {
        if (style === 'formal') {
            console.log('Good ' + timeOfDay + ', ledies and gentlemen ! I\'m ' + this.name + ', I\'m a ' + this.job + ', and I\'m ' + this.age + ' years old.');
        } else if (style === 'friendly') {
            console.log('Hey what\'s up ? I\'m ' + this.name + ', I\'m a ' + this.job + ', and I\'m ' + this.age + ' years old. Have a nice ' + timeOfDay + '.');
        }
    }
}

john.presentation('formal', 'Morning')

var emily = {
    name: 'Emily',
    age: 25,
    job: 'teacher'
}

john.presentation.call(emily, 'friendly', 'Afternoon'); // call method : simply used to borrow the method and use to set the this variable

// john.presentation.apply(emily, ['friendly', 'Morning']); // apply method: same as call method only difference is it accept other arguments is in array
var emilyFriendly = john.presentation.bind(emily, 'friendly'); // bind method : first it store the function in a variable or say 
// copy it to the variable and then we can use that variable as function later. 
emilyFriendly('Morning');



var year = [1990, 1985, 1960, 2002, 1996];

function arrayCalc(arr, fn) {
    var arrResult = [];
    for (var i = 0; i < arr.length; i++) {
        arrResult.push(fn(arr[i]));
    }
    return arrResult;
}

function calculateAge(elem) {
    return 2018 - elem;
}

function isFullAge(limit, elem) {
    return elem >= limit;
}

var ages = arrayCalc(year, calculateAge);
var fullJapan = arrayCalc(ages, isFullAge.bind(this, 20));

console.log(ages);
console.log(fullJapan);
*/

/////////////////////////////
// CODING CHALLENGE


/*
--- Let's build a fun quiz game in the console! ---

1. Build a function constructor called Question to describe a question. A question should include:
a) question itself
b) the answers from which the player can choose the correct one 
(choose an adequate data structure here, array, object, etc.)
c) correct answer (I would use a number for this)

2. Create a couple of questions using the constructor

3. Store them all inside an array

4. Select one random question and log it on the console, together with the possible answers 
(each question should have a number) (Hint: write a method for the Question objects for this task).

5. Use the 'prompt' function to ask the user for the correct answer. The user should input the 
number of the correct answer such as you displayed it on Task 4.

6. Check if the answer is correct and print to the console whether the answer is correct ot nor 
(Hint: write another method for this).

7. Suppose this code would be a plugin for other programmers to use in their code. 
So make sure that all your code is private and doesn't interfere with the other programmers code 
(Hint: we learned a special technique to do exactly that).
*/
/*
// implemented IIFE
(function() {
// step - 1 created function contructure 
    var Question = function (question, answers, correct) {
        this.question = question;
        this.answers = answers;
        this.correct = correct;
    }
    // step - 3 console the question with the options
    Question.prototype.displayQuestion = function() {
        console.log(this.question);
        for(var i = 0; i < this.answers.length; i++ ) {
            console.log(i + ': ' + this.answers[i]);
        }
    }
    //step - 4 check the input option whether it is right or wrong
    Question.prototype.checkAnswer = function(ans) {
        if (ans === this.correct) {
            console.log('Correct answer!');
        } else {
            console.log('Wrong Answer !! ')
        }
    }
    // step 2 - inserted value in contructure
    var q1 = new Question('Is JavaScript is the coolest Language ?', ['Yes','No'], 0);
    var q2 = new Question('What is instructure name of this course?', ['Mike','John','Jonas'], 2);
    var q3 = new Question('What is best describe cooding ?', ['Boring','Fun','Hard'], 1);
    // created  array of question 
    var questions = [q1, q2, q3];

    // generated random question
    var n = Math.floor(Math.random()*questions.length);
    // calling the function for display the question and its option
    questions[n].displayQuestion();
// for prompting to take input from user
    var answer = parseInt(prompt('Please select correct answer. '));
    // calling the prototype fuction for chaecking answer
    questions[n].checkAnswer(answer);
})();

*/


/*
--- Expert level ---

8. After you display the result, display the next random question, so that the game never ends 
(Hint: write a function for this and call it right after displaying the result)

9. Be careful: after Task 8, the game literally never ends. So include the option to quit 
the game if the user writes 'exit' instead of the answer. In this case, DON'T call the function 
from task 8.

10. Track the user's score to make the game more fun! So each time an answer is correct, 
add 1 point to the score (Hint: I'm going to use the power of closures for this, but you 
don't have to, just do this with the tools you feel more comfortable at this point).

11. Display the score in the console. Use yet another method for this.
*/


// implemented IIFE
(function () {
    // step - 1 created function contructure 
    var Question = function (question, answers, correct) {
        this.question = question;
        this.answers = answers;
        this.correct = correct;
    }
    // step - 3 console the question with the options
    Question.prototype.displayQuestion = function () {
        console.log(this.question);
        for (var i = 0; i < this.answers.length; i++) {
            console.log(i + ': ' + this.answers[i]);
        }
    }
    //step - 4 check the input option whether it is right or wrong
    Question.prototype.checkAnswer = function (ans, callback) { // 2nd parameter is for calling the score function which is a callback fn
        if (ans === this.correct) {
            var sc;
            console.log('Correct answer!');
            sc = callback(true); // calling the callback function
        } else {
            console.log('Wrong Answer !! ')
            sc = callback(false); // calling the callback function
        }
        this.displayScore(sc);
    }

    Question.prototype.displayScore = function (sc) {
        console.log('your Current Score Is : ' + sc);
        console.log('------------------------------------------');
    }
    // step 2 - inserted value in contructure
    var q1 = new Question('Is JavaScript is the coolest Language ?', ['Yes', 'No'], 0);
    var q2 = new Question('What is instructure name of this course?', ['Mike', 'John', 'Jonas'], 2);
    var q3 = new Question('What is best describe cooding ?', ['Boring', 'Fun', 'Hard'], 1);
    // created  array of question 
    var questions = [q1, q2, q3];

    // counting the score if true using clouser
function score () {
   var sc = 0;
    return function (correct) {
        if (correct) {
            sc++;
        }
        return sc;
    }
}
var keepScore = score(); // keep the value of score function in it and use for calling the function


    function nextQuestion() {
        // generated random question
        var n = Math.floor(Math.random() * questions.length);
        // calling the function for display the question and its option
        questions[n].displayQuestion();
        // for prompting to take input from user
        var answer = prompt('Please select correct answer. ');
        // calling the prototype fuction for chaecking answer
        if (answer !== 'exit') {
            questions[n].checkAnswer(parseInt(answer), keepScore); // keepScore is the 2nd parameter to the checkAnswer function
            nextQuestion();
        }
    }
    nextQuestion();    

})();
