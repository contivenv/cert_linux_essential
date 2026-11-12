---
tags: [lpi, linux-essentials, 010-160]
topico: 2
certificacao: LPI Linux Essentials 010-160 (v1.6)
---

# Tópico 2: Encontrando seu caminho em um Sistema Linux

## 2.1 O básico sobre a linha de comando

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 2.1
- **Peso**: 3

**Áreas chave de conhecimento**

- Shell básico
- Sintaxe da linha de comando
- Variáveis
- Globbing (Englobamento)
- Uso de aspas

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- Bash
- `echo`
- `history`
- Variável de ambiente `PATH`
- `export`
- `type`

### 2.1 Lição 1

#### Introdução

As distribuições Linux modernas oferecem uma ampla variedade de interfaces gráficas de usuário, mas um administrador sempre precisará saber como trabalhar com a linha de comando, ou *shell*. O shell é um programa que permite a comunicação por texto entre o sistema operacional e o usuário. Trata-se normalmente de um programa em modo texto que lê os dados inseridos pelo usuário e os interpreta na forma de comandos para o sistema.

Existem vários shells diferentes no Linux; estes são apenas alguns exemplos:

- Bourne-again shell (Bash)
- C shell (csh ou tcsh, a versão aprimorada do csh)
- Korn shell (ksh)
- Z shell (zsh)

No Linux, o mais comum é o shell Bash. É o que será usado em nossos exemplos e exercícios.

Ao usar um shell interativo, o usuário insere comandos no chamado prompt. Para cada distribuição Linux, o prompt padrão tem uma aparência um pouco diferente, mas ele geralmente segue esta estrutura:

```
username@hostname diretório_atual tipo_de_shell
```

No Ubuntu ou Debian GNU/Linux, o prompt de um usuário comum provavelmente será assim:

```
carol@mycomputer:~$
```

O prompt do superusuário terá a seguinte aparência:

```
root@mycomputer:~#
```

No CentOS ou Red Hat Linux, o prompt para um usuário comum será semelhante a este:

```
[dave@mycomputer ~]$
```

E o prompt do superusuário será assim:

```
[root@mycomputer ~]#
```

Vamos entender melhor cada componente da estrutura:

`username`

Nome do usuário que está rodando o shell

`hostname`

Nome da máquina hospedeira na qual o shell é executado. Também existe um comando `hostname`, que permite exibir ou definir o nome de hospedeiro do sistema.

`current_directory`

O diretório em que o shell está atualmente. Um `~` indica que o shell está no diretório Home do usuário atual.

`shell_type`

`$` indica que o shell está sendo executado por um usuário comum.

`#` indica que o shell está sendo executado pelo superusuário `root`.

Como não precisamos de privilégios especiais, usaremos um prompt sem privilégios nos exemplos a seguir. Por questões de concisão, usaremos apenas o `$` como prompt.

##### Estrutura da linha de comando

A maioria dos comandos na linha de comando segue a mesma estrutura básica:

```
comando [opção(ões)/parâmetro(s)...] [argumento(s)...]
```

Veja, por exemplo, o seguinte comando:

```bash
$ ls -l /home
```

Vamos entender a finalidade de cada componente:

- **Comando**: Programa que o usuário pretende executar — `ls`, no exemplo acima.
- **Opção(ões)/Parâmetro(s)**: Um “botão” que modifica o comportamento do comando de alguma forma, como `-l` no exemplo acima. As opções podem ser acessadas na forma curta ou longa. Por exemplo, `-l` é idêntico a `--format = long`.

  Também é possível combinar múltiplas opções e, no caso do formato abreviado, as letras geralmente podem ser digitadas juntas. Por exemplo, os seguintes comandos fazem todos a mesma coisa:

  ```bash
  $ ls -al
  $ ls -a -l
  $ ls --all --format=long
  ```

- **Argumento(s)**: Dados adicionais exigidos pelo programa, como um nome de arquivo ou caminho, como `/home` no exemplo acima.

A única parte obrigatória dessa estrutura é o próprio comando. Em geral, todos os outros elementos são opcionais, mas um programa pode exigir que determinadas opções, parâmetros ou argumentos sejam especificados.

> [!note]
> A maioria dos comandos exibe uma visão geral dos comandos disponíveis quando executados com o parâmetro `--help`. Em breve, veremos maneiras adicionais de saber mais sobre os comandos do Linux.

##### Tipos de comportamento dos comandos

O shell aceita dois tipos de comandos:

- **Internos**: Comandos que fazem parte do próprio shell e não são programas separados. Existem cerca de 30 desses comandos. Seu principal objetivo é executar tarefas dentro do shell (por exemplo, `cd`, `set`, `export`).
- **Externos**: Comandos que residem em arquivos individuais. Esses arquivos geralmente são programas binários ou scripts. Quando um comando externo ao shell é executado, o shell usa a variável `PATH` para procurar um arquivo executável com o mesmo nome que o comando. Além dos programas instalados com o gerenciador de pacotes da distribuição, os usuários também podem criar seus próprios comandos externos.

O comando `type` mostra a que tipo pertence um comando específico:

```bash
$ type echo
echo is a shell builtin
$ type man
man is /usr/bin/man
```

##### Citação

Como usuário de Linux, você precisa saber criar ou manipular arquivos ou variáveis de diversas maneiras. Isso é fácil quando se trabalha com nomes de arquivos curtos e valores simples, mas fica mais complicado quando, por exemplo, precisamos usar espaços, caracteres especiais e variáveis. Os shells oferecem um recurso chamado citação, que encapsula esses dados usando diversos tipos de aspas (" ", ' '). No Bash, há três tipos de citações:

- Aspas duplas
- Aspas simples
- Caracteres de escape

Por exemplo, os seguintes comandos não agem da mesma maneira devido à citação:

```bash
$ TWOWORDS="two words"
$ touch $TWOWORDS
$ ls -l
-rw-r--r-- 1 carol carol     0 Mar 10 14:56 two
-rw-r--r-- 1 carol carol     0 Mar 10 14:56 words
$ touch "$TWOWORDS"
$ ls -l
-rw-r--r-- 1 carol carol     0 Mar 10 14:56  two
-rw-r--r-- 1 carol carol     0 Mar 10 14:58 'two words'
-rw-r--r-- 1 carol carol     0 Mar 10 14:56  words
$ touch '$TWOWORDS'
$ ls -l
-rw-r--r-- 1 carol carol     0 Mar 10 15:00 '$TWOWORDS'
-rw-r--r-- 1 carol carol     0 Mar 10 14:56  two
-rw-r--r-- 1 carol carol     0 Mar 10 14:58 'two words'
-rw-r--r-- 1 carol carol     0 Mar 10 14:56  words
```

> [!note]
> A linha com `TWOWORDS =` é uma variável Bash que nós mesmos criamos. Falaremos das variáveis mais tarde. Isso serve apenas para mostrar como as citações afetam a saída das variáveis.

###### Aspas duplas

As aspas duplas dizem ao shell para considerar o texto entre as aspas ("...") como caracteres regulares. Todos os caracteres especiais perdem o significado, exceto `$` (cifrão), `\` (barra invertida) e ``` (crase). Isso significa que as variáveis, substituições de comando e funções aritméticas ainda podem ser usadas.

Por exemplo, a substituição da variável `$USER` não é afetada pelas aspas duplas:

```bash
$ echo I am $USER
I am tom
$ echo "I am $USER"
I am tom
```

Um caractere de espaço, por outro lado, perde seu significado como separador de argumentos:

```bash
$ touch new file
$ ls -l
```

```
-rw-rw-r-- 1 tom students 0 Oct 8 15:18 file
-rw-rw-r-- 1 tom students 0 Oct 8 15:18 new
$ touch "new file"
$ ls -l
-rw-rw-r-- 1 tom students 0 Oct 8 15:19 new file
```

Como explicado, no primeiro exemplo o comando `touch` cria dois arquivos individuais; o comando interpreta as duas seqüências como argumentos individuais. No segundo exemplo, o comando interpreta as duas seqüências como um argumento e, portanto, cria apenas um arquivo. No entanto, recomenda-se evitar o caractere de espaço nos nomes de arquivos. Em vez disso, é preferível usar um sublinhado (`_`) ou um ponto (`.`).

###### Aspas simples

As aspas simples não têm as exceções das aspas duplas. Elas revogam qualquer significado especial de cada caractere. Se retomarmos um dos primeiros exemplos acima:

```bash
$ echo I am $USER
I am tom
```

Ao aplicar aspas simples, obtemos um resultado diferente:

```bash
$ echo 'I am $USER'
I am $USER
```

O comando agora exibe a sequência exata, sem substituir a variável.

###### Caracteres de escape

Podemos usar *caracteres de escape* para remover os significados especiais dos caracteres do Bash. Voltando à variável de ambiente `$USER`:

```bash
$ echo $USER
carol
```

