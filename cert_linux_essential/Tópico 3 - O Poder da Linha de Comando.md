---
tags: [lpi, linux-essentials, 010-160]
topico: 3
certificacao: LPI Linux Essentials 010-160 (v1.6)
---

# Tópico 3: O Poder da Linha de Comando

## 3.1 Empacotando arquivos na linha de comando

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 3.1
- **Peso**: 2

**Áreas chave de conhecimento**

- Arquivos, diretórios
- Pacotes, compressão

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `tar`
- Opções comuns do `tar`
- `gzip`, `bzip2`, `xz`
- `zip`, `unzip`

### 3.1 Lição 1

| **Certificate:** | Linux Essentials |
|---|---|
| **Version:** | 1.6 |
| **Topic:** | 3 O poder da linha de comando |
| **Objective:** | 3.1 Como comprimir arquivos com a linha de comando |
| **Lesson:** | 1 of 1 |

#### Introdução

A compressão é usada para reduzir a quantidade de espaço que um conjunto específico de dados consome. Em geral, recorremos a ela para reduzir a quantidade de espaço necessária para armazenar um arquivo. Outro uso comum é reduzir a quantidade de dados enviados através de uma conexão de rede.

A compressão substitui os padrões repetitivos presentes nos dados. Imagine um romance. Algumas palavras são extremamente comuns, mas têm mais de um caractere, como a palavra “mas”. É possível reduzir bastante o tamanho do romance substituindo essas palavras comuns com vários caracteres por outras formadas por um único caractere - por exemplo, substituindo “mas” por uma letra grega que não é usada em nenhuma outra parte do texto. Os algoritmos de compressão de dados funcionam de maneira semelhante, mas mais complexa.

Há duas variedades de compressão: *sem perda* e *com perda*. Os arquivos comprimidos com um algoritmo sem perda podem ser descomprimidos em sua forma original. Já os dados comprimidos com um algoritmo com perda não podem ser recuperados. Os algoritmos com perda são frequentemente usados para imagens, vídeos e áudios em que a perda de qualidade é imperceptível para os seres humanos, irrelevante para o contexto, ou em que a economia de espaço e de taxa de transferência de rede compensam a perda.

Usamos ferramentas de empacotamento para agrupar arquivos e diretórios em um único arquivo. Alguns usos comuns são backups, empacotamento de código-fonte de software e retenção de dados.

O empacotamento e a compressão são comumente usados juntos. Algumas ferramentas de empacotamento também comprimem seu conteúdo por padrão. Outras trazem a opção de comprimir o conteúdo. Algumas ferramentas de empacotamento devem ser usadas em conjunto com ferramentas de compressão independentes, caso se deseje comprimir o conteúdo.

A ferramenta mais comum para empacotar arquivos em sistemas Linux é o `tar`. A maioria das distribuições Linux é fornecida com a versão GNU do `tar`, e por isso a usaremos nesta lição. O `tar`, por si só, gerencia o empacotamento de arquivos, mas não os comprime.

Existem muitas ferramentas de compressão disponíveis no Linux. Dentre as sem perdas, encontramos comumente `bzip2`, `gzip` e `xz`. As três estão presentes na maioria dos sistemas. Em sistemas antigos ou muito minimalistas, o `xz` ou o `bzip` talvez não estejam instalados. Se você se tornar um usuário regular do Linux, provavelmente vai encontrar arquivos comprimidos com todas as três. Elas usam algoritmos diferentes; portanto, um arquivo comprimido com uma ferramenta não pode ser descomprimido por outra. As ferramentas de compressão exigem uma escolha: se você deseja uma alta taxa de compressão, levará mais tempo para comprimir e descomprimir o arquivo. Isso ocorre porque uma compressão mais alta demanda mais trabalho para encontrar padrões mais complexos. Todas essas ferramentas comprimem dados, mas não podem criar pacotes contendo vários arquivos.

Ferramentas exclusivas para compressão não costumam estar disponíveis nos sistemas Windows. As ferramentas de empacotamento e compressão do Windows geralmente são agrupadas. Lembre-se disso caso possua sistemas Linux e Windows que precisam compartilhar arquivos.

Os sistemas Linux também trazem ferramentas para lidar com os arquivos `.zip`, comumente usados no sistema Windows. Elas se chamam `zip` e `unzip`. Essas ferramentas não vêm instaladas por padrão em todos os sistemas; se você precisar delas, poderá ser necessário instalá-las. Felizmente, elas costumam estar presentes nos repositórios de pacotes das distribuições.

##### Ferramentas de compressão

A quantidade de espaço em disco economizada pela compressão de arquivos depende de alguns fatores: a natureza dos dados que estão sendo comprimidos, o algoritmo usado para comprimir os dados e o nível de compressão. Nem todos os algoritmos suportam níveis de compressão diferentes.

Vamos começar preparando alguns arquivos de teste para comprimir:

```bash
$ mkdir ~/linux_essentials-3.1
$ cd ~/linux_essentials-3.1
$ mkdir compression archiving
$ cd compression
$ cat /etc/* > bigfile 2> /dev/null
```

Agora, criamos três cópias desse arquivo:

```bash
$ cp bigfile bigfile2
$ cp bigfile bigfile3
$ cp bigfile bigfile4
$ ls -lh
total 2.8M
-rw-r--r-- 1 emma emma 712K Jun 23 08:08 bigfile
-rw-r--r-- 1 emma emma 712K Jun 23 08:08 bigfile2
-rw-r--r-- 1 emma emma 712K Jun 23 08:08 bigfile3
-rw-r--r-- 1 emma emma 712K Jun 23 08:08 bigfile4
```

Em seguida vamos comprimir os arquivos com cada uma das ferramentas de compressão mencionadas:

```bash
$ bzip2 bigfile2
$ gzip bigfile3
$ xz bigfile4
$ ls -lh
total 1.2M
-rw-r--r-- 1 emma emma 712K Jun 23 08:08 bigfile
-rw-r--r-- 1 emma emma 170K Jun 23 08:08 bigfile2.bz2
-rw-r--r-- 1 emma emma 179K Jun 23 08:08 bigfile3.gz
-rw-r--r-- 1 emma emma 144K Jun 23 08:08 bigfile4.xz
```

Compare o tamanho dos arquivos comprimidos com o arquivo descomprimido chamado `bigfile`. Observe também como as ferramentas de compressão adicionaram extensões aos nomes dos arquivos e removeram os arquivos não comprimidos.

Use `bunzip2`, `gunzip` ou `unxz` para descomprimir os arquivos:

```bash
$ bunzip2 bigfile2.bz2
$ gunzip bigfile3.gz
$ unxz bigfile4.xz
$ ls -lh
total 2.8M
-rw-r--r-- 1 emma emma 712K Jun 23 08:20 bigfile
-rw-r--r-- 1 emma emma 712K Jun 23 08:20 bigfile2
-rw-r--r-- 1 emma emma 712K Jun 23 08:20 bigfile3
-rw-r--r-- 1 emma emma 712K Jun 23 08:20 bigfile4
```

Observe que, desta vez, o arquivo comprimido foi excluído depois de descomprimido.

Certas ferramentas permitem diferentes níveis de compressão. Um nível de compressão mais alto geralmente requer mais memória e ciclos de CPU, mas resulta em um arquivo comprimido menor. O oposto é verdadeiro para um nível mais baixo. Veja abaixo uma demonstração com `xz` e `gzip`:

```bash
$ cp bigfile bigfile-gz1
$ cp bigfile bigfile-gz9
$ gzip -1 bigfile-gz1
$ gzip -9 bigfile-gz9
$ cp bigfile bigfile-xz1
$ cp bigfile bigfile-xz9
$ xz -1 bigfile bigfile-xz1
$ xz -9 bigfile bigfile-xz9
$ ls -lh bigfile bigfile-* *
total 3.5M
-rw-r--r-- 1 emma emma 712K Jun 23 08:08 bigfile
-rw-r--r-- 1 emma emma 205K Jun 23 13:14 bigfile-gz1.gz
-rw-r--r-- 1 emma emma 178K Jun 23 13:14 bigfile-gz9.gz
-rw-r--r-- 1 emma emma 156K Jun 23 08:08 bigfile-xz1.xz
-rw-r--r-- 1 emma emma 143K Jun 23 08:08 bigfile-xz9.xz
```

Não é necessário descomprimir um arquivo toda vez que ele for usado. As ferramentas de compressão geralmente vêm com versões especiais de ferramentas comuns usadas para ler arquivos de texto. Por exemplo, o `gzip` tem uma versão de `cat`, `grep`, `diff`, `less`, `more` e algumas outras. No `gzip`, as ferramentas são prefixadas com um `z`, enquanto o prefixo `bz` existe para o `bzip2` e `xz` para o `xz`. Veja abaixo um exemplo do uso de `zcat` para ler um arquivo compactado com `gzip`:

```bash
$ cp /etc/hosts ./
$ gzip hosts
```

