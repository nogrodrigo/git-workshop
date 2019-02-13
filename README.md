# Git e Github

Sejam bem vindos ao material do workshop de git e github. Aqui estarão a explicação de conceitos do git, comandos que frequentemente são utilizados e muito mais.

## Aprenda Antes

Você precisará saber alguns comandos básicos do Terminal Linux para conseguir ter um fluxo de aprendizado interessante no Workshop. Logo, eu deixarei aqui uma lista de comandos e o que eles fazem.

A primeira observação a ser feita é o diretório padrão que o terminal se localizará quando você abri-lo. Abra o terminal e veja que tem algo parecido com `Username@PC_Name:~$`.

O `~` indica o diretório home. É onde por padrão o terminal começará.

Sabendo isso, agora queremos listar os diretórios e arquivos do diretório home. Para fazer isso basta digitar `ls`

Listado os diretórios e arquivos, podemos acessar outras pastas de `~` digitando `cd nome_diretório`. Para voltar, basta escrever `..`

O comando `mkdir nome_pasta` criará uma nova pasta e o `rmdir nome_pasta` deletará a pasta de nome `nome_pasta`.

Para arquivos, o comando `touch nome_arquivo.extensão_arquivo` criará o arquivo enquanto `rm nome_arquivo.extensão_arquivo` deletará.

A título de curiosidade, o comando `rm nome_pasta -rf` é equivalente a `rmdir`. Além disso, você não precisará digitar o nome do arquivo por completo. Ao digitar algumas letras e apertar `TAB`, o terminal completa para você na maioria dos casos. Basicamente são esses os comandos necessários para você conseguir prosseguir bem no Workshop de Git.

## Git

Podemos definir Git como um controle de versão. Parece uma definição válida, mas para quem não sabe o que é um controle de versão, essa explicação ainda parece muito vaga. Por isso precisamos primeiro definir o que é um controle de versão.

Então o que é um controle de versão? Um controle de versão é um sistema que grava as diferentes versões dos arquivos de um projeto durante o passar do tempo. Assim o utilizador do sistema pode caminhar entre essas versões caso ele queira, veja que ocorreu alguma falha ou não gostou da nova implementação no projeto.

Fixado esse conceito, agora podemos entender melhor o que é o Git.

## Sistema Git

O Git funciona com um sistema de snapshots. A cada versão, ele guarda todos os estados de todos os arquivos daquele momento. Por exemplo, na versão 1 foi criado o arquivo square.py e circle.py. Logo o Git irá salvar os estados desses arquivos na primeira versão. Caso seja feito alguma alteração em circle.py, ele irá guardar o novo estado desse arquivo na versão 2 e terá um link simbólico para o ultimo estado de square.py. Observe que para casos em que nao foram feitas alterações, ele nao salva de novo o estado do arquivo.

## Commit

Um commit é uma versão que guarda os estados de todos arquivo daquele momento. Esse conceito é muito importante para as proximas explicações. Pois em vez de utilizar a palavra versão, utilizaremos commit e seus derivados da lingua portuguesa com inglesa tipo "Commitar", "Commitou", etc.

## Ciclo de vida dos status dos arquivos

Os arquivos, quando gerenciados pelo Git, Tem quatro estados:

1. **Untracked**: ocorre quando o arquivo existe no repositório, mas não é reconhecido pelo Git para versionamento.
2. **Unmodified**: é reconhecido pelo Git e não fo alterado do commit anterior para o commit a ser criado.
3. **Modified**: é reconhecido pelo Git e sofreu alterações.
4. **Staged**: foi alterado e esta pronto para ser **commitado**.

## Configurar o Git

Precisamos definir alguns dados pessoais. Assim o Git saberá o autor e o e-mail do criador daquele commit. Além disso também saberá qual editor de texto você utiliza para escrever suas mensagens de commit.

Para definir o nome:
```shellscript
$git config --global user.name "meu_nome"
```

Para definir o e-mail:
```shellscript
$git config --global  user.email "meu_email"
```

Para definir o editor:
```
$git config --global core.editor "comando_do_editor"
```