Vemos que, por padrão, o conteúdo da variável é exibido no terminal. No entanto, se colocarmos um caractere de barra invertida (`\`) antes do cifrão, o significado especial do cifrão será cancelado. Por sua vez, isso não permitirá que o Bash expanda o valor da variável para o nome de usuário da pessoa que está executando o comando, mas, em vez disso, interpretará o nome da variável literalmente:

```bash
$ echo \$USER
$USER
```

Como você deve lembrar, é possível obter resultados semelhantes usando aspas simples, que imprimem o conteúdo literal do que estiver entre elas. No entanto, o funcionamento do caractere de escape é diferente, pois instrui o Bash a ignorar qualquer significado especial do caractere que ele precede.

#### Exercícios Guiados

1. Divida as linhas abaixo nos componentes de comando, opção(ões)/parâmetro(s) e argumento(s):

  - Exemplo: `cat -n /etc/passwd`

| Comando: |  | `cat` |
|---|---|---|
| Opção: |  | `-n` |
| Argumento: |  | `/etc/passwd` |

  - `ls -l /etc`

  Comando:

  Opção:

  Argumento:

  - `ls -l -a`

  Comando:

  Opção:

  Argumento:

  - `cd /home/user`

  Comando:

  Opção:

  Argumento:

2. Descubra de que tipo são os comandos a seguir:

  Exemplo:

| `pwd` |  |  | Embutido no Shell |
|---|---|---|---|
| `mv` |  |  | Comando externo |
| `cd` |  |  |  |

| `cat` |  |
|---|---|
| `exit` |  |

3. Resolva os seguintes comandos que usam citações:

  Exemplo:

| `echo "$HOME is my home directory"` |  |  | `echo /home/user is my home directory` |
|---|---|---|---|
| `touch "$USER"` |  |  |  |
| `touch 'touch'` |  |  |  |

#### Exercícios Exploratórios

1. Com um só comando e usando a expansão de chaves no Bash (veja a página de manual do Bash), crie 5 arquivos numerados de 1 a 5 com o prefixo `game` (`game1`, `game2`, …).

2. Remova os cinco arquivos que acaba de criar com um único comando, usando um caractere especial diferente (consulte *Pathname Expansion* nas páginas de manual do Bash).

3. Existem outros jeitos de fazer com que dois comandos interajam entre si? Quais?

#### Resumo

Nesta lição, você aprendeu:

- Conceitos do shell do Linux
- O que é o shell Bash
- A estrutura da linha de comando
- Uma introdução às citações

Comandos usados nos exercícios:

`bash`

O shell mais popular em computadores com Linux.

`echo`

Gera texto no terminal.

`ls`

Lista o conteúdo de um diretório.

`type`

Mostra como um comando específico é executado.

`touch`

Cria um arquivo vazio ou atualiza a data de modificação de um arquivo existente.

`hostname`

Mostra ou altera o nome do host de um sistema.

#### Respostas aos Exercícios Guiados

1. Divida as linhas abaixo nos componentes de comando, opção(ões)/parâmetro(s) e argumento(s):

  - `ls -l /etc`

| Comando: |  | `ls` |
|---|---|---|
| Opção: |  | `-l` |
| Argumento: |  | `/etc` |

  - `ls -l -a`

| Comando: |  | `ls` |  |
|---|---|---|---|
| Opção: |  |  | `-l -a` |
| Argumento: |  |  |  |

  - `cd /home/user`

| Comando: |  | `cd` |
|---|---|---|
| Opção: |  |  |
| Argumento: |  | `/home/user` |

2. Descubra de que tipo são os comandos a seguir:

| `cd` |  |  |  | Embutido no shell |
|---|---|---|---|---|
| `cat` |  |  |  | Comando externo |
| `exit` |  |  |  | Embutido no shell |

3. Resolva os seguintes comandos que usam citações:

| `touch "$USER"` | `tom` |
|---|---|
| `touch 'touch'` | Cria um arquivo chamado `touch` |

#### Respostas aos Exercícios Exploratórios

1. Com um só comando e usando a expansão de chaves no Bash (veja a página de manual do Bash), crie 5 arquivos numerados de 1 a 5 com o prefixo `game` (`game1`, `game2`, …).

  É possível usar faixas para expressar os números de 1 a 5 dentro de um só comando:

  ```bash
  $ touch game{1..5}
  $ ls
  game1  game2  game3  game4  game5
  ```

2. Remova os cinco arquivos que acaba de criar com um único comando, usando um caractere especial diferente (consulte *Pathname Expansion* nas páginas de manual do Bash).

  Como todos os arquivos começam com `game` e terminam com um só caractere (neste caso, um número de 1 a 5), `?` pode ser usado como caractere especial no lugar do último caractere de um nome de arquivo:

  ```bash
  $ rm game?
  ```

3. Existem outros jeitos de fazer com que dois comandos interajam entre si? Quais?

  Sim, um comando pode, por exemplo, escrever dados em um arquivo que é em seguida processado por outro comando. O Linux também pode coletar a saída de um comando e usá-la como entrada de outro comando. Isso se chama *piping* e aprenderemos mais a respeito em uma lição futura.

### 2.1 Lição 2

#### Introdução

Todos os shells gerenciam um conjunto de informações de status ao longo das sessões do shell. Essas informações de tempo de execução podem mudar durante a sessão e influenciar o comportamento do shell. Esses dados também são usados pelos programas para determinar aspectos da configuração do sistema. A maioria desses dados é armazenada nas chamadas *variáveis*, que abordaremos nesta lição.

##### Variáveis

As variáveis são espaços de armazenamento para dados, como texto ou números. Uma vez definido, o valor de uma variável pode ser acessado posteriormente. As variáveis têm um nome, o que permite acessar uma variável específica mesmo quando seu conteúdo é alterado. Elas são uma ferramenta muito comum na maioria das linguagens de programação.

Na maioria dos shells do Linux, existem dois tipos de variáveis:

- **Variáveis locais**: Essas variáveis estão disponíveis apenas para o processo atual do shell. Se você criar uma

  variável local e, em seguida, iniciar outro programa nesse shell, a variável não poderá mais ser acessada por esse programa. Como não são herdadas por subprocessos, essas variáveis são chamadas *variáveis locais*.

- **Variáveis de ambiente**: Essas variáveis estão disponíveis tanto em uma sessão de shell específica quanto em subprocessos gerados a partir dessa sessão de shell. Essas variáveis podem ser usadas para transmitir dados de configuração para os comandos executados. Como os programas podem acessar essas variáveis, elas são chamadas *variáveis de ambiente*. A maioria das variáveis de ambiente aparece em letras maiúsculas (por exemplo, `PATH`, `DATE`, `USER`). Um conjunto de variáveis de ambiente padrão fornece, por exemplo, informações sobre o diretório inicial ou o tipo de terminal do usuário. Em certos casos, nos referimos ao conjunto completo de todas as variáveis de ambiente como *ambiente*.

> [!note]
> As variáveis não são persistentes. Quando o shell em que foram configuradas é fechado, todas as variáveis e seus conteúdos são perdidos. A maioria dos shells oferece arquivos de configuração que contêm variáveis definidas sempre que um novo shell é iniciado. As variáveis que devem ser definidas permanentemente precisam ser adicionadas a um desses arquivos de configuração.

##### Manipulação de variáveis

Como administrador do sistema, você precisará criar, modificar ou remover variáveis locais e de ambiente.

###### Trabalhando com variáveis locais

Você pode configurar uma variável local usando o operador `=` (igual). Uma atribuição simples criará uma variável local:

```bash
$ greeting=hello
```

> [!note]
> Não coloque espaço antes ou depois do operador `=`.

É possível exibir qualquer variável usando o comando `echo`. O comando geralmente exibe o texto na seção de argumentos:

```bash
$ echo greeting
greeting
```

Para acessar o valor da variável, você terá de usar `$` (cifrão) na frente do nome da variável.

```bash
$ echo $greeting
hello
```

Como vimos, a variável foi criada. Agora abra outro shell e tente exibir o conteúdo da variável criada.

```bash
$ echo $greeting
```

Nada é exibido. Isso ilustra o fato de que as variáveis existem somente em um shell específico.

Para verificar se a variável é de fato uma variável local, tente gerar um novo processo e confira se esse processo é capaz de acessar a variável. Para isso, inicie outro shell e execute nele o comando `echo`. Como o novo shell roda em um novo processo, ele não herdará as variáveis locais do processo pai:

```bash
$ echo $greeting world
hello world
$ bash -c 'echo $greeting world'
world
```

> [!note]
> Lembre-se de usar aspas simples no exemplo acima.

Para remover uma variável, usamos o comando `unset`:

```bash
$ echo $greeting
hey
$ unset greeting
$ echo $greeting
```

> [!note]
> O `unset` requer o nome da variável como argumento. Portanto, não é possível adicionar `$` ao nome, já que isso resolveria a variável e passaria o valor da variável para `unset` em vez do nome da variável.

###### Trabalhando com variáveis globais

Para disponibilizar uma variável local para subprocessos, podemos transformá-la em variável de ambiente. Usamos para isso o comando `export`. Quando ele é invocado junto ao nome da variável, essa variável é adicionada ao ambiente do shell:

```bash
$ greeting=hello
$ export greeting
```

> [!note]
> Aqui também não se deve usar `$` ao executar `export`, já que queremos transmitir o nome da variável e não seu conteúdo.

Uma maneira mais fácil de criar a variável de ambiente é combinar os dois métodos acima, atribuindo o valor da variável na parte de argumento do comando.

```bash
$ export greeting=hey
```

Vamos conferir novamente se a variável está acessível aos subprocessos:

```bash
$ export greeting=hey
$ echo $greeting world
hey world
$ bash -c 'echo $greeting world'
hey world
```

Outra maneira de usar variáveis de ambiente é colocá-las na frente dos comandos. Vamos testar essa possibilidade com a variável de ambiente `TZ`, que contém o fuso horário. Essa variável é usada pelo comando `date` para determinar qual hora do fuso horário deve ser exibida:

```bash
$ TZ=EST date
Thu 31 Jan 10:07:35 EST 2019
$ TZ=GMT date
Thu 31 Jan 15:07:35 GMT 2019
```

Para exibir todas as variáveis de ambiente, use o comando `env`.

###### A variável `PATH`

A variável `PATH` é uma das variáveis de ambiente mais importantes de um sistema Linux. Ela armazena uma lista de diretórios, separados por dois pontos, que contêm programas executáveis que funcionam como comandos do shell do Linux.

```bash
$ echo $PATH
```

```
/home/user/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```

Para acrescentar um novo diretório à variável, usamos o sinal de dois pontos (`:`).

```bash
$ PATH=$PATH:new_directory
```

Eis um exemplo:

```bash
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
$ PATH=$PATH:/home/user/bin
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/user/bin
```

Como vimos, `$PATH` é usado no novo valor atribuído a `PATH`. Essa variável é resolvida durante a execução do comando e garante que o conteúdo original da variável seja preservado. Obviamente, também dá para usar outras variáveis na atribuição:

```bash
$ mybin=/opt/bin
$ PATH=$PATH:$mybin
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/user/bin:/opt/bin
```

A variável `PATH` deve ser usada com cautela, pois é crucial para o trabalho na linha de comando. Vamos considerar a seguinte variável `PATH`:

```bash
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Para descobrir como o shell chama um comando específico, `which` pode ser executado com o nome do comando como argumento. Podemos, por exemplo, tentar descobrir onde o `nano` está armazenado:

```bash
$ which nano
/usr/bin/nano
```

Neste exemplo, o executável `nano` está localizado no diretório `/usr/bin`. Vamos remover o diretório da variável e verificar se o comando ainda funciona:

```bash
$ PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin:/bin:/usr/games
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin:/bin:/usr/games
```

Vamos procurar pelo comando `nano` novamente:

```bash
$ which nano
which: no nano in (/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin:/bin:/usr/games)
```

Como vimos, o comando não foi encontrado, e portanto não foi executado. A mensagem de erro também explica o motivo pelo qual o comando não foi encontrado e em quais locais foi buscado.

Vamos readicionar os diretórios e tentar executar o comando novamente.

```bash
$ PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
$ which nano
/usr/bin/nano
```

Agora nosso comando voltou a funcionar.

> [!tip]
> A ordem dos elementos em `PATH` também define a ordem de pesquisa. O primeiro executável da lista que corresponda às especificações será executado.

#### Exercícios Guiados

1. Crie uma variável local `number`.

2. Crie uma variável de ambiente `ORDER` usando um dos dois métodos acima.

3. Exiba o nome das variáveis e seu conteúdo.

4. Qual o escopo das variáveis criadas anteriormente?

#### Exercícios Exploratórios

1. Crie uma variável local `nr_files` e atribua o número de linhas encontrado no arquivo `/etc/passwd`. Dica: pesquise sobre o comando `wc` e substituição de comandos, e não se esqueça das aspas.

2. Crie uma variável de ambiente `ME`. Atribua a ela o valor de variável `USER`.

3. Inclua o valor da variável `HOME` a `ME`, usando o delimitador `:`. Exiba o conteúdo da variável `ME`.

4. Usando o exemplo acima, crie uma variável chamada `today` e atribua a data de um dos fusos horários.

5. Crie outra variável chamada `today1` e atribua a ela a data do sistema.

#### Sumário

Nesta lição, você aprendeu:

- Tipos de variáveis
- Como criar variáveis
- Como manipular variáveis

Comandos usados nos exercícios:

`env`

Exibe o ambiente atual.

`echo`

Gera uma saída de texto.

`export`

Torna as variáveis locais disponíveis para os subprocessos.

`unset`

Remove uma variável.

#### Respostas aos Exercícios Guiados

1. Crie uma variável local `number`.

  ```bash
  $ number=5
  ```

2. Crie uma variável de ambiente `ORDER` usando um dos dois métodos acima.

  ```bash
  $ export ORDER=desc
  ```

3. Exiba o nome das variáveis e seu conteúdo.

  ```bash
  $ echo number
  number
  $ echo ORDER
  ORDER
  $ echo $number
  5
  $ echo $ORDER
  desc
  ```

4. Qual o escopo das variáveis criadas anteriormente?

  - O escopo da variável `number` é somente o shell atual.
  - O escopo da variável `ORDER` é o shell atual e todos os subshells gerados por ele.

#### Respostas aos Exercícios Exploratórios

1. Crie uma variável local `nr_files` e atribua o número de linhas encontrado no arquivo `/etc/passwd`. Dica: pesquise sobre o comando `wc` e substituição de comandos, e não se esqueça das aspas.

  ```bash
  $ nr_files=`wc -l /etc/passwd`
  ```

2. Crie uma variável de ambiente `ME`. Atribua a ela o valor de variável `USER`.

  ```bash
  $ export ME=$USER
  ```

3. Inclua o valor da variável `HOME` a `ME`, usando o delimitador `:`. Exiba o conteúdo da variável `ME`.

  ```bash
  $ ME=$ME:$HOME
  $ echo $ME
  user:/home/user
  ```

4. Usando o exemplo acima, crie uma variável chamada `today` e atribua a data de um dos fusos horários.

  O exemplo a seguir usa os fusos horários GMT e EST, mas você pode escolher o que quiser.

  ```bash
  $ today=$(TZ=GMT date)
  $ echo $today
  Thu 31 Jan 15:07:35 GMT 2019
  ```

  or

  ```bash
  $ today=$(TZ=EST date)
  $ echo $today
  Thu 31 Jan 10:07:35 EST 2019
  ```

5. Crie outra variável chamada `today1` e atribua a ela a data do sistema.

  Se você estiver no horário GMT:

  ```bash
  $ today1=$(date)
  ```

  ```bash
  $ echo today1
  Thu 31 Jan 10:07:35 EST 2019
  ```

## 2.2 O Usando a linha de comando para conseguir ajuda

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 2.2
- **Peso**: 2

**Áreas chave de conhecimento**

- Man
- Info

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `man`
- `info`
- `/usr/share/doc/`
- `locate`

### 2.2 Lição 1

#### Introdução

A linha de comando é uma ferramenta bastante complexa. Cada comando possui suas próprias opções únicas; por isso, é essencial conhecer a documentação ao se trabalhar com um sistema Linux. Além do diretório `/usr/share/doc/`, que armazena a maior parte da documentação, diversas outras ferramentas fornecem informações sobre o uso dos comandos do Linux. Este capítulo se concentra em métodos para acessar essa documentação, com o objetivo de obter ajuda.

Existem vários métodos para obter ajuda na linha de comando do Linux. Alguns exemplos são `man`, `help` e `info`. Para o Linux Essentials, focaremos em `man` e `info`, que são as ferramentas mais usadas para obter ajuda.

Outro tópico deste capítulo será a localização de arquivos. Trabalharemos principalmente com o comando `locate`.

##### Como obter ajuda na linha de comando

###### Ajuda interna

Quando são iniciados com o parâmetro `--help`, a maioria dos comandos exibe algumas breves instruções sobre seu uso. Embora nem todos os comandos ofereçam essa opção, ainda vale a pena experimentá-la na primeira vez que se usa o comando para aprender mais sobre os parâmetros dele. Esteja ciente de que as instruções de `--help` geralmente são bastante concisas em comparação com outras fontes de documentação que discutiremos nesta lição.

###### Páginas man

A maioria dos comandos inclui uma página de manual, ou página “man”. Essa documentação geralmente é instalada com o software e pode ser acessada com o comando `man`. O comando cuja página de manual deve ser exibida é adicionado a `man` na forma de argumento:

```bash
$ man mkdir
```

Esse comando abre a página man de `mkdir`. Use as setas direcionais ou a barra de espaço para navegar pela página do manual. Para sair da página man, pressione `Q` .

Cada página man é dividida em no máximo 11 seções, embora muitas delas sejam opcionais:

| **Seção** | **Descrição** |
|---|---|
| NAME | Nome do comando e breve descrição |
| SYNOPSIS | Descrição da sintaxe do comando |
| DESCRIPTION | Descrição dos efeitos do comando |
| OPTIONS | Opções disponíveis |
| ARGUMENTS | Argumentos disponíveis |
| FILES | Arquivos auxiliares |
| EXAMPLES | Uma amostra da linha de comando |
| SEE ALSO | Referências cruzadas aos tópicos relacionados |
| DIAGNOSTICS | Mensagens de Advertência e Erro |
| COPYRIGHT | Autor(es) do comando |
| BUGS | Limitações conhecidas do comando |

Na prática, a maioria das páginas de manual não contém todas essas partes.

As páginas man estão organizadas em oito categorias, numeradas de 1 a 8:

| **Categoria** | **Descrição** |
|---|---|
| 1 | Comando do usuário |
| 2 | Chamadas do sistema |
| 3 | Funções da biblioteca C |
| 4 | Drivers e arquivos de dispositivo |
| 5 | Arquivos de configuração e formatos de arquivo |
| 6 | Jogos |
| 7 | Miscelânea |
| 8 | Comandos do administrador do sistema |
| 9 | Funções do kernel (não padrão) |

Cada página de manual pertence a exatamente uma seção. No entanto, seções diferentes podem conter páginas de manual com o mesmo nome. Vejamos, por exemplo, o comando `passwd`. Esse comando pode ser usado para alterar a senha de um usuário. Como `passwd` é um comando do usuário, sua página de manual reside na seção 1. Além do comando `passwd`, o arquivo de banco de dados de senhas `/etc/passwd` também possui uma página de manual chamada `passwd`. Como neste caso se trata de um arquivo de configuração, ele pertence à seção 5. Nas referências a uma página de manual, a categoria é frequentemente adicionada ao nome da página, por exemplo `passwd(1)` ou `passwd(5)`, para identificar a página respectiva.

Por padrão, `man passwd` exibe a primeira página man disponível; neste caso, `passwd(1)`. A categoria da página man desejada pode ser especificada em um comando como `man 1 passwd` ou `man 5 passwd`.

Já explicamos como navegar por uma página man e como retornar à linha de comando. Internamente, o `man` usa o comando `less` para exibir o conteúdo da página. `less` permite procurar texto dentro de uma página man. Para procurar a palavra `linux`, podemos simplesmente digitar `/linux` para pesquisar a partir do ponto em que estamos na página, ou `?Linux` para iniciar uma pesquisa reversa. Esta ação destaca todos os resultados correspondentes e move a página para a primeira correspondência destacada. Nos dois casos, basta digitar `N` para pular até a correspondência seguinte. Para encontrar mais informações sobre esses recursos adicionais, pressione `H` ; será exibido um menu com todas as informações.

###### Páginas info

Outra ferramenta muito útil ao trabalhar com o sistema Linux são as páginas de informações, ou info. As páginas info geralmente são mais detalhadas que as páginas man e são formatadas em hipertexto, semelhantes às páginas web na internet.

Para exibir as páginas info, usamos:

```bash
$ info mkdir
```

Nessas páginas, o comando `info` lê um arquivo de informações estruturado em nós individuais dentro de uma árvore. Cada nó contém um tópico simples e o comando `info` inclui hiperlinks que ajudam a passar de um para o outro. Para acessar o link, pressione `Enter` , com o cursor pousado sobre um dos asteriscos principais.

A exemplo de `man`, a ferramenta `info` também inclui comandos de navegação na página. Para descobrir mais sobre esses comandos, pressione `?` enquanto estiver na página de informações. Essas ferramentas o ajudarão a navegar na página mais facilmente e a entender como acessar os nós e mover-se dentro da árvore de nós.

###### O diretório `/usr/share/doc/`

Como já mencionado, o diretório `/usr/share/doc/` armazena a maior parte da documentação dos comandos que estão em uso. Essa pasta contém um diretório para a maioria dos pacotes instalados no sistema. O nome do diretório geralmente é o nome do pacote e, ocasionalmente, a versão. Esses diretórios incluem um arquivo `README` ou `readme.txt` contendo a documentação básica do pacote. Juntamente com o arquivo `README`, a pasta também pode conter outros arquivos de documentação, como o registro de alterações (changelog), que inclui o histórico do programa em detalhes, ou exemplos de arquivos de configuração para aquele pacote específico.

As informações contidas no arquivo `README` variam de um pacote a outro. Todos os arquivos são gravados em texto simples e, portanto, podem ser lidos em qualquer editor de texto de sua preferência. O número exato e os tipos de arquivos dependem do pacote. Verifique alguns dos diretórios para obter uma visão geral de seu conteúdo.

##### Como localizar arquivos

###### O comando `locate`

Um sistema Linux é construído a partir de diversos diretórios e arquivos. O Linux tem muitas ferramentas que permitem localizar um arquivo específico em um sistema. A mais rápida é o comando `locate`.

O `locate` pesquisa dentro de um banco de dados e, em seguida, gera todos os nomes que correspondem à cadeia de caracteres (string) especificada:

```bash
$ locate note
/lib/udev/keymaps/zepto-znote
/usr/bin/zipnote
/usr/share/doc/initramfs-tools/maintainer-notes.html
/usr/share/man/man1/zipnote.1.gz
```

O comando `locate` também suporta o uso de curingas e expressões regulares; assim, o termo de pesquisa não precisa corresponder ao nome inteiro do arquivo desejado. Trataremos mais a fundo das expressões regulares em um capítulo posterior.

Por padrão, `locate` se comporta como se o termo de busca estivesse cercado por asteriscos. Portanto, `locate TERMO` é o mesmo que `locate *TERMO*`. Isso permite fornecer apenas substrings em vez do nome exato do arquivo. Se quiser modificar esse comportamento, use as diferentes opções especificadas na página man de `locate`.

Como `locate` consulta um banco de dados, você pode não encontrar um arquivo que foi criado recentemente. O banco de dados é gerenciado por um programa chamado `updatedb`. Ele costuma ser executado periodicamente, mas se você possui privilégios de root e precisa atualizar o banco de dados imediatamente, pode executar o comando `updatedb` a qualquer momento.

###### O comando `find`

O `find` é outra ferramenta muito popular usada para procurar arquivos. Esse comando tem uma abordagem diferente do `locate`. O comando `find` pesquisa recursivamente em uma árvore de diretórios, incluindo os subdiretórios. O `find` faz essa pesquisa a cada chamada, em vez de manter um banco de dados como o `locate`. A exemplo do `locate`, o `find` também suporta caracteres curinga e expressões regulares.

O `find` requer pelo menos o local em que ele deve procurar. Além disso, podemos adicionar expressões para filtrar os arquivos a exibir. Um exemplo é a expressão `-name`, que procura por arquivos com um nome específico:

```
~$ cd Downloads
~/Downloads
$ find . -name thesis.pdf
```

```
./thesis.pdf
~/Downloads
$ find ~ -name thesis.pdf
/home/carol/Downloads/thesis.pdf
```

O primeiro comando `find` procura por arquivos dentro do atual diretório `Downloads`, ao passo que o segundo busca pelo arquivo no diretório Home do usuário.

O comando `find` é muito complexo e, portanto, não será tratado no exame Linux Essentials. No entanto, trata-se de uma ferramenta poderosa e particularmente útil no cotidiano.

#### Exercícios Guiados

1. Use o comando `man` para descobrir o que cada comando faz:

| **Comando** | **Descrição** |
|---|---|
| `ls` | Exibe o conteúdo de um diretório. |
| `cat` |  |
| `cut` |  |
| `cd` |  |
| `cp` |  |
| `mv` |  |
| `mkdir` |  |
| `touch` |  |
| `wc` |  |
| `passwd` |  |
| `rm` |  |
| `rmdir` |  |
| `more` |  |
| `less` |  |
| `whereis` |  |
| `head` |  |
| `tail` |  |
| `sort` |  |
| `tr` |  |
| `chmod` |  |
| `grep` |  |

2. Abra a página info de `ls` e identifique o MENU.

  - Quais são as opções?
  - Encontre a opção que permite classificar os dados de saída por data de modificação.

3. Exiba o caminho para os três primeiros arquivos `README`. Use o comando `man` para identificar a opção correta para `locate`.

4. Crie um arquivo chamado `test` em seu diretório Home. Encontre seu caminho absoluto usando o comando `locate`.

5. Você o encontrou imediatamente? O que teve de fazer para que `locate` o encontrasse?

6. Procure pelo arquivo de teste criado anteriormente usando o comando `find`. Qual sintaxe você usou e qual o caminho absoluto?

#### Exercícios Exploratórios

1. Um dos comandos na tabela acima não tem uma página `man`. Qual é esse comando e por que você acha que ele não tem uma página man?

2. Usando os comandos da tabela acima, crie a seguinte árvore de arquivos. Os nomes que começam com letra maiúscula são diretórios e os que começam em minúscula são arquivos.

  ```
  User
  ├── Documents
  |   ├──Hello
  |   |   ├──hey2
  |   |   ├──helloa
  |   |   └──ola5
  |   └──World
  |       └──earth9
  ├── Downloads
  |   ├──Music
  |   └──Songs
  |       ├──collection1
  |       └──collection2
  ├── Test
  |   └── passa
  └── test
  ```

3. Exiba na tela o diretório de trabalho atual, incluindo as subpastas.

4. Procure dentro da árvore por todos os arquivos terminados com um número.

5. Remova a árvore de diretórios inteira com um único comando.

#### Resumo

Nesta lição, você aprendeu:

- Como conseguir ajuda
- Como usar o comando `man`
- Como navegar na página `man`
- Diferentes seções da página `man`
- Como usar o comando `info`
- Como navegar entre diferentes nós
- Como buscar arquivos dentro do sistema

Comandos usados nos exercícios:

`man`

Exibe uma página de manual.

`info`

Exibe uma página de informações.

`locate`

Busca no banco de dados de `locate` por arquivos com um nome específico.

`find`

Busca no sistema de arquivos por nomes que correspondam a uma série de critérios de seleção.

`updatedb`

Atualiza o banco de dados de `locate`.

#### Respostas aos Exercícios Guiados

1. Use o comando `man` para descobrir o que cada comando faz:

| **Comando** | **Descrição** |
|---|---|
| `ls` | Exibe o conteúdo de um diretório. |
| `cat` | Concatena ou visualiza arquivos de texto |
| `cut` | Remove seções de um arquivo de texto |
| `cd` | Passa para um diretório diferente |
| `cp` | Copia um arquivo |
| `mv` | Move um arquivo (também pode ser usado para renomear) |
| `mkdir` | Cria um novo diretório |
| `touch` | Cria um arquivo ou modifica a hora e data da última modificação de um arquivo existente |
| `wc` | Conta o número de palavras, linhas ou bytes de um arquivo |
| `passwd` | Muda a senha de um usuário |
| `rm` | Remove um arquivo |
| `rmdir` | Remove um diretório |
| `more` | Visualiza arquivos de texto uma tela de cada vez |
| `less` | Visualiza arquivos de texto, permite rolar uma linha ou página por vez, para cima ou para baixo |
| `whereis` | Exibe o caminho até um programa especificado e arquivos de manual relacionados |
| `head` | Exibe as primeiras linhas de um arquivo |
| `tail` | Exibe as últimas linhas de um arquivo |
| `sort` | Ordena um arquivo numérica ou alfabeticamente |

| **Comando** | **Descrição** |
|---|---|
| `tr` | Traduz ou remove caracteres de um arquivo |
| `chmod` | Altera as permissões de um arquivo |
| `grep` | Busca dentro de um arquivo |

2. Abra a página info de `ls` e identifique o MENU.\*

  - Quais são as opções?

  ▪Quais arquivos são listados

  ▪Qual informação é listada

  ▪Classificação do resultado

  ▪Informações sobre a versão

  ▪Formatação geral da saída

  ▪Formatação dos registros de data e hora do arquivo

  ▪Formatação dos nomes dos arquivos

  - Encontre a opção que permite classificar os dados de saída por data de modificação.

  `-t` ou `--sort=time`

3. Exiba o caminho para os três primeiros arquivos `README`. Use o comando `man` para identificar a opção correta para `locate`.

  ```bash
  $ locate -l 3 README
  /etc/alternatives/README
  /etc/init.d/README
  /etc/rc0.d/README
  ```

4. Crie um arquivo chamado `test` em seu diretório Home. Encontre seu caminho absoluto usando o comando `locate`.

  ```bash
  $ touch test
  $ locate test
  /home/user/test
  ```

5. Você o encontrou imediatamente? O que teve de fazer para que `locate` o encontrasse?

  ```bash
  $ sudo updatedb
  ```

  O arquivo acaba de ser criado, portanto ainda não foi registrado no banco de dados.

6. Procure pelo arquivo de teste criado anteriormente usando o comando `find`. Qual sintaxe você usou e qual o caminho absoluto?

  ```bash
  $ find ~ -name test
  ```

  ou

  ```bash
  $ find . -name test
  /home/user/test
  ```

#### Respostas aos Exercícios Exploratórios

1. Um dos comandos na tabela acima não tem uma página `man`. Qual é esse comando e por que você acha que ele não tem uma página man?

  O comando `cd`. Ele não tem uma página man porque é um comando interno do shell.

2. Usando os comandos da tabela acima, crie a seguinte árvore de arquivos. Os nomes que começam com letra maiúscula são diretórios e os que começam em minúscula são arquivos.

  ```
  User
  ├── Documents
  |   ├──Hello
  |   |   ├──hey2
  |   |   ├──helloa
  |   |   └──ola5
  |   └──World
  |       └──earth9
  ├── Downloads
  |   ├──Music
  |   └──Songs
  |       ├──collection1
  |       └──collection2
  ├── Test
  |   └── passa
  └── test
  ```

  A solução é uma combinação dos comandos `mkdir` e `touch`.

3. Exiba na tela o diretório de trabalho atual, incluindo as subpastas.

  ```bash
  $ ls -R
  ```

4. Procure dentro da árvore por todos os arquivos terminados com um número.

  ```bash
  $ find ~ -name "*[0-9]"
  $ locate "*[0-9]"
  ```

5. Remova a árvore de diretórios inteira com um único comando.

  ```bash
  $ rm -r Documents Downloads Test test
  ```

## 2.3 Usando diretórios e listando arquivos

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 2.3
- **Peso**: 2

**Áreas chave de conhecimento**

- Arquivos, diretórios
- Arquivos e diretórios ocultos
- Home
- Caminhos relativos e absolutos

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- Opções comuns para `ls`
- Listagens recursivas
- `cd`
- `.` e `..`
- `home` e `~`

### 2.3 Lição 1

#### Introdução

##### Arquivos e diretórios

O sistema de arquivos do Linux é semelhante ao sistema de arquivos de outros sistemas operacionais, pois contém *arquivos* e *diretórios*. Os arquivos contêm dados, como texto legível por humanos, programas executáveis ou dados binários usados pelo computador. Os diretórios são usados para organizar o sistema de arquivos. Eles podem conter arquivos e outros diretórios.

```bash
$ tree

Documents
├── Mission-Statement.txt
└── Reports
└── report2018.txt

1 directory, 2 files
```

Neste exemplo, `Documents` é um diretório que contém um arquivo (`Mission-Statement.txt`) e um *subdiretório* (`Reports`). O diretório `Reports`, por sua vez, contém um arquivo chamado `report2018.txt`. O diretório `Documents` é considerado o *pai* do diretório `Reports`.

> [!tip]
> Se o comando `tree` não estiver disponível no seu sistema, instale-o usando o gerenciador de pacotes da sua distribuição Linux. Consulte a lição sobre gerenciamento de pacotes para aprender como fazer isso.

##### Nomes de arquivos e diretórios

Os nomes de arquivos e diretórios no Linux podem conter letras minúsculas e maiúsculas, números, espaços e caracteres especiais. No entanto, como muitos caracteres especiais têm um significado preciso no shell do Linux, é recomendável não usar espaços ou caracteres especiais ao nomear arquivos ou diretórios. Para usar espaços, por exemplo, é preciso que o *caractere de* *escape* `\` seja inserido corretamente:

```bash
$ cd Mission\ Statements
```

Além disso, veja o nome do arquivo `report2018.txt`. Os nomes de arquivos podem conter um *sufixo* após o ponto final (`.`). Ao contrário do que acontece no Windows, esse sufixo não tem significado especial no Linux; ele existe para a compreensão humana. Em nosso exemplo, `.txt` indica para nós que este é um arquivo de texto sem formatação, embora, tecnicamente, ele possa conter qualquer tipo de dados.

##### Navegando no sistema de arquivos

###### Como obter a localização atual

Os shells do Linux, como o Bash, são baseados em texto, e por isso é importante conhecer sua localização atual ao navegar no sistema de arquivos. O *prompt de comando* fornece essas informações:

```
user@hostname ~/Documents/Reports $
```

Trataremos de informações como `user` e `hostname` futuramente. Graças ao prompt, sabemos que nossa localização atual é o diretório `Reports`. Da mesma forma, o comando `pwd` serve para *imprimir o diretório de trabalho*:

```
user@hostname ~/Documents/Reports $ pwd
```

```
/home/user/Documents/Reports
```

A relação entre os diretórios é representada com uma barra (`/`). Sabemos que `Reports` é um subdiretório de `Documents`, que por sua vez é um subdiretório de `user`, localizado em um diretório chamado `home`. O `home` não parece ter um diretório pai, mas isso não é verdade. O pai de `home` se chama *root* e é representado pela primeira barra (`/`). Explicaremos o diretório root em uma seção posterior.

Note que a saída do comando `pwd` difere um pouco do caminho mostrado no prompt de comando. Em vez de `/ home/user`, o prompt de comando contém um til (`~`). O til é um caractere especial que representa o diretório inicial do usuário. Trataremos disso em mais detalhes na próxima lição.

###### Como listar o conteúdo do diretório

O conteúdo do diretório atual é listado com o comando `ls`:

```
user@hostname ~/Documents/Reports $ ls
report2018.txt
```

Note que o `ls` não fornece informações sobre o diretório pai. Da mesma forma, por padrão, `ls` não exibe nenhuma informação sobre o conteúdo dos subdiretórios. O `ls` pode apenas “ver” o que está no diretório atual.

###### Como mudar de diretório

A navegação no Linux é feita principalmente com o comando `cd`. Esse comando *muda de diretório*. Usando o comando `pwd` como anteriormente, sabemos que nosso diretório atual é `/home/user/Documents/Reports`. Podemos mudar nosso diretório atual inserindo um novo caminho:

```
user@hostname ~ $ cd /home/user/Documents
user@hostname ~/Documents $ pwd
/home/user/Documents
user@hostname ~/Documents $ ls
Mission-Statement.txt Reports
```

Neste novo local, podemos “ver” `Mission-Statement.txt` e o subdiretório `Reports`, mas não o conteúdo de nosso subdiretório. Podemos navegar de volta para `Relatórios` assim:

```
user@hostname ~/Documents $ cd Reports
user@hostname ~/Documents/Reports $ pwd
/home/user/Documents/Reports
user@hostname ~/Documents/Reports $ ls
report2018.txt
```

Agora estamos de volta onde começamos.

##### Caminhos absolutos e relativos

O comando `pwd` sempre imprime um *caminho absoluto*, ou seja, o caminho contém todas as etapas, desde o início do sistema de arquivos (`/`) até o final (`Reports`). Os caminhos absolutos sempre começam com um `/`.

```
/
└── home
└── user
└── Documents
└── Reports
```

O caminho absoluto contém todas as informações necessárias para se chegar a `Reports` a partir de qualquer lugar no sistema de arquivos. A desvantagem é que é tedioso digitá-lo inteiro.

O segundo exemplo (`cd Reports`) foi muito mais fácil de digitar. Esse é um exemplo de *caminho* *relativo*. Os caminhos relativos são mais curtos, mas só têm significado em relação à sua localização atual. Considere esta analogia: eu estou visitando você em sua casa. Você me diz que seu amigo mora na casa ao lado. Entenderei esse local porque tem relação com meu local atual. Mas se você me disser isso por telefone, não poderei encontrar a casa do seu amigo. Você precisará me fornecer o endereço completo.

###### Caminhos relativos especiais

O shell do Linux oferece maneiras de encurtar os caminhos durante a navegação. Para revelar os primeiros caminhos especiais, inserimos o comando `ls` com a flag `-a`. Essa flag modifica o comando `ls` para que *todos* os arquivos e diretórios sejam listados, incluindo os arquivos e diretórios ocultos:

```
user@hostname ~/Documents/Reports $ ls -a
.
..
```

```
report2018.txt
```

> [!note]
> Consulte a página `man` de `ls` para entender o que `-a` está fazendo aqui.

Esse comando revelou dois resultados adicionais: Estes são caminhos especiais. Eles não representam novos arquivos ou diretórios, mas sim diretórios que você já conhece:

`.`

Indica o *local atual* (neste caso, `Reports`).

`..`

Indica o *diretório pai* (neste caso, `Documents`).

Geralmente, não é necessário usar o caminho relativo especial para o local atual. É mais fácil e compreensível digitar `report2018.txt` do que digitar `./Report2018.txt`. Mas o `.` tem usos que você aprenderá nas próximas seções. Por enquanto, vamos nos concentrar no caminho relativo para o diretório pai:

```
user@hostname ~/Documents/Reports $ cd ..
user@hostname ~/Documents $ pwd
/home/user/Documents
```

O exemplo de `cd` é muito mais fácil quando se usa `..` em vez do caminho absoluto. Além disso, podemos combinar esse padrão para subir rapidamente pela árvore de arquivos.

```
user@hostname ~/Documents $ cd ../..
$ pwd
/home
```

#### Exercícios Guiados

1. Identifique se cada um dos caminhos a seguir é *absoluto* ou *relativo*:

  `/home/user/Downloads`

  `../Reports`

  `/var`

  `docs`

  `/`

2. Observe a seguinte estrutura de arquivo. Nota: Os diretórios terminam com uma barra (`/`) quando `tree` é chamado com a opção `-F`. Você precisará de privilégios elevados para executar o comando `tree` no diretório root (`/`). O exemplo de saída a seguir é apenas demonstrativo e não é indicativo de uma estrutura de diretório completa. Use-o para responder às seguintes questões:

  ```bash
  $ tree /

  /
  ├── etc/
  │   ├── network/
  │   │   └── interfaces
  │   ├── systemd/
  │   │   ├── resolved.conf
  │   │   ├── system/
  │   │   ├── system.conf
  │   │   ├── user/
  │   │   └── user.conf
  │   └── udev/
  │       ├── rules.d/
  │       └── udev.conf
  └── home/
  ├── lost+found/
  └── user/
  └── Documents/

  12 directories, 5 files
  ```

  Use essa estrutura para responder às questões a seguir.

  Um usuário insere os seguintes comandos:

  ```bash
  $ cd /etc/udev
  $ ls -a
  ```

  Qual será a saída do comando `ls -a`?

3. Digite o comando mais curto possível para cada um dos seguintes enunciados:

  - Seu local atual é root (`/`). Digite o comando para navegar até `lost+found` dentro do diretório `home` (exemplo):

  ```bash
  $ cd home/lost+found
  ```

  - Seu local atual é root (`/`). Digite o comando para navegar até o diretório `/etc/network/`.
  - Seu local atual é `/home/user/Documents/`. Navegue até o diretório `/etc/`.
  - Seu local atual é `/etc/systemd/system/`. Navegue até o diretório `/home/user/`.

4. Considere os seguintes comandos:

  ```bash
  $ pwd
  /etc/udev/rules.d
  $ cd ../../systemd/user
  $ cd ..
  $ pwd
  ```

  Qual a saída do comando `pwd` final?

#### Exercícios Exploratórios

1. Supondo que um usuário tenha inserido os seguintes comandos:

  ```bash
  $ mkdir "this is a test"
  $ ls
  this is a test
  ```

  Qual comando `cd` permitiria entrar nesse diretório?

2. Tente o mesmo exercício novamente, mas depois de digitar `cd this`, pressione a tecla TAB. O que é exibido no prompt?

  Isso é um exemplo de *autocompletar*, uma ferramenta inestimável não somente para poupar tempo como também para evitar erros de digitação.

3. Tente criar um diretório cujo nome contenha um caractere `\`. Exiba o nome do diretório com `ls` e remova o diretório.

#### Resumo

Nesta lição, você aprendeu:

- As bases do sistema de arquivos do Linux
- A diferença entre diretórios *pai* e *subdiretórios*
- A diferença entre caminhos de arquivo *absolutos* e *relativos*
- Os caminhos relativos especiais `.` e `..`
- Navegação no sistema de arquivos usando `cd`
- Mostrar seu local atual usando `pwd`
- Listar *todos* os arquivos e diretórios usando `ls -a`

Os seguintes comandos foram discutidos nesta lição:

`cd`

Muda o diretório atual.

`pwd`

Imprime o caminho do diretório de trabalho atual

`ls`

Lista o conteúdo de um diretório e exibe as propriedades dos arquivos

`mkdir`

Cria um novo diretório

`tree`

Exibe uma lista hierárquica de uma árvore de diretórios

#### Respostas aos Exercícios Guiados

1. Identifique se cada um dos caminhos a seguir é *absoluto* ou *relativo*:

| `/home/user/Downloads` |  |  |  | absoluto |
|---|---|---|---|---|
| `../Reports` |  |  |  | relativo |
| `/var` |  |  |  | absoluto |
| `docs` |  |  |  | relativo |
| `/` |  |  |  | absoluto |

2. Observe a seguinte estrutura de arquivo. Nota: Os diretórios terminam com uma barra (`/`) quando `tree` é chamado com a opção `-F`. Você precisará de privilégios elevados para executar o comando `tree` no diretório root (`/`). O exemplo de saída a seguir é apenas demonstrativo e não é indicativo de uma estrutura de diretório completa. Use-o para responder às seguintes questões:

  ```bash
  $ tree /

  /
  ├── etc/
  │   ├── network/
  │   │   └── interfaces
  │   ├── systemd/
  │   │   ├── resolved.conf
  │   │   ├── system/
  │   │   ├── system.conf
  │   │   ├── user/
  │   │   └── user.conf
  │   └── udev/
  │       ├── rules.d/
  │       └── udev.conf
  └── home/
  ├── lost+found/
  └── user/
  └── Documents/

  12 directories, 5 files
  ```

  Um usuário insere os seguintes comandos:

  ```bash
  $ cd /etc/udev
  $ ls -a
  ```

  Qual será a saída do comando `ls -a`?

  ```
  . .. rules.d udev.conf
  ```

3. Digite o comando mais curto possível para cada um dos seguintes enunciados:

  - Seu local atual é root (`/`). Digite o comando para navegar até `lost+found` dentro do diretório `home` (exemplo):

  ```bash
  $ cd home/lost+found
  ```

  - Seu local atual é root (`/`). Digite o comando para navegar até o diretório `/etc/network/`.

  ```bash
  $ cd etc/network
  ```

  - Seu local atual é `/home/user/Documents/`. Navegue até o diretório `/etc/`.

  ```bash
  $ cd /etc
  ```

  - Seu local atual é `/etc/systemd/system/`. Navegue até o diretório `/home/user/`.

  ```bash
  $ cd /home/user
  ```

4. Considere os seguintes comandos:

  ```bash
  $ pwd
  /etc/udev/rules.d
  $ cd ../../systemd/user
  $ cd ..
  $ pwd
  ```

  Qual a saída do comando `pwd` final?

  ```
  /etc/systemd
  ```

#### Respostas aos Exercícios Exploratórios

1. Supondo que um usuário tenha inserido os seguintes comandos:

  ```bash
  $ mkdir "this is a test"
  $ ls
  this is a test
  ```

  Qual comando `cd` permitiria entrar nesse diretório?

  ```bash
  $ cd this\ is\ a\ test
  ```

2. Tente o mesmo exercício novamente, mas depois de digitar `cd this`, pressione a tecla TAB. O que é exibido no prompt?

  ```bash
  $ cd this\ is\ a\ test
  ```

  Isso é um exemplo de *autocompletar*, uma ferramenta inestimável não somente para poupar tempo como também para evitar erros de digitação.

3. Tente criar um diretório cujo nome contenha um caractere `\`. Exiba o nome do diretório com `ls` e remova o diretório.

  É possível escapar da barra usando outra barra (`\\`) ou aspas simples ou duplas em torno do nome completo do diretório:

  ```bash
  $ mkdir my\\dir
  $ ls
  'my\dir'
  $ rmdir 'my\dir'
  ```

### 2.3 Lição 2

#### Introdução

O sistema operacional Unix foi originalmente projetado para computadores mainframe em meados da década de 1960. Esses computadores eram compartilhados entre muitos usuários, que acessavam os recursos do sistema através de *terminais*. Essas idéias fundamentais ainda estão presentes nos sistemas Linux de hoje em dia. Ainda falamos sobre o uso de “terminais” para inserir comandos no shell, e os sistemas Linux são organizados de tal maneira que é fácil criar diversos usuários em um único sistema.

##### Diretórios Home

Eis um exemplo de um sistema de arquivos normal no Linux:

```bash
$ tree -L 1 /
/
├── bin
├── boot
├── cdrom
├── dev
```

```
├── etc
├── home
├── lib
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

A maioria desses diretórios existe em todos os sistemas Linux. De servidores a supercomputadores, passando por pequenos sistemas embarcados, um usuário experiente do Linux pode ter a certeza de que vai encontrar o comando `ls` dentro de `/bin`, que pode alterar a configuração do sistema modificando arquivos em `/etc` e ler os logs do sistema em `/var`. A localização padrão desses arquivos e diretórios é definida pelo FHS (Filesystem Hierarchy Standard, ou padrão de sistema de arquivos hierárquico), que será discutido em uma lição mais pra frente. Você aprenderá mais sobre o conteúdo desses diretórios à medida que continuar estudando o Linux, mas por enquanto, é importante saber que:

- as alterações feitas no sistema de arquivos raiz (root) afetarão todos os usuários, e
- alterar arquivos no sistema de arquivos raiz exigirá permissões de administrador.

Isso significa que os usuários normais não terão a permissão para alterar esses arquivos, e talvez nem mesmo para a leitura deles. Abordaremos o tópico das permissões em uma seção posterior.

Agora, vamos nos concentrar no diretório `/home`, que você já deve conhecer bem:

```bash
$ tree -L 1 /home
/home
├── user
├── michael
└── lara
```

Nosso sistema de exemplo tem três usuários normais e cada um deles tem acesso a seu próprio local dedicado, no qual é possível criar e modificar arquivos e diretórios sem afetar o vizinho. Por exemplo, na lição anterior, estávamos trabalhando com a seguinte estrutura de arquivos:

```bash
$ tree /home/user
user
└── Documents
├── Mission-Statement
└── Reports
└── report2018.txt
```

Na realidade, o sistema de arquivos pode ser assim:

```bash
$ tree /home
/home
├── user
│   └── Documents
│       ├── Mission-Statement
│       └── Reports
│           └── report2018.txt
├── michael
│   ├── Documents
│   │   └── presentation-for-clients.odp
│   └── Music
```

…e assim por diante para `lara`.

No Linux, `/home` é semelhante a um prédio de apartamentos. Muitos usuários podem ter seu espaço aqui, separados em apartamentos dedicados. As instalações básicas e a manutenção do próprio edifício são de responsabilidade do usuário root, que representa o síndico.

##### O caminho relativo especial para home

Ao iniciar uma nova sessão no terminal do Linux, vemos um prompt de comando semelhante a este:

```
user@hostname ~ $
```

O til (`~`) representa, aqui, o diretório *home*. Se executarmos o comando `ls`, veremos um resultado conhecido:

```bash
$ cd ~
$ ls
```

```
Documents
```

Compare-o ao sistema de arquivos acima para entender melhor.

Considere agora o que sabemos sobre o Linux: ele é semelhante a um prédio de apartamentos, com muitos usuários residentes em `/home`. Portanto, a casa de `user` será diferente da casa do usuário `michael`. Para demonstrar isso, usaremos o comando `su` para *trocar de usuário*.

```
user@hostname ~ $ pwd
/home/user
user@hostname ~ $ su - michael
Password:
michael@hostname ~ $ pwd
/home/michael
```

O significado de `~` muda dependendo de quem for o usuário. Para `michael`, o caminho absoluto de `~` é `/home/michael`. Para `lara`, o caminho absoluto de `~` é `/home/lara`, e assim por diante.

##### Caminhos de arquivos relativos-a-home

A possibilidade de usar `~` para os comandos é muito conveniente, desde que você não troque de usuário. Vamos considerar o exemplo a seguir para `user`, que iniciou uma nova sessão:

```bash
$ ls
Documents
$ cd Documents
$ ls
Mission-Statement
Reports
$ cd Reports
$ ls
report2018.txt
$ cd ~
$ ls
Documents
```

Note que os usuários sempre iniciam uma nova sessão em seu diretório pessoal. Neste exemplo, `user` trocou para o subdiretório `Documents/Reports` e, com o comando `cd ~`, voltou ao ponto de partida. É possível executar a mesma ação usando o comando `cd` sem argumentos:

```bash
$ cd Documents/Reports
$ pwd
/home/user/Documents/Reports
$ cd
$ pwd
/home/user
```

E por fim: podemos especificar os diretórios pessoais de *outros usuários* especificando o nome de usuário após o til. Por exemplo:

```bash
$ ls ~michael
Documents
Music
```

Porém, isso só funciona se `michael` nos der permissão para visualizar o conteúdo de seu diretório pessoal.

Vamos considerar uma situação em que `michael` gostaria de visualizar o arquivo `report2018.txt` no diretório inicial de `user`. Supondo que `michael` tenha permissão para fazê- lo, ele pode usar o comando `less`.

```bash
$ less ~user/Documents/Reports/report2018.txt
```

Qualquer caminho de arquivo que contenha o caractere `~` é chamado de caminho *relativo-a-home*.

##### Arquivos e diretórios ocultos

Na lição anterior, introduzimos a opção `-a` para o comando `ls`. Usamos `ls -a` para introduzir os dois caminhos relativos especiais: `.` e `..`. A opção `-a` lista todos os arquivos e diretórios, incluindo os arquivos e diretórios *ocultos*.

```bash
$ ls -a ~
.
..
.bash_history
.bash_logout
.bash-profile
.bashrc
Documents
```

Os arquivos e diretórios ocultos sempre começam com um ponto (`.`). Por padrão, o diretório home de um usuário inclui diversos arquivos ocultos. Eles servem geralmente para estabelecer as configurações específicas do usuário e devem ser modificados somente por um usuário experiente.

##### A opção de lista longa

Existem muitas opções que permitem mudar o comportamento do comando `ls`. Vamos conhecer uma das mais comuns:

```bash
$ ls -l
-rw-r--r-- 1 user staff      3606 Jan 13  2017 report2018.txt
```

`-l` cria uma *lista longa*. Os arquivos e diretórios ocuparão uma linha cada, mas também serão exibidas informações adicionais sobre cada arquivo e diretório.

`-rw-r--r--`

Tipo de arquivo e permissões do arquivo. Note que um arquivo regular começa com traço e um diretório começa com `d`.

`1`

Número de links para o arquivo.

`user staff`

Especifica a posse do arquivo. `user` é o proprietário do arquivo, o qual também está associado ao grupo `staff`.

`3606`

Tamanho do arquivo em bytes.

`Jan 13 2017`

Registro de data e hora da última modificação do arquivo.

`report2018.txt`

Nome do arquivo.

Temas como posse, permissões e links serão abordados em lições futuras. Como vemos, a versão em lista longa do `ls` é muitas vezes preferível à padrão.

##### Opções adicionais de ls

Eis algumas das maneiras mais comuns de se usar o comando `ls`. O usuário pode combinar várias opções para obter a saída desejada.

`ls -lh`

A combinação de *lista longa* com tamanhos de arquivo *legíveis para humanos* fornece sufixos úteis como `M` para megabytes ou `K` para quilobytes.

`ls -d */`

A opção `-d` lista os diretórios, mas não seu conteúdo. A combinação com `*/` mostra apenas os subdiretórios e nenhum arquivo.

`ls -lt`

Combina a *lista longa* com a opção de classificar por *data de modificação*. Os arquivos com as alterações mais recentes aparecem na parte superior e os arquivos com as alterações mais antigas, na parte inferior. Mas essa ordem pode ser invertida com:

`ls -lrt`

Combina a *lista longa* com *classificar por data (de modificação)*, junto com `-r`, que *inverte* a classificação. Agora, os arquivos com as alterações mais recentes aparecem na parte inferior da lista. Além de classificar por data de *modificação*, os arquivos também podem ser classificados por data de *acesso* ou data de alteração de *status*.

`ls -lX`

Combina a *lista longa* com a opção de classificar por *eXtensão de arquivo*. Serve, por exemplo, para agrupar todos os arquivos que terminam com `.txt`, todos os arquivos que terminam com `.jpg` e assim por diante.

`ls -S`

O `-S` classifica por *tamanho* de arquivo, da mesma forma que `-t` e `-X` classificam por data e extensão, respectivamente. Os arquivos maiores aparecerão primeiro e os menores, por último. Observe que o conteúdo dos subdiretórios *não* está incluído na classificação.

`ls -R`

A opção `-R` modifica o comando `ls` para exibir uma lista *recursiva*. O que isso significa?

##### A recursão no Bash

A recursão (ou recursividade) é uma situação em que “algo é definido em termos de si mesmo”. A recursão é um conceito importantíssimo nas ciências da computação, mas aqui seu significado é bem mais simples. Vamos considerar nosso exemplo de antes:

```bash
$ ls ~
Documents
```

Já sabemos que `user` possui um diretório inicial (home) e que nesse diretório existe um subdiretório. Até agora, o `ls` nos mostrou apenas os arquivos e subdiretórios de um local, sem informar qual o conteúdo desses subdiretórios. Nestas lições, usamos o comando `tree` para exibir o conteúdo de vários diretórios. Infelizmente, o `tree` não é um dos utilitários integrantes do Linux e, portanto, nem sempre está disponível. Compare a saída de `tree` com a saída de `ls -R` nos seguintes exemplos:

```bash
$ tree /home/user
user
└── Documents
├── Mission-Statement
└── Reports
└── report2018.txt

$ ls -R ~
/home/user/:
Documents

/home/user/Documents:
Mission-Statement
Reports

/home/user/Documents/Reports:
report2018.txt
```

Como você pode ver, com a opção recursiva, temos uma lista muito maior de arquivos. Na verdade, é como se rodássemos o comando `ls` no diretório inicial de `user` e encontrássemos um subdiretório. Entramos então nesse subdiretório e executamos o comando `ls` novamente. Encontramos o arquivo `Mission-Statement` e outro subdiretório chamado `Reports`. E, novamente, entramos nesse subdiretório e executamos o comando `ls` outra vez. Basicamente, executar o comando `ls -R` é como dizer ao Bash: “Execute o `ls` aqui e repita o comando em todos os subdiretórios que encontrar”.

A recursividade é particularmente importante nos comandos de modificação de arquivos, como copiar ou remover diretórios. Por exemplo, se você quiser copiar o subdiretório `Documents`, precisará especificar uma cópia recursiva para estender esse comando a todos os subdiretórios.

#### Exercícios Guiados

1. Use a estrutura de arquivos abaixo para responder às três questões a seguir:

  ```
  /
  ├── etc/
  │   ├── network/
  │   │   └── interfaces/
  │   ├── systemd/
  │   │   ├── resolved.conf
  │   │   ├── system/
  │   │   ├── system.conf
  │   │   ├── user/
  │   │   └── user.conf
  │   └── udev/
  │       ├── rules.d
  │       └── udev.conf
  └── home/
  ├── lost+found/
  ├── user/
  │   └── Documents/
  └── michael/
  └── Music/
  ```

  - Qual comando permite navegar até o diretório `network` independentemente de seu local atual?
  - Qual comando `user` poderia digitar para navegar até seu diretório `Documents` a partir de `/etc/udev`? Use o caminho mais curto possível.
  - Qual comando `user` poderia digitar para navegar até o diretório `Music` de `michael`? Use o caminho mais curto possível.

2. Considere a seguinte saída de `ls -lh` para responder às duas questões a seguir. Note que os diretórios são indicados com um `d` no início da linha.

  ```
  drwxrwxrwx  5 eric eric  4.0K Apr 26  2011 China/
  -rwxrwxrwx  1 eric eric  1.5M Jul 18  2011 img_0066.jpg
  ```

  ```
  -rwxrwxrwx  1 eric eric  1.5M Jul 18  2011 img_0067.jpg
  -rwxrwxrwx  1 eric eric  1.6M Jul 18  2011 img_0074.jpg
  -rwxrwxrwx  1 eric eric  1.8M Jul 18  2011 img_0075.jpg
  -rwxrwxrwx  1 eric eric   46K Jul 18  2011 scary.jpg
  -rwxrwxrwx  1 eric eric  469K Jan 29  2018 Screenshot from 2017-08-13 21-22-24.png
  -rwxrwxrwx  1 eric eric  498K Jan 29  2018 Screenshot from 2017-08-14 21-18-07.png
  -rwxrwxrwx  1 eric eric  211K Jan 29  2018 Screenshot from 2018-01-06 23-29-30.png
  -rwxrwxrwx  1 eric eric  150K Jul 18  2011 tobermory.jpg
  drwxrwxrwx  6 eric eric  4.0K Apr 26  2011 Tokyo/
  -rwxrwxrwx  1 eric eric  1.4M Jul 18  2011 Toronto 081.jpg
  -rwxrwxrwx  1 eric eric  1.4M Jul 18  2011 Toronto 085.jpg
  -rwxrwxrwx  1 eric eric  944K Jul 18  2011 Toronto 152.jpg
  -rwxrwxrwx  1 eric eric  728K Jul 18  2011 Toronto 173.jpg
  drwxrwxrwx  2 eric eric  4.0K Jun  5  2016 Wallpapers/
  ```

  - Ao rodar o comando `ls -lrS`, qual arquivo aparecerá no início?
  - Descreva o que você espera ver como saída de `ls -ad */`.

#### Exercícios Exploratórios

1. Rode o comando `ls -lh` num diretório que contenha subdiretórios. Observe o tamanho listado desses diretórios. Esses tamanhos de arquivo parecem corretos? Eles representam com precisão o conteúdo de todos os arquivos contidos naquele diretório?

2. Eis um novo comando a experimentar: `du -h`. Rode esse comando e descreva a saída resultante.

3. Em muitos sistemas Linux, podemos digitar `ll` e obter a mesma saída que teríamos com `ls -l`. Porém, note que `ll` não é um comando. Por exemplo, `man ll` exibirá a mensagem de que não existe uma página de manual para esse caso. Este é um exemplo de *alias*. Por que os aliases seriam úteis para um usuário?

#### Resumo

Nesta lição, você aprendeu:

- que cada usuário do Linux tem um diretório home,
- o diretório home do usuário atual pode ser acessado usando `~`,
- qualquer caminho de arquivo que use `~` é chamado de caminho *relativo-a-home*.

Você também aprendeu algumas das maneiras mais comuns de modificar o comando `ls`.

`-a` **(all)**

imprime todos os arquivos/diretórios, incluindo os ocultos

`-d` **(directories)**

lista os diretórios, mas não seu conteúdo

`-h` **(human readable)**

imprime o tamanho dos arquivos em formato legível para humanos

`-l` **(long list)**

fornece detalhes extras, um arquivo/diretório por linha

`-r` **(reverse)**

inverte a ordem de uma classificação

`-R` **(recursive)**

lista todos os arquivos, incluindo os que estão em cada subdiretório

`-S` **(size)**

classifica por tamanho de arquivo

`-t` **(time)**

classifica por data de modificação

`-X` **(eXtension)**

classifica por extensão de arquivo

#### Respostas aos Exercícios Guiados

1. Use a estrutura de arquivos abaixo para responder às três questões a seguir:

  ```
  /
  ├── etc/
  │   ├── network/
  │   │   └── interfaces/
  │   ├── systemd/
  │   │   ├── resolved.conf
  │   │   ├── system/
  │   │   ├── system.conf
  │   │   ├── user/
  │   │   └── user.conf
  │   └── udev/
  │       ├── rules.d
  │       └── udev.conf
  └── home/
  ├── lost+found/
  ├── user/
  │   └── Documents/
  └── michael/
  └── Music/
  ```

  - Qual comando permite navegar até o diretório `network` independentemente de seu local atual?

  ```
  cd /etc/network
  ```

  - Qual comando `user` poderia digitar para navegar até seu diretório `Documents` a partir de `/etc/udev`? Use o caminho mais curto possível.

  ```
  cd ~/Documents
  ```

  - Qual comando `user` poderia digitar para navegar até o diretório `Music` de `michael`? Use o caminho mais curto possível.

  ```
  cd ~michael/Music
  ```

2. Considere a seguinte saída de `ls -lh` para responder às duas questões a seguir. Note que os diretórios são indicados com um `d` no início da linha.

  ```
  drwxrwxrwx  5 eric eric  4.0K Apr 26  2011 China/
  -rwxrwxrwx  1 eric eric  1.5M Jul 18  2011 img_0066.jpg
  -rwxrwxrwx  1 eric eric  1.5M Jul 18  2011 img_0067.jpg
  -rwxrwxrwx  1 eric eric  1.6M Jul 18  2011 img_0074.jpg
  -rwxrwxrwx  1 eric eric  1.8M Jul 18  2011 img_0075.jpg
  -rwxrwxrwx  1 eric eric   46K Jul 18  2011 scary.jpg
  -rwxrwxrwx  1 eric eric  469K Jan 29  2018 Screenshot from 2017-08-13 21-22-24.png
  -rwxrwxrwx  1 eric eric  498K Jan 29  2018 Screenshot from 2017-08-14 21-18-07.png
  -rwxrwxrwx  1 eric eric  211K Jan 29  2018 Screenshot from 2018-01-06 23-29-30.png
  -rwxrwxrwx  1 eric eric  150K Jul 18  2011 tobermory.jpg
  drwxrwxrwx  6 eric eric  4.0K Apr 26  2011 Tokyo/
  -rwxrwxrwx  1 eric eric  1.4M Jul 18  2011 Toronto 081.jpg
  -rwxrwxrwx  1 eric eric  1.4M Jul 18  2011 Toronto 085.jpg
  -rwxrwxrwx  1 eric eric  944K Jul 18  2011 Toronto 152.jpg
  -rwxrwxrwx  1 eric eric  728K Jul 18  2011 Toronto 173.jpg
  drwxrwxrwx  2 eric eric  4.0K Jun  5  2016 Wallpapers/
  ```

  - Ao rodar o comando `ls -lrS`, qual arquivo aparecerá no início?

  Todas as pastas têm 4.0K, que é o menor tamanho de arquivo. Nesse caso, `ls` classifica alfabeticamente por padrão. A resposta correta é o arquivo `scary.jpg`

  - Descreva o que você espera ver como saída de `ls -ad */`.

  Esse comando exibe todos os subdiretórios, incluindo subdiretórios ocultos.

#### Respostas aos Exercícios Exploratórios

1. Rode o comando `ls -lh` num diretório que contenha subdiretórios. Observe o tamanho listado desses diretórios. Esses tamanhos de arquivo parecem corretos? Eles representam com precisão o conteúdo de todos os arquivos contidos naquele diretório?

  A resposta é não. Cada diretório tem um tamanho de arquivo listado como 4096 bytes. Isso acontece porque os diretórios, aqui, são uma abstração: eles não existem em forma de estrutura em árvore no disco. Quando vemos um diretório listado, na verdade estamos vendo um *link* para uma lista de arquivos. O tamanho desses links é de 4096 bytes.

2. Eis um novo comando a experimentar: `du -h`. Rode esse comando e descreva a saída resultante.

  O comando `du` gera uma lista com todos os arquivos e diretórios e indica o tamanho de cada um. Por exemplo, `du -s` exibe o tamanho de todos os arquivos, diretórios e subdiretórios em um determinado local.

3. . Em muitos sistemas Linux, podemos digitar `ll` e obter a mesma saída que teríamos com `ls` `-l`. Porém, note que `ll` não é um comando. Por exemplo, `man ll` exibirá a mensagem de que não existe uma página de manual para esse caso. Você acha que isso se relaciona a qual recurso da linha de comando?

  `ll` é um *alias* de `ls -l`. No Bash, podemos usar aliases para simplificar comandos usados com frequência. `ll` costuma já vir definido no Linux, mas também é possível criar os seus.

## 2.4 Criando, Movendo e Deletando Arquivos

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 2.4
- **Peso**: 2

**Áreas chave de conhecimento**

- Arquivos e diretórios
- Uso de maiúsculas e minúsculas
- Englobamento e uso de aspas

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `mv`, `cp`, `rm`, `touch`
- `mkdir`, `rmdir`

### 2.4 Lição 1

#### Introdução

Esta lição aborda o gerenciamento de arquivos e diretórios no Linux usando ferramentas de linha de comando.

Um arquivo é uma coleção de dados com um nome e um conjunto de atributos. Se, por exemplo, você transferisse algumas fotos de seu telefone para um computador e lhes desse nomes descritivos, você teria uma porção de arquivos de imagem no computador. Esses arquivos têm atributos, como a data e hora em que o arquivo foi acessado ou modificado pela última vez.

Um diretório é um tipo especial de arquivo usado para organizar arquivos. Uma boa maneira de pensar em diretórios é compará-los às pastas suspensas usadas para organizar papéis em um gaveteiro metálico. Porém, ao contrário das pastas de documentos em papel, podemos facilmente colocar diretórios dentro de outros diretórios.

A linha de comando é a maneira mais eficaz de gerenciar arquivos em um sistema Linux. As ferramentas da linha de comando e do shell têm recursos que tornam o uso da linha de comando mais rápido e fácil do que num gerenciador de arquivos gráfico.

Nesta seção, usaremos os comandos `ls`, `mv`, `cp`, `pwd`, `find`, `touch`, `rm`, `rmdir`, `echo`, `cat` e `mkdir` para gerenciar e organizar arquivos e diretórios.

##### Maiúsculas e minúsculas

Ao contrário do Microsoft Windows, os nomes de arquivos e diretórios nos sistemas Linux diferenciam maiúsculas de minúsculas. Isso significa que os nomes `/etc/` e `/ETC/` designam diretórios diferentes. Experimente os seguintes comandos:

```bash
$ cd /
$ ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
$ cd ETC
bash: cd: ETC: No such file or directory
$ pwd
/
$ cd etc
$ pwd
/etc
```

O `pwd` mostra o diretório em que você está no momento. Como vemos, tentar mudar para `/ETC` não funcionou, pois esse diretório não existe. Mas quando mudamos para o diretório `/etc`, que existe, a operação foi bem-sucedida.

##### Criando diretórios

O comando `mkdir` é usado para criar diretórios.

Vamos criar um novo diretório dentro do nosso diretório pessoal:

```bash
$ cd ~
$ pwd
/home/emma
$ ls
Desktop  Documents  Downloads
$ mkdir linux_essentials-2.4
$ ls
Desktop  Documents  Downloads  linux_essentials-2.4
$ cd linux_essentials-2.4
$ pwd
/home/emma/linux_essentials-2.4
```

Ao longo de toda esta lição, todos os comandos serão dados neste diretório ou em um de seus subdiretórios.

Para retornar facilmente ao diretório da lição a partir de qualquer outra posição em seu sistema de arquivos, use o comando:

```bash
$ cd ~/linux_essentials-2.4
```

O shell interpreta o caracter `~` como seu diretório inicial (home).

Quando estiver no diretório da lição, crie mais alguns diretórios para usar nos exercícios. Podemos adicionar todos os nomes de diretório, separados por espaços, ao `mkdir`:

```bash
$ mkdir creating moving copying/files copying/directories deleting/directories
deleting/files globs
mkdir: cannot create directory 'copying/files': No such file or directory
mkdir: cannot create directory 'copying/directories': No such file or directory
mkdir: cannot create directory 'deleting/directories': No such file or directory
mkdir: cannot create directory 'deleting/files': No such file or directory
$ ls
creating  globs  moving
```

Observe a mensagem de erro e que apenas `moving`, `globs` e `creating` foram criados. Os diretórios `copying` e `deleting` ainda não existem. O `mkdir`, por padrão, não cria um diretório dentro de um diretório que não existe. A opção `-p` ou `--parents` instrui o `mkdir` a criar diretórios pai caso eles não existam. Experimente o mesmo comando `mkdir` com a opção `-p`:

```bash
$ mkdir -p creating moving copying/files copying/directories deleting/directories
deleting/files globs
```

Desta vez, não apareceu nenhuma mensagem de erro. Vamos ver quais diretórios existem agora:

```bash
$ find
.
./creating
./moving
./globs
./copying
./copying/files
./copying/directories
```

```
./deleting
./deleting/directories
./deleting/files
```

O programa `find` é geralmente usado para procurar arquivos e diretórios, mas quando não definimos nenhuma opção, ele mostra uma lista de todos os arquivos, diretórios e subdiretórios do seu diretório atual.

> [!tip]
> Ao listar o conteúdo de um diretório com `ls`, as opções `-t` e `-r` são particularmente úteis. Elas ordenam a saída por tempo (`-t`) e invertem a ordem de classificação (`-r`). Nesse caso, os arquivos mais recentes estarão na parte inferior da saída.

##### Criando arquivos

Normalmente, os arquivos são criados pelos programas que trabalham com os dados armazenados nos arquivos. Um arquivo vazio pode ser criado usando o comando `touch`. Se executarmos o `touch` em um arquivo existente, o conteúdo do arquivo não será alterado, mas o registro de data e hora de modificação do arquivo será atualizado.

Execute o seguinte comando para criar alguns arquivos para a lição de globbing:

```bash
$ touch globs/question1 globs/question2012 globs/question23 globs/question13
globs/question14
$ touch globs/star10 globs/star1100 globs/star2002 globs/star2013
```

Em seguida, vamos verificar se todos os arquivos existem no diretório `globs`:

```bash
$ cd globs
$ ls
question1   question14    question23  star1100  star2013
question13  question2012  star10      star2002
```

Viu como o `touch` criou os arquivos? Podemos visualizar o conteúdo de um arquivo de texto com o comando `cat`. Experimente em um dos arquivos que acabamos de criar:

```bash
$ cat question14
```

Como `touch` cria arquivos vazios, não devem aparecer resultados. Podemos usar `echo` com `>` para criar arquivos de texto simples. Experimente:

```bash
$ echo hello > question15
$ cat question15
hello
```

`echo` exibe texto na linha de comando. O caractere `>` instrui o shell a escrever a saída de um comando no arquivo especificado, em vez do terminal. Isso faz com que a saída de `echo`, neste caso `hello`, seja gravada no arquivo `question15`. Isso não é específico ao `echo`, podendo ser usado com qualquer comando.

> [!warning]
> Cuidado ao usar `>`! Se já existir um arquivo com aquele nome, ele será sobrescrito!

##### Renomeando arquivos

O comando `mv` serve para mover e renomear arquivos.

Defina `moving` como seu diretório de trabalho:

```bash
$ cd ~/linux_essentials-2.4/moving
```

Crie alguns arquivos para praticar. Neste momento, você já deve estar familiarizado com estes comandos:

```bash
$ touch file1 file22
$ echo file3 > file3
$ echo file4 > file4
$ ls
file1  file22  file3  file4
```

Suponha que `file22` seja um erro de digitação; o correto seria `file2`. Corrija o nome com o comando `mv`. Ao renomear um arquivo, o primeiro argumento é o nome atual, o segundo é o novo nome:

```bash
$ mv file22 file2
$ ls
file1  file2  file3  file4
```

Tenha cuidado ao usar o comando `mv`. Se o novo nome já estiver atribuído a um arquivo existente, ele será sobrescrito. Vamos testar com `file3` e `file4`:

```bash
$ cat file3
file3
$ cat file4
file4
$ mv file4 file3
$ cat file3
file4
$ ls
file1  file2  file3
```

Note que o conteúdo de `file3` agora está em `file4`. Use a opção `-i` para que `mv` avise caso você esteja prestes a sobrescrever um arquivo existente. Experimente:

```bash
$ touch file4 file5
$ mv -i file4 file3
mv: overwrite 'file3'? y
```

##### Movendo arquivos

Os arquivos são movidos de um diretório para outro com o comando `mv`.

Crie alguns diretórios para os quais moveremos arquivos:

```bash
$ cd ~/linux_essentials-2.4/moving
$ mkdir dir1 dir2
$ ls
dir1  dir2  file1  file2  file3  file5
```

Mova `file1` para `dir1`:

```bash
$ mv file1 dir1
$ ls
dir1  dir2  file2  file3  file5
$ ls dir1
file1
```

Observe como o último argumento para `mv` é o diretório de destino. Sempre que o último argumento para `mv` for um diretório, os arquivos serão movidos para ele. É possivel especificar diversos arquivos em um único comando `mv`:

```bash
$ mv file2 file3 dir2
$ ls
dir1  dir2  file5
$ ls dir2
file2  file3
```

Também podemos usar o `mv` para mover e renomear diretórios. Renomeie `dir1` como `dir3`:

```bash
$ ls
dir1  dir2  file5
$ ls dir1
file1
$ mv dir1 dir3
$ ls
dir2  dir3  file5
$ ls dir3
file1
```

##### Excluindo arquivos e diretórios

O comando `rm` serve para excluir arquivos e diretórios, ao passo que o comando `rmdir` pode excluir apenas diretórios. Vamos limpar o diretório `moving` excluindo `file5`:

```bash
$ cd ~/linux_essentials-2.4/moving
$ ls
dir2  dir3  file5
$ rmdir file5
rmdir: failed to remove 'file5': Not a directory
$ rm file5
$ ls
dir2  dir3
```

Por padrão, o `rmdir` pode excluir apenas diretórios vazios; portanto, tivemos de usar `rm` para excluir um arquivo comum. Tente excluir o diretório `deleting`:

```bash
$ cd ~/linux_essentials-2.4/
$ ls
copying  creating  deleting  globs  moving
$ rmdir deleting
rmdir: failed to remove 'deleting': Directory not empty
```

```bash
$ ls -l deleting
total 0
drwxrwxr-x. 2 emma emma 6 Mar 26 14:58 directories
drwxrwxr-x. 2 emma emma 6 Mar 26 14:58 files
```

Como vimos, o `rmdir` se recusa a excluir um diretório que não esteja vazio. Use `rmdir` para remover um dos subdiretórios vazios do diretório `deleting`:

```bash
$ ls -a deleting/files
.  ..
$ rmdir deleting/files
$ ls -l deleting
directories
```

Excluir um grande número de arquivos ou estruturas de diretórios profundas, com muitos subdiretórios, pode parecer uma tarefa entediante, mas na verdade é fácil. Por padrão, o `rm` funciona apenas em arquivos regulares. A opção `-r` é usada para anular esse comportamento. Tenha cuidado, `rm -r` pode acabar sendo um tiro no pé! Quando usamos a opção `-r`, o `rm` não somente exclui qualquer diretório, como também tudo o que estiver dentro desse diretório, incluindo os subdiretórios e seu conteúdo. Veja você mesmo como o `rm -r` funciona:

```bash
$ ls
copying  creating  deleting  globs  moving
$ rm deleting
rm: cannot remove 'deleting': Is a directory
$ ls -l deleting
total 0
drwxrwxr-x. 2 emma emma 6 Mar 26 14:58 directories
$ rm -r deleting
$ ls
copying  creating  globs  moving
```

Percebeu que `deleting` se foi, mesmo não estando vazio? Como o `mv`, o `rm` tem uma opção `-i` para exibir um aviso antes de executar qualquer ação. Use `rm -ri` para remover os diretórios da seção `moving` que não forem mais necessários:

```bash
$ find
.
./creating
./moving
```

```
./moving/dir2
./moving/dir2/file2
./moving/dir2/file3
./moving/dir3
./moving/dir3/file1
./globs
./globs/question1
./globs/question2012
./globs/question23
./globs/question13
./globs/question14
./globs/star10
./globs/star1100
./globs/star2002
./globs/star2013
./globs/question15
./copying
./copying/files
./copying/directories
$ rm -ri moving
rm: descend into directory 'moving'? y
rm: descend into directory 'moving/dir2'? y
rm: remove regular empty file 'moving/dir2/file2'? y
rm: remove regular empty file 'moving/dir2/file3'? y
rm: remove directory 'moving/dir2'? y
rm: descend into directory 'moving/dir3'? y
rm: remove regular empty file 'moving/dir3/file1'? y
rm: remove directory 'moving/dir3'? y
rm: remove directory 'moving'? y
```

##### Copiando arquivos e diretórios

O comando `cp` é usado para copiar arquivos e diretórios. Copie alguns arquivos para o diretório `copying`:

```bash
$ cd ~/linux_essentials-2.4/copying
$ ls
directories  files
$ cp /etc/nsswitch.conf files/nsswitch.conf
$ cp /etc/issue /etc/hostname files
```

Se o último argumento for um diretório, o `cp` criará uma cópia dos argumentos anteriores dentro do diretório. Como no caso de `mv`, vários arquivos podem ser especificados ao mesmo tempo, desde que o destino seja um diretório.

Quando os dois operandos de `cp` são arquivos e os dois arquivos existem, o `cp` sobrescreve o segundo arquivo com uma cópia do primeiro arquivo. Para comprovar, vamos substituir o arquivo `issue` pelo arquivo `hostname`:

```bash
$ cd ~/linux_essentials-2.4/copying/files
$ ls
hostname  issue  nsswitch.conf
$ cat hostname
mycomputer
$ cat issue
Debian GNU/Linux 9 \n \l

$ cp hostname issue
$ cat issue
mycomputer
```

Agora, vamos tentar criar uma cópia do diretório `files` dentro do diretório `directory`:

```bash
$ cd ~/linux_essentials-2.4/copying
$ cp files directories
cp: omitting directory 'files'
```

Como vemos, o `cp`, por padrão, só funciona em arquivos individuais. Para copiar um diretório, usamos a opção `-r`. Lembre-se de que a opção `-r` fará com que `cp` também copie o conteúdo do diretório que está sendo copiado:

```bash
$ cp -r files directories
$ find
.
./files
./files/nsswitch.conf
./files/fstab
./files/hostname
./directories
./directories/files
./directories/files/nsswitch.conf
./directories/files/fstab
./directories/files/hostname
```

Percebeu que, quando um diretório existente é usado como destino, o `cp` cria uma cópia do diretório de origem dentro dele? Se o destino não existir, ele será criado e preenchido com o conteúdo do diretório de origem:

```bash
$ cp -r files files2
$ find
.
./files
./files/nsswitch.conf
./files/fstab
./files/hostname
./directories
./directories/files
./directories/files/nsswitch.conf
./directories/files/fstab
./directories/files/hostname
./files2
./files2/nsswitch.conf
./files2/fstab
./files2/hostname
```

##### Globbing

Costumamos chamar de globbing uma linguagem simples de correspondência de padrões. Os shells da linha de comando nos sistemas Linux usam essa linguagem para buscar grupos de arquivos cujos nomes correspondam a um padrão específico. O POSIX.1-2017 especifica os seguintes padrões para a correspondência de caracteres:

`*`

Corresponde a qualquer número de quaisquer caracteres, incluindo nenhum caractere

`?`

Corresponde a qualquer caractere

`[]`

Corresponde a uma classe de caracteres

Em bom português, isso significa que você pode dizer ao seu shell para procurar por um padrão, em vez de uma sequência literal de texto. Geralmente, os usuários do Linux especificam diversos arquivos com um glob em vez de digitar o nome de cada arquivo. Execute os seguintes comandos:

```bash
$ cd ~/linux_essentials-2.4/globs
$ ls
question1   question14  question2012  star10    star2002
question13  question15  question23    star1100  star2013
$ ls star1*
star10  star1100
$ ls star*
star10  star1100  star2002  star2013
$ ls star2*
star2002  star2013
$ ls star2*2
star2002
$ ls star2013*
star2013
```

O shell expande `*` para qualquer número de qualquer coisa, e assim ele interpreta `star*` como sendo qualquer coisa, dentro do contexto relevante, que comece com `star`. Quando você executa o comando `ls star*`, o shell não executa o programa `ls` com um argumento `star*`, mas sim procura por arquivos no diretório atual que correspondam ao padrão `star*`(incluindo apenas `star`), e transforma cada arquivo correspondente ao padrão em um argumento para `ls`:

```bash
$ ls star*
```

No que diz respeito ao `ls`, isso é o equivalente a

```bash
$ ls star10  star1100  star2002  star2013
```

O caractere `*` não significa nada para `ls`. Para comprovar, execute o seguinte comando:

```bash
$ ls star\*
ls: cannot access star*: No such file or directory
```

Quando colocamos `\` antes de um caractere, estamos instruindo seu shell a não interpretá-lo. Neste caso, queremos que `ls` tenha um argumento `star*`, em vez da expansão feita pelo glob `star*`.

O `?` expande para qualquer caractere único. Experimente os seguintes comandos para ver por si mesmo:

```bash
$ ls
question1   question14  question2012  star10    star2002
question13  question15  question23    star1100  star2013
$ ls question?
question1
$ ls question1?
question13  question14  question15
$ ls question?3
question13  question23
$ ls question13?
ls: cannot access question13?: No such file or directory
```

Os colchetes `[]` são usados para combinar faixas ou classes de caracteres. Os colchetes `[]` funcionam como nas expressões regulares POSIX, exceto porque, nos globs, o `^` é usado no lugar de `!`.

Crie alguns arquivos para experimentar:

```bash
$ mkdir brackets
$ cd brackets
$ touch file1 file2 file3 file4 filea fileb filec file5 file6 file7
```

Os intervalos entre colchetes `[]` são expressos usando um `-`:

```bash
$ ls
file1  file2  file3  file4  file5  file6  file7  filea  fileb  filec
$ ls file[1-2]
file1  file2
$ ls file[1-3]
file1  file2  file3
```

É possível especificar vários intervalos:

```bash
$ ls file[1-25-7]
file1  file2  file5  file6  file7
$ ls file[1-35-6a-c]
file1  file2  file3  file5  file6  filea  fileb  filec
```

Os colchetes também podem ser usados para encontrar um conjunto específico de caracteres correspondentes.

```bash
$ ls file[1a5]
file1  file5  filea
```

Também usamos o caractere `^` como o primeiro caractere para encontrar todas as correspondências, exceto determinados caracteres.

```bash
$ ls file[^a]
file1  file2  file3  file4  file5  file6  file7  fileb  filec
```

A última coisa que abordaremos nesta lição são as classes de caracteres. Para buscar correspondências em uma classe de caracteres, use `[:classname:]`. Por exemplo, para usar a classe digit, que corresponde aos números, faríamos algo assim:

```bash
$ ls file[[:digit:]]
file1  file2  file3  file4  file5  file6  file7
$ touch file1a file11
$ ls file[[:digit:]a]
file1  file2  file3  file4  file5  file6  file7  filea
$ ls file[[:digit:]]a
file1a
```

O glob `file[[:digit:]a]` corresponde a `file` seguido por um dígito ou `a`.

As classes de caracteres suportadas dependem da sua localidade atual. O POSIX requer as seguintes classes de caracteres para todas as localidades:

`[:alnum:]`

Letras e números.

`[:alpha:]`

Maiúsculas ou minúsculas.

`[:blank:]`

Espaços e tabulações.

`[:cntrl:]`

Caracteres de controle, como backspace, bell, confirmação negativa, escape.

`[:digit:]`

Numerais (`0123456789`).

`[:graph:]`

Caracteres gráficos (todos os caracteres, exceto `ctrl` e o caractere de espaço)

`[:lower:]`

Letras minúsculas (`a-z`).

`[:print:]`

Caracteres imprimíveis (`alnum`, `punct` e o caractere de espaço).

`[:punct:]`

Caracteres de pontuação, ou seja, `!`, `&`, `"`.

`[:space:]`

Caracteres de espaço em branco, por exemplo, tabulações, espaços, novas linhas.

`[:upper:]`

Letras maiúsculas (`A-Z`).

`[:xdigit:]`

Números hexadecimais (geralmente `0123456789abcdefABCDEF`).

#### Exercícios Guiados

1. Dadas as informações a seguir, selecione os diretórios que seriam criados com o comando `mkdir -p /tmp/outfiles/text/today /tmp/infiles/text/today`

  ```bash
  $ pwd
  /tmp
  $ find
  .
  ./outfiles
  ./outfiles/text
  ```

| `/tmp` |  |
|---|---|
| `/tmp/outfiles` |  |
| `/tmp/outfiles/text` |  |
| `/tmp/outfiles/text/today` |  |
| `/tmp/infiles` |  |
| `/tmp/infiles/text` |  |
| `/tmp/infiles/text/today` |  |

2. O que `-v` faz em `mkdir`, `rm` e `cp`?

3. O que acontece se você acidentalmente tentar copiar três arquivos na mesma linha de comando para um arquivo que já existe em vez de um diretório?

4. O que acontece quando você usa `mv` para mover um diretório para dentro de si mesmo?

5. Como você excluiria todos os arquivos no diretório atual que começa com `old`?

6. Qual dos seguintes arquivos corresponderia a `log_[a-z]_201?_*_01.txt`?

  `log_3_2017_Jan_01.txt`

  `log_+_2017_Feb_01.txt`

| `log_b_2007_Mar_01.txt` |  |
|---|---|
| `log_f_201A_Wednesday_01.txt` |  |

7. Crie alguns globs que correspondam à seguinte lista de nomes de arquivos:

  ```
  doc100
  doc200
  doc301
  doc401
  ```

#### Exercícios Exploratórios

1. Use a página do manual de `cp` para descobrir como fazer uma cópia de um arquivo com as permissões e a data de modificação correspondentes às do original.

2. O que o comando `rmdir -p` faz? Experimente-o e explique como ele difere de `rm -r`.

3. NÃO EXECUTE ESTE COMANDO: O que você acha que `rm -ri / *` pode fazer? (É SÉRIO, NÃO TENTE EXECUTÁ-LO!)

4. Além de usar `-i`, é possível impedir que o `mv` sobrescreva os arquivos de destino?

5. Explique o comando `cp -u`.

#### Resumo

O ambiente de linha de comando do Linux fornece ferramentas para gerenciar arquivos. Algumas das mais usadas são `cp`, `mv`, `mkdir`, `rm` e `rmdir`. Essas ferramentas, combinadas com globs, permitem realizar tarefas com mais rapidez.

Muitos comandos têm uma opção `-i`, que solicita uma confirmação antes de fazer qualquer coisa. Essa confirmação ajuda a evitar muitos aborrecimentos se você digitar algo errado.

Muitos comandos incluem uma opção `-r`. A opção `-r` normalmente significa recursão. Em matemática e ciência da computação, uma função recursiva é uma função que utiliza a si mesma em sua definição. Quando se trata de ferramentas de linha de comando, geralmente significa aplicar o comando a um diretório e tudo o que está contido nele.

Comandos usados nesta lição:

`cat`

Lê e exibe o conteúdo de um arquivo.

`cp`

Copia arquivos ou diretórios.

`echo`

Exibe um conjunto de caracteres.

`find`

Atravessa uma árvore do sistema de arquivos e procura por arquivos que correspondam a um conjunto específico de critérios.

`ls`

Mostra as propriedades dos arquivos e diretórios e lista o conteúdo de um diretório.

`mkdir`

Cria novos diretórios.

`mv`

Move ou renomeia arquivos ou diretórios.

`pwd`

Exibe o diretório de trabalho atual.. `rm`

Exclui arquivos ou diretórios.

`rmdir`

Exclui diretórios.

`touch`

Cria novos arquivos vazios ou atualiza a data de modificação de um arquivo existente.

#### Respostas aos Exercícios Guiados

1. Dadas as informações a seguir, selecione os diretórios que seriam criados com o comando `mkdir -p /tmp/outfiles/text/today /tmp/infiles/text/today`

  ```bash
  $ pwd
  /tmp
  $ find
  .
  ./outfiles
  ./outfiles/text
  ```

  Os diretórios marcados seriam criados. Os diretórios `/tmp`, `/tmp/outfiles` e `/tmp/outfiles/text` já existem, por isso o `mkdir` os ignora.

| `/tmp` |  |
|---|---|
| `/tmp/outfiles` |  |
| `/tmp/outfiles/text` |  |
| `/tmp/outfiles/text/today` | X |
| `/tmp/infiles` | X |
| `/tmp/infiles/text` | X |
| `/tmp/infiles/text/today` | X |

2. O que `-v` faz em `mkdir`, `rm` e `cp`?

  Normalmente, `-v` ativa a saída detalhada. Ele faz com que os programas respectivos exibam o que estão fazendo no momento em que o fazem:

  ```bash
  $ rm -v a b
  removed 'a'
  removed 'b'
  $ mv -v a b
  'a' -> 'b'
  $ cp -v b c
  'b' -> 'c'
  ```

3. O que acontece se você acidentalmente tentar copiar três arquivos na mesma linha de comando para um arquivo que já existe em vez de um diretório? `cp` se recusará a fazer qualquer coisa e exibirá uma mensagem de erro:

  ```bash
  $ touch a b c d
  $ cp a b c d
  cp: target 'd' is not a directory
  ```

4. O que acontece quando você usa `mv` para mover um diretório para dentro de si mesmo?

  Aparece uma mensagem de erro dizendo que `mv` não pode fazer isso.

  ```bash
  $ mv a a
  mv: cannot move 'a' to a subdirectory of itself, 'a/a'
  ```

5. Como você excluiria todos os arquivos no diretório atual que começa com `old`?

  Seria preciso usar o glob `old*` com `rm`:

  ```bash
  $ rm old*
  ```

6. Qual dos seguintes arquivos corresponderia a `log_[a-z]_201?_*_01.txt`?

  `log_3_2017_Jan_01.txt`

  `log_+_2017_Feb_01.txt`

  `log_b_2007_Mar_01.txt`

  `log_f_201A_Wednesday_01.txt` X

  ```bash
  $ ls log_[a-z]_201?_*_01.txt
  log_f_201A_Wednesday_01.txt
  ```

  `log_[a-z]` busca por `log_` seguido por qualquer letra minúscula, então `log_f_201A_Wednesday_01.txt` e `log_b_2007_Mar_01.txt` corresponderiam. `_201?` busca qualquer caractere único, então apenas `log_f_201A_Wednesday_01.txt` corresponderia. Finalmente, `*_01.txt` busca qualquer coisa que termine com `_01.txt`, o que corresponderia à opção restante.

7. Crie alguns globs que correspondam à seguinte lista de nomes de arquivos:

  ```
  doc100
  ```

  ```
  doc200
  doc301
  doc401
  ```

  Existem várias soluções. Eis algumas delas:

  ```
  doc*
  doc[1-4]*
  doc?0?
  doc[1-4]0?
  ```

#### Respostas aos Exercícios Exploratórios

1. Use a página do manual de `cp` para descobrir como fazer uma cópia de um arquivo com as permissões e a data de modificação correspondentes às do original.

  Usaríamos nesse caso a opção `-p`. Segundo a página man:

  ```bash
  $ man cp
  -p     same as --preserve=mode,ownership,timestamps
  --preserve[=ATTR_LIST]
  preserve the specified attributes (default: mode,ownership,time‐
  stamps), if  possible  additional  attributes:  context,  links,
  xattr, all
  ```

2. O que o comando `rmdir -p` faz? Experimente-o e explique como ele difere de `rm -r`.

  Ele faz com que `rmdir` se comporte de maneira semelhante a `mkdir -p`. Se for passado em uma árvore de diretórios vazios, ele removerá todos eles.

  ```bash
  $ find
  .
  ./a
  ./a/b
  ./a/b/c
  $ rmdir -p a/b/c
  $ ls
  ```

3. NÃO EXECUTE ESTE COMANDO: O que você acha que `rm -ri / *` pode fazer? (É SÉRIO, NÃO TENTE EXECUTÁ-LO!)

  Ele remove todos os arquivos e diretórios com permissão de escrita em sua conta de usuário. Isso inclui quaisquer sistemas de arquivos de rede.

4. Além de usar `-i`, é possível impedir que o `mv` sobrescreva os arquivos de destino?

  Sim, a opção `-n` ou `--no-clobber` impede que `mv` sobrescreva arquivos.

  ```bash
  $ cat a
  a
  $ cat b
  b
  ```

  ```bash
  $ mv -n a b
  $ cat b
  b
  ```

5. Explique `cp -u`.

  A opção `-u` faz com que `cp` só copie um arquivo se o destino estiver ausente ou for mais antigo que o arquivo de origem.

  ```bash
  $ ls -l
  total 24K
  drwxr-xr-x 123 emma student  12K Feb  2 05:34 ..
  drwxr-xr-x   2 emma student 4.0K Feb  2 06:56 .
  -rw-r--r--   1 emma student    2 Feb  2 06:56 a
  -rw-r--r--   1 emma student    2 Feb  2 07:00 b
  $ cat a
  a
  $ cat b
  b
  $ cp -u a b
  $ cat b
  b
  $ cp -u a c
  $ ls -l
  total 12
  -rw-r--r-- 1 emma student 2 Feb  2 06:56 a
  -rw-r--r-- 1 emma student 2 Feb  2 07:00 b
  -rw-r--r-- 1 emma student 2 Feb  2 07:00 c
  ```

---
*Fonte: Linux Professional Institute, Materiais Didáticos Linux Essentials (learning.lpi.org), licença CC BY-NC-ND 4.0. Conversão do PDF para Markdown apenas para estudo pessoal.*