```bash
$ zcat hosts.gz
127.0.0.1   localhost

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

##### Ferramentas de empacotamento

O programa `tar` é provavelmente a ferramenta de empacotamento mais usada nos sistemas Linux. Caso você esteja se perguntando por que ela tem esse nome, trata-se de uma abreviação de “tape archive” (arquivo de fita). Os arquivos criados com o `tar` são apelidados de *tar balls*. É muito comum que aplicativos distribuídos na forma de código-fonte estejam em tar balls.

A versão GNU do `tar` incluída nas distribuições Linux tem muitas opções. Esta lição abordará o subconjunto mais usado.

Vamos começar criando um pacote com os arquivos usados para a compressão:

```bash
$ cd ~/linux_essentials-3.1
$ tar cf archiving/3.1.tar compression
```

A opção `c` instrui o `tar` a criar um novo arquivo e a opção `f` é o nome do arquivo a ser criado. O argumento imediatamente após as opções sempre será o nome do arquivo no qual trabalhar. O restante dos argumentos são os caminhos para quaisquer arquivos ou diretórios que você deseje adicionar, listar ou extrair do arquivo. No exemplo, adicionamos o diretório `compression` e todo o seu conteúdo ao pacote.

Para visualizar o conteúdo de um tar ball, use a opção `t` do `tar`:

```bash
$ tar -tf 3.1.tar
compression/
compression/bigfile-xz1.xz
compression/bigfile-gz9.gz
compression/hosts.gz
compression/bigfile2
compression/bigfile
compression/bigfile-gz1.gz
compression/bigfile-xz9.xz
compression/bigfile3
```

```
compression/bigfile4
```

Note que as opções são precedidas por `-`. Ao contrário da maioria dos programas, com o `tar` o `-` não é necessário ao especificar opções, embora não cause nenhum dano se for usado.

> [!note]
> Use a opção `-v` para permitir que o `tar` exiba o nome dos arquivos nos quais opera ao criar ou extrair um pacote.

Agora vamos extrair o arquivo:

```bash
$ cd ~/linux_essentials-3.1/archiving
$ ls
3.1.tar
$ tar xf 3.1.tar
$ ls
3.1.tar  compression
```

Suponha que você precise apenas de um arquivo que esteja no pacote. Se for esse o caso, você pode especificá-lo após o nome de arquivo do pacote. É possível especificar vários arquivos, se necessário:

```bash
$ cd ~/linux_essentials-3.1/archiving
$ rm -rf compression
$ ls
3.1.tar
$ tar xvf 3.1.tar compression/hosts.gz
compression/
compression/bigfile-xz1.xz
compression/bigfile-gz9.gz
compression/hosts.gz
compression/bigfile2
compression/bigfile
compression/bigfile-gz1.gz
compression/bigfile-xz9.xz
compression/bigfile3
compression/bigfile4
$ ls
3.1.tar  compression
$ ls compression
hosts.gz
```

Com exceção dos caminhos absolutos (caminhos começando com `/`), os arquivos `tar` preservam todo o caminho dos arquivos quando eles são criados. Como o arquivo `3.1.tar` foi criado com um único diretório, esse diretório será criado em relação ao seu diretório de trabalho atual quando for extraído. Para que isso fique mais claro, eis outro exemplo:

```bash
$ cd ~/linux_essentials-3.1/archiving
$ rm -rf compression
$ cd ../compression
$ tar cf ../tar/3.1-nodir.tar *
$ cd ../archiving
$ mkdir untar
$ cd untar
$ tar -xf ../3.1-nodir.tar
$ ls
bigfile   bigfile3  bigfile-gz1.gz  bigfile-xz1.xz  hosts.gz
bigfile2  bigfile4  bigfile-gz9.gz  bigfile-xz9.xz
```

> [!tip]
> Caso queira usar o caminho absoluto em um arquivo `tar`, é necessário empregar a opção `P`. Esteja ciente de que isso pode sobrescrever arquivos importantes e causar erros no sistema.

O programa `tar` também pode gerenciar a compressão e descompressão de arquivos em tempo real. Para isso, o `tar` chama uma das ferramentas de compressão discutidas anteriormente nesta seção. Basta adicionar a opção apropriada ao algoritmo de compressão. As mais usadas são `j`, `J` e `z` para `bzip2`, `xz` e `gzip`, respectivamente. Eis alguns exemplos usando os algoritmos mencionados acima:

```bash
$ cd ~/linux_essentials-3.1/compression
$ ls
bigfile   bigfile3  bigfile-gz1.gz  bigfile-xz1.xz  hosts.gz
bigfile2  bigfile4  bigfile-gz9.gz  bigfile-xz9.xz
$ tar -czf gzip.tar.gz bigfile bigfile2 bigfile3
$ tar -cjf bzip2.tar.bz2 bigfile bigfile2 bigfile3
$ tar -cJf xz.tar.xz bigfile bigfile2 bigfile3
$ ls -l | grep tar
-rw-r--r-- 1 emma emma  450202 Jun 27 05:56 bzip2.tar.bz2
-rw-r--r-- 1 emma emma  548656 Jun 27 05:55 gzip.tar.gz
-rw-r--r-- 1 emma emma  147068 Jun 27 05:56 xz.tar.xz
```

Observe como, no exemplo, os arquivos `.tar` têm tamanhos diferentes. Isso mostra que foram compactados com sucesso. Ao criar arquivos compactados `.tar`, sempre se deve adicionar uma segunda extensão de arquivo indicando o algoritmo usado. Elas são `.xz`, `.bz` e `.gz` para `xz`, `bzip2` e `gzip`, respectivamente. Às vezes, usam-se extensões encurtadas, como `.tgz`.

É possível adicionar arquivos a pacotes tar não comprimidos já existentes. Para isso, usamos a opção `u`. Se você tentar adicionar arquivos a um arquivo comprimido, aparecerá uma mensagem de erro.

```bash
$ cd ~/linux_essentials-3.1/compression
$ ls
bigfile   bigfile3  bigfile-gz1.gz  bigfile-xz1.xz  bzip2.tar.bz2  hosts.gz
bigfile2  bigfile4  bigfile-gz9.gz  bigfile-xz9.xz  gzip.tar.gz    xz.tar.xz
$ tar cf plain.tar bigfile bigfile2 bigfile3
$ tar tf plain.tar
bigfile
bigfile2
bigfile3
$ tar uf plain.tar bigfile4
$ tar tf plain.tar
bigfile
bigfile2
bigfile3
bigfile4
$ tar uzf gzip.tar.gz bigfile4
tar: Cannot update compressed archives
Try 'tar --help' or 'tar --usage' for more information.
```

##### Gerenciando arquivos ZIP

As máquinas Windows geralmente não têm aplicativos para lidar com tar balls ou muitas das ferramentas de compressão comumente encontradas nos sistemas Linux. Se você precisar interagir com sistemas Windows, é aconselhável usar arquivos ZIP. Um arquivo ZIP é um pacote semelhante a um arquivo `tar` compactado.

Os programas `zip` e `unzip` servem para trabalhar com arquivos ZIP em sistemas Linux. O exemplo abaixo mostra todo o necessário para você começar a usá-los. Primeiro, criamos um conjunto de arquivos:

```bash
$ cd ~/linux_essentials-3.1
$ mkdir zip
$ cd zip/
$ mkdir dir
```

```bash
$ touch dir/file1 dir/file2
```

Em seguida, usamos `zip` para comprimir esses arquivos em um arquivo ZIP:

```bash
$ zip -r zipfile.zip dir
adding: dir/ (stored 0%)
adding: dir/file1 (stored 0%)
adding: dir/file2 (stored 0%)
$ rm -rf dir
```

Por fim, descompactamos o arquivo ZIP novamente:

```bash
$ ls
zipfile.zip
$ unzip zipfile.zip
Archive:  zipfile.zip
creating: dir/
extracting: dir/file1
extracting: dir/file2
$ find
.
./zipfile.zip
./dir
./dir/file1
./dir/file2
```

Ao adicionar diretórios aos arquivos ZIP, a opção `-r` faz com que o `zip` inclua o conteúdo desses diretórios. Sem ele, teríamos um diretório vazio no arquivo ZIP.

#### Exercícios Guiados

1. Com base nas extensões, quais das seguintes ferramentas foram usadas para criar estes arquivos?

| **Nome do** **Arquivo** | `tar` | `gzip` | `bzip2` | `xz` |
|---|---|---|---|---|
| `archive.tar` |  |  |  |  |
| `archive.tgz` |  |  |  |  |
| `archive.tar.xz` |  |  |  |  |

2. Com base nas extensões, quais destes arquivos estão empacotados e quais estão comprimidos?

| **Nome do Arquivo** | **Empacotado** | **Comprimido** |
|---|---|---|
| `file.tar` |  |  |
| `file.tar.bz2` |  |  |
| `file.zip` |  |  |
| `file.xz` |  |  |

3. Como se adiciona um arquivo a um arquivo `tar` comprimido com `gzip`?

4. Qual opção de `tar` instrui o `tar` a incluir o caractere inicial `/` nos caminhos absolutos?

5. O `zip` suporta diferentes níveis de compressão?

#### Exercícios Exploratórios

1. Ao extrair arquivos, o `tar` suporta globs na lista de arquivos?

2. Como garantir que um arquivo descomprimido fique igual ao arquivo antes da compressão?

3. O que acontece quando tentamos extrair de um pacote `tar` um arquivo que já existe em seu sistema de arquivos?

4. Como extrair o arquivo `archive.tgz` sem usar a opção `tar` `z`?

#### Resumo

Os sistemas Linux oferecem diversas ferramentas de compressão e empacotamento. Esta lição abordou as mais comuns. A ferramenta de empacotamento mais comum é o `tar`. Se for necessário interagir com sistemas Windows, `zip` e `unzip` ajudam a criar e extrair arquivos ZIP.

O comando `tar` tem algumas opções que vale a pena memorizar. Elas são: `x` para extrair, `c` para criar, `t` para visualizar o conteúdo e `u` para adicionar ou substituir arquivos. A opção `v` lista os arquivos que são processados pelo `tar` ao criar ou extrair um arquivo.

O repositório típico de uma distribuição Linux inclui muitas ferramentas de compressão. As mais comuns são `gzip`, `bzip2` e `xz`. Os algoritmos de compressão geralmente oferecem suporte a diferentes níveis de compressão para otimizar a velocidade ou o tamanho do arquivo. Os arquivos podem ser descomprimidos com `gunzip`, `bunzip2` e `unxz`.

As ferramentas de compressão geralmente têm programas que se comportam como ferramentas comuns para arquivos de texto, com a diferença de que funcionam em arquivos comprimidos. Dentre eles temos o `zcat`, `bzcat` e `xzcat`. As ferramentas de compressão costumam vir com programas com as funcionalidades `grep`, `more`, `less`, `diff` e `cmp`.

Comandos usados nos exercícios:

`bunzip2`

Descomprime um arquivo comprimido `bzip2`.

`bzcat`

Exibe o conteúdo de um arquivo comprimido `bzip`.

`bzip2`

Comprime arquivos usando o algoritmo e o formato `bzip2`.

`gunzip`

Descomprime um arquivo comprimido `gzip`.

`gzip`

Comprime arquivos usando o algoritmo e o formato `gzip`.

`tar`

Cria, atualiza, lista e extrai pacotes `tar`. `unxz`

Descomprime um arquivo comprimido `xz`.

`unzip`

Descomprime e extrai conteúdo de um arquivo ZIP.

`xz` Comprime arquivos usando o algoritmo e o formato `xz`.

`zcat`

Exibe o conteúdo de um arquivo comprimido `gzip`.

`zip`

Cria e comprime pacotes ZIP.

#### Respostas aos Exercícios Guiados

1. Com base nas extensões, quais das seguintes ferramentas foram usadas para criar estes arquivos?

| **Nome do** **Arquivo** | `tar` | `gzip` | `bzip2` | `xz` |
|---|---|---|---|---|
| `archive.tar` | X |  |  |  |
| `archive.tgz` | X | X |  |  |
| `archive.tar.xz` X |  |  |  | X |

2. Com base nas extensões, quais destes arquivos estão empacotados e quais estão comprimidos?

| **Nome do Arquivo** | **Empacotado** | **Comprimido** |
|---|---|---|
| `file.tar` | X |  |
| `file.tar.bz2` | X | X |
| `file.zip` | X | X |
| `file.xz` |  | X |

3. Como se adiciona um arquivo a um arquivo `tar` comprimido com `gzip`?

  Descomprimimos o arquivo com `gunzip`, adicionamos o arquivo com `tar uf` e em seguida o comprimimos com `gzip`

4. Qual opção de `tar` instrui o `tar` a incluir o caractere inicial `/` nos caminhos absolutos?

  A opção `-P`. Segundo a página man:

  ```
  -P, --absolute-names
  Don't strip leading slashes from file names when creating  archives
  ```

5. O `zip` suporta diferentes níveis de compressão?

  Sim. Usaríamos `-#`, substituindo `#` por um número de 0-9. Segundo a página man:

  ```
  -#
  (-0, -1, -2, -3, -4, -5, -6, -7, -8, -9)
  Regula a velocidade da compressão usando o dígito especificado #, onde -0 indica
  ```

  ```
  sem compressão (armazena todos os arquivos), -1 indica a velocidade de compressão mais
  rápida (menos compressão) e -9 indica a velocidade de compressão mais lenta (compressão
  ideal, ignora a lista de sufixos). O nível de compressão padrão é -6.

  Embora ainda esteja sendo trabalhada, a intenção é que essa configuração controle
  a velocidade de compressão para todos os métodos de compressão. Atualmente, apenas a
  deflação é controlada.
  ```

