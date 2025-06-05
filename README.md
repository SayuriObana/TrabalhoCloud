**Envio de Email com AWS Lambda e SES**

Este projeto é uma função AWS Lambda que envia e-mails utilizando o serviço Amazon SES (Simple Email Service). A função recebe parâmetros via query string ou corpo da requisição JSON, processa-os e envia o e-mail para o destinatário especificado.


**Pré-requisitos**

Conta ativa na AWS com permissões para criar funções Lambda e configurar SES.
Email remetente verificado no SES (exemplo: testeumfg@gmail.com).
AWS CLI ou acesso ao AWS Management Console.
Postman instalado para testes via API HTTP.


**Configuração do AWS SES**

Acesse o AWS SES Console.
Verifique o email remetente (de onde os e-mails serão enviados). Isso é obrigatório para evitar limitações do sandbox.
Caso esteja em sandbox, verifique também os destinatários (emails para onde enviará) ou solicite a saída do sandbox.


**Criando a função Lambda**

Acesse o AWS Lambda Console.
Clique em Criar função.
Selecione Autor do zero.
Defina um nome para a função, por exemplo: EnviarEmailSES.
Escolha a runtime Python 3.x.
Crie ou selecione uma role IAM com permissões para executar Lambda e enviar e-mail via SES (AmazonSESFullAccess ou política customizada).
Clique em Criar função.


**Inserindo o código na Lambda**

No editor de código da função Lambda, cole o código Python responsável pelo envio do e-mail (no arquivo lambda_function.py).
Ajuste o endereço de e-mail remetente no código para o e-mail verificado no SES (Source) se for preciso.


**Criando e salvando o teste**

No console da função Lambda, acesse a aba Testar.
Crie um novo evento de teste, nomeie-o (ex: EnvioEmailTeste).
Configure o evento com um corpo JSON contendo os parâmetros necessários (to, subject, body).
Salve o evento de teste.

Código JSON para colar no teste

```json

{
  "queryStringParameters": {
    "to": "testeumfg2@gmail.com",
    "subject": "Olá",
    "body": "E-mail enviado via Lambda por Rayani ;))))"
  }
}

```


**Fazendo o deploy da função**

Após inserir o código e salvar o teste, o deploy é automático no console da AWS Lambda. Caso use pipelines CI/CD, faça o deploy conforme seu fluxo.
Testando via AWS Console
Selecione o evento de teste criado.
Clique em Testar.
O retorno esperado é um status 200 e uma mensagem confirmando o envio do e-mail, incluindo o MessageId.
Caso haja erros, o console retornará a mensagem de erro.


**POSTMAN**

Através do método POST 

Cole esta URL:

https://ziug2fcposdcxgwhaw4eibusta0cajop.lambda-url.us-east-1.on.aws/

No Body (RAW) coloque o seguinte JSON:

```json
{
  "to": "testeumfg2@gmail.com",
  "subject": "Enviado pelo Postman!",
  "body": "Esta mensagem foi enviada usando Postman e AWS Lambda via API Gateway."
}

```
Deverá aparecer uma mensagem de e-mail enviado com sucesso.
A mensagem vai aparecer na caixa Spam do e-mail.

**PS: Observações**

Eu e meu namorado (Pedro turma A) criamos os novos emails para fazer essa atividade ;)
