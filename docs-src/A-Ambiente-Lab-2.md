# Lab 2: Github

Nesse laboratório iremos trabalhar com o uso do git de forma colaborativa.

### Clonando

!!! warning "Individual"
    Todos do grupo devem realizar de maneira individual!

Uma vez criado o **fork** e adicionado os colegas vocês deverão clonar o repositório para o computador de vocês com o comando:

``` bash
$ git clone URL_DO_FORK
```

??? note "URL_DO_FORK"
    A URL do seu fork pode ser obtida pelo botão 'Clone or Download' do github: 
    ![](figs/A-Transistores/url-fork.png)

!!! linux 
    O símbolo `$` indica que é um comando para ser executado no 
    terminal do Linux (`bash`), mas ele não deve fazer parte do comando.
    No caso anterior, o comando a ser colado deve ser: `git clone URL_DO_FORK`.
    
!!! Linux
    Para abrir o terminal: `meta`+`t` 

## Referenciando a raiz

Para começar será necessário atualizar o fork do repositório que vocês criaram, com novos dados que serão colocados no repositório da disciplina. Uma vez clonado o repositório, você deve entrar na pasta via o terminal:

``` bash
$ cd Z01.1-NomeDoGrupo
```

Estando na pasta do repositório precisamos agora indicar para o repositório original na qual o repositório que deu origem a esse fork, para isso devemos executar a seguinte linha de código: 

``` bash
$ git remote add upstream https://github.com/insper/Z01.1
```

Para verificar se deu certo, execute:

``` bash
$ git remote -v
```

E deve aparecer além do link para o repositório de vocês a referência ao repositório original:

``` bash
upstream	https://github.com/insper/Z01.1 (fetch)
upstream	https://github.com/insper/Z01.1 (push)
```

!!! tip 
    Dúvidas?
    
    - https://gist.github.com/CristinaSolana/1885435
    - https://help.github.com/articles/syncing-a-fork/

## Sincronizando com upstream

!!! warning "Apenas mediador"
    Essa etapa deve ser realizada apenas pelo mediador do projeto!

Para atualizar o repositório do grupo de vocês com as novas atualizações inseridas no repositório da disciplina basta executar:

``` bash
$ git fetch upstream
```

Agora precisamos realizar um merge desse branch (que contém as atualizações do repositório da disciplina) com o master:

``` bash
$ git checkout master
$ git merge upstream/master
```

Precisamos submeter essa atualização para o repositório remoto a fim de todos do grupo terem acesso a versão mais nova.

``` bash
$ git push origin master
```


## Adicionando nomes ao `INTEGRANTES.json`

!!! warning "Individual"
    Deve ser realizado individual por todos do grupo.

!!! tip
    Antes de começar, atualize seu repositório com o remote:
    
    ```bash
    $ git pull origin master
    ```
    
Nesse etapa cada integrante do grupo irá editar um arquivo no seu computador e realizar um pull-request para o repositório do grupo. Para isso seguiremos as etapas a seguir:

1. Gerar mudanças no repositório local
1. Criando um branch com as mudanças 
1. Enviar mudanças para o repositório remoto
1. Gerar pull-request

### Atualizando `INTEGRANTES.json`

**Cada integrante** do grupo deve editar o documento com na raiz do projeto com nome `INTEGRANTES.json` 
e adicionar a esse arquivo o seu nome, e-mail (insper) e usuário gituhb. Conforme o exemplo a seguir:

``` json
{
  "aluno-1": {
    "nome": "Rafae Corsi",
    "email-insper": "rafael.corsi@insper.edu.br",
    "user-github": "rafaelcorsi"
  },
```

!!! warning 
    Uma única pessoa não deve editar o documento com todos os nomes.
    
    - Cada um deve realizar individualmente em seu computador.

### Testando

A disciplina utiliza uma técnica chamada de ["Test Driven Development"](https://en.wikipedia.org/wiki/Test-driven_development) onde utilizamos de teste unitário e de integração para validarmos se a implementação está correta. 

Nesse caso, iremos utilizar um script para validar se o arquivo `.json` editado está com formatação correta. Para isso, execute no terminal:

```bash
$ ./Projetos/A-AmbienteDesenvolvimento/testeAmbienteDesenvolvimento.py
```

Você deve obter:

```
➜  Z01.1 git:(master) ✗ ./Projetos/A-AmbienteDesenvolvimento/testeAmbienteDesenvolvimento.py
===================================================
[OK] GRUPO.json
===================================================
===================================================
[OK] INTEGRANTES.json
===================================================
```

!!! warning
    Se obter **[FAIL]** em algum dos dois arquivos, editar o arquivo e executar a etapa anterior novamente. **Só continuar se não tiver falhas!**

### Criando um branch para fazer o commit.

A fim de realizarmos um pull-request ao mediador do projeto é preciso salvarmos essas modificações em um novo branch. O comando a seguir faz isso:

``` bash
$ # criando um novo branch
$ git checkout -B $NOME
```

!!! tip "git"
    Substitua nos comandos o termo `$NOME` pelo seu nome.

Agora vamos fazer um commit com o seu nome nesse novo branch:

``` bash
$ git add INTEGRANTES.json
$ git commit -m "Adicionado meu $NOME ao arquivo"
```

Será necessário enviarmos esse branch ao servidor (github) antes de realizarmos o `pull-request`:

``` bash
$ # enviando o branch para o repositório remoto
$ git push origin $NOME
```

!!! tip "git"
    Esse comando diz para o git que é para enviar o branch `$NOME` 
    para o repositório remoto `origin`. Aquele que aparece no comando `$ git remote -v`.

### Realizando pull-request

Uma vez enviando o branch para o servidor, podemos via a interface **web** do `github` realizar o `pull-request`. Abra a pagína do github do repositório do seu grupo. 

!!! tip "git"
    Se tiver instalado o software [`hub`](https://github.com/github/hub) digite na linha de comando: `$ hub browser`.

Vamos agora gerar o pull-request na interface do github, de forma similar ao exemplo a seguir:

!!! warning
    Cuidado! Escolher o seu repositório no momento de realizar o pullrequest.

![](figs/B-CI/pullrequest.gif)

!!! tip
    Ao realizar o PR, o `Travis` irá verificar o seu arquivo com o mesmo teste que você executou anteriormente, esse será o fluxo geral da disciplina, onde o mesmo teste é realizado local na máquina de cada aluno e remoto automaticamente pelo Travis.

## Aceitando pull-request

!!! warning "Apenas o mediador"
    Essa etapa deve ser realizada apenas pelo mediador do projeto!

O **mediador** do projeto deve revisar os pull-requests (e corrigir eventuais erros de merge) 
e aceitar ou negar o pedido. 

![](figs/B-CI/pullrequest-accept.gif)