#### Respostas aos Exercícios Exploratórios

1. Ao extrair arquivos, o `tar` suporta globs na lista de arquivos?

  Sim, com a opção `--wildcards`. `--wildcards` deve ser colocado logo após o arquivo `tar` ao se usar o estilo de opções sem hífen. Por exemplo:

  ```bash
  $ tar xf tarfile.tar --wildcards dir/file*
  $ tar --wildcards -xf tarfile.tar dir/file*
  ```

2. Como garantir que um arquivo descomprimido fique igual ao arquivo antes da compressão?

  Não é preciso fazer nada com as ferramentas mostradas nesta lição. As três incluem somas de controle no formato de arquivo, que são verificadas quando eles são descomprimidos.

3. O que acontece quando tentamos extrair de um pacote `tar` um arquivo que já existe em seu sistema de arquivos?

  O arquivo no sistema de arquivos é sobrescrito com a versão que está no arquivo `tar`.

4. Como extrair o arquivo `archive.tgz` sem usar a opção `tar` `z`?

  Seria preciso descomprimi-lo antes com o `gunzip`.

  ```bash
  $ gunzip archive.tgz
  $ tar xf archive.tar
  ```

## 3.2 Pesquisando e extraindo dados de arquivos

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 3.2
- **Peso**: 3

**Áreas chave de conhecimento**

- Pipes da linha de comando
- Redirecionamento I/O
- Expressões regulares básicas utilizando `.`, `[ ]`, `*`, e `?`

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `grep`
- `less`
- `cat`, `head`, `tail`
- `sort`
- `cut`
- `wc`

### 3.2 Lição 1

| **Certificate:** | Linux Essentials |
|---|---|
| **Version:** | 1.6 |
| **Topic:** | 3 O poder da linha de comando |
| **Objective:** | 3.2 Como buscar e extrair dados de arquivos |
| **Lesson:** | 1 of 2 |

#### Introdução

Nesta lição, vamos nos concentrar no redirecionamento ou transmissão de informações de uma fonte para outra com a ajuda de ferramentas específicas. A linha de comando do Linux redireciona as informações através de canais padrão específicos. O teclado é considerado a entrada padrão (*stdin* ou canal 0) do comando, e a tela, a saída padrão (*stdout* ou canal 1). Há também um terceiro canal destinado a redirecionar a saída de erro (*stderr* ou canal 2) de um comando ou as mensagens de erro de um programa. A entrada e/ou saída podem ser redirecionadas.

Ao executar um comando, às vezes queremos transmitir determinadas informações a ele ou redirecionar a saída para um arquivo específico. Cada uma dessas funcionalidades será discutida nas duas seções a seguir.

##### Redirecionamento de E/S

O redirecionamento de E/S permite que o usuário redirecione informações de ou para um comando usando um arquivo de texto. Como explicado anteriormente, a entrada, a saída e a saída de erro padrão podem ser redirecionadas, e as informações, obtidas de arquivos de texto.

###### Redirecionando a saída padrão

Para redirecionar a saída padrão para um arquivo em vez da tela, devemos usar o operador `>` seguido pelo nome do arquivo. Se o arquivo não existir, um novo será criado; caso contrário, a informação vai sobrescrever o arquivo existente.

Para ver o conteúdo do arquivo que acabamos de criar, podemos usar o comando `cat`. Por padrão, esse comando exibe o conteúdo de um arquivo na tela. Consulte a página do manual para saber mais sobre suas funcionalidades.

O exemplo abaixo demonstra a funcionalidade do operador. Na primeira instância, um novo arquivo é criado contendo o texto “Hello World!”:

```bash
$ echo "Hello World!" > text
$ cat text
Hello World!
```

Na segunda invocação, o mesmo arquivo é sobrescrito com o novo texto:

```bash
$ echo "Hello!" > text
$ cat text
Hello!
```

Se quisermos adicionar novas informações ao final do arquivo, usamos o operador `>>`. Esse operador também cria um novo arquivo caso não encontre um arquivo existente.

O primeiro exemplo mostra a adição do texto. Como vemos, o novo texto é adicionado na linha seguinte:

```bash
$ echo "Hello to you too!" >> text
$ cat text
Hello!
Hello to you too!
```

O segundo exemplo demonstra que um novo arquivo será criado:

```bash
$ echo "Hello to you too!" >> text2
$ cat text2
Hello to you too!
```

###### Redirecionando o erro padrão

Para redirecionar apenas as mensagens de erro, o administrador do sistema precisará usar o operador `2>` seguido pelo nome do arquivo no qual os erros serão escritos. Se o arquivo não existir, um novo será criado; caso contrário, o arquivo será sobrescrito.

Como explicado, o canal para redirecionar o erro padrão é o *canal 2*. Ao redirecionar o erro padrão, o canal deve ser especificado, ao contrário da outra saída padrão, em que o *canal 1* já está definido a princípio. O comando no exemplo a seguir procura por um arquivo ou diretório chamado `games` e escreve apenas o erro no arquivo `text-error`, enquanto exibe a saída padrão na tela:

```bash
$ find /usr games 2> text-error
/usr
/usr/share
/usr/share/misc
---------Omitted output----------
/usr/lib/libmagic.so.1.0.0
/usr/lib/libdns.so.81
/usr/games
$ cat text-error
find: `games': No such file or directory
```

> [!note]
> Para saber mais sobre o comando `find`, consulte a página de manual correspondente.

O comando do exemplo a seguir será executado sem erros e, portanto, nenhuma informação será gravada no arquivo `text-error`:

```bash
$ sort /etc/passwd 2> text-error
$ cat text-error
```

Além da saída padrão, o erro padrão também pode ser incluído em um arquivo com o operador `2` `>>`. Isso adicionará o novo erro no final do arquivo. Se o arquivo não existir, um novo será criado. O primeiro exemplo mostra a adição das novas informações ao arquivo. O segundo exemplo mostra que o comando cria um novo arquivo quando um arquivo existente com o mesmo nome não pode ser encontrado:

```bash
$ sort /etc 2>> text-error
$ cat text-error
```

```
sort: read failed: /etc: Is a directory



$ sort /etc/shadow 2>> text-error2
$ cat text-error2
sort: open failed: /etc/shadow: Permission denied
```

Usando esse tipo de redirecionamento, apenas as mensagens de erro serão redirecionadas para o arquivo; a saída normal será escrita na tela ou passará pela saída padrão ou *stdout*.

Existe um arquivo em particular que tecnicamente é um *bit bucket* (um arquivo que aceita entrada e não faz nada com ela): `/dev/null`. É possível redirecionar para lá qualquer informação irrelevante que não precise ser exibida ou redirecionada para um arquivo importante, como mostrado no exemplo abaixo:

```bash
$ sort /etc 2> /dev/null
```

###### Redirecionando a entrada padrão

Esse tipo de redirecionamento é usado para inserir dados em um comando a partir de um arquivo especificado em vez de um teclado. Nesse caso, o operador `<` é usado, como no exemplo abaixo:

```bash
$ cat < text
Hello!
Hello to you too!
```

Em geral, redirecionamos a entrada padrão com comandos que não aceitam argumentos de arquivo. O comando `tr` é um deles. Esse comando pode ser usado para traduzir o conteúdo do arquivo modificando as palavras de maneira específica, como por exemplo a exclusão de um determinado caractere. O exemplo abaixo mostra a exclusão do caractere `l`:

```bash
$ tr -d "l" < text
Heo!
Heo to you too!
```

Para saber mais, consulte a página de manual do `tr`.

###### Here documents

Ao contrário dos redirecionamentos de saída, o operador `<<` age de maneira diferente em comparação com os outros operadores. Esse fluxo de entrada também é chamado de *here* *document*. O *here document* representa o bloco de código ou texto que pode ser redirecionado para o comando ou o programa interativo. Diferentes tipos de linguagens de script, como `bash`, `sh` e `csh`, podem receber entradas diretamente da linha de comando, sem usar nenhum arquivo de texto.

Como vemos no exemplo abaixo, o operador é usado para inserir dados no comando, ao passo que a palavra que vem depois não especifica o nome do arquivo. A palavra é interpretada como o delimitador da entrada e não será levada em consideração como conteúdo; portanto, o `cat` não a exibirá:

```bash
$ cat << hello
> hey
> ola
> hello
hey
ola
```

Consulte a página de manual do comando `cat` para saber mais.

###### Combinações

A primeira combinação de que trataremos combina o redirecionamento da saída padrão e o da saída de erro padrão para o mesmo arquivo. Os operadores `&>` e `&>>` são usados: `&` representa a combinação do *canal 1* e do *canal 2*. O primeiro operador substituirá o conteúdo existente no arquivo e o segundo incluirá ou adicionará as novas informações ao final do arquivo. Ambos os operadores permitem a criação de um novo arquivo se já não existir um, como nas seções anteriores:

```bash
$ find /usr admin &> newfile
$ cat newfile
/usr
/usr/share
/usr/share/misc
---------Omitted output----------
/usr/lib/libmagic.so.1.0.0
/usr/lib/libdns.so.81
/usr/games
```

```
find: `admin': No such file or directory
$ find /etc/calendar &>> newfile
$ cat newfile
/usr
/usr/share
/usr/share/misc
---------Omitted output----------
/usr/lib/libmagic.so.1.0.0
/usr/lib/libdns.so.81
/usr/games
find: `admin': No such file or directory
/etc/calendar
/etc/calendar/default
```

Vamos ver um exemplo que usa o comando `cut`:

```bash
$ cut -f 3 -d "/" newfile
$ cat newfile

