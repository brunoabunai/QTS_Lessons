# Derivação
Uma tentativa de explicação pratica sobre derivações nos códigos.

Para criar uma calculadora podemos fazer:
```js
function MakeCalc(num1,num2){
	Console.log(‘O resultado é: ’+(num1+num2));  
}
MakeCalc(2,3) // O resultado é 5
```
porém, pense um pouco, e se em algum momento tivermos que refazer a calculadora e ela tiver que ter uma mensagem diferente. Imagine que tivéssemos vários tipos de calculadoras e o quanto de trabalho teríamos para refazer cada calculadora com a mensagem nova, com o nome de quem fez a conta, e se mudasse e tivéssemos uma operação diferente e ela subtraísse? E ser agora não fossem mais 2 números e sim 5??

```js
Function MakeCalc(name,num1,num2,num3,num4,num5){
	Console.log(name+‘ | o resultado é: ’+(num1+num2+num3+num4+num5));  
}
```
agora imagine mudar isso em diversas partes do código, personalizar tipos de entrada e saída, e imagina começar um novo projeto de calculadora mas totalmente diferente, não iria compensar usar isso como base e teríamos que fazer os mesmos processos de um jeito diferente para chegar a um resultado parecido: 😅

```js
function MakeCalc1(name,num1,num2,num3,num4,num5){
	Console.log(name+‘ o resultado é: ’+(num1+num2+num3+num4+num5)); 
	function MakeCalc2(name,num1,num2,num3){
	Console.log(name+‘ o resultado é: ’+(num1+num2+num3));   
}
function MakeCalc3435345345345(name,num1,num2,num3){
	Console.log(name+‘ o resultado é: ’+???????????  
}
```

Porém, creio que a derivação dos artefatos solucione isso, veja o exemplo:
```js
function InitCalculator(...args){
	const [account,numbers] = getArgs(args);
	const result = makeCalc(numbers);
	const message = createMessage(account,result);
	showResult(message); 
}

function getArgs(arguments){
	return [arguments[0],[arguments[1][0],arguments[1][0]]]
}

function makeCalc(numbers){
	let result=0;
	for(let i=0; i<numbers.length; i++){
		result+=numbers[i];
	};
	return result;
};

function createMessage(account,result){
	return `| ${account}, o resultado é: ${result}`;
}

function showResult(message){
	console.log(message);
}

InitCalculator('Carlos',3,5); // | Carlos, o resultado é: 5
```
Parece que nada mudou, que faz a mesma coisa e que criar esse tanto de função é uma perca de tempo, mas se agora quisermos trocar a mensagem, vamos na função da mensagem, se quisermos trocar de soma para subtração, vamos na função makeCalc, e assim por diante... Exemplo, vamos mudar a quantidades de argumentos passados (numeros a ser somados);
```js

//function getArgs(arguments){
//	return [arguments[0],[arguments[1][0],arguments[1][0]]]
//} ::BEFORE::

function getArgs(arguments){ //after
	return [arguments[0],arguments[1].map(item => item)];
}

InitCalculator('Daniel',3,4); // | Carlos, o resultado é: 7
InitCalculator('Carlos',3,5,5,5,5,5,5,5); // | Carlos, o resultado é: 33

```
pronto agora nós passamos qualquer quantidade e números e conseguimos somar todos eles, e se algum dia quisermos criar uma calculadora em html, basta chamar um evento de onclick e passar a função InitCalculator, com os valores digitados. Exemplo:

```js
	let calculator=[]
	let i=0;
	input.onkeyup= (event) => {
		if(Number(event.key)){
			calculator.push(event.key);
			InitCalculator('Carlos',calculator.map(
				number=>number));
			i++;
		}
	}
```
Agora pense em como faríamos isso com aquela função antiga sem derivações, seria um pouco mais trabalho e para mudar isso depois kkk 😨.
