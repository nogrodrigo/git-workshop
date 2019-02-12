# Git e Github

Sejam bem vindos ao material do workshop de git e github. Aqui estarão a explicação de conceitos do git,
comandos que frequentemente são utilizados e muito mais.

## Aprenda Antes

Você precisará saber alguns comandos básicos do Terminal Linux para conseguir ter um fluxo de aprendizado interessante no Workshop. Logo, eu deixarei aqui uma lista de comandos e o que eles fazem.

A primeira observação a ser feita é o diretório padrão que o terminal se localizará quando você abri-lo. Abra o terminal e veja que tem algo parecido com `Username@PC_Name:~$`.

O `~` indica o diretório home. É onde por padrão o terminal começará.

Sabendo isso, agora queremos listar os diretórios e arquivos do diretório home. Para fazer isso basta digitar `ls`

Listado os diretórios e arquivos, podemos acessar outras pastas de `~` digitando `cd nome_diretório`. Para voltar para o diretório anterior, basta escrever `..`

Já o comando `mkdir nome_pasta` criará uma nova pasta enquanto o comando `rmdir nome_pasta` deletará a pasta de nome `nome_pasta`.

Para arquivos, o comando `touch nome_arquivo.extensão_arquivo` criará o arquivo enquanto `rm nome_arquivo.extensão_arquivo` deletará o arquivo.

A título de curiosidade, o comando `rm nome_pasta -rf` é equivalente a `rmdir`. Além disso, você não precisará digitar o nome do arquivo por completo. Ao digitar algumas letras e apertar `TAB`, o terminal completa para você na maioria dos casos. Basicamente são esses os comandos necessários para você conseguir prosseguir bem no Workshop de Git.

## Git

Podemos definir Git como um controle de versão. Parece uma definição válida, mas para quem não sabe o que é um controle de versão, essa explicação ainda parece muito vaga. Por isso precisamos primeiro definir o que é um controle de versão.

Então o que é um controle de versão? Um controle de versão é um sistema que grava as diferentes versões dos arquivos de um projeto durante o passar do tempo. Assim o utilizador do sistema pode caminhar entre essas versões caso ele queira, veja que ocorreu alguma falha ou não gostou da nova implementação no projeto.

Fixado esse conceito, agora podemos entender melhor o que é o Git.

## Sistema Git

O Git funciona com um sistema de snapshots. A cada versão, ele guarda todos os estados de todos os arquivos daquele momento. Por exemplo, na versão 1 foi criado o arquivo square.py e circle.py. Logo o Git irá salvar os estados desses arquivos na primeira versão. Caso seja feito alguma alteração em circle.py, ele irá guardar o novo estado desse arquivo na versão 2 e terá um link simbólico para o ultimo estado de square.py. Observe que para casos em que nao foram feitas alterações, ele nao salva de novo o estado do arquivo.

## Ciclo de vida dos status dos arquivos

Os arquivos, quando gerenciados pelo Git, Tem quatro estados:

1. **Untracked**: ocorre quando o arquivo existe no repositório, mas não é reconhecido pelo Git para versionamento.
2. **Unmodified**: é reconhecido pelo Git e não fo alterado da versão anterior para a futura nova versão.
3. **Modified**: é reconhecido pelo Git e sofreu alterações.
4. **Staged**: foi alterado e esta pronto para ser lançado na próxima versão.

## Configurar o Git

Precisamos definir alguns dados pessoais. Assim o Git saberá o autor e o e-mail do criador daquela versão. Além disso também saberá qual editor de texto você utiliza para escrever suas mensagens de versão.

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

A opção `--wait` é para o Git esperar ate que o arquivo de mensagem seja fechado para criar a versão.

**Obs**.: Foram utilizados termos como versão em vez de commit para não ficar muito confuso.