share
share
share
---------Omitted output----------
lib
games
find: `admin': No such file or directory
calendar
calendar
find: `admin': No such file or directory
```

O comando `cut` corta campos especificados do arquivo de entrada usando a opção `-f`, o terceiro campo em nosso caso. Para que o comando encontre o campo, um delimitador também deve ser especificado com a opção `-d`. Em nosso caso, o delimitador será o caractere `/`.

Para saber mais sobre o comando `cut`, consulte a página man correspondente.

##### Pipes na linha de comando

O redirecionamento é usado principalmente para armazenar o resultado de um comando a ser processado por um comando diferente. Esse tipo de processo intermediário pode se tornar tedioso e complicado quando os dados precisam passar por múltiplos processos. Para evitar isso, podemos vincular o comando diretamente usando *pipes*. Em outras palavras, a saída do primeiro comando se torna automaticamente a entrada do segundo comando. Essa conexão é feita usando o operador `|` (barra vertical):

```bash
$ cat /etc/passwd | less
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
:
```

No exemplo acima, o comando `less`, após o operador pipe, modifica a maneira como o arquivo é exibido. O comando `less` exibe o arquivo de texto, permitindo ao usuário rolar uma linha por vez para cima e para baixo.`less` também é usado por padrão para exibir as páginas de manual, conforme discutido nas lições anteriores.

É possível empregar várias pipes ao mesmo tempo. Os comandos intermediários que recebem uma entrada, a alteram e produzem uma saída são chamados de *filtros*. Vamos pegar o comando `ls -l` e tentar contar o número de palavras das 10 primeiras linhas da saída. Para isso, teremos de usar o comando `head` que, por padrão, exibe as 10 primeiras linhas de um arquivo, e em seguida contar as palavras usando o comando `wc`:

```bash
$ ls -l | head | wc -w
10
```

Como já mencionado, por padrão, o `head` exibe apenas as 10 primeiras linhas do arquivo de texto especificado. Esse comportamento pode ser modificado usando opções específicas. Verifique a página man do comando para saber mais.

Existe outro comando para exibir o final de um arquivo: `tail`. Por padrão, esse comando seleciona as últimas 10 linhas e as exibe, mas, como em `head`, esse número também pode ser modificado. Verifique a página de manual de `tail` para mais detalhes.

> [!note]
> A opção `-f` mostra as últimas linhas de um arquivo enquanto ele está sendo atualizado. Esse recurso pode ser muito útil ao se monitorar a atividade em andamento em um arquivo como o `syslog`.

O comando `wc` (contagem de palavras) conta por padrão as linhas, palavras e bytes de um arquivo. Como mostrado no exercício, a opção `-w` faz com que o comando conte apenas as palavras dentro das linhas selecionadas. As opções mais comuns desse comando são: `-l`, que especifica que o comando deve contar apenas as linhas, e `-c`, usado para contar apenas os bytes. Mais variações e opções do comando, bem como informações sobre o `wc`, podem ser encontradas na página de manual do comando.

#### Exercícios Guiados

1. Liste o conteúdo do diretório atual, incluindo o proprietário e as permissões, e redirecione a saída para um arquivo chamado `contents.txt` dentro de seu diretório inicial.

2. Ordene o conteúdo do arquivo `contents.txt` a partir do diretório atual e inclua esse conteúdo ordenado no final de um novo arquivo chamado `contents-sorted.txt`

3. Exiba as últimas 10 linhas do arquivo `/etc/passwd` e redirecione-as para um novo arquivo no diretório `Documents` do seu usuário.

4. Conte o número de palavras no arquivo `contents.txt` e inclua a saída ao final de um arquivo chamado `field2.txt` em seu diretório inicial. Você precisará usar redirecionamentos de entrada e de saída.

5. Exiba as 5 primeiras linhas do arquivo `/etc/passwd` e classifique a saída em ordem alfabética reversa.

6. Usando o arquivo `contents.txt` criado anteriormente, conte o número de caracteres das últimas 9 linhas.

7. Conte o número de arquivos chamados `test` no diretório `/usr/share` e em seus subdiretórios. Nota: cada linha da saída do comando `find` representa um arquivo.

#### Exercícios Exploratórios

1. Selecione o segundo campo do arquivo `contents.txt` e redirecione a saída padrão e a saída de erro para outro arquivo chamado `field1.txt`.

2. Usando o operador de redirecionamento de entrada e o comando `tr`, exclua os hífens (`-`) do arquivo `contents.txt`.

3. Qual é a maior vantagem de redirecionar apenas os erros para um arquivo?

4. Substitua todos os espaços repetidos no arquivo `contents.txt` classificado em ordem alfabética por um único espaço.

5. Em uma linha de comando, elimine os espaços repetidos (como feito no exercício anterior), selecione o nono campo e ordene-o em ordem alfabética reversa e sem distinção entre maiúsculas e minúsculas. Quantos pipes você teve de usar?

#### Resumo

Nesta lição, você aprendeu:

- Tipos de redirecionamento
- Como usar os operadores de redirecionamento
- Como usar pipes pra filtrar a saída dos comandos

Comandos usados nesta lição:

`cut`

Remove seções de cada linha de um arquivo.

`cat`

Exibe ou concatena arquivos.

`find`

Busca por arquivos em uma hierarquia de diretórios.

`less`

Exibe um arquivo, permitindo que o usuário role uma linha por vez.

`more`

Exibe um arquivo, uma página por vez.

`head`

Exibe as primeiras 10 linhas de um arquivo.

`tail`

Exibe as últimas 10 linhas de um arquivo.

`sort`

Classifica os arquivos.

`wc`

Conta por padrão as linhas, palavras ou bytes de um arquivo.

#### Respostas aos Exercícios Guiados

1. Liste o conteúdo do diretório atual, incluindo o proprietário e as permissões, e redirecione a saída para um arquivo chamado `contents.txt` dentro de seu diretório inicial.

  ```bash
  $ ls -l > contents.txt
  ```

2. Ordene o conteúdo do arquivo `contents.txt` a partir do diretório atual e inclua esse conteúdo ordenado no final de um novo arquivo chamado `contents-sorted.txt`

  ```bash
  $ sort contents.txt >> contents-sorted.txt
  ```

3. Exiba as últimas 10 linhas do arquivo `/etc/passwd` e redirecione-as para um novo arquivo no diretório `Documents` do seu usuário.

  ```bash
  $ tail /etc/passwd > Documents/newfile
  ```

4. Conte o número de palavras no arquivo `contents.txt` e inclua a saída no final de um arquivo chamado `field2.txt` em seu diretório inicial. Você precisará usar redirecionamentos de entrada e de saída.

  ```bash
  $ wc -w < contents.txt >> field2.txt
  ```

5. Exiba as 5 primeiras linhas do arquivo `/etc/passwd` e classifique a saída em ordem alfabética reversa.

  ```bash
  $ head -n 5 /etc/passwd | sort -r
  ```

6. Usando o arquivo `contents.txt` criado anteriormente, conte o número de caracteres das últimas 9 linhas.

  ```bash
  $ tail -n 9 contents.txt | wc -c
  531
  ```

7. Conte o número de arquivos chamados `test` no diretório `/usr/share` e em seus subdiretórios. Nota: cada linha da saída do comando `find` representa um arquivo.

  ```bash
  $ find /usr/share -name test | wc -l
  125
  ```

#### Respostas aos Exercícios Exploratórios

1. Selecione o segundo campo do arquivo `contents.txt` e redirecione a saída padrão e a saída de erro para outro arquivo chamado `field1.txt`.

  ```bash
  $ cut -f 2 -d " " contents.txt &> field1.txt
  ```

2. Usando o operador de redirecionamento de entrada e o comando `tr`, exclua os hífens (`-`) do arquivo `contents.txt`.

  ```bash
  $ tr -d "-" < contents.txt
  ```

3. Qual é a maior vantagem de redirecionar apenas os erros para um arquivo?

  O redirecionamento dos erros para um arquivo ajuda a manter um arquivo de log monitorado com frequência.

4. Substitua todos os espaços repetidos no arquivo `contents.txt` classificado em ordem alfabética por um único espaço.

  ```bash
  $ sort contents.txt | tr -s " "
  ```

5. Em uma linha de comando, elimine os espaços repetidos (como feito no exercício anterior), selecione o nono campo e ordene-o em ordem alfabética reversa e sem distinção entre maiúsculas e minúsculas. Quantos pipes você teve de usar?

  ```bash
  $ cat contents.txt | tr -s " " | cut -f 9 -d " " | sort -fr
  ```

  O exercício usa 3 pipes, um para cada filtro.

### 3.2 Lição 2

#### Introdução

Nesta lição, trataremos de ferramentas para a manipulação de texto. Elas são frequentemente usadas por administradores de sistema ou programas para monitorar ou identificar automaticamente informações recorrentes específicas.

##### Pesquisando dentro de arquivos com `grep`

A primeira ferramenta que discutiremos nesta lição é o comando `grep`. `grep` é a abreviação da frase “global regular expression print” (impressão de expressão regular global) e sua principal funcionalidade é buscar por um padrão especificado dentro de arquivos. O comando exibe, destacada em vermelho, a linha que contém o padrão especificado.

```bash
$ grep bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
user:x:1001:1001:User,,,,:/home/user:/bin/bash
```

O `grep`, como a maioria dos comandos, também pode ser refinado com opções. As mais comuns são:

`-i`

a busca não diferencia maiúsculas de minúsculas

`-r`

a busca é recursiva (pesquisa todos os arquivos dentro do diretório especificado, mais seus subdiretórios)

`-c`

a busca conta o número de correspondências

`-v`

inverte o termo de correspondência para imprimir linhas que não correspondem ao termo de pesquisa

`-E`

ativa expressões regulares estendidas (necessárias para alguns dos metacaracteres mais avançados, como `|`, `+` e `?`)

O `grep` tem muitas outras opções úteis. Consulte a página do manual para saber mais sobre ele.

##### Expressões regulares

A segunda ferramenta é muito poderosa. É usada para descrever pedacinhos de texto dentro de arquivos, também chamados de *expressões regulares*. As expressões regulares são utilíssimas na extração de dados de arquivos de texto através da construção de padrões. São comumente usadas em scripts ou em programação com linguagens de alto nível, como Perl ou Python.

Ao trabalhar com expressões regulares, é muito importante ter em mente que *todos os caracteres* *contam*; o padrão é escrito com o objetivo de corresponder a uma sequência específica de caracteres, conhecida como string. A maioria dos padrões usa os símbolos ASCII normais, como letras, dígitos, sinais de pontuação ou outros símbolos, mas também pode usar caracteres Unicode para corresponder a qualquer outro tipo de texto.

A lista a seguir explica os metacaracteres das expressões regulares usadas para formar os padrões.

`.`

Corresponde a qualquer caractere único (exceto nova linha)

`[abcABC]`

Corresponde a qualquer caractere dentro dos colchetes

`[^abcABC]`

Corresponde a qualquer caractere, exceto os que estão entre colchetes

`[a-z]`

Corresponde a qualquer caractere no intervalo

`[^a-z]`

Corresponde a qualquer caractere, exceto os do intervalo

`sun|moon`

Busca qualquer uma das strings listadas

`^`

Início de uma linha

`$`

Fim de uma linha

Todas as funcionalidades das expressões regulares também podem ser implementadas através do `grep`. Você pode constatar que, no exemplo acima, a palavra não está entre aspas duplas. Para impedir que o shell interprete o próprio metacaractere, é recomendável que o padrão mais complexo esteja entre aspas duplas (" "). Para fins de prática, usaremos aspas duplas ao implementar expressões regulares. As outras aspas mantêm sua funcionalidade normal, conforme discutido nas lições anteriores.

Os exemplos a seguir enfatizam a funcionalidade das expressões regulares. Precisaremos de dados que estão dentro do arquivo, e portanto o próximo conjunto de comandos somente inclui strings diferentes no arquivo `text.txt`.

```bash
$ echo "aaabbb1" > text.txt
$ echo "abab2" >> text.txt
$ echo "noone2" >> text.txt
$ echo "class1" >> text.txt
$ echo "alien2" >> text.txt
$ cat text.txt
aaabbb1
abab2
noone2
```

```
class1
alien2
```

O primeiro exemplo é uma combinação de buscas no arquivo sem e com expressões regulares. Para entender bem as expressões regulares, é muito importante mostrar a diferença. O primeiro comando procura pela string exata em qualquer lugar da linha, enquanto o segundo comando procura por conjuntos de caracteres que contenham qualquer um dos caracteres entre colchetes. Portanto, os resultados dos comandos são diferentes.

```bash
$ grep "ab" text.txt
aaabbb1
abab2
$ grep "[ab]" text.txt
aaabbb1
abab2
class1
alien2
```

O segundo conjunto de exemplos mostra a aplicação do metacaractere de início e fim da linha. É muito importante especificar a necessidade de colocar os 2 caracteres no lugar certo dentro da expressão. Ao se especificar o início da linha, o metacaractere precisa vir antes da expressão; já ao se especificar o final da linha, o metacaractere deve ser posto após a expressão.

```bash
$ grep "^a" text.txt
aaabbb1
abab2
alien2
$ grep "2$" text.txt
abab2
noone2
alien2
```

Além dos metacaracteres explicados anteriormente, as expressões regulares também possuem metacaracteres que permitem a multiplicação do padrão especificado anteriormente:

`*`

Zero ou mais do padrão anterior

`+`

Um ou mais do padrão anterior

`?`

Zero ou um do padrão anterior

Para os metacaracteres multiplicadores, o comando abaixo busca uma sequência que contenha `ab`, um único caractere e um ou mais dos caracteres encontrados anteriormente. O resultado mostra que o `grep` encontrou a string `aaabbb1`, correspondendo à parte do `abbb`, bem como `abab2`. Como o caractere `+` é um caractere de expressão regular *estendida* , precisamos passar a opção `-E` para o comando `grep`.

```bash
$ grep -E "ab.+" text.txt
aaabbb1
abab2
```

A maioria dos metacaracteres é autoexplicativa, mas no início eles podem ser meio difíceis de assimilar. Os exemplos anteriores representam uma pequena parte da funcionalidade das expressões regulares. Experimente todos os metacaracteres da tabela acima para entender melhor como eles funcionam.

#### Exercícios Guiados

Usando `grep` e o arquivo `/usr/share/hunspell/en_US.dic`, encontre as linhas que correspondem aos seguintes critérios:

1. Todas as linhas que contêm a palavra `cat` em qualquer lugar da linha.

2. Todas as linhas que não contêm nenhum dos seguintes caracteres: `sawgtfixk`.

3. Todas as linhas que começam com 3 letras quaisquer e a palavra `dig`.

4. Todas as linhas que terminam com pelo menos um `e`.

5. Todas as linhas que contêm uma das seguintes palavras: `org` , `kay` ou `tuna`.

6. Número de linhas que começam com um ou nenhum `c` seguido pela string `ati`.

#### Exercícios Exploratórios

1. Encontre a expressão regular que corresponde às palavras na linha “Incluir” e que não corresponde às da linha “Excluir”::

  - Incluir: `pot`, `spot`, `apot`

  Excluir: `potic`, `spots`, `potatoe`

  - Incluir: `arp99`, `apple`, `zipper`

  Excluir: `zoo`, `arive`, `attack`

  - Incluir: `arcane`, `capper`, `zoology`

  Excluir: `air`, `coper`, `zoloc`

  - Incluir: `0th/pt`, `3th/tc`, `9th/pt`

  Excluir: `0/nm`, `3/nm`, `9/nm`

  - Incluir: `Hawaii`, `Dario`, `Ramiro`

  Excluir: `hawaii`, `Ian`, `Alice`

2. Que outro comando útil é comumente usado para pesquisar dentro de arquivos? Quais funcionalidades adicionais ele oferece?

3. Escolha um dos exemplos da lição anterior e tente buscar por um padrão específico na saída do comando com a ajuda do `grep`.

#### Resumo

Nesta lição, você aprendeu:

- Metacaracteres em expressões regulares
- Como criar padrões com expressões regulares
- Como buscar dentro de arquivos

Comandos usados nos exercícios:

`grep`

Busca por caracteres ou sequências dentro de um arquivo

#### Respostas aos Exercícios Guiados

Usando `grep` e o arquivo `/usr/share/hunspell/en_US.dic`, encontre as linhas que correspondem aos seguintes critérios:

1. Todas as linhas que contêm a palavra `cat` em qualquer lugar da linha.

  ```bash
  $ grep "cat" /usr/share/hunspell/en_US.dic
  Alcatraz/M
  Decatur/M
  Hecate/M
  ...
  ```

2. Todas as linhas que não contêm nenhum dos seguintes caracteres: `sawgtfixk`.

  ```bash
  $ grep -v "[sawgtfixk]" /usr/share/hunspell/en_US.dic
  49269
  0/nm
  1/n1
  2/nm
  2nd/p
  3/nm
  3rd/p
  4/nm
  5/nm
  6/nm
  7/nm
  8/nm
  ...
  ```

3. Todas as linhas que começam com 3 letras quaisquer e a palavra `dig`.

  ```bash
  $ grep "^...dig" /usr/share/hunspell/en_US.dic
  cardigan/SM
  condign
  predigest/GDS
  ...
  ```

4. Todas as linhas que terminam com pelo menos um `e`.

  ```bash
  $ grep -E "e+$" /usr/share/hunspell/en_US.dic
  Anglicize
  Anglophobe
  Anthropocene
  ...
  ```

5. Todas as linhas que contêm uma das seguintes palavras: `org` , `kay` ou `tuna`.

  ```bash
  $ grep -E "org|kay|tuna" /usr/share/hunspell/en_US.dic
  Borg/SM
  George/MS
  Tokay/M
  fortunate/UY
  ...
  ```

6. Número de linhas que começam com um ou nenhum `c` seguido pela string `ati`.

  ```bash
  $ grep -cE "^c?ati" /usr/share/hunspell/en_US.dic
  3
  ```

#### Respostas aos Exercícios Exploratórios

1. Encontre a expressão regular que corresponde às palavras na linha “Incluir” e que não corresponde às da linha “Excluir”:

  - Incluir: `pot`, `spot`, `apot`

  Excluir: `potic`, `spots`, `potatoe`

  Resposta: `pot$`

  - Incluir: `arp99`, `apple`, `zipper`

  Excluir: `zoo`, `arive`, `attack`

  Resposta: `p+`

  - Incluir: `arcane`, `capper`, `zoology`

  Excluir: `air`, `coper`, `zoloc`

  Resposta: `arc|cap|zoo`

  - Incluir: `0th/pt`, `3th/tc`, `9th/pt`

  Excluir: `0/nm`, `3/nm`, `9/nm`

  Resposta: `[0-9]th.+`

  - Incluir: `Hawaii`, `Dario`, `Ramiro`

  Excluir: `hawaii`, `Ian`, `Alice`

  Resposta: `^[A-Z]a.*i+`

2. Que outro comando útil é comumente usado para pesquisar dentro de arquivos? Quais funcionalidades adicionais ele oferece?

  O comando `sed`. Ele é capaz de encontrar e substituir caracteres ou conjuntos de caracteres dentro de um arquivo.

3. Escolha um dos exemplos da lição anterior e tente buscar por um padrão específico na saída do comando com a ajuda do `grep`.

  Peguei uma das respostas dos Exercícios Exploratórios e busquei pela linha que tem as permissões de grupo para leitura, escrita e execução. Sua resposta pode ser diferente, dependendo do comando que você escolher e do padrão que criar.

  ```bash
  $ cat contents.txt | tr -s " " | grep "^....rwx"
  ```

  Este exercício serve para demonstrar que o `grep` também pode receber entrada de diferentes comandos e ajudar a filtrar as informações geradas.

## 3.3 Transformando comandos em Scripts

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 3.3
- **Peso**: 4

**Áreas chave de conhecimento**

- Shell scripting básico
- Reconhecimento de editores de texto comuns (vi e nano).

**Partial list of the used files, terms and utilities**

- `#!` (shebang)
- `/bin/bash`
- Variáveis
- Argumentos
- `for` loops
- `echo`
- Exit status

