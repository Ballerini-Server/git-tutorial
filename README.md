# Tutorial de Git

Esse é um tutorial para aqueles que não sabem nada sobre git, o intuito desse repositório é explicar o básico sobre como manipular arquivos no git e como fazer commit/push/pull requests

#### Disclaimer

Só gostaria de lembrar de tomar cuidado quando falamos de git e github, apesar de serem usadas em conjunto, são duas coisas diferentes, git é um *sistema de controle de versões*, muito usado para desenvolvimento de softwares; Já o github é uma *plataforma de hospedagem de código* que usa git para controle de versão;

## Instalando o git

Antes de tudo, você precisa é ter o git instalado, verifique se ele está instalado com o seguinte comando:

```
git --version
```

Ao fazer isso deve aparecer a versão do git que foi instalada, no meu caso, essa foi a resposta, mas no seu pode ser diferente, o importante é aparecer "git", "version" e um número:

```
git version 2.30.0.windows.2
```

Caso não apareça nada, achei esse link da [hostinger](https://www.hostinger.com.br/tutoriais/tutorial-do-git-basics-introducao) mostrando como instalar nos 3 principais sistemas operacionais (Mac, Windows e Debian/Ubuntu que são 2 versões de Linux), para se certificar que o git está instalado corretamente, reinicie o terminal (feche o powershell/cmd/terminal (no Mac)/bash(do Linux)/... depois abra-o novamente) e rode o comando que mostrei acima.

## Configurações iniciais

Após fazer a instalação, você precisa configurar o seu git, para que cada commit seja identificado, e para isso rode os dois próximos comandos:

```
git config --global user.name "Fulano de Tal"
git config --global user.email fulanodetal@exemplo.br
```

Esses comandos são para a configuração do nome da pessoa que estará fazendo commit e também o e-mail, é usado aspas no primeiro caso para que o git entenda que é um texto só, caso contrário, o que seria registrado no exemplo seria apenas "Fulano" como user.name, e não "Fulano de Tal".
Imagino que vocês perceberam que coloquei "--global" junto com os comandos de configuração de usuário, isso porque você também pode usar a flag "--local", assim, o repositório que você está programando vai entender que você quer usar identificações diferentes pra fazer os commits, nunca usei, mas provavelmente seja usado para representações em empresas. 

Quase pronto, tem mais uma configuração que você deve verificar, por favor digite o comando a seguir:

```
git config --get init.defaultbranch
```

Eu tive a seguinte resposta

<img src="./assets/gitbranch.png" width="500px">

### Leve tangente sobre Branchs

Branchs são, basicamente, uma forma do seu código seguir dois caminhos diferentes, por exemplo: 
- O meu programa está rodando com MySQL como banco de dados, mas quero ver se é muito complicado migrar para Postgres, então vou fazer uma branch nova aqui para fazer esse teste.

Criando uma nova branch, o seu código passa a ter dois caminhos, e você pode ir trabalhando nesses caminhos de forma isolada, sem que um caminho afete o outro;
Uma outra analogia para branch são jogos online competitivos, é comum que nos jogos competitivos, existam mais de um servidor (o servidor de testes, o servidor público e o servidor onde acontecem as competições oficiais), e cada servidor está rodando uma versão diferente do jogo, o servidor de testes provavelmente é o mais avançado, e quando os testes são finalizados, esse 'código novo' é mandado para o servidor público, uma vez que o jogo está rodando bem também no servidor público por um tempo, é atualizado o servidor competitivo.

### Configurando Branch principal

Espero que tenham entendido um pouco sobre branchs, mas espero que não tenham preocupações com relação a isso, no começo, isso pode ser um pouco chato de trabalhar, para evitar problemas futuros, vamos voltar e fazer uma alteração nas configurações do git, vocês viram que o meu git está com a branch principal como "master", isso é um problema porque hoje em dia o GitHub quando cria um repositório, usa "main" como branch principal, mas não é difícil de resolver, vamos fazer o mesmo que fizemos com nome e email dos commits, só digitar o seguinte comando:

```
git config --global init.defaultbranch main
```

E vamos conferir se deu tudo certo com o mesmo comando que usamos antes;

```
git config --get init.defaultbranch
```

<img src="./assets/gitbranchmain.png" width="500px">

Pronto, agora podemos finalmente fazer commits/pushs sem nos preocuparmos com os erros mais comuns.

## Iniciando um repositório

Para iniciar um repositório git, basta digitar o comando `git init`, que ele vai criar uma pasta no seu projeto com nome de ".git", e vai começar a se preocupar com as alterações que são feitas no seu projeto.

<img src="./assets/gitinit.png" width="500px">

## Observação

Estou usando o vscode como meu editor desse projeto, e vou mandar fotos de como o 'Source Control' do vscode mostra para nós o que está acontecendo no git, imagino que assim fique mais fácil para que todos entendam o que está acontecendo.

## Changes/Stage & Commit

### Changes

Sempre que o seu código está diferente do seu último commit, o git entende que houve uma alteração, essa alteração pode ser, basicamente: Um arquivo foi criado, um arquivo sofreu uma alteração, um arquivo foi deletado, e essas alterações ficam na lista de Changes do seu repositório, uma forma simples de você verificar essas alterações, é você digitar o comando `git status` no seu terminal preferido;

<img src="./assets/gitstatus1.png" width="500px">

Nesse projeto, você pode ver que eu tenho um arquivo e uma pasta "Untracked" com o nome de README.md, e a pasta "assets", os arquivos "Untracked são arquivos/pastas que ainda não existiam antes no projeto, e agora existem.

No vscode, ele mostra assim:

<img src="./assets/gitstatus1vscode.png" width="500px">

Os arquivos *Untracked* ficam com um 'U' do lado, e também mostra o caminho onde encontrar esse arquivos (note que todas as imagens tem uma palavra "assets" do lado, isso indica que essas imagens são encontradas na pasta assets);

### Stage

Um commit é quando você salva uma alteração no seu projeto, quando o projeto como um todo tem uma nova versão do código, mas nem sempre você quer que todas as alterações que você fez sejam salvas imediatamente nessa nova versão, porque algumas funcionalidades novas ainda não estão concluídas, é pra isso que serve o *Stage*.

Vamos adicionar a pasta assets ao Stage para ver o que acontece, para adicionar a pasta, você só precisa digitar `git add assets` vamos ver no terminal e no vscode o que acontece agora, `git status`;

<img src="./assets/gitstatusassets.png" width="500px">
<img src="./assets/gitstatusassetsvscode.png" width="500px">

Veja que agora no terminal aparece um novo grupo de arquivos, os arquivos que foram adicionados ao Stage tem o título "Changes to be committed", cada arquivo mostrado tem um texto antes "new file:" indicando que o arquivo foi recém adicionado, e não existia antes no projeto, na parte visual do vscode, agora tem também uma nova lista de "Staged Changes" que indicam a mesma coisa que o terminal (arquivos que estão prontos para ser commitados), também esse arquivos tem a letra 'A' no lado, indicando que estão sendo adicionados ao projeto.
Também veja que o README.md não teve nenhuma alteração, ele continua igual a última foto.

### Commit

Vamos fazer finalmente um *Commit*, digite no terminal:

```
git commit -m "Adicionando fotos da pasta assets"
```

Sempre que fazemos um commit passamos a flag -m e entre áspas uma descrição do que foi feito, essa descrição deve ter menos de 50 caracteres, por isso existem alguns padrões de como escrever essas mensagens, e também de quais arquivos você faz commit, pois você não consegue descrever mais de uma ação, por exemplo: "Criei rota de autenticação/criação de usuário, e rota de listagem de serviços", essa mensagem é muito grande, e dependendo das ações que fez, podem te levar a fazer várias abreviações ao ponto da mensagem não ser compreendida, mas não vou me extender mais ainda nesse assunto hoje, e vamos o que o git nos mostra com o comando `git status` novamente

<img src="./assets/gitstatus2.png" width="500px">

<img src="./assets/gitstatus2vscode.png" width="500px">

Veja que os arquivos da pasta assets não estão mais visíveis como alterados, isso porque eles foram commitados, ou seja, foram salvos em uma nova versão do projeto.
Agora só o que aparece é o README.md da forma que tínhamos antes, vamos fazer um commit adicionando ele, para isso, lembrem-se: vamos adicionar o arquivo ao *Stage* com `git add README.md`e depois vamos fazer um commit com `git commit -m 'Adicionando README.md'`, e vamos ver novamente o que o git nos mostra com `git status`;

<img src="./assets/gitstatus3.png" width="500px">

<img src="./assets/gitstatus3vscode.png" width="500px">

Absolutamente nada, o nosso projeto está atualizado, com as últimas alterações feitas até agora, porém, percebam que eu ainda não terminei de fazer esse tutorial, e ainda estou adicionando fotos e mensagens no README.md, vamos ver o que aparece com essas alterações novamente `git status`;

<img src="./assets/gitstatus4.png" width="500px">

<img src="./assets/gitstatus4vscode.png" width="500px">

Com relação as novas imagens, não tem nenhuma mudança, elas estão marcadas como *Untracked* com o 'U' do lado, porém o nosso README.md está diferente, Ele está num novo campo "Changes not staged for commit", marcado com o 'M' do lado, isso indica que ele foi modificado, tanto é, que no terminal aparece o texto "modified:". 
Vamos dessa vez adicionar todos os arquivos juntos no próximo commit, e existe um comando pra isso:

```
git add .
```

Usar o "." no final indica que você está adicionando tudo que está dentro da nossa pasta principal, uma espiadinha com `git status`novamente:

<img src="./assets/gitstatus5.png" width="500px">

<img src="./assets/gitstatus5vscode.png" width="500px">

No terminal, vejam que tudo é muito parecido, todos os arquivos agora estão em "Changes to be committed", a novidade é que o README.md está marcado como "modified:", no vscode aparecem todos os arquivos no campo "Staged Changes", e ao fazer o commit, todos sairão de lá, e o projeto estará em uma nova versão, `git commit -m "Último commit"`, vou deixar essa imagem mostrando o que aparece quando você faz o commit;

<img src="./assets/gitcommit.png" width="500px">

Vejam, 7 arquivos foram salvos (eu coloquei algumas imagems a mais), 31 linhas inseridas, 3 linhas deletadas (eu fiz algumas alterações nesse texto também, que vovês só vão perceber se baixarem o projeto, e começarem a voltar nos commits);

Por fim, existe o comando `git log` que mais mostrar o que aconteceu no seu projeto ao longo do tempo, vamos dar uma olhada no nosso projeto

<img src="./assets/gitlog.png" width="500px">

O histórico do git me mostra que a primeira coisa que fiz foi um commit com o nome de "Adicionando fotos da pasta assets", num Domingo ("Sun" de Sunday) no dia 7 de Março (Mar 7) as 09:42:02 (horas:minutos:segundos) de 2021 com o fuso-horário -0300 (indicando -03:00)

## Push/Pull

Entendo que possa ser contra-intuitivo de início, mas *PUSH* é quando você quer *EMPURRAR* o seu código para algum lugar, e *PULL* é quando você quer *PUXAR* o código de algum lugar, mas juro que a culpa não é minha, pois o git foi feito em inglês. E é importante enteder esses conceitos, mas o que seria esse *LUGAR*?

### Remote

Esse Lugar é chamado pelo git de *REMOTE*, e ele pode ser qualquer local: o servidor privado da sua empresa, o github, o servidor onde o seu programa está ativo, como DigitalOcean, Vercel, AWS, etc.

Vamos criar um repositório no github, e fazer um PUSH para ele;

<img src="./assets/newrepository.png" width="500px">

Como configurações no github, eu deixei ele como repositório Privado, e selecionei para criar um README.md, outras opções importantes é sobre adicionar um .gitignore e uma licença

#### Tangente sobre .gitignore e license

* .gitignore: É um arquivo que vai definir quais pastas ou arquivos o git não deve se preocupar, pois são informações desnecessárias para o repositório de uma forma geral, alguns exemplos de arquivos a serem ignorados pelo git são:
    * node_modules: É uma pasta usada no nodejs (javascript), onde todas as bibliotecas ficam ali, dentro da pasta do seu projeto, e como ela pode ter muitas, mas muitas informações, ela é ignorada, e no momento de alguém copiar o projeto, esse alguém deve instalar as dependências com algum comando específico do node;
    * .env: É um arquivo que vai definir as variáveis de ambiente, e essa variáveis são geralmente sensíveis, exemplos de variáveis que são guardadas nesse arquivo: chave de acesso a serviços externos (AWS para envio de e-mails (SES) ou para guardar arquivos (S3 bucket));
    * Configurações de acesso aos bancos de dados: Apesar de essas informações também poderem estar em .env, algumas bibliotecas as vezes usam suas próprias formas de conectar no banco de dados, e se for uma conexão como a conexão no mongodb.com por exemplo, é importante que o texto não esteja explícito no seu código, pois quem tiver acesso ao seu projeto, também vai ter acesso ao banco de dados;
* Licença: Não vou me aprofundar nesse tema, mas licença é o que vai definir quem e como podem usar o seu código, algumas licenças são de uso aberto permitindo que você use/copie/altere/venda o seu projeto e a interação do seu projeto com esse programa, outras vão te dar limitações em um ou outro ponto, vou deixar esse vídeo do [Código Fonte TV](https://www.youtube.com/watch?v=fPfzp6ov2bQ) para dar um pouco mais de informações, mas ainda recomendo que pesquise a parte sobre; 

#### Remote Add

Agora o nosso repositório está criado no github, e temos que deixar o repositório lá atualizado, para que todos tenham acesso ao nosso código, para isso vamos adicionar o repositório do github como remote do nosso projeto local:

```
git remote add origin https://github.com/Matan18/git-tutorial.git
```

O comando não é complexo, o que estamos fazendo, basicamenteo, é acessando a funcionalidade *add* do *remote* do *git* passando como parâmetros o apelido desse remote "origin", e o local dele `https://github.com/Matan18/git-tutorial.git`, podemos verificar todos os repositórios que adicionamos com o comando `git remote -v`, e temos a seguinte imagem:

<img src="./assets/gitremoteverbose.png" width="500px">

Temos 2 remotes, pois um serve para fazermos a busca do projeto (fetch), e outro para a publicação dele (push);

Para fazermos a publicação do nosso projeto no github, só temos que digitar o comando;

```
git push origin main
```

E temos um erro no comando (eu juro que foi de propósito);

<img src="./assets/gitpusherror.png" width="500px">

Esse erro acontece pois o nosso repositório no github tem informações que não existem no nosso projeto local (criamos o arquivo README.md com o título do nosso projeto lá no momento que criamos o repositório, e aquele arquivo não aparece no nosso histórico local), para termos esse arquivo localmente, temos que fazer a busca dessas informações, e usaremos o *pull* para puxar as informações;

```
git pull origin main
```