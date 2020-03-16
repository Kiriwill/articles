### Vantagens e desvantagens das promises

Promises são processamentos que podem ser executados no mesmo instante, no futuro ou nunca. São formas de processamento assíncrono que não comprometem o processamento da aplicação. Uma promise pode estar em quatro estados: pending, fulfilled, rejected ou settled.

Elas vêm como resposta a alguns problemas das funções callbacks. Callbacks quando mal escritos tendiam a gerar o que se chama de *callback hell*, isto é, múltiplos aninhamentos de funções callbacks, o que dificultava a leitura do código. Além disso, tornava dificil atribuir o erro a função ao qual pertence. 

Por exemplo, para atualizar dados de pagamento de um usuário em uma pagina cada uma das funções precisa conter seu proprio tratamento de erro: 

```javascript
// Um callback
getUser("username", (user) => {
  getPayments(user, (payments) => {
    updateUI({
      user,
      payments: payments.query.results
    })
  }, error)
}, error)
```

Para solucionar isso, as promises são construidas em sintaxe que deixa mais claro quais são os passos da execução.

```javascript
// Uma promise
getUser("username")
.then(getPayments)
.then((data) => updateUI(data))
.catch(error);
```
A função *updateUi* foi desacoplada de dentro da função *getPayments* e o restante tornou-se parametros de *then()*. O *then* retorna uma nova promise que  permite que se escreva o código sequencialmente e o *catch* unifica o tratamento de erro em uma só linha.

Ainda que solucione tais problemas as promises ainda são evidentemente assincronas. No meio de um código sincrono isso pode causar confusão. Por isso, foi proposta a sintaxe async/await. 

```javascript
async function getUserAsync(){
  try{
    let response = await getUser('username');
    let data = await getPayments(response);
    updateUi(data);
  }
  catch(error){
    console.log(`Error: ${error}`);
  }
}

request()
```

Com o async/await é só codificar como síncrono. A palavra *await* é o indicativo de que ali há uma promise. Após a execução da promise, o resultado já é armazenado na variável *response*. Em caso de erro, *catch* se encarrega de processa-lo.
