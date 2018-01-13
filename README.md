## Resumo de tags do GIT

Adicionando auto complete no terminal:

Opcionalmente, é possível configurar o Terminal para completar os comandos do Git ao pressionarmos a tecla "tab", além de mostrar na linha de comando se a pasta atual está sendo rastreada pelo Git. Para isso é necessário adicionar as seguintes linhas ao arquivo de perfil do usuário para o prompt de comando, habitualmente encontrado na pasta home do usuário com o nome de .bash_profile (ou .bashrc).

Adicione as seguintes linhas ao fim do arquivo:

## Arquivos de configuração para o GIT
parse_git_branch() {

    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'

}

export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
if [ -f /usr/local/git/contrib/completion/git-completion.bash ]; then
    . /usr/local/git/contrib/completion/git-completion.bash
fi

**Adicionando cores na saida do console:**
Abra o arquivo ~/.gitconfig:
```
[color]
  diff = auto
```

## Configure multiple SSH identities for GitBash, Mac OSX, & Linux
**Gerando chave:**
   - ssh-keygen -f ~/.ssh/personalid -C "personalid"

**Crie um arquivo:**
   - ~/.ssh/config file

**Dentro dele set o char para cada dominio ex:**

Host github.com
 HostName github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/rodrigorahman




## Comandos Basicos

**Criando tag:**
```
git tag <nome da tag>
```

**Baixando tag**
```
git checkout <nome da tag>
```

**Comparando Tags:**
```
git diff v0.1 v0.2
```

**Detalhando alterações de um arquivo.**
```
git blame README.md
```


**Listando arquivos controlados pelo git:**
```
git ls-files
```

**Para alterar o editor padrão de mensagens basta criar uma variavel de ambiente EDITOR com o comando que ele pode abrir **


**Para ver os logs e o que foi alterado basta executar:**
```
git whatchanged
```

**Adicionando repositorio remoto:**
```
git remote add <apelido do repositorio remoto: normalmente 'origin'> <url do projeto>
```   


## Branchs

**Para enviar um branch para o repositorio e dizer que ela é igual a nossa local devemos utilizar o comando**
```
git push -u origin design
```

**Isso é importante para quando agente fizer um git pull não precisar ficar especificando qual branch ele deve puxar**

**Quando você quer baixar uma branch do repositorio que ainda você nao tem basta executar o comando**
```
git branch -t      design            origin/design
              <nome da branch>  <Nome da branch remota>
```

**Remover um branch:**
```
git branch -d <Nome da branch>
```

**Listar todas as branchs locais e remotas:**
```
git branch -a
```

Realizando o comando **git checkout -t origin/design**, uma nova branch local chamada design é criada, muda-se para essa branch, copiamos todo o conteúdo da branch remota design do repositório referente ao origin e trackeamos as duas branches.

**Removendo uma branch remota design:**
```
git push origin :design
```


**Verificando se existem branchs novas no repositorio remoto:**

Realizando o comando git fetch origin, podemos verificar todas as atualizações que foram realizadas no repositório referente ao origin.

## Rebase
**Rebase é responsável por integrar uma branch em outra branch**
````
git rebase master desenvolvimento.
````

O comando está pegando todos os comits da branch master e adicionando na branch desenvolvimento um a um

**Em caso de querer abortar o rebase utilizar:**
```
git rebase --abort.
```

**Caso queira ignorar esse comite e ir para o próximo:**
```
git rebase --skip
```



## Merge
```
git merge desenvolvimento
```

Com esse comando o git irá buscar todos os comites de desenvolvimento e jogar dentro da sua branch


## Revert
Para reverter a alteração de um arquivo utilize o checkout ex:
```
git checkout <nome do arquivo>
```
Só funciona quando o arquivo ainda está como untracked (não adicionado -> não foi feito o **git add**)

Caso exista uma brach com o mesmo nome do arquivo que queremos reverter utilize:
```
git checkout -- arquivo
```
O **--** serve para dizer que deve procurar por um arquivo


## Reset

**Caso já tenha adicionado basta rodar o:**
```
git reset HEAD <nome do arquivo>
```
O arquivo mencionado voltará para o estado inicial

**Existem 3 formas de fazer o reset**

A diferença entre essas três opções se refere ao local onde as modificações serão enviadas: com o git reset, as alterações serão enviadas para o Working Directory; com o git reset --soft, para o Index. Já para o git reset --hard, as alterações serão removidas permanentemente.

