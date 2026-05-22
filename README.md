# Introdução ao Node-RED

## O que é o Node-RED?

O Node-RED é uma ferramenta de programação visual baseada em fluxos. Em vez de criar programas escrevendo muitas linhas de código, o usuário monta aplicações conectando blocos visuais chamados de nós.

Cada nó possui uma função específica, como:

* enviar mensagens;
* receber dados;
* processar informações;
* realizar cálculos;
* acessar serviços;
* controlar dispositivos;
* automatizar tarefas.

A programação é feita de maneira visual, arrastando e conectando elementos na tela.

---

## Para que serve?

O Node-RED é bastante utilizado em:

* automação;
* Internet das Coisas (IoT);
* integração entre sistemas;
* monitoramento de dados;
* criação de dashboards;
* testes rápidos;
* prototipagem de projetos.

Ele é muito usado por iniciantes por ser simples de aprender e também por profissionais devido à sua flexibilidade.

---

## Como funciona?

No Node-RED, os programas são chamados de fluxos.

Os fluxos são criados conectando nós.

Exemplo simples:

Inject → Debug

Nesse exemplo:

* o nó Inject envia uma mensagem;
* o nó Debug mostra essa mensagem na tela.

---

<details>
<summary> <h2> Executando o Node-RED com Docker </h2> </summary>

O que é Docker?

Docker é uma ferramenta que permite executar aplicações em ambientes isolados chamados containers.

O container já possui tudo que o programa precisa para funcionar, evitando instalações complexas no computador.

---

### Pré-requisitos

Antes de começar:

* ter o Docker Desktop instalado;
* deixar o Docker Desktop em execução.

---

### Verificando se o Docker está funcionando

Abra o PowerShell e execute:

```powershell
docker --version
```

Depois:

```powershell
docker ps
```

Se os comandos funcionarem sem erro, o Docker está pronto para uso.

---

### Executando o Node-RED pela primeira vez

No PowerShell, execute:

```powershell
docker run -it -p 1880:1880 --name mynodered nodered/node-red
```

Esse comando irá:

* baixar a imagem do Node-RED;
* criar um container;
* iniciar o Node-RED.

---

### Abrindo o Node-RED

Quando aparecer uma mensagem parecida com:

Server now running at [http://127.0.0.1:1880/](http://127.0.0.1:1880/)

Abra o navegador e acesse:

[http://localhost:1880](http://localhost:1880)

A interface do Node-RED será exibida.

---

### Parando o Node-RED

No terminal:

CTRL + C

---

### Executando novamente depois

Depois da primeira execução, utilize:

```powershell
docker start -ai mynodered
```
</details>

---

<details>
<summary> <h2> Conhecendo a Interface </h2> </summary>

Área de Fluxo

É o espaço principal onde os programas serão montados.

---

### Paleta de Nós

Fica no lado esquerdo da tela.

Contém todos os blocos disponíveis para uso.

Alguns exemplos:

* inject;
* debug;
* function;
* switch.

---

### Painel Debug

Fica na lateral direita.

Serve para visualizar mensagens e resultados dos fluxos.

---

### Primeiro Fluxo

Objetivo

Criar um fluxo simples que envia uma mensagem.

---

#### Passo 1: Adicionar os nós

Arraste para a área de trabalho:

* 1 nó Inject;
* 1 nó Debug.

---

#### Passo 2: Conectar os nós

Clique no ponto cinza do Inject e arraste até o Debug.

---

#### Passo 3: Publicar o fluxo

Clique no botão:

Deploy

---

#### Passo 4: Executar

Clique no botão do nó Inject.

---

#### Resultado

A mensagem será exibida no painel Debug.

---

## Editando Mensagens

Dê dois cliques no nó Inject.

No campo Payload:

* altere o tipo para string;
* escreva:

Olá, Node-RED!

Clique em Done e depois em Deploy.

Execute novamente o fluxo.

---

## Nó Function

O nó Function permite escrever pequenos códigos em JavaScript.

---

## Exemplo simples

Monte o fluxo:

Inject → Function → Debug

Dentro do nó Function, escreva:

```javascript
msg.payload = "Mensagem criada no Function";
return msg;
```

Clique em Done e depois em Deploy.

</details>

---

<details>
<summary> <h2> Exercícios Iniciais </h2> </summary>

### Exercício 1

Crie um fluxo:

Inject → Debug

Faça o Inject enviar:

Bom dia!

---

### Exercício 2

Crie um fluxo que envie:

* seu nome;
* sua turma;
* sua cidade.

---

### Exercício 3

Crie o fluxo:

Inject → Function → Debug

No Function, escreva:

```javascript
msg.payload = 10 + 5;
return msg;
```

---

### Exercício 4

Modifique o exercício anterior para:

* multiplicar dois números;
* dividir dois números.

---

### Exercício 5

Crie um fluxo que exiba:

Hoje estou aprendendo Node-RED!

utilizando o nó Function.

---

### Exercício 6

Crie dois nós Inject:

* um enviando “Ligado”;
* outro enviando “Desligado”.

Conecte ambos ao mesmo nó Debug.

---

### Desafio

Monte um fluxo que:

1. receba um número;
2. some 10;
3. mostre o resultado.

Dica:

Use:

Inject → Function → Debug

</details>

---

## Conclusão

O Node-RED facilita a criação de aplicações e automações através de programação visual. Mesmo usuários iniciantes conseguem criar fluxos simples rapidamente utilizando nós e conexões visuais.
