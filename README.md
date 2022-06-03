# Comandos Git

A partir desse documento, serão exemplificados comandos de Git via Prompt de Comando do Windows.

## 1)	Clone de Repositório

Como primeiro passo deve ser aberto o Prompt de Comando (cmd) e por meio do comando “cd” buscar o diretório desejado.

Para este tutorial, iremos utilizar o repositório público hospedado no GitHub com de url (https://github.com/phporath/git_examples.git). Com o diretório ajustado, para o clone de um repositório remoto para a máquina local deve ser utilizado o seguinte comando:

```
git clone  https://github.com/phporath/git_examples.git
```

Em caso de sucesso o log da operação deve ser o seguinte:

```
Cloning into 'git_examples'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

Agora, para verificar o status do repositório, primeiramente via “cmd”, deve ser acessado o diretório do repositório “git_examples”. Na sequência deve ser utilizado o seguinte comando:

```
git status
```

Após rodar o comando de “git status”, é retornado a mensagem que a branch em ação é a “main”. Além disso, também é informado que não há nada para ser “commitado”.

```
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

## 2)	Criação de nova branch

No passo anterior já vimos que a branch em ação é a “main”, mas para se certificar se existem mais branches nesse repositório é possível lista-los a partir do seguinte comando:

```
git branch
```

Como resultado, deve ser apresentado apenas a branch “main”. Agora para a criação da nova branch de nome “feature01”, deve ser utilizado o seguinte comando:
git checkout -b feature01

Com esse comando, além de criar a nova branch, ela também passa a ser a branch em ação.

## 3)	Adição e commit de novo arquivo
Agora vamos fazer o exercício de adicionar o arquivo “hello_world.py” à branch feature01 a partir do seguinte comando:

```
git add hello_world.py
```

Da mesma forma podemos adicionar a mudança de um arquivo já existente na branch.

```
git add README.md
```

Agora se for utilizada novamente o comando “git status” como resultado poderá ser vista a seguinte mensagem:

```
On branch feature01
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md
        new file:   hello_world.py
```

Dessa forma, após a adição do arquivo, vamos confirmar e salvar alterações por meio do seguinte comando:

```
git commit -m “adicionar arquivo python de Hello World e adicionar modificações no README.md”
```

Esse comando busca todas as alterações feitas na branch que ainda não foram salvas. Veja o log dessa operação:

```
[feature01 f04fc94] adicionar arquivo python de Hello World e adicionar modificações no README.md.
 2 files changed, 126 insertions(+), 1 deletion(-)
 rewrite README.md (100%)
 create mode 100644 hello_world.py
```

## 4)	Enviar alterações da branch para o repositório remoto

Com as alterações realizadas na branch em máquina local, pode-se querer disponibilizar a branch para acesso remoto de outros profissionais. Para isso, deve-se utilizar o seguinte comando:

```
git push origin feature01
```

O sistema poderá retornar duas opções de autenticação, Web Browser ou Personal Access Token. Escolha uma das opções para finalizar o processo. Na sequência é possível ver o log da operação.

```
Select an authentication method for 'https://github.com/':
  1. Web browser (default)
  2. Personal access token
option (enter for default): 1
info: please complete authentication in your browser...
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 2.09 KiB | 1.04 MiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'feature01' on GitHub by visiting:
remote:      https://github.com/phporath/git_examples/pull/new/feature01
remote:
To https://github.com/phporath/git_examples.git
 * [new branch]      feature01 -> feature01
Branch 'feature01' set up to track remote branch 'feature01' from 'origin'.
```

Ao fim desse processo, percebe-se que no GitHub (repositório remoto) existirão duas branches também (main e feature01). 

## 5)	Junção de branches (local)

Primeiramente será necessário ativar a branch principal (main). Para isso, deve ser utilizado o seguinte comando:

```
git checkout main
```

Na sequência, para realizar a junção da branche “feature01” com a “main” na máquina local, basta realizar o seguinte comando:

```
git merge feature01
```

Veja o log da operação:
```
Updating 61154f9..f04fc94
Fast-forward
 README.md      | 126 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++-
 hello_world.py |   1 +
 2 files changed, 126 insertions(+), 1 deletion(-)
 create mode 100644 hello_world.py
```

Agora será necessário a adição do arquivos na branch main. Como é sabido que mais de um arquivo foi criado ou modificado, pode ser utilizado o seguinte comando:

```
git add .
```

Na sequência, assimo como anteriormente, será necessário fazer o commit da alteração.

```
git commit -m "atualizações de arquivos na branch main"
```

Por fim, para enviar as atualizações para o repositório remoto, deve ser novamente utilizado o comando push, mas agora na branch main.

```
git push origin main
```