### 3.3 Lição 1

#### Introdução

Até agora, aprendemos a executar comandos a partir do shell, mas também é possível inserir comandos em um arquivo e depois configurá-lo para ser executável. Quando executamos o arquivo, os comandos são rodados um após o outro. Esses arquivos executáveis são chamados *scripts* e representam uma ferramenta absolutamente essencial para qualquer administrador de sistema Linux. Basicamente, podemos dizer que o Bash, além de um shell, é uma verdadeira linguagem de programação.

##### Exibindo a saída

Vamos começar demonstrando um comando que você deve ter visto nas lições anteriores: o `echo` imprime na tela um argumento na saída padrão.

```bash
$ echo "Hello World!"
Hello World!
```

Agora, usaremos um redirecionamento de arquivo para enviar este comando para um novo arquivo chamado `new_script`.

```bash
$ echo 'echo "Hello World!"' > new_script
$ cat new_script
echo "Hello World!"
```

O arquivo `new_script` agora contém o mesmo comando de antes.

##### Tornando um script executável

Vamos demonstrar algumas das etapas necessárias para executar esse arquivo da maneira esperada. A primeira ideia de um usuário pode ser simplesmente digitar o nome do script, assim como digitaria o nome de qualquer outro comando:

```bash
$ new_script
/bin/bash: new_script: command not found
```

Sabemos que `new_script` existe em nossa localização atual, mas note que a mensagem de erro não está dizendo que o *arquivo* não existe, mas sim que o *comando* não existe. Seria útil discutir como o Linux lida com comandos e executáveis.

##### Comandos e `PATH`

Quando digitamos o comando `ls` no shell, por exemplo, estamos na verdade executando um arquivo chamado `ls` que existe em nosso sistema de arquivos. Para comprovar, use `which`:

```bash
$ which ls
/bin/ls
```

Seria cansativo digitar o caminho absoluto de `ls` toda vez que desejássemos examinar o conteúdo de um diretório, por isso o Bash tem uma *variável de ambiente* que contém todos os diretórios em que ficam os comandos que queremos executar. Para ver o conteúdo dessa variável, use `echo`.

```bash
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/sn
ap/bin
```

O shell espera encontrar um comando em cada um desses locais, delimitado por dois pontos (`:`).

Note que `/bin` está presente, mas é seguro supor que nossa localização atual não está. O shell procurará por `new_script` em cada um desses diretórios, mas não o encontrará e, portanto, exibirá a mensagem de erro que vimos acima.

Existem três soluções para esse problema: podemos mover `new_script` para um dos diretórios de `PATH`, podemos adicionar o diretório atual a `PATH`, ou podemos mudar a maneira de chamar o script. A última solução é a mais fácil, pois simplesmente requer que especifiquemos o *local atual* ao chamar o script usando ponto e barra (`./`).

```bash
$ ./new_script
/bin/bash: ./new_script: Permission denied
```

A mensagem de erro já está diferente, o que indica que fizemos alguns progressos.

##### Permissões de execução

A primeira investigação que um usuário deve fazer nesse caso é usar `ls -l` para examinar o arquivo:

```bash
$ ls -l new_script
-rw-rw-r-- 1 user user 20 Apr 30 12:12 new_script
```

Podemos ver que as permissões para este arquivo estão definidas como `664` por padrão. Ainda não configuramos este arquivo para ter *permissões de execução*.

```bash
$ chmod +x new_script
$ ls -l new_script
-rwxrwxr-x 1 user user 20 Apr 30 12:12 new_script
```

Este comando concede permissões de execução a todos os usuários. Esteja ciente de que isso pode ser um risco de segurança, mas, por enquanto, esse é um nível aceitável de permissão.

