# ljs
Lua with C/C++/Java/Javascript syntax

Here is some code to see how it's like:

```js
/* Limited json style table declaration */
var json = {"name": "bob"};
var A = {t: {f: 7}, n: 3}
var ary = [1,2,3,4]; //Array style declaration, syntax sugar for {}
var num = 5;

if(json.name == "bob") print("Hello Bob !"); // if/ese like in C/C++/Java/Javascript 
else if(json.name == "mary") print("A pretty woman !");
else print("Nice to meet you !");

for(i=1, 10) print(i);
for(k,v in pairs(json)) print(k,v);

for(k,v in pairs(A)) { // blocks are curly braces delimited
	if(k == "one") continue;
	print(k, type(k), v);
}

while(num > 0) --num; //pre inc/dec operators
num += 5; // compound operators
while(num > 0) {
	print(num--);
}
num += 5;
do { //conventional do/while
	if(num == 3) goto update;
	//inline boolean expression
	print(num == 2 ? "it's a two" : "it's a " .. num);
update:
	--num;
} while(num > 0);

function doIt(p : string) : string { // functions and variables can have an anotation
	return "Done " .. p;
}

print(doIt("car"));

function doAgain(p) {
	if(p == null) return "I don't know what to do !"; // uses "null" instead of "nil"
	return "Done " .. p;
}

print(doAgain("car"));

var Engine = {
	speed : 0
};

function Engine::speedTo(v : integer) { //synatx sugar for function member with "this"
	this.speed = v; // use "this" instead of "self"
}

print(Engine.speed);
Engine->speedTo(12); //syntax sugar for method call with inplicity "this"
print(Engine.speed);
```

I took code and ideas from :

https://github.com/ex/Killa

https://github.com/sajonoso/jual



The default extension is ".ljs".

On folder lua2ljs there is a program to convert lua sources to ljs.

```
lua2ljs afile.lua > afile.ljs
```

This is based on Lua 5.3.5, released on 26 Jun 2018.

For installation instructions, license details, and
further information about Lua, see doc/readme.html.

There is also the following port from lua to ljs:

ljsjit at https://github.com/mingodad/ljsjit

ljs-5.1 at https://github.com/mingodad/ljs-5.1

ZeroBraneStudio port at https://github.com/mingodad/ZeroBraneStudioLJS

raptorjit-ljs at https://github.com/mingodad/rpatorjit-ljs

snabb-ljs at https://github.com/mingodad/snabb-ljs

premake5-ljs at https://github.com/mingodad/premake-core/tree/ljs

CorsixTH-0.62-ljs at https://github.com/mingodad/CorsixTH-ljs

The tool lua2ljs does the convertion on almost all Lua code, except dynamic Lua code inside strings, C/C++ code, auxiliar scripts and makefiles, LJS also flag as warning/error duplicate variable declarations and a revision is needed mainly using "ljsc -p -l ljsSource.ljs > /dev/null" to only compile and emit the warnings/error to stderr, then several text scans to search and replace "nil", ".lua" and Lua code inside strings, ...

Finally run the tests if available to check that it's working properly (at least with the tests).