Nesse caso, eu utilizo o [Visual Studio Code](https://code.visualstudio.com/) e o comando para abri-lo no terminal é `code nome_arquivo` ou `code .` para todo o diretório.

Logo a configuração seria:
```
$git config --global core.editor "core --wait"
```

A opção `--wait` é para o Git esperar ate que o arquivo de mensagem seja fechado para criar o commit.

Quando você quiser ver as configurações, basta utilizar o comando `git config --list`.

Observe a opção `--global`. Ela usará aquelas configurações para todo projeto Git criado naquela máquina. Para definir configurações ao projeto local, basta utilizar a opção `--local`.

## Iniciando e usando o git

Feito a configuração, agora devemos acessar a pasta em que queremos versionar com o git e depois utilizar o comando `git init`. Feito isso se você digitar `git status`, terminal retornará uma mensagem dizendo que não tem nenhum commit e nada para enviar para um commit. Quando você criar um arquivo e digitar o mesmo comando, o git agora informa que existe um arquivo novo, porém ainda não é reconhecido por ele. Qual o status desse arquivo? Untracked é a resposta correta. Vamos adiciona-lo com o comando `git add nome_arquivo`. E agora, qual o status do arquivo? Se você respondeu staged, acertou. O arquivo esta pront para ser commitado e portanto agora você pode criar o commit digitando `git commit -m "mensagem_commit"`.

Veja a opção `-m`. Ela indica que você passará uma mensagem para o commit. É sempre bom que essas mensagens tenha escrito algo breve e que indique o que foi feito naquela versão. Existem modelos de mensagem de commit e cada empresa escolhe o melhor para seus projetos.

Se você preferir digitar a mensagem em seu editor de texto configurando no início, digite apenas `git commit`. Isso abrirá o editor de texto. Quando você fechar o arquivo, o commit será criado.

Criado o commit, agora podemos visualizar a lista de commits com `git log`. Caso deseje filtrar por quantidade, use `git log -número`. Se preferir algo menos poluído, escreva `git log --oneline`. Agora se quiser buscar por autor, digite `git log --author='nome_autor'`.

Existem diversas outras opções que você pode passar para o comando `git log`. Para saber mais, olhe a [documentação](https://git-scm.com/docs/git-log).

Agora se você desejar ver quais foram as mudanças feitas naquele commit? Observe que ao digitar `git log`, aparecem os diversos commits feitos e todos tem um hash(varias letras e números de forma aleatoria). Esse hash será importante para você realizar algumas operações no Git. Entre elas, ver o que foi alterado naquele commit. Para ver as mudanças feitas, basta digitar `git show hash_commit`.

Mas como ver as diferenças de um arquivo que esta em estado de modified. É necessário apenas digitar `git diff nome_arquivo`.

## Revertendo

Para entender a reversão bem, é necessário primeiro estar sabendo o ciclo de vida dos status dos arquivos. Revise rapidamente caso não esteja familiarizado.

### Revertendo arquivos adicionado recentemente

Suponha que você criou um arquivo. Agora o status dele é de Untracked. Adicionando ele com `git add nome_arquivo`, ele passa a ser conhecido pelo Git, mas ainda não esta em nenhuma versão. Para reverte, ou seja, coloca-lo no status de Untracked de novo, basta digitar `git rm --cache nome_arquivo`

### Revertendo arquivos em status de modified

Suponha agora que um arquivo seu esta em status de modified. Você olhou para as alterações feita nele com `git diff nome_arquivo` e não gostou. Para reverter, basta escrever `git checkout nome_arquivo`.

### Revertendo arquivos em status de staged

Agora seu arquivo esta pronto para ser commitado, mas de novo você verificou com `git diff nome_arquivo` e não gostou muito do que foi feito. Para voltar, basta digitar `git reset HEAD nome_arquivo`. Feito isso, o arquivo voltará ao status de modified e assim você poderá usar o comando da seção acima.

## Revertendo Commit

Existem três formas de reverter um commit. As três se diferenciam pelo status que elas colocarão os arquivos alterado naquele commit.

1. `--soft`: O commit será desfeito e os arquivos estarão prontos para serem commitados de novo.
2. `--mixed`: O commit será desfeito e os arquivos estarão com status de modified.
3. `--hard`: O commit será eliminado totalmente.

Para desfazer um commit, digite `git reset [--soft|--mixed|--hard] hash_commit_anterior`.

**Obs**.: Não é recomendado utilizar o `--hard`, pois isso fará com que o commit morra e todas as alterações feitas nele sejam perdidas para sempre. Tenha bastante certeza do que quer fazer ao utiliza-lo.

## Branch

Um branch é um ponteiro móvel para um commit. Ele permite que nós trabalhemos em novas features, correções de bug, etc em paralelo ao desenvolvimento principal. Isso possibilita um melhor fluxo de trabalho em equipe.

O comando `git branch nome_branch` criará umm novo branch. caso você queira saber os branchs criados, `git branch` irá lista-los. Enquanto `git branch -D nome_branch` deletará o branch. Para mudar para o branch desejado, digite `git checkout nome_branch`.

Tenha em mente que o trabalho desenvolvido em cada branch é distinto. Ou seja, caso você realize um commit no branch `testing` e depois mude para o branch `master`, o commit criado em `testing` não estará no branch `master`. Então o comando `git checkout testing` realiza duas operações:

1. Muda para o branch `testing`
2. Carrega as mudanças daquele branch ou remove as feitas no branch que você se encontrava antes.

## Merge e Rebase

Agora se quisermos juntar os commits de um branch com outro? Para isso existe o `merge` e o `rebase`. Os dois chegam ao mesmo objetivo, porém com abordagem diferente.

O `merge` irá criar um novo commit. Esse commit contem commits do branch merged não feitos no branch atual e vice-versa. A vantagem de utiliza-lo é que ele nao bagunça o histórico, mas sua desvantagem é criar um novo commit apenas para juntar as alterações de um branch com o outro.

Já o `rebase` moverá todos os commits feito no branch rebased para frente do branch atual. A vantagem de utiliza-lo é fato de que ele nao cria um novo commit, porém ele quebra a ordem cronológica dos commits já que move os commits para frente.

Suponha que no branch `testing` foram feitas alterações e elas foram commitadas. Agora você muda para o branch `master` e decide criar um merge do `testing` e `master`. Para fazer isso, digite `git merge testing`. Em uma situação em que se prefira o rebase, basta digitar `git rebase testing`.

## Referências

[Curso de Git na Udemy](https://www.udemy.com/git-e-github-para-iniciantes/)
[Documentação do Git](https://git-scm.com/docs)
[ProGit Book](https://git-scm.com/book/en/v2)