**Revertendo um commit**
```
git revert <id do commit>
```

## Stash
Stash é um comando que guarda os commits caso precise voltar o código e fazer alguma alteração.

**Para adicionar utilize**
```
git stash
```

**O GIT irá voltar o código antes dessa alteração podendo assim realizar uma correção**

Após feito quero retomar meu código guardado para visualizar um stash utilizo:
```
git stash list
```

Para recuperar um stash basta
```
git stash pop
```
Ele irá retomar o ultimo stash


**Para remover o stash utilize**
```
git stash drop
```


## Bisect
É uma ferramenta do git para buscar um commit, nela você vai dizendo qual commit é bom ou ruim para achar um que interessa
```
git bisect start
git bisect bad HEAD
```
Acima, iniciamos uma sessão de "bisect" e marcamos o commit HEAD como "bad" (ruim), ou seja, indicamos que ele contém o bug o qual queremos encontrar o momento em que foi introduzido.

Agora precisamos marcar qual commit deve ser utilizado como estando OK:
```
git bisect good 02bfc44
```

Podemos testar agora se, nesse ponto, nossa funcionalidade estava OK. Caso não esteja, precisamos marcar o commit atual como "ruim":
```
git bisect bad
```


## Aliases
Para criar um alias basta editar o arquivo **.gitconfig** dentro da home do seu usuário ex:

```
[user]
        name = Rodrigo Silva Rahman de Almeida
        email = dgrodrigo@gmail.com
[core]
        autocrlf = input

[alias]
        st = status

```

Sendo assim para fazer o git status basta eu utilizar git st **(st seria o alias que criamos para status)**

Note que o nosso alias, além de ter ficado grande, pois queremos resumir vários comandos em apenas um, também utiliza os comandos git e o && para realizar a sequência de comandos. Os alias, por padrão, não suportam a execução de outros comandos, como estamos fazendo, porém, é algo possível de ser habilitado. Para isso, basta adicionar uma ! ao começo do comando:
```
[alias]
  envia = !git checkout master && git pull && git checkout desenvolvimento && git rebase master && git checkout master && git merge desenvolvimento && git push
```

## LOG
Para visualizar os logs de uma forma melhor utilize:

```
git log --pretty=oneline
```
Será apresentado de uma forma mais bonita ex:
```
626c1940661b66331b6cd7a495936c3c62030af9 removendo ear pphands-ear-3.21.5-release_RFC-827.ear
a22de9e8e9eafe5775477cceee4fddad141e0155 Alterado as credenciais da msc.
e17cc939740ddf63ca68c8b86fa79d58af75e4f3 alteracao na inclusao da filial no systur
c5480ded20ba31a486ad9744f1494bbb9b8dc712 incluindo pacote portal-fornecedor-ear-1.51.13.ear
aa529d216934e500236f816c4ef3794ae9eee302 Nova versão do Portal do Fornecedor
c5fdbb9cbd79266b2f4a289b244dac9d1a0b71c1 Nova versao do Portal do Fornecedor
5eb0df8ef00d1f7b453e3d16dea115dd2742a4be Nova versao do Portal do Fornecedor
95388843d967602b6fa3b05f9b9a3374dd53dedf alterando cache coherence
27f9497f8a80d039f78ef50e7adca3d19c099545 corrigindo apontamento
a235a15b49dd37831b5a9203645e9f8e3f8faf63 alterando CVC_HOME
b61d40a8ea3ad99619d1dd5b57784abaa0723de0 deploy
```

**Mostrar os arquivos alterados**
```
git log -p

OU

git log -stat
```

## Cherry-Pick
Comando serve para enviar um commit especifico para um branch
```
git cherry-pick 19f0bb7d8b4be8ecd687b48fca301b71b95eab41
```

## Remover do controle de versão arquivos já comitados ##


Caso não tenha feito o commit ainda, utilize:
```
git reset <arquivo-ou-diretório>
```

Caso já tenha realizado um commit, utilize:
```
git rm --cached <arquivo>
git rm -r --cached <diretório>
```

## Recuperando dados do origin ##

***Recuperando a URL***
```
git config --get remote.origin.url
```

***Recuperando todos os dados do repositorio remoto***

```
git remote show origin
```

***Recuperando o hash e recuperando somente 7 caracteres ***
```
git rev-parse --short=7 HEAD
```

