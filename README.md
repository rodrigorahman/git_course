Git Course:

Adicionando auto complete no terminal:

Opcionalmente, é possível configurar o Terminal para completar os comandos do Git ao pressionarmos a tecla "tab", além de mostrar na linha de comando se a pasta atual está sendo rastreada pelo Git. Para isso é necessário adicionar as seguintes linhas ao arquivo de perfil do usuário para o prompt de comando, habitualmente encontrado na pasta home do usuário com o nome de .bash_profile (ou .bashrc).

Adicione as seguintes linhas ao fim do arquivo:

### Arquivos de configuração para o GIT
parse_git_branch() {

    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'

}

export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
if [ -f /usr/local/git/contrib/completion/git-completion.bash ]; then
    . /usr/local/git/contrib/completion/git-completion.bash
fi



### Comandos Basicos

Criando tag:
  - git tag <nome da tag>

Baixando tag
  - git checkout <nome da tag>

Comparando Tags:
  - git diff v0.1 v0.2

Detalhando alterações de um arquivo.
  - git blame README.md
  
  
Listando arquivos controlados pelo git:
  - git ls-files
    
Para alterar o editor padrão de mensagens basta criar uma variavel de ambiente EDITOR com o comando que ele pode abrir 


Para ver os logs e o que foi alterado basta executar:
   - git whatchanged
    
Adicionando repositorio remoto:
   - git remote add <apelido do repositorio remoto: normalmente 'origin'> <url do projeto>
   
   
   
### Branchs

Para enviar um branch para o repositorio e dizer que ela é igual a nossa local devemos utilizar o comando
   - git push -u origin design
   
Isso é importante para quando agente fizer um git pull não precisar ficar especificando qual branch ele deve puxar

Quando você quer baixar uma branch do repositorio que ainda você nao tem basta executar o comando
   - git branch -t      design            origin/design
              <nome da branch>  <Nome da branch remota>
              
Remover um branch:
   - git branch -d <Nome da branch>
   
Listar todas as branchs locais e remotas:
   - git branch -a
   
Realizando o comando git checkout -t origin/design, uma nova branch local chamada design é criada, muda-se para essa branch, copiamos todo o conteúdo da branch remota design do repositório referente ao origin e trackeamos as duas branches.

Removendo uma branch remota design:
   - git push origin :design
   
   
Verificando se existem branchs novas no repositorio remoto: 
   - Realizando o comando git fetch origin, podemos verificar todas as atualizações que foram realizadas no repositório referente ao origin.