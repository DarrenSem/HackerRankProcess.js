# process.js-for-HackerRank
Minimal polyfill (324 characters minified) for client-side JS to add missing NodeJS functions for completing HackerRank.com challenges -- process.stdin/stdout/env.OUTPUT_PATH and require("fs").createWriteStream

(So I can complete HackerRank.com challenges on my cell using my custom REPL bookmarklet.)

```
// process.js-HackerRank.com-NodeJS-polyfill.js
// paste into TOP of HackerRank problem solution (JavaScript version, or TypeScript too I guess)



// Usage: paste [process.js-HackerRank.com-NodeJS-polyfill.js] here (code is below)

[
	"5\noptional\ninput\ntest\ndata\nhere",
	["test", "data"],
	7,
	null,
	,
	"etc.",
].forEach(this_input => {

require._ = this_input;

function processData(input) {
    console.log("processData: Enter your code here, which processes this input:", {input});
}
process.stdin.resume();
process.stdin.setEncoding("ascii");

if("STORE_AS_STRING" === "STORE_AS_STRING")_input = "";
// if("STORE_AS_ARRAY" === "STORE_AS_ARRAY")_input = [];
process.stdin.on("data", function (input) {
	if(typeof _input === "string")_input += input;
	if(Array.isArray(_input))if(Array.isArray(input)){for(var i in input)_input.push(input[i])}else{_input.push(input)};
});

process.stdin.on("end", function () {
   processData(_input);
});

});



// [process.js-HackerRank.com-NodeJS-polyfill.js]

// minified = 324 chars
"function"!=typeof require&&((a,b,c,d,e)=>(c=a=>(b||=[]).push(a),d=()=>b=console.log((b||=[]).join("")),e=a=>"process"==a&&{stdin:{resume(){},setEncoding(){},on(a,b){b(e._),d()}},env:{OUTPUT_PATH:"<OUTPUT_PATH>"},stdout:{write:c}}||"fs"==a&&{createWriteStream:()=>({write:c,end:d})},e._=a,process=e("process"),require=e))(
	"5\noptional\ninput\ntest\ndata\nhere" || ["test", "data"] || 7 || "etc."
);

// if("xyzCLEAR" === "CLEAR")console.clear();
if(
	"xyzFORCE" === "FORCE" ||
	"function" != typeof require
) ( ( testData, _buffer, _write, _flush, _require ) => (

	_write = data => ( _buffer ||= [] ).push(data),

	_flush = _ => _buffer = console.log( ( _buffer ||= [] ).join("") ),

	_require = moduleId => (
		moduleId == "process" && {
			stdin: {
				resume(){},
				setEncoding(){},
				on(eventName, fn) { fn(_require._); _flush(); }
			},
			env: {
				OUTPUT_PATH: "<OUTPUT_PATH>"
			},
			stdout: { write: _write }
			// ^ needed for Day 15: hackerrank.com/challenges/30-linked-list
		}
		|| moduleId == "fs" && {
			createWriteStream: streamPath => ( { write: _write, end: _flush } )
			// ^ needed for Day 9: hackerrank.com/challenges/30-recursion
		}
	),

	_require._ = testData,
	process = _require("process"),
	require = _require

) ) (	// pass (testData) below...
	["1", "2", "3"]
);



// Usage example #1 (of 2) = Day 15: hackerrank.com/challenges/30-linked-list
require._ = "3\n11\n99\n33";	// result = "11 99 33 "

process.stdin.resume();
process.stdin.setEncoding('ascii');
var input_stdin = "";
var input_stdin_array = "";
var input_currentline = 0;
process.stdin.on('data', function (data) {
    input_stdin += data;
});
process.stdin.on('end', function () {
    input_stdin_array = input_stdin.split("\n");
    main15();
});
function readLine15() {
    return input_stdin_array[input_currentline++];
}
function Node15(data){
    this.data=data;
    this.next=null;
}
function Solution15(){

	this.insert=function(head,data){
        //complete this method
        let newNode = new Node15(data);

        let start = head;
        if(!start)return newNode;

        let next;

        while(next = start.next) {
            start = next;
        };
        start.next = newNode;

        return head;
    };

	this.display=function(head){
        var start=head;
            while(start){
                process.stdout.write(start.data+" ");
                start=start.next;
            }
    };
}
function main15(){
    var T=parseInt(readLine15());
    var head=null;
    var mylist=new Solution15();
    for(i=0;i<T;i++){
        var data=parseInt(readLine15());
        head=mylist.insert(head,data);
    }
    mylist.display(head);
}		



// Usage example #2 (of 2) = Day 09: hackerrank.com/challenges/30-recursion
require._ = "5";	// result = 120

'use strict';

const fs = require('fs');

process.stdin.resume();
process.stdin.setEncoding('utf-8');

let inputString = '';
let currentLine = 0;

process.stdin.on('data', function(inputStdin) {
    inputString += inputStdin;
});

process.stdin.on('end', function() {
    inputString = inputString.split('\n');

    main09();
});

function readLine09() {
    return inputString[currentLine++];
}

/*
 * Complete the 'factorial' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts INTEGER n as parameter.
 */

function factorial(n) {
	
    // Write your code here

  let exitCondition = n < 2;

  if(!exitCondition) {
    return n * factorial(n - 1);
  } else {
    // return n;
    return 1;
  };
  // ideal is to make sure the exit condition is at the end.

  // one-liner: return n > 1 ? n * factorial(n - 1) : 1;
}

function main09() {
    const ws = fs.createWriteStream(process.env.OUTPUT_PATH);

    const n = parseInt(readLine09().trim(), 10);

    const result = factorial(n);

    ws.write(result + '\n');

    ws.end();
}
```

