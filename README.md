# ViaCep
> Aprendendo sobre Promises, utilização de API e manipulação de JSON

## Consultando de dados do Códigos de Endereçamento Postal (CEP)
### O objetivo deste projeto é obter dados a partir de um CEP,  utilizando a API [ViaCEP](https://viacep.com.br/)
Os dados recebidos são os seguintes:
 - Bairro
 - Complemento
 - DDD
 - GIA
 - IBGE
 - Localidade
 - Logradouro
 - Siafi
 - UF
 - 
## Utilizando a aplicação

![](https://github.com/ArthurGNogueira/ConsultaViaCep/blob/3c15460fdff76e9fdde538379bfb1b8513da0132/Peek%2010-11-2020%2015-10.gif)

### Podemos ainda copiar os dados recebidos com um simples click

![](https://github.com/ArthurGNogueira/ConsultaViaCep/blob/3c15460fdff76e9fdde538379bfb1b8513da0132/Peek%2010-11-2020%2015-12.gif)


## Como funciona ?
Podemos ver abaixo o principal trecho de código, nele utilizamos uma função chamada receberDados, e esta função por sua vez, recebe o parâmetro cep
Em seguida nós convertemos o valor recebido em cep para uma string, para evitar futuros problemas. 

Então realizamos uma requisição com fetch ao endereço: https://viacep.com.br/ws/CEP/json
Porém passamos a nossa variável cep do tipo string no lugar da palavra CEP

O retorno pode demorar algum tempo, pois se trata de uma **Promise** por isso devemos utilizar o método [**then( )**](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)

Após receber o retorno como data, utilizamos a função **.json( )** para converter o retorno em  um **Javascript Object**, assim fica mais fácil de manipular os dados.

Por último,  utilizamos uma **Operação ternária** em cada propriedade do objeto para verificar de o retorno está vazio, caso verdadeiro, a propriedade do objeto recebe o valor "Informação não encontrada", caso negativo recebe o próprio valor. 

O console.log( ) utilizamos para debugar a aplicação

    function receberDados(cep){
    	this.cep = toString(cep);
    	return window.fetch ('https://viacep.com.br/ws/'+ cep +'/json')
    	.then((data) => data.json())
    		.then(function(data){
    			for(i in data){
    			data[i] = data[i] == '' ? "Informação não encontrada" : data[i];
    			console.log(data[i]);
    };