```bash
$ ./new_script
Hello World!
```

Agora já é possível executar nosso script.

##### Definindo o intérprete

Como demonstramos, é possível simplesmente inserir texto em um arquivo, configurá-lo como executável e executá-lo. O `new_script` ainda é tecnicamente um arquivo de texto normal, mas pode ser interpretado pelo Bash. Mas e se ele estiver escrito em Perl ou Python?

É extremamente recomendável especificar o tipo de intérprete que queremos usar na primeira linha de um script. Essa linha é chamada de *bang line*, ou, mais comumente, *shebang*. Ela indica ao sistema como queremos que aquele arquivo seja executado. Como estamos aprendendo Bash, usaremos o caminho absoluto para o nosso executável do Bash, mais uma vez usando `which`:

```bash
$ which bash
/bin/bash
```

Nosso shebang começa com um sinal de hash e um ponto de exclamação, seguidos pelo caminho absoluto acima. Vamos abrir `new_script` em um editor de texto e inserir o shebang. Vamos também aproveitar a oportunidade para inserir um *comentário* em nosso script. Os comentários são ignorados pelo intérprete. Eles são escritos para o benefício de outros usuários que queiram entender seu script.

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

echo "Hello World!"
```

Também faremos uma alteração adicional no nome do arquivo: salvaremos o arquivo como `new_script.sh`. O sufixo do arquivo ".sh" não altera em nada a execução do arquivo. É uma convenção que os scripts do bash sejam rotulados com `.sh` ou `.bash` para identificá-los mais facilmente, assim como os scripts em Python são geralmente identificados com o sufixo `.py`.

###### Editores de texto comuns

Os usuários do Linux geralmente precisam trabalhar em ambientes nos quais editores de texto gráficos não estão disponíveis. Portanto, é altamente recomendável aprender ao menos o básico sobre a edição de arquivos de texto na linha de comando. Dois dos editores de texto mais comuns são `vi` e `nano`.

**vi**

O `vi` é um editor de texto venerável, que vem instalado por padrão em quase todos os sistemas Linux existentes. O `vi` gerou um clone chamado *vi IMproved* ou `vim`, que tem algumas funcionalidades adicionais, mas mantém a interface do `vi`. Embora trabalhar com o `vi` seja assustador para um novo usuário, o editor é popular e amado pelos usuários que conhecem seus muitos recursos.

A diferença mais importante entre o `vi` e aplicativos como o Bloco de Notas é que o `vi` possui três modos diferentes. Na inicialização, as teclas `H` , `J` , `K` e `L` são usadas para navegar, e não para digitar. Nesse \_ modo de navegação\_, pressionamos `I` para entrar no *modo de inserção*. A partir daí, você pode digitar normalmente. Para sair do modo de inserção, pressione `Esc` para retornar ao *modo de* *navegação*. No *modo de navegação*, pressione `:` para entrar no *modo de comando*. Nesse modo, podemos salvar, excluir, sair ou alterar opções.

Embora o `vi` tenha uma curva de aprendizado, os diferentes modos permitem que um usuário experiente seja mais eficiente do que com outros editores.

**nano**

O `nano` é uma ferramenta mais recente, criada para ser mais simples e fácil de usar do que o `vi`. O `nano` não oferece modos diferentes. Em vez disso, um usuário pode começar a digitar já na inicialização, usando `Ctrl` para acessar as ferramentas impressas na parte inferior da tela.

```
[ Welcome to nano.  For basic help, type Ctrl+G. ]
^G Get Help   ^O Write Out  ^W Where Is   ^K Cut Text   ^J Justify    ^C Cur Pos    M-U Undo
^X Exit       ^R Read File  ^\ Replace    ^U Uncut Text ^T To Spell   ^_ Go To Line M-E Redo
```

Os editores de texto são uma questão de preferência pessoal, e o editor que você escolher não fará diferença para esta lição. Mas vale muito a pena procurar conhecer e se familiarizar com um ou mais editores de texto.

##### Variáveis

As variáveis são uma parte importante de qualquer linguagem de programação, e o mesmo vale para o Bash. Quando iniciamos uma nova sessão no terminal, o shell já define algumas variáveis automaticamente. A variável `PATH` é um bom exemplo. Nós as chamamos de *variáveis de ambiente*, porque geralmente definem características do nosso ambiente shell. É possível modificar e adicionar variáveis de ambiente, mas por enquanto vamos nos concentrar na configuração de variáveis dentro do nosso script.

Vamos modificar o script da seguinte forma:

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username=Carol

echo "Hello $username!"
```

Neste caso, criamos uma *variável* chamada `username` e atribuímos a ela o *valor* `Carol`. Note que não há espaços entre o nome da variável, o sinal de igual ou o valor atribuído.

Na linha seguinte, usamos o comando `echo` com a variável, mas há um cifrão (`$`) na frente do nome da variável. Isso é importante, pois indica para o shell que queremos tratar `username` como uma variável, e não apenas como uma palavra normal. Ao digitar `$username` no comando, indicamos que queremos executar uma *substituição*, trocando o *nome* de uma variável pelo *valor* atribuído a essa variável.

Ao executar o novo script, obtemos esta saída:

```bash
$ ./new_script.sh
Hello Carol!
```

- As variáveis devem conter apenas caracteres alfanuméricos ou sublinhados (underline) e diferenciam maiúsculas de minúsculas. `Username` e `username` serão tratados como variáveis distintas.
- A substituição de variáveis também pode ter o formato `${username}`, com a adição de `{ }`. Isso também é aceitável.
- As variáveis no Bash têm um *tipo implícito*, sendo consideradas strings. Isso significa que executar funções matemáticas no Bash é mais complicado do que seria em outras linguagens de programação, como C/C++:

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username=Carol
x=2
y=4
```

```
z=$x+$y
echo "Hello $username!"
echo "$x + $y"
echo "$z"



$ ./new_script.sh
Hello Carol!
2 + 4
2+4
```

##### Usando aspas com variáveis

Vamos fazer a seguinte alteração no valor da nossa variável `username`:

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username=Carol Smith

echo "Hello $username!"
```

A execução desse script resultará em um erro:

```bash
$ ./new_script.sh
./new_script.sh: line 5: Smith: command not found
Hello !
```

Lembre-se de que o Bash é um intérprete e, como tal, *interpreta* o script linha por linha. Neste caso, ele interpretou corretamente `username=Carol` como a definição de uma variável `username` com o valor `Carol`. Mas, em seguida, ele interpretou que o espaço indicava o final dessa tarefa e que `Smith` era o nome de um comando. Para que o espaço e o nome `Smith` sejam incluídos como o novo valor da variável, colocamos aspas duplas (`"`) ao redor do nome.

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username="Carol Smith"
```

```
echo "Hello $username!"



$ ./new_script.sh
Hello Carol Smith!
```

Uma coisa importante a ser observada no Bash é que aspas duplas e aspas simples (`'`) se comportam de maneira muito diferente. As aspas duplas são consideradas “fracas” porque permitem que o intérprete efetue a substituição dentro das aspas. Aspas simples são consideradas “fortes” por impedirem a substituição. Considere o seguinte exemplo:

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username="Carol Smith"

echo "Hello $username!"
echo 'Hello $username!'



$ ./new_script.sh
Hello Carol Smith!
Hello $username!
```

No segundo comando `echo`, o intérprete foi impedido de substituir `$username` por `Carol Smith`, e assim a saída é interpretada literalmente.

##### Argumentos

Você já aprendeu a usar argumentos nos utilitários principais do Linux. Por exemplo, `rm` `testfile` contém tanto o executável `rm` quanto um argumento `testfile`. Os argumentos podem ser passados para o script na execução e modificam o comportamento do script. É fácil implementá-los.

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username=$1
```

```
echo "Hello $username!"
```

Em vez de atribuir um valor a `username` diretamente dentro do script, atribuímos a ele o valor de uma nova variável `$1`. Ela faz referência ao valor do *primeiro argumento*.

```bash
$ ./new_script.sh Carol
Hello Carol!
```

Os nove primeiros argumentos são tratados dessa maneira. Há modos de lidar com mais de nove argumentos, mas isso está fora do alcance desta lição. Eis um exemplo usando apenas dois argumentos:

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username1=$1
username2=$2
echo "Hello $username1 and $username2!"



$ ./new_script.sh Carol Dave
Hello Carol and Dave!
```

Existe uma consideração importante ao usar argumentos: no exemplo acima, temos dois argumentos, `Carol` e `Dave`, atribuídos a `$1` e `$2`, respectivamente. Se o segundo argumento estiver ausente, por exemplo, o shell não emitirá uma mensagem de erro. O valor de `$2` será simplesmente *nulo*, ou nada.

```bash
$ ./new_script.sh Carol
Hello Carol and !
```

Em nosso caso, seria recomendável introduzir alguma lógica em nosso script para que diferentes *condições* afetem a *saída* que desejamos imprimir. Começaremos introduzindo outra variável útil e, em seguida, criaremos *declarações if*.

##### Retorno do número de argumentos

Enquanto variáveis como `$1` e `$2` contêm o valor dos argumentos posicionais, a variável `$#` contém o *número de argumentos*.

```bash
#!/bin/bash

# Este é nosso primeiro comentário. Também é recomendável documentar todos os scripts.

username=$1

echo "Hello $username!"
echo "Number of arguments: $#."



$ ./new_script.sh Carol Dave
Hello Carol!
Number of arguments: 2.
```

##### Lógica Condicional

O uso da lógica condicional na programação é um tópico vasto que não será abordado em profundidade nesta lição. Vamos nos concentrar na *sintaxe* dos condicionais no Bash, que é diferente da maioria das outras linguagens de programação.

Primeiro, vamos rever nosso objetivo. Temos um script simples capaz de imprimir uma saudação para um único usuário. Se houver algo diferente de um único usuário, temos de imprimir uma mensagem de erro.

- A *condição* que estamos testando é o número de usuários, que está contido na variável `$#`. Gostaríamos de saber se o valor de `$#` é `1`.
- Se a condição for *verdadeira*, a *ação* executada será saudar o usuário.
- Se a condição for *falsa*, imprimiremos uma mensagem de erro.

Agora que a lógica está clara, vamos nos concentrar na *sintaxe* necessária para implementá-la.

```bash
#!/bin/bash

# Um script simples para saudar um único usuário.
```

```
if [ $# -eq 1 ]
then
username=$1

echo "Hello $username!"
else
echo "Please enter only one argument."
fi
echo "Number of arguments: $#."
```

A lógica condicional está contida entre `if` e `fi`. A condição a ser testada fica entre colchetes `[ ]` e a ação a tomar caso a condição seja verdadeira é indicada após `then`. Observe os espaços entre os colchetes e a lógica contida neles. A omissão desses espaços causará erros.

Esse script exibirá a nossa saudação *ou* a mensagem de erro. Mas ele sempre imprimirá a linha `Number of arguments`.

```bash
$ ./new_script.sh
Please enter only one argument.
Number of arguments: 0.
$ ./new_script.sh Carol
Hello Carol!
Number of arguments: 1.
```

