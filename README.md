Git Course:

Adicionando auto complete no terminal:

Opcionalmente, é possível configurar o Terminal para completar os comandos do Git ao pressionarmos a tecla "tab", além de mostrar na linha de comando se a pasta atual está sendo rastreada pelo Git. Para isso é necessário adicionar as seguintes linhas ao arquivo de perfil do usuário para o prompt de comando, habitualmente encontrado na pasta home do usuário com o nome de .bash_profile (ou .bashrc).

Adicione as seguintes linhas ao fim do arquivo:

if [ -f /usr/local/git/contrib/completion/git-completion.bash ]; then
    . /usr/local/git/contrib/completion/git-completion.bash
fi
GIT_PS1_SHOWDIRTYSTATE=true

PS1='\u@\h:\w $(__git_ps1 "(%s)")\$ '


Criando tag:
  - git tag <nome da tag>

Baixando tag
  - git checkout <nome da tag>

Comparando Tags:
  - git diff v0.1 v0.2

Detalhando alterações de um arquivo.
  - git blame README.md
  
  
Listando arquivos controlados pelo git:
    git ls-files
    
Para alterar o editor padrão de mensagens basta criar uma variavel de ambiente EDITOR com o comando que ele pode abrir 


Para ver os logs e o que foi alterado basta executar:
    git whatchanged
    
Adicionando repositorio remoto:
    git remote add <apelido do repositorio remoto: normalmente 'origin'> <url do projeto>