Tome nota da declaração `if`. Usamos `-eq` para fazer uma *comparação numérica*. Nesse caso, estamos testando se o valor de `$#` é *igual* a um. As outras comparações que podemos realizar são:

`-ne`

Diferente de

`-gt`

Maior que

`-ge`

Maior que ou igual a

`-lt`

Menos que

`-le`

Menos que ou igual a

#### Exercícios guiados

1. Um usuário insere o seguinte no shell:

  ```bash
  $ PATH=~/scripts
  $ ls
  Command 'ls' is available in '/bin/ls'
  The command could not be located because '/bin' is not included in the PATH environment
  variable.
  ls: command not found
  ```

  - O que o usuário fez?
  - Qual comando pode combinar o valor atual de `PATH` com o novo diretório `~/scripts`?

2. Considere o script a seguir. Note que ele usa `elif` para conferir uma segunda condição:

  ```
  >  /!bin/bash

  > fruit1 = Apples
  > fruit2 = Oranges

  if [ $1 -lt $# ]
  then
  echo "This is like comparing $fruit1 and $fruit2!"
  > elif [$1 -gt $2 ]
  then
  >   echo '$fruit1 win!'
  else
  >   echo "Fruit2 win!"
  > done
  ```

  - As linhas marcadas com um `>` contêm erros. Corrija esses erros.

3. Qual será a saída nas seguintes situações?

  ```bash
  $ ./guided1.sh 3 0
  ```

  ```bash
  $ ./guided1.sh 2 4



  $ ./guided1.sh 0 1
  ```

#### Exercícios Exploratórios

1. Escreva um script simples que verifique se exatamente dois argumentos são passados. Se for o caso, imprima os argumentos em ordem inversa. Considere o exemplo (nota: seu código pode ser diferente do nosso, mas deve produzir uma saída idêntica):

  ```
  if [ $1 == $number ]
  then
  echo "True!"
  fi
  ```

2. Este código está correto, mas não é uma comparação numérica. Pesquise na internet para descobrir como este código é diferente de usar `-eq`.

3. Existe uma variável de ambiente para imprimir o diretório atual. Use `env` para descobrir o nome dessa variável.

4. Usando o que aprendeu nas questões 2 e 3, escreva um script curto que aceite um argumento. Se um argumento for passado, confira se ele corresponde ao nome do diretório atual. Se a resposta for sim, imprima `yes`. Caso contrário, imprima `no`.

#### Resumo

Nesta lição, você aprendeu:

- Como criar e executar scripts simples
- Como usar um shebang para especificar um intérprete
- Como definir e usar variáveis dentro de scripts
- Como lidar com argumentos em scripts
- Como construir declarações `if`
- Como comparar números usando operadores numéricos

Comandos usados nos exercícios:

`echo`

Imprime uma string na saída padrão.

`env`

Imprime todas as variáveis de ambiente na saída padrão.

`which`

Imprime o caminho absoluto de um comando.

`chmod`

Altera as permissões de um arquivo.

Variáveis especiais usadas nos exercícios:

`$1, $2, … $9`

Contêm argumentos posicionais passados para o script.

`$#`

Contém o número de argumentos passados para o script.

`$PATH`

Contém os diretórios que possuem executáveis usados pelo sistema.

Operadores usados nos exercícios:

`-ne`

Diferente de

`-gt`

Maior que

`-ge`

Maior que ou igual a

`-lt`

Menos que

`-le`

Menos que ou igual a

#### Respostas aos Exercícios Guiados

1. Um usuário insere o seguinte no shell:

  ```bash
  $ PATH=~/scripts
  $ ls
  Command 'ls' is available in '/bin/ls'
  The command could not be located because '/bin' is not included in the PATH environment
  variable.
  ls: command not found
  ```

  - O que o usuário fez?

  O usuário sobrescreveu o conteúdo de PATH com o diretório `~/scripts`. O comando `ls` não pode mais ser encontrado, já que não está contido em PATH. Note que essa alteração afeta somente a sessão atual; basta se deslogar e se relogar novamente para reverter a mudança.

  - Qual comando pode combinar o valor atual de `PATH` com o novo diretório `~/scripts`?

  `PATH=$PATH:~/scripts`

2. Considere o script a seguir. Note que ele usa `elif` para conferir uma segunda condição:

  ```
  >  /!bin/bash

  > fruit1 = Apples
  > fruit2 = Oranges

  if [ $1 -lt $# ]
  then
  echo "This is like comparing $fruit1 and $fruit2!"
  > elif [$1 -gt $2 ]
  then
  >   echo '$fruit1 win!'
  else
  >   echo "Fruit2 win!"
  > done
  ```

  - As linhas marcadas com um `>` contêm erros. Corrija esses erros.

  ```bash
  #!/bin/bash
  ```

  ```
  fruit1=Apples
  fruit2=Oranges

  if [ $1 -lt $# ]
  then
  echo "This is like comparing $fruit1 and $fruit2!"
  elif [ $1 -gt $2 ]
  then
  echo "$fruit1 win!"
  else
  echo "$fruit2 win!"
  fi
  ```

3. Qual será a saída nas seguintes situações?

  ```bash
  $ ./guided1.sh 3 0
  ```

  `Apples win!`

  ```bash
  $ ./guided1.sh 2 4
  ```

  `Oranges win!`

  ```bash
  $ ./guided1.sh 0 1
  ```

  `This is like comparing Apples and Oranges!`

#### Respostas aos Exercícios Exploratórios

1. Escreva um script simples que verifique se exatamente dois argumentos são passados. Se for o caso, imprima os argumentos em ordem inversa. Considere o exemplo (nota: seu código pode ser diferente do nosso, mas deve produzir uma saída idêntica):

  ```
  if [ $1 == $number ]
  then
  echo "True!"
  fi



  #!/bin/bash

  if [ $# -ne 2 ]
  then
  echo "Error"
  else
  echo "$2 $1"
  fi
  ```

2. Este código está correto, mas não é uma comparação numérica. Pesquise na internet para descobrir como este código é diferente de usar `-eq`.

  Podemos comparar *strings* com `==`. Ou seja, se os caracteres de ambas as variáveis corresponderem exatamente, a condição é verdadeira.

| `abc == abc` |  |  |  | *true* |
|---|---|---|---|---|
| `abc == ABC` |  |  |  | *false* |
| `1 == 1` |  |  |  | *true* |
| `1+1 == 2` |  |  |  | *false* |

  A comparação de strings provoca comportamentos inesperados se estivermos testando com números.

3. Existe uma variável de ambiente para imprimir o diretório atual. Use `env` para descobrir o nome dessa variável.

  `PWD`

4. Usando o que aprendeu nas questões 2 e 3, escreva um script curto que aceite um argumento. Se um argumento for passado, confira se ele corresponde ao nome do diretório atual. Se a resposta for sim, imprima `yes`. Caso contrário, imprima `no`.

  ```bash
  #!/bin/bash

  if [ "$1" == "$PWD" ]
  then
  echo "yes"
  else
  echo "no"
  fi
  ```

### 3.3 Lição 2

#### Introdução

Na última seção, usamos este exemplo simples para demonstrar a criação de scripts no Bash:

```bash
#!/bin/bash

# Um script simples para saudar um único usuário.

if [ $# -eq 1 ]
then
username=$1

echo "Hello $username!"
else
echo "Please enter only one argument."
fi
echo "Number of arguments: $#."
```

- Todos os scripts devem começar com um *shebang*, que define o caminho para o intérprete.
- Todos os scripts devem incluir comentários para descrever seu uso.
- Este script em particular trabalha com um *argumento*, que é passado para o script quando chamado.
- Este script contém uma *declaração if*, que testa as condições de uma variável interna `$#`. Essa variável foi configurada para o número de argumentos.
- Se o número de argumentos passados para o script for igual a 1, o valor do primeiro argumento é passado para uma nova variável chamada `username` e o script ecoa uma saudação ao usuário. Caso contrário, uma mensagem de erro é exibida.
- Finalmente, o script ecoa o número de argumentos. Isso é útil para a depuração (debugging).

Este é um exemplo útil para começar a explicar alguns dos outros recursos dos scripts Bash.

##### Códigos de saída

Você deve ter notado que nosso script tem dois estados possíveis: ou ele imprime `"Hello` `<usuário>!"` ou uma mensagem de erro. Isso é bastante normal para muitos dos utilitários fundamentais. Veja o `cat`, que você já deve estar conhecendo bem.

Vamos comparar um uso bem-sucedido do `cat` com uma situação em que ele falha. Relembrando, o exemplo acima é um script chamado `new_script.sh`.

```bash
$ cat -n new_script.sh

1  #!/bin/bash
2
3  # Um script simples para saudar um único usuário.
4
5  if [ $# -eq 1 ]
6  then
7    username=$1
8
9    echo "Hello $username!"
10  else
11    echo "Please enter only one argument."
12  fi
13  echo "Number of arguments: $#."
```

Este comando é bem-sucedido; vemos que a flag `-n` também imprimiu os números de linha. Isso é muito útil na depuração de scripts, mas note eles não fazem parte do script.

Agora vamos verificar o valor de uma nova variável interna `$?`. Por enquanto, observe somente a saída:

```bash
$ echo $?
0
```

Agora, vamos considerar uma situação em que o `cat` não funcionará. Primeiro, veremos uma mensagem de erro e, em seguida, verificaremos o valor de `$?`.

```bash
$ cat -n dummyfile.sh
cat: dummyfile.sh: No such file or directory
$ echo $?
1
```

A explicação para esse comportamento é a seguinte: qualquer execução do utilitário `cat` retornará um *código de saída*. O código de saída informa se o comando foi bem-sucedido ou se ocorreu um erro. Um código de saída *zero* indica que o comando foi concluído com êxito. Isso vale para quase todos os comandos do Linux com os quais trabalhamos. Qualquer outro código de saída indica algum tipo de erro. O código de saída do *último comando a ser executado* será armazenado na variável `$?`.

Os códigos de saída geralmente não são vistos por usuários humanos, mas são muito úteis ao escrever scripts. Considere um script que serve para copiar arquivos para uma unidade de rede remota. A tarefa de cópia pode falhar de diversas maneiras: por exemplo, a máquina local talvez não esteja conectada à rede ou a unidade remota pode estar cheia. Graças ao código de saída do nosso utilitário de cópia, podemos alertar o usuário sobre esses problemas ao executar o script.

É sempre uma boa ideia implementar códigos de saída, e é o que faremos agora. Temos dois caminhos em nosso script, um sucesso e um fracasso. Vamos usar zero para indicar o sucesso e um para indicar o fracasso.

```
1  #!/bin/bash
2
3  # Um script simples para saudar um único usuário.
4
5  if [ $# -eq 1 ]
6  then
7    username=$1
8
9    echo "Hello $username!"
```

```
10    exit 0
11  else
12    echo "Please enter only one argument."
13    exit 1
14  fi
15  echo "Number of arguments: $#."



$ ./new_script.sh Carol
Hello Carol!
$ echo $?
0
```

Note que o comando `echo` na linha 15 foi totalmente ignorado. O uso de `exit` encerra o script imediatamente e, portanto, essa linha nunca é encontrada.

##### Como manipular múltiplos argumentos

Até agora, nosso script pode tratar apenas de um único nome de usuário por vez. Qualquer número de argumentos além de um causará um erro. Vamos explorar como é possível tornar esse script mais versátil.

O primeiro instinto de um usuário pode ser usar mais variáveis posicionais como `$2`, `$3` e assim por diante. Infelizmente, não podemos prever o número de argumentos que um usuário pode querer usar. Para resolver esse problema, será útil introduzir mais variáveis internas.

Vamos modificar a lógica do nosso script. Se houver zero argumentos, aparecerá um erro, mas qualquer outro número de argumentos fará o script ser bem-sucedido. Este novo script será chamado `friendly2.sh`.

```
1  #!/bin/bash
2
3  # um script simples para saudar os usuários
4
5  if [ $# -eq 0 ]
6  then
7    echo "Please enter at least one user to greet."
8    exit 1
9  else
10    echo "Hello $@!"
11    exit 0
```

```
12  fi



$ ./friendly2.sh Carol Dave Henry
Hello Carol Dave Henry!
```

Existem duas variáveis internas que contêm todos os argumentos passados para o script: `$@` e `$*`. Na maioria das vezes, ambas se comportam da mesma forma. O Bash analisará (*parse*) os argumentos e separará cada argumento quando encontrar um espaço entre eles. De fato, o conteúdo de `$@` é o seguinte:

| `0` |  |  |  | `1` |  |  |  | `2` |
|---|---|---|---|---|---|---|---|---|
| `Carol` |  |  |  | `Dave` |  |  |  | `Henry` |

Se você conhece outras linguagens de programação, vai reconhecer esse tipo de variável como um *arranjo* (array). Para criar arranjos no Bash, basta pôr um espaço entre elementos como a variável `FILES` no script `arraytest` abaixo:

```
FILES="/usr/sbin/accept /usr/sbin/pwck/ usr/sbin/chroot"
```

Ele contém uma lista de diversos itens. Por enquanto, ele não é muito útil, porque ainda não introduzimos nenhuma maneira de gerir esses itens individualmente.

##### Loops for

Vamos voltar ao exemplo `arraytest`, mostrado anteriormente. Se você se lembra, neste exemplo estamos especificando um arranjo chamado FILES. O que precisamos é de uma maneira de “desdobrar” esta variável e acessar cada valor individual, um após o outro. Para isso, usaremos uma estrutura chamada *loop for*, presente em todas as linguagens de programação. Existem duas variáveis às quais nos referiremos: uma é o intervalo e a outra é o valor individual em que estamos trabalhando no momento. Este é o script em sua totalidade:

```bash
#!/bin/bash

FILES="/usr/sbin/accept /usr/sbin/pwck/ usr/sbin/chroot"

for file in $FILES
do
ls -lh $file
```

```
done



$ ./arraytest
lrwxrwxrwx 1 root root 10 Apr 24 11:02 /usr/sbin/accept -> cupsaccept
-rwxr-xr-x 1 root root 54K Mar 22 14:32 /usr/sbin/pwck
-rwxr-xr-x 1 root root 43K Jan 14 07:17 /usr/sbin/chroot
```

Se você consultar novamente o exemplo `friendly2.sh` acima, verá que estamos trabalhando com um intervalo de valores contidos dentro de uma única variável `$@`. Por uma questão de clareza, chamaremos a última variável de `username`. Nosso script fica assim:

```
1  #!/bin/bash
2
3  # um script simples para saudar os usuários
4
5  if [ $# -eq 0 ]
6  then
7    echo "Please enter at least one user to greet."
8    exit 1
9  else
10    for username in $@
11    do
12      echo "Hello $username!"
13    done
14    exit 0
15  fi
```

Lembre-se de que a variável definida aqui pode ter qualquer nome, e que todas as linhas entre `do… done` serão executadas uma vez para cada elemento do arranjo. Vamos observar a saída de nosso script:

```bash
$ ./friendly2.sh Carol Dave Henry
Hello Carol!
Hello Dave!
Hello Henry!
```

Agora vamos supor que queremos fazer a saída parecer um pouco mais humana. Queremos que a saudação apareça em uma só linha.

```
1  #!/bin/bash
```

```
2
3  # um script simples para saudar os usuários
4
5  if [ $# -eq 0 ]
6  then
7    echo "Please enter at least one user to greet."
8    exit 1
9  else
10    echo -n "Hello $1"
11    shift
12    for username in $@
13    do
14      echo -n ", and $username"
15    done
16    echo "!"
17    exit 0
18  fi
```

A notar:

- Ao usar `-n` com `echo` , *suprimimos a nova linha* após a impressão. Isso significa que todos os ecos serão impressos na mesma linha, e a nova linha será impressa somente após o `!` na linha 16.
- O comando `shift` removerá o primeiro elemento do arranjo, de modo que:

| `0` |  |  |  | `1` |  |  |  | `2` |
|---|---|---|---|---|---|---|---|---|
| `Carol` |  |  |  | `Dave` |  |  |  | `Henry` |

Se torna:

| `0` |  |  |  | `1` |
|---|---|---|---|---|
| `Dave` |  |  |  | `Henry` |

Observemos a saída:

```bash
$ ./friendly2.sh Carol
Hello Carol!
$ ./friendly2.sh Carol Dave Henry
Hello Carol, and Dave, and Henry!
```

##### Verificando erros com expressões regulares

Podemos querer verificar todos os argumentos que o usuário está inserindo. Por exemplo, se quisermos garantir que todos os nomes passados para `friendly2.sh` contenham *apenas letras* e que quaisquer caracteres ou números especiais causem um erro. Para executar essa verificação de erro, usaremos `grep`.

Lembre-se de que podemos usar expressões regulares com `grep`.

```bash
$ echo Animal | grep "^[A-Za-z]*$"
Animal
$ echo $?
0



$ echo 4n1ml | grep "^[A-Za-z]*$"
$ echo $?
1
```

O `^` e o `$` indicam, respectivamente, o início e o fim da linha. O `[A-Za-z]` indica um intervalo de letras, maiúsculas ou minúsculas. O `*` é um *quantificador* e modifica o intervalo de letras para que ele vá de zero a muitas letras. Em resumo, o `grep` será bem-sucedido se a entrada consistir *somente* de letras, mas se não for o caso ele falhará.

A próxima coisa a observar é que o `grep` está retornando códigos de saída com base nas correspondências que encontra. Uma correspondência positiva retorna `0` e uma negativa retorna `1`. Podemos usar isso para testar os argumentos dentro de nosso script.

```
1  #!/bin/bash
2
3  # um script simples para saudar os usuários
4
5  if [ $# -eq 0 ]
6  then
7    echo "Please enter at least one user to greet."
8    exit 1
9  else
10    for username in $@
11    do
12      echo $username | grep "^[A-Za-z]*$" > /dev/null
13      if [ $? -eq 1 ]
14      then
```

```
15        echo "ERROR: Names must only contains letters."
16        exit 2
17      else
18        echo "Hello $username!"
19      fi
20    done
21    exit 0
22  fi
```

Na linha 12, estamos redirecionando a saída padrão para `/dev/null`, que é uma maneira simples de suprimi-la. Não queremos ver nenhuma saída do comando `grep`, mas somente testar seu código de saída, o que acontece na linha 13. Observe também que estamos usando um código de saída `2` para indicar um argumento inválido. Geralmente, é recomendável usar códigos de saída distintos para indicar erros diferentes; assim, um usuário mais experiente pode usar esses códigos de saída para solucionar problemas.

```bash
$ ./friendly2.sh Carol Dave Henry
Hello Carol!
Hello Dave!
Hello Henry!
$ ./friendly2.sh 42 Carol Dave Henry
ERROR: Names must only contains letters.
$ echo $?
2
```

#### Exercícios guiados

1. Leia o conteúdo de `script1.sh`, abaixo:

  ```bash
  #!/bin/bash

  if [ $# -lt 1 ]
  then
  echo "This script requires at least 1 argument."
  exit 1
  fi

  echo $1 | grep "^[A-Z]*$" > /dev/null
  if [ $? -ne 0 ]
  then
  echo "no cake for you!"
  exit 2
  fi

  echo "here's your cake!"
  exit 0
  ```

  Qual a saída destes comandos?

  - `./script1.sh`
  - `echo $?`
  - `./script1.sh cake`
  - `echo $?`
  - `./script1.sh CAKE`
  - `echo $?`

2. Leia o conteúdo do arquivo `script2.sh`:

  ```
  for filename in $1/*.txt
  do
  cp $filename $filename.bak
  done
  ```

  Descreva a finalidade deste script em seu entendimento.

#### Exercícios Exploratórios

1. Crie um script capaz de receber qualquer número de argumentos do usuário e que imprima apenas os argumentos com números maiores que 10.

#### Resumo

Nesta lição, você aprendeu:

- O que são códigos de saída, o que significam e como implementá-los
- Como verificar o código de saída de um comando
- O que são os loops `for` e como usá-los com arranjos
- Como usar `grep`, expressões regulares e códigos de saída para verificar dados inseridos pelo usuário em scripts.

Comandos usados nos exercícios:

`shift`

Remove o primeiro elemento de um arranjo.

Variáveis Especiais:

`$?`

Contém o código de saída do último comando executado

`$@`**,** `$*`

Contém todos os argumentos passados para o script, como um arranjo.

#### Respostas aos Exercícios Guiados

1. Leia o conteúdo de `script1.sh`, abaixo:

  ```bash
  #!/bin/bash

  if [ $# -lt 1 ]
  then
  echo "This script requires at least 1 argument."
  exit 1
  fi

  echo $1 | grep "^[A-Z]*$" > /dev/null
  if [ $? -ne 0 ]
  then
  echo "no cake for you!"
  exit 2
  fi

  echo "here's your cake!"
  exit 0
  ```

  Qual a saída destes comandos?

  - Comando: `./script1.sh`

  Saída: `This script requires at least 1 argument.`

  - Comando: `echo $?`

  Saída: `1`

  - Comando: `./script1.sh cake`

  Saída: `no cake for you!`

  - Comando: `echo $?`

  Saída: `2`

  - Comando: `./script1.sh CAKE`

  Saída: `here's your cake!`

  - Comando: `echo $?`

  Saída: `0`

2. Leia o conteúdo do arquivo `script2.sh`:

  ```
  for filename in $1/*.txt
  do
  cp $filename $filename.bak
  done
  ```

  Descreva a finalidade deste script em seu entendimento.

  Este script faz cópias de segurança de todos os arquivos que terminam com `.txt` em um subdiretório definido no primeiro argumento.

#### Respostas aos Exercícios Exploratórios

1. Crie um script capaz de receber qualquer número de argumentos do usuário e que imprima apenas os argumentos com números maiores que 10.

  ```bash
  #!/bin/bash

  for i in $@
  do
  echo $i | grep "^[0-9]*$" > /dev/null
  if [ $? -eq 0 ]
  then
  if [ $i -gt 10 ]
  then
  echo -n "$i "
  fi
  fi
  done
  echo ""
  ```

---
*Fonte: Linux Professional Institute, Materiais Didáticos Linux Essentials (learning.lpi.org), licença CC BY-NC-ND 4.0. Conversão do PDF para Markdown apenas para estudo pessoal.*
