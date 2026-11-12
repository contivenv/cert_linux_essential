---
tags: [lpi, linux-essentials, 010-160]
topico: 5
certificacao: LPI Linux Essentials 010-160 (v1.6)
---

# Tópico 5: Segurança e Permissões de Arquivos

## 5.1 Segurança Básica e Identificação de Tipos de Usuários

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 5.1
- **Peso**: 2

**Áreas chave de conhecimento**

- Root e Usuários padrão
- Usuários do sistema

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `/etc/passwd`, `/etc/shadow`, `/etc/group`
- `id`, `last`, `who`, `w`
- `sudo`, `su`

### 5.1 Lição 1

#### Introdução

Esta lição abordará a terminologia básica relacionada a contas, controles de acesso e segurança dos sistemas Linux locais, as ferramentas da interface da linha de comando (CLI) em um sistema Linux para controles de acesso básicos e os arquivos essenciais para oferecer suporte a contas de usuários e grupos, incluindo os usados para aumentar os privilégios elementares.

A segurança básica nos sistemas Linux deriva-se dos controles de acesso do Unix que, apesar de terem quase cinquenta anos, são bastante eficazes em comparação com outros sistemas operacionais populares de linhagem muito mais recente. Mesmo certos sistemas operacionais populares baseados em Unix tendem a “tomar liberdades” com o argumento da “facilidade de acesso”, coisa que o Linux não faz.

Os ambientes e interfaces modernos do Linux simplificam a criação e o gerenciamento de usuários e frequentemente automatizam a atribuição de controles de acesso quando um usuário faz login — por exemplo, permitindo acesso ao monitor, áudio e outros serviços — sem a necessidade de praticamente nenhuma intervenção manual do administrador do sistema. No entanto, é importante entender os conceitos básicos por trás de um sistema operacional Linux.

##### Contas

A segurança engloba muitos conceitos, sendo um dos mais comuns o conceito geral de controles de acesso. Antes de tratar dos controles de acesso a arquivos, como propriedade e permissões, é necessário compreender os conceitos básicos relacionados às *contas* de usuário do Linux, que são divididas em vários tipos.

Todo usuário de um sistema Linux possui uma conta associada que, além das informações de login (como nome de usuário e senha), também define como e onde o usuário pode interagir com o sistema. Os privilégios e controles de acesso definem os “limites” dentro dos quais cada usuário pode operar.

###### Identificadores (UIDs/GIDs)

Os *Identificadores de Usuário* e *Grupos* (UIDs/GIDs) são as referências básicas, numeradas, às contas. As implementações iniciais eram números inteiros limitados de 16 bits (valores de 0 a 65535), mas os sistemas do século XXI suportam UIDs e GIDs de 64 bits. Os usuários e grupos são enumerados de forma independente, de modo que o mesmo ID pode representar tanto um usuário quanto um grupo.

Todo usuário possui não apenas um UID, mas também um *GID primário*. O GID primário de um usuário pode ser exclusivo apenas para esse usuário, não sendo usado por outros usuários. No entanto, o grupo pode ser compartilhado por diversos usuários. Além desses grupos primários, cada usuário também pode ser membro de outros grupos.

Por padrão, nos sistemas Linux, todo usuário é incluído em um grupo com o mesmo nome que seu nome de usuário e um GID idêntico a seu UID. Por exemplo, se criarmos um novo usuário chamado `newuser`, seu grupo por padrão também será `newuser`.

###### A conta de superusuário

No Linux, a conta do superusuário é `root`, que sempre terá o UID 0. O superusuário também pode ser chamado de *administrador do sistema* e dispõe de acesso e controle ilimitados sobre o sistema, incluindo outros usuários.

O grupo padrão do superusuário tem o GID `0` e também é chamado de `root`. O diretório inicial do superusuário é um diretório dedicado, de nível superior, `/root`, acessível apenas pelo próprio usuário `root`.

###### Contas de usuário padrão

Todas as contas que não sejam `root` são, tecnicamente, contas de usuário regulares, mas em um sistema Linux o termo coloquial *conta de usuário* geralmente indica uma conta de usuário “regular” (sem privilégios). Elas têm geralmente as seguintes propriedades, com algumas exceções:

- UIDs iniciando em 1000 (4 dígitos), embora alguns sistemas legados possam iniciar em 500.
- Um diretório inicial definido, geralmente um subdiretório de `/home`, dependendo da configuração local.
- Um shell de login definido. No Linux, o shell padrão é geralmente o *Bourne Again Shell* (`/bin/bash`), embora outros possam estar disponíveis.

Se uma conta de usuário não tiver um shell válido em seus atributos, o usuário não poderá abrir um shell interativo. Normalmente, `/sbin/nologin` é usado como um shell inválido. Isso pode ser proposital, no caso de o usuário ser autenticado apenas para serviços que excluam o console ou o acesso SSH; por exemplo, somente acesso FTP seguro (`sftp`).

> [!note]
> Para evitar confusões, o termo *conta de usuário* será aplicado apenas a contas de usuário padrão ou regulares daqui para a frente. Usaremos *conta de sistema* para nos referir uma conta de usuário Linux pertencente ao tipo de conta de usuário do sistema.

###### Contas do sistema

As *contas de sistema* são tipicamente pré-criadas no momento da instalação do sistema. São destinadas a recursos, programas e serviços que não serão executados como superusuário. Em um mundo ideal, todos eles seriam funcionalidades do sistema operacional.

As contas de sistema variam, mas dentre seus atributos temos:

- Os UIDs normalmente são menores de 100 (2 dígitos) ou entre 500-1000 (3 dígitos).
- Não têm *nenhum* diretório inicial dedicado ou têm um diretório que normalmente não está em `/home`.
- Nenhum shell de login válido (tipicamente `/sbin/nologin`), com raras exceções.

A maioria das contas de sistema no Linux nunca faz login e não precisa de um shell definido em seus atributos. Muitos processos que pertencem e são executados por contas de sistema são transferidos para o seu próprio ambiente pelo gerenciamento do sistema, sendo executados com a conta de sistema especificada. Essas contas geralmente têm privilégios limitados ou, na maioria das vezes, *nenhum* privilégio.

> [!note]
> Do ponto de vista do LPI Linux Essentials, as contas de sistema têm UIDs \<1000, com UIDs (e GIDs) de 2 ou 3 dígitos.

Em geral, as contas de sistema *não* devem ter um shell de login válido. O contrário representaria um problema de segurança na maioria dos casos.

###### Contas de serviço

As *contas de serviço* são criadas tipicamente quando instalamos e configuramos serviços. Como no caso das contas de sistema, elas são destinadas aos recursos, programas e serviços que não serão executados como superusuário.

Em muitas documentações, as contas de sistema e de serviço são semelhantes e intercambiáveis. Isso inclui a localização dos diretórios pessoais, que normalmente ficam fora de `/home`, quando definidos (as contas de serviço têm mais probabilidade de ter um diretório pessoal do que as contas de sistema) e a ausência de um shell de login válido. Embora não exista uma definição estrita, a principal diferença entre contas de sistema e de serviço está no UID/GID.

- **Conta de sistema**: UID/GID \<100 (2 dígitos) ou \<500-1000 (3 digitos)
- **Conta de serviço**: UID/GID >1000 (4+ dígitos), mas não uma conta de usuário “padrão” ou “regular” , uma conta para os serviços, com um UID/GID >1000 (4+ dígitos)

Algumas distribuições Linux ainda têm contas de serviço pré-reservadas com UID \<100, e estas também podem ser consideradas contas de sistema, mesmo que não sejam criadas na instalação. Por exemplo, nas distribuições Linux baseadas no Fedora (incluindo o Red Hat), o usuário do servidor web Apache tem um UID (e GID) 48, claramente uma conta de sistema, apesar de contar com um diretório inicial (geralmente em `/usr/share/httpd` ou `/var/www/html/`).

> [!note]
> Do ponto de vista do LPI Linux Essentials, as contas de sistema têm UIDs \<1000 e as contas de usuário regulares têm UIDs >1000. Como as contas de usuário regulares são >1000, esses UIDs também podem incluir contas de serviço.

###### Shells de login e diretórios iniciais

Algumas contas têm um shell de login, enquanto outras não os têm por motivos de segurança, já que não requerem acesso interativo. O shell de login padrão na maioria das distribuições Linux é o *Bourne Again Shell*, ou `bash`, mas outros shells podem estar disponíveis, como o C Shell (`csh`),

Korn shell (`ksh`) ou Z shell (`zsh`), dentre outros.

O usuário pode alterar seu shell de login usando o comando `chsh`. Por padrão, o comando é executado no modo interativo e exibe um prompt perguntando qual shell deve ser usado. A resposta deve ser o caminho completo para o binário do shell, como mostrado abaixo:

```bash
$ chsh

Changing the login shell for emma
Enter the new value, or press ENTER for the default
Login Shell [/bin/bash]: /usr/bin/zsh
```

Também é possível executar o comando no modo não interativo, com o parâmetro `-s` seguido pelo caminho para o binário, da seguinte forma:

```bash
$ chsh -s /usr/bin/zsh
```

A maioria das contas tem um diretório inicial definido. No Linux, esse é geralmente o único local em que a conta do usuário tem acesso garantido de gravação, com algumas exceções (por exemplo, áreas temporárias do sistema de arquivos). No entanto, algumas contas são configuradas propositalmente para não ter acesso de gravação, mesmo no próprio diretório pessoal, por motivos de segurança.

##### Obtendo informações sobre os usuários

Listar informações básicas de usuário é uma prática cotidiana comum em um sistema Linux. Em alguns casos, os usuários precisarão trocar de usuário e ganhar privilégios para concluir tarefas privilegiadas.

Os usuários comuns podem listar atributos e acessos na linha de comando usando os comandos abaixo. As informações básicas em contexto limitado não são uma operação privilegiada.

Para listar as informações atuais de um usuário na linha de comando, basta um comando de duas letras: `id`. A saída vai depender de seu ISD de login:

```bash
$ id
uid=1024(emma) gid=1024(emma) 1024(emma),20(games),groups=10240(netusers),20480(netadmin)
context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

Na listagem anterior, o usuário (`emma`) tem identificadores detalhados da seguinte maneira:

- `1024` = ISD de usuário (UID), seguido pelo nome de usuário (nome comum ou nome de login) entre parênteses.
- `1024` = o ID *primário* de grupo (GID), seguido pelo nome do grupo (nome comum) entre parênteses.
- Uma lista de GIDs adicionais (nomes de grupo) a que o usuário também pertence.

Para listar a última vez em que os usuários se logaram no sistema, usamos o comando `last`:

```bash
$ last
emma     pts/3        ::1              Fri Jun 14 04:28   still logged in
reboot   system boot  5.0.17-300.fc30. Fri Jun 14 04:03   still running
reboot   system boot  5.0.17-300.fc30. Wed Jun  5 14:32 - 15:19  (00:46)
reboot   system boot  5.0.17-300.fc30. Sat May 25 18:27 - 19:11  (00:43)
reboot   system boot  5.0.16-100.fc28. Sat May 25 16:44 - 17:06  (00:21)
reboot   system boot  5.0.9-100.fc28.x Sun May 12 14:32 - 14:46  (00:14)
root     tty2                          Fri May 10 21:55 - 21:55  (00:00)
...
```

As informações listadas nas colunas podem variar, mas dentre os itens relevantes na listagem anterior podemos destacar:

- Um usuário (`emma`) fez login através da rede (pseudo TTY `pts/3`) e ainda está logado.
- A hora da inicialização atual está listada, junto com o kernel. No exemplo acima, cerca de 25 minutos antes do usuário fazer login.
- O superusuário (`root`) se logou através de um console virtual (TTY `tty2`), brevemente, em meados de maio.

Uma variante do comando `last` é o comando `lastb`, que lista as últimas tentativas malsucedidas de login.

Os comandos `who` e `w` listam somente os logins ativos no sistema:

```bash
$ who
emma  pts/3        2019-06-14 04:28 (::1)

$ w
05:43:41 up  1:40,  1 user,  load average: 0.25, 0.53, 0.51
USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT
emma  pts/3     04:28    1:14m  0.04s  0.04s -bash
```

Algumas informações são comuns aos dois comandos. Por exemplo, um usuário (`emma`) está logado com um pseudo-dispositivo TTY (`pts/3`) e a hora de login é 04:28.

O comando `w` lista mais informações, incluindo o seguinte:

- A hora atual e há quanto tempo o sistema está ativo
- Quantos usuários estão conectados
- As *cargas médias* dos últimos 1, 5 e 15 minutos

E as informações adicionais para cada sessão de usuário ativo.

- Tempos selecionados e totais de uso da CPU (`IDLE`, `JCPU` e `PCPU`)
- O processo atual (`-bash`). O tempo total de uso da CPU desse processo é o último item (`PCPU`).

Ambos os comandos têm mais opções para listar várias informações adicionais.

##### Troca de usuário e aumento de privilégios

Em um mundo ideal, os usuários nunca precisariam de privilégios adicionais para concluir suas tarefas. O sistema sempre “funcionaria” e tudo estaria configurado para diversos tipos de acesso.

Felizmente para nós, o Linux — desde a instalação — já funciona dessa maneira para a maioria dos usuários que não são administradores de sistema, apesar de sempre seguir o modelo de segurança do *menor privilégio*.

No entanto, existem comandos que permitem aumentar os privilégios quando necessário. Dois dos mais importantes são `su` e `sudo`.

Atualmente, na maioria dos sistemas Linux, o comando `su` é usado apenas para conceder privilégios de root ao usuário padrão (se um nome de usuário não for especificado após o nome do comando). Embora possa ser usado para alternar para outro usuário, não é uma boa prática: os usuários devem fazer login a partir de outro sistema, pela rede, console físico ou terminal no sistema.

```
emma ~$ su -
Password:
root ~#
```

Após digitar a senha do superusuário (`root`), o usuário adquire um shell de superusuário (observe o `#` no final do prompt de comando) e se torna, para todos os efeitos, o superusuário (`root`).

Compartilhar senhas é uma péssima ideia para a segurança, e por isso deve haver pouquíssima necessidade do comando `su` em um sistema Linux moderno.

O cifrão (`$`) deve encerrar o prompt da linha de comando no shell de usuário não privilegiado, enquanto o símbolo da cerquilha (`#`) deve encerrar o prompt da linha de comando no shell do superusuário (`root`). É altamente recomendável que o caractere final de qualquer prompt *nunca* se afaste desse padrão “universalmente aceito”, uma vez que essa nomenclatura é empregada em materiais de aprendizado, incluindo estes.

> [!warning]
> Nunca mude para o superusuário (`root`) sem passar o parâmetro do shell de login (`-`). A menos que haja instruções explícitas do fornecedor do SO ou do software, quando o `su` for necessário sempre se deve executar `su -`, com pouquíssimas exceções. Os ambientes de usuário podem causar problemas e alterações indesejáveis de configuração quando usados no modo de privilégio total como superusuário.

Qual o grande problema de se usar `su` para passar ao modo superusuário (`root`)? Se a sessão de um usuário regular tiver sido comprometida, a senha do superusuário (`root`) poderia ser capturada. É aí que entra o “Switch User Do” (ou “Superuser Do”):

```bash
$ cat /sys/devices/virtual/dmi/id/board_serial
cat: /sys/devices/virtual/dmi/id/board_serial: Permission denied

$ sudo cat /sys/devices/virtual/dmi/id/board_serial
[sudo] password for emma:
/6789ABC/
```

Na listagem anterior, o usuário está tentando procurar o número de série da placa do sistema. No entanto, a permissão é negada, pois essas informações estão marcadas como privilegiadas.

Porém, usando o `sudo`, o usuário digita sua própria senha para se autenticar. Se ele tiver sido autorizado na configuração `sudoers` para executar esse comando com privilégio, com as opções permitidas, ele funcionará.

> [!tip]
> Por padrão, o primeiro comando autorizado `sudo` autenticará os comandos `sudo` subsequentes por um período (muito curto) de tempo. Isso pode ser configurado pelo administrador do sistema.

##### Arquivos de controle de acesso

Quase todos os sistemas operacionais têm um conjunto de locais usados para armazenar os controles de acesso. No Linux, esses são tipicamente arquivos de texto localizados no diretório `/etc`, que é onde costumam ser armazenados os arquivos de configuração do sistema. Por padrão, esse diretório é legível por todos os usuários no sistema, mas modificável apenas por `root`.

Os principais arquivos relacionados a contas de usuário, atributos e controle de acesso são:

`/etc/passwd`

Este arquivo armazena informações básicas sobre os usuários no sistema, incluindo UID e GID, diretório inicial, shell etc. Apesar do nome, nenhuma senha é armazenada aqui.

`/etc/group`

Este arquivo armazena informações básicas sobre todos os grupos de usuários no sistema, como nome do grupo, GID e membros.

`/etc/shadow`

É aqui que as senhas dos usuários são armazenadas. Elas são criptografadas por segurança.

`/etc/gshadow`

Este arquivo armazena informações mais detalhadas sobre grupos, incluindo uma senha criptografada com hash que permite que os usuários se tornem membros do grupo temporariamente, uma lista de usuários que podem se tornar membros do grupo a qualquer momento e uma lista de administradores do grupo.

> [!warning]
> Esses arquivos não foram projetados para ser editados diretamente e isso jamais deve ser feito. Esta lição aborda apenas as informações armazenadas nesses arquivos e não a edição deles.

Por padrão, qualquer usuário pode acessar o `/etc` e ler os arquivos `/etc/passwd` e `/etc/group`. E também por padrão nenhum usuário, exceto `root`, pode ler os arquivos `/etc/shadow` ou `/etc/gshadow`.

Também existem arquivos relacionados ao aumento básico de privilégios em sistemas Linux, como nos comandos `su` e `sudo`. Por padrão, eles só estão acessíveis ao usuário `root`.

`/etc/sudoers`

Este arquivo controla quem pode usar o comando `sudo` e como.

`/etc/sudoers.d`

Este diretório pode conter arquivos que suplementam as configurações do arquivo `sudoers`.

No que diz respeito ao exame LPI Linux Essentials, basta conhecer o caminho e o nome do arquivo padrão de configuração do sudo, `/etc/sudoers`. A configuração dele está além do escopo destes materiais.

> [!warning]
> Embora `/etc/sudoers` seja um arquivo de texto, ele jamais deve ser editado diretamente. Se for necessário fazer alterações em seu conteúdo, elas devem ser efetuadas através do utilitário `visudo`.

###### /etc/passwd

O arquivo `/etc/passwd` é popularmente chamado “arquivo password” (senha). Cada linha contém diversos campos, sempre delimitados por dois pontos (`:`). Apesar do nome, o hash one- way das senhas não é armazenado neste arquivo atualmente.

A sintaxe típica de uma linha nesse arquivo é:

```
USERNAME:PASSWORD:UID:GID:GECOS:HOMEDIR:SHELL
```

Onde:

`USERNAME`

O nome de usuário ou nome de login (nome), como `root`, `nobody`, `emma`.

`PASSWORD`

Antigo local do hash de senhas. Quase sempre é `x`, indicando que a senha está armazenada no arquivo `/etc/shadow`.

`UID`

ID de usuário (UID), como `0`, `99`, `1024`.

`GID`

ID de grupo padrão (GID), como `0`, `99`, `1024`.

`GECOS`

Uma lista em formato CSV de informações de usuários, incluindo nome, localização, número de telefone. Por exemplo: `Emma Smith,42 Douglas St,555.555.5555`

`HOMEDIR`

Caminho para o diretório inicial do usuário, como `/root`, `/home/emma`, etc.

`SHELL`

O shell padrão para este usuário, como `/bin/bash`, `/sbin/nologin`, `/bin/ksh` etc.

Por exemplo, a linha a seguir descreve o usuário `emma`:

```
emma:x:1000:1000:Emma Smith,42 Douglas St,555.555.5555:/home/emma:/bin/bash
```

**Compreendendo o campo GECOS**

O campo GECOS contém três (3) ou mais campos delimitados por vírgula (`,`), sendo também conhecido como lista de Valores Separados por Vírgula (*Comma Separated Values*, ou CSV). Embora não exista um padrão imposto, os campos geralmente estão na seguinte ordem:

```
NAME,LOCATION,CONTACT
```

Onde:

`NAME`

é o “Full Name” (nome completo) do usuário, ou o “Software Name” (nome do software) no caso de uma conta de serviço.

`LOCATION`

normalmente é a localização física do usuário dentro de um prédio, o número da sala ou o departamento ou pessoa a contatar no caso de uma conta de serviço.

`CONTACT`

lista as informações de contato, como o telefone pessoal ou profissional.

Os campos adicionais podem incluir outras informações de contato, como um número residencial ou endereço de email. Para alterar as informações no campo GECOS, use o comando `chfn` e responda às perguntas, como abaixo. Se nenhum nome de usuário for fornecido após o nome do comando, serão alteradas as informações do usuário atual:

```bash
$ chfn

Changing the user information for emma
Enter the new value, or press ENTER for the default
Full Name: Emma Smith
Room Number []: 42
Work Phone []: 555.555.5555
Home Phone []: 555.555.6666
```

###### /etc/group

O arquivo `/etc/group` contém arquivos delimitados por dois pontos (`:`), armazenando informações básicas sobre os grupos no sistema. Ele às vezes é chamado “arquivo de grupo”. A sintaxe de cada linha é:

```
NAME:PASSWORD:GID:MEMBERS
```

Onde:

`NAME`

é o nome do grupo, como `root`, `users`, `emma` etc.

`PASSWORD`

Antigo local do hash opcional de senhas de grupos. Quase sempre é `x`, indicando que a senha (caso definida) está armazenada no arquivo `/etc/gshadow`.

`GID`

ID de grupo (GID), como `0`, `99`, `1024`.

`MEMBERS`

uma lista de nomes de usuário que são membros do grupo, separados por vírgula, como `jsmith,emma`.

O exemplo abaixo mostra uma linha contendo informações sobre o grupo `students`:

```
students:x:1023:jsmith,emma
```

O usuário não precisa ser listado no campo members quando o grupo é o grupo principal de um usuário. Se um usuário estiver listado, o item é redundante — ou seja, não há alterações na funcionalidade, estando listado ou não.

> [!note]
> O uso de senhas para grupos está além do escopo desta seção; no entanto, se houver uma, o hash da senha é armazenado no arquivo `/etc/gshadow`. Isso também está além do escopo desta seção.

###### /etc/shadow

A tabela a seguir lista os atributos armazenados no arquivo `/etc/shadow`, comumente chamado de “arquivo de sombra”. O arquivo contém campos sempre delimitados por dois pontos (`:`).

Embora o arquivo tenha muitos campos, a maioria está além do escopo desta lição, exceto os dois primeiros.

A sintaxe básica para uma linha nesse arquivo é:

```
USERNAME:PASSWORD:LASTCHANGE:MINAGE:MAXAGE:WARN:INACTIVE:EXPDATE
```

Onde:

`USERNAME`

O nome de usuário (igual a `/etc/passwd`), como `root`, `nobody`, `emma`.

`PASSWORD`

Um hash unidirecional da senha, incluindo o sal anterior. Por exemplo: `!!`, `!$1$01234567$ABC…`, `$6$012345789ABCDEF$012…`.

`LASTCHANGE`

Data da última alteração da senha em dias desde a “época”, como `17909`.

`MINAGE`

Idade mínima da senha em dias.

`MAXAGE`

Idade máxima da senha em dias.

`WARN`

Período de aviso antes da expiração da senha, em dias.

`INACTIVE`

Idade máxima da senha após a expiração, em dias.

`EXPDATE`

Data da expiração da senha, em dias desde a “época”.

No exemplo abaixo vemos um exemplo de entrada do arquivo `/etc/shadow`. Note que certos valores, como `INACTIVE` e `EXPDATE`, estão indefinidos.

```
emma:$6$nP532JDDogQYZF8I$bjFNh9eT1xpb9/n6pmjlIwgu7hGjH/eytSdttbmVv0MlyTMFgBIXESFNUmTo9EGxxH1
OT1HGQzR0so4n1npbE0:18064:0:99999:7:::
```

A “época” de um sistema POSIX é meia-noite (0000) do Tempo Universal Coordenado (UTC), na quinta-feira, 1º de janeiro de 1970. A maioria das datas e horas POSIX estão em segundos desde a “época” ou, no caso do arquivo `/etc/shadow`, dias desde a “época”.

> [!note]
> O arquivo de sombra foi desenvolvido para ser legível apenas pelo superusuário e serviços selecionados de autenticação do sistema principal que verificam o hash de senha unidirecional no login ou em outro momento da autenticação.

Embora existam soluções de autenticação diferentes, o método básico de armazenamento de senha é a *função de hash* unidirecional (one-way). Isso é feito para que a senha nunca seja armazenada em texto não criptografado em um sistema, já que a função de hash não é reversível. Você pode transformar uma senha em um hash, mas (idealmente) não é possível transformar um hash novamente em uma senha.

No máximo, é necessário um método de força bruta para experimentar todas as combinações de uma senha até que uma delas corresponda. Para atenuar o risco de um hash de senha ser quebrado em um sistema, os sistemas Linux aplicam um “sal” aleatório em cada hash de senha de um usuário. Assim, o hash para uma senha de usuário em um sistema Linux geralmente não será o mesmo que em outro sistema Linux, mesmo que a senha seja idêntica.

No arquivo `/etc/shadow`, a senha pode assumir diversas formas. Elas tipicamente incluem o seguinte:

`!!`

Indica uma conta “desativada” (a autenticação não é possível), sem hash de senha armazenado.

`!$1$01234567$ABC…`

Uma conta “desativada” (indicado pelo ponto de exclamação inicial), com uma função de hash anterior, sal de hash e string de hash armazenados.

`$1$0123456789ABC$012…`

Uma conta “ativada”, com uma função de hash, sal de hash e string de hash armazenados.

A função de hash, o sal de hash e a string de hash são precedidos e delimitados por um cifrão (`$`). O comprimento do sal de hash deve ser entre oito e dezesseis (8-16) caracteres. Eis exemplos dos três mais comuns:

`$1$01234567$ABC…`

Uma função de hash de MD5 (`1`), com um hash de exemplo com oito caracteres.

`$5$01234567ABCD$012…`

Uma função de hash de SHA256 (`5`), com um hash de exemplo com doze caracteres.

`$6$01234567ABCD$012…`

Uma função de hash de SHA512 (`6`), com um hash de exemplo com doze caracteres.

> [!note]
> A função de hash MD5 é considerada criptograficamente insegura em relação ao nível atual (2010 e posterior) dos ASICs e até mesmo para os SIMD usados para computação em geral. Na verdade, o FIPS (Federal Information Processing Standards) dos EUA não permite que o MD5 seja usado para quaisquer funções criptográficas, exceto em aspectos muito limitados de validação, mas não para garantir a integridade das assinaturas digitais ou finalidades similares.

Do ponto de vista dos objetivos e do exame LPI Linux Essentials, basta entender que o hash da senha de um usuário local é armazenado no arquivo `/etc/shadow`, que apenas serviços selecionados de autenticação podem ler e o superusuário pode modificar através de outros comandos.

#### Exercícios Guiados

1. Considere a seguinte saída do comando `id`:

  ```bash
  $ id emma
  uid=1000(emma) gid=1000(emma)
  groups=1000(emma),4(adm),5(tty),10(uucp),20(dialout),27(sudo),46(plugdev)
  ```

  Em quais arquivos estão armazenados os atributos a seguir?

  UID e GID

  Grupos

  - Adicionalmente, em qual arquivo a senha do usuário é armazenada?

2. Quais dos tipos de criptografia a seguir é usado por padrão para armazenar senhas localmente em um sistema Linux?

  - Asymmetric
  - One-way Hash
  - Symmetric
  - ROT13

3. Se uma conta tem um ID de usuário (UID) com número menor que 1000, de que tipo de conta se trata?

4. Como é possivel obter uma lista dos logins ativos de seu sistema e uma contagem deles?

5. Usando o comando `grep`, temos o resultado abaixo com informações sobre o usuário `emma`.

  ```bash
  $ grep emma /etc/passwd
  emma:x:1000:1000:Emma Smith,42 Douglas St,555.555.5555,:/home/emma:/bin/ksh
  ```

  Preencha as lacunas da tabela com as informações apropriadas usando a saída do comando anterior.

  Nome de usuário

  Senha

  UID

  GID principal

  GECOS

  Diretório inicial

  Shell

#### Exercícios Exploratórios

1. Compare os resultados de `last` com `w` e `who`. Quais detalhes estão faltando em cada um dos comandos em comparação com os outros?

2. Tente lançar os comandos `who` e `w -his`.

  - Quais informações foram removidas da saída do comando `w` com as opções “no header” (`-h`) e “short” (`-s`)?
  - Quais informações foram adicionadas à saída do comando `w` com a opção “ip address” (`-i`)?

3. Qual é o arquivo que armazena o hash de senha unidirecional de uma conta de usuário?

4. Qual arquivo contém a lista dos grupos de que uma conta de usuário faz parte? Qual lógica poderia ser usada para compilar uma lista dos grupos de que uma conta de usuário faz parte?

5. Um ou mais (1+) dos seguintes arquivos não é legível por usuários regulares, sem privilégios especiais, por padrão. Quais?

  - `/etc/group`
  - `/etc/passwd`
  - `/etc/shadow`
  - `/etc/sudoers`

6. Como seria possível trocar o shell de login do usuário atual pelo Korn Shell (`/usr/bin/ksh`) em modo não-interativo?

7. Por que o diretório inicial do usuário `root` não fica dentro do diretório `/home`?

#### Resumo

Nesta lição, descobrimos os bancos de dados de usuários e grupos do Linux. Aprendemos as propriedades mais importantes de usuários e grupos, incluindo seus nomes e IDs numéricos. Também investigamos como o hash de senhas funciona no Linux e como os grupos são atribuídos aos usuários.

Todas essas informações são armazenadas nos quatro arquivos a seguir, que fornecem os controles de acesso de segurança local mais básicos em um sistema Linux:

`/etc/passwd`

Todos os atributos POSIX locais da conta de usuário, exceto o hash da senha, legíveis por todos.

`/etc/group`

Todos os atributos POSIX locais da conta de grupo, legíveis por todos.

`/etc/shadow`

Todos os hashes de senha locais de usuário (e informações de expiração), ilegíveis por qualquer um (apenas processos selecionados).

`/etc/sudoers`

Todas as informações/permissões locais de aumento de privilégios pelo comando `sudo`.

Os seguintes comandos foram discutidos nesta lição:

`id`

Lista IDs de usuários e grupos reais (ou efetivos).

`last`

Lista os usuários que fizeram login por último.

`who`

Lista usuários que estão conectados no momento.

`w`

Semelhante a `who`, mas com contexto adicional.

`su`

Alterna para outro usuário com um shell de login ou executa comandos como aquele usuário, contornando a senha desse usuário. `sudo`

Switch User Do (Substituição de Usuário) ou Superuser Do (Fazer como Superusuário). Caso esteja autorizado, o usuário atual digita sua própria senha (se necessário) para aumentar os privilégios.

`chsh`

Troca o shell de um usuário.

`chfn`

Altera as informações do usuário no campo GECOS.

#### Respostas aos Exercícios Guiados

1. Considere a seguinte saída do comando `id`:

  ```bash
  $ id emma
  uid=1000(emma) gid=1000(emma)
  groups=1000(emma),4(adm),5(tty),10(uucp),20(dialout),27(sudo),46(plugdev)
  ```

  Em quais arquivos estão armazenados os atributos a seguir?

  UID e GID `/etc/passwd`

  Grupos `/etc/group`

  - Adicionalmente, em qual arquivo a senha do usuário é armazenada?

  A senha de usuário criptografada fica armazenada em `/etc/shadow`.

2. Quais dos tipos de criptografia a seguir é usado por padrão para armazenar senhas localmente em um sistema Linux?

  Por padrão, um hash unidirecional é usado para armazenar senhas.

3. Se uma conta tem um ID de usuário (UID) com número menor que 1000, de que tipo de conta se trata?

  Contas com UID menor que 1000 geralmente são contas de sistema.

4. Como é possivel obter uma lista dos logins ativos de seu sistema e uma contagem deles?

  Use o comando `w`. Além de uma lista de logins ativos, ele também mostra informações como a quantidade de usuários conectados, além da carga e tempo de atividade do sistema.

5. Usando o comando `grep`, temos o resultado abaixo com informações sobre o usuário `emma`.

  ```bash
  $ grep emma /etc/passwd
  emma:x:1000:1000:Emma Smith,42 Douglas St,555.555.5555,:/home/emma:/bin/ksh
  ```

  Preencha as lacunas da tabela com as informações apropriadas usando a saída do comando anterior.

| Nome de usuário | `emma` |
|---|---|
| Senha | `x` - deve sempre ser `x` para um login ativo válido |
| UID | `1000` |
| GID principal | `1000` |
| GECOS | `Emma Smith,42 Douglas St,555.555.5555` |
| Diretório inicial | `/home/emma` |
| Shell | `/bin/ksh` |

#### Respostas aos Exercícios Exploratórios

1. Compare os resultados de `last` com `w` e `who`. Quais detalhes estão faltando em cada um dos comandos em comparação com os outros?

  As ferramentas `w` e `who` listam apenas os usuários atualmente conectados ao sistema, ao passo que `last` também lista os usuários que se desconectaram. O comando `w` lista a utilização do sistema, enquanto `who` não faz isso.

2. Tente lançar os comandos `who` e `w -his`.

  - Quais informações foram removidas da saída do comando `w` com as opções “no header” (`-h`) e “short” (`-s`)?

  O cabeçalho não é impresso, o que é útil para análise, e o tempo de login e informações selecionadas da CPU não são listados, respectivamente.

  - Quais informações foram adicionadas à saída do comando `w` com a opção “ip address” (`-i`)?

  Essa opção imprime o endereço IP, em vez de tentar a resolução de DNS, imprimindo o nome do host. Essa opção de `w` é mais adequada à saída padrão do comando `last`.

3. Qual é o arquivo que armazena o hash de senha unidirecional de uma conta de usuário?

  O arquivo `/etc/shadow` armazena o hash unidirecional de uma conta de usuário, já que ele não é legível por uma conta de usuário regular, sem privilégios, ao contrário do arquivo `/etc/passwd`.

4. Qual arquivo contém a lista dos grupos de que uma conta de usuário faz parte? Qual lógica poderia ser usada para compilar uma lista dos grupos de que uma conta de usuário faz parte?

  O arquivo `/etc/group` tem uma lista em formato CSV de nomes de usuários no último campo (“members”) de qualquer linha correspondente a um grupo.

  Qualquer linha no arquivo `/etc/group` na qual o usuário aparece listado no último campo, “members”, implica que o usuário é membro daquele grupo — supondo-se que ele esteja corretamente formatado (valores delimitados por vírgulas). Além disso, a participação do usuário em seu grupo principal no arquivo `/etc/passwd` também terá uma entrada correspondente no arquivo `/etc/group`, incluindo tanto o nome do grupo quanto o GID.

5. Um ou mais (1+) dos seguintes arquivos não é legível por usuários regulares, sem privilégios especiais, por padrão. Quais?

  - `/etc/group`
  - `/etc/passwd`
  - `/etc/shadow`
  - `/etc/sudoers`

  Os arquivos `/etc/shadow` e `/etc/sudoers` não são legíveis por padrão, exceto por serviços selecionados ou o superusuário. Estas respostas serão personalizadas com base nos sistemas e nomes de usuário usados no laboratório.

6. Como seria possível trocar o shell de login do usuário atual pelo Korn Shell (`/usr/bin/ksh`) em modo não-interativo?

  ```bash
  $ chsh -s /usr/bin/ksh
  ```

7. Por que o diretório inicial do usuário `root` não fica dentro do diretório `/home`?

  Porque a conta `root` é necessária para resolver problemas e corrigir erros, o que pode incluir problemas no sistema de arquivos relacionados ao diretório `/home`. Nesses casos, `root` deve estar plenamente funcional mesmo que o sistema de arquivos de `/home` esteja indisponível.

## 5.2 Criando Usuários e Grupos

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 5.2
- **Peso**: 2

**Áreas chave de conhecimento**

- Comandos de usuários e de grupos
- IDs de usuários

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `/etc/passwd`, `/etc/shadow`, `/etc/group`, `/etc/skel/`
- `useradd`, `groupadd`
- `passwd`

### 5.2 Lição 1

#### Introdução

Gerenciar usuários e grupos em uma máquina Linux é um dos principais aspectos da administração do sistema. De fato, o Linux é um sistema operacional multiusuário no qual vários usuários podem usar a mesma máquina ao mesmo tempo.

As informações sobre usuários e grupos são armazenadas em quatro arquivos na árvore de diretórios `/etc/`:

`/etc/passwd`

um arquivo de sete campos delimitados por dois pontos contendo informações básicas sobre os usuários

`/etc/group`

um arquivo de quatro campos delimitados por dois pontos contendo informações básicas sobre os grupos

`/etc/shadow`

um arquivo de nove campos delimitados por dois pontos contendo senhas de usuário criptografadas

`/etc/gshadow`

um arquivo de quatro campos delimitados por dois pontos contendo senhas de grupo criptografadas

Todos esses arquivos são atualizados por um conjunto de ferramentas de linha de comando para gerenciamento de usuários e grupos, de que falaremos mais adiante nesta lição. Também existem aplicativos gráficos, específicos para cada distribuição Linux, com interfaces de gerenciamento mais simples e imediatas.

> [!warning]
> Mesmo que os arquivos sejam em texto simples, não os edite diretamente. Sempre use as ferramentas fornecidas com sua distribuição.

##### O Arquivo `/etc/passwd`

`/etc/passwd` é um arquivo legível por todos contendo uma lista de usuários em linhas separadas:

```
frank:x:1001:1001::/home/frank:/bin/bash
```

Cada linha consiste em sete campos delimitados por dois pontos:

- **Nome de usuário**: O nome usado quando o usuário se loga no sistema.
- **Senha**: A senha criptografada (ou um `x` no caso de senhas shadow).
- **ID de usuário (UID)**: O número de identificação atribuído ao usuário no sistema.
- **ID de grupo (GID)**: O número do grupo principal do usuário no sistema.
- **GECOS**: Um campo de comentário opcional, usado para adicionar informações extras sobre o usuário (como o nome completo). O campo pode conter diversas entradas separadas por vírgula.
- **Diretório inicial**: O caminho absoluto do diretório inicial do usuário.
- **Shell**: O caminho absoluto do programa que é iniciado automaticamente quando o usuário efetua login no sistema (geralmente um shell interativo como `/bin/bash`).

##### O arquivo `/etc/group`

`/etc/group` é um arquivo legível por todos contendo uma lista de grupos em linhas separadas:

```
developer:x:1002:
```

Cada linha consiste em quatro campos delimitados por dois pontos:

- **Nome do grupo**: O nome do grupo.
- **Senha do grupo**: A senha criptografada do grupo (ou um `x` se forem usadas senhas shadow).
- **ID do grupo (GID)**: O número de identificação atribuído ao grupo no sistema.
- **Lista de membros**: Uma lista delimitada por vírgulas de usuários pertencentes ao grupo, exceto aqueles cujo grupo principal é este.

##### O arquivo `/etc/shadow`

`/etc/shadow` é um arquivo legível apenas pelo usuário root ou com privilégios de root e contém as senhas criptografadas dos usuários em linhas separadas:

```
frank:$6$i9gjM4Md4MuelZCd$7jJa8Cd2bbADFH4dwtfvTvJLOYCCCBf/.jYbK1IMYx7Wh4fErXcc2xQVU2N1gb97yI
YaiqH.jjJammzof2Jfr/:18029:0:99999:7:::
```

Cada linha consiste em nove campos delimitados por dois pontos:

- **Nome de usuário**: O nome usado quando o usuário se loga no sistema.
- **Senha criptografada**: A senha do usuário criptografada (se o valor for `!`, a conta está bloqueada).
- **Data da última alteração de senha**: A data da última mudança de senha em número de dias desde 01/01/1970. Um valor de `0` indica que o usuário precisa trocar a senha em seu próximo acesso.
- **Idade mínima da senha**: O número mínimo de dias que o usuário deve aguardar após uma alteração de senha para poder trocar a senha novamente.
- **Idade máxima da senha**: O número máximo de dias que devem passar antes que uma alteração de senha seja solicitada.
- **Período de aviso de senha**: O número de dias para a expiração da senha, durante os quais o usuário é avisado de que a senha deve ser alterada.
- **Período de inatividade da senha**: O número de dias após a expiração de uma senha, durante os quais o usuário deve atualizá-la. Após esse período, se o usuário não alterar a senha, a conta é desativada.
- **Data de expiração da conta**: A data, em número de dias desde 01/01/1970, na qual a conta do usuário será desativada. Um campo vazio indica que a conta do usuário nunca expirará.
- **Um campo reservado**: Um campo reservado para uso futuro.

##### O arquivo `/etc/gshadow`

`/etc/gshadow` é um arquivo legível apenas pelo root e por usuários com privilégios de root que contém senhas criptografadas para grupos em linhas separadas:

```
developer:$6$7QUIhUX1WdO6$H7kOYgsboLkDseFHpk04lwAtweSUQHipoxIgo83QNDxYtYwgmZTCU0qSCuCkErmyR2
63rvHiLctZVDR7Ya9Ai1::
```

Cada linha consiste em quatro campos delimitados por dois pontos:

- **Nome do grupo**: O nome do grupo.
- **Senha criptografada**: A senha criptografada do grupo (é usada quando um usuário que não é membro do grupo deseja ingressar no grupo usando o comando `newgrp` — se a senha começar com `!`, ninguém tem permissão de acessar o grupo com `newgrp`).
- **Administradores do grupo**: Uma lista dos administradores do grupo delimitada por vírgulas (eles podem alterar a senha do grupo, bem como adicionar ou remover membros do grupo com o comando `gpasswd`)
- **Membros do grupo**: Uma lista dos membros do grupo delimitada por vírgulas.

Agora que vimos onde as informações de usuários e grupos são armazenadas, vamos falar sobre as ferramentas de linha de comando mais importantes para atualizar esses arquivos.

##### Adicionando e removendo contas de usuário

No Linux, adicionamos uma nova conta de usuário com o comando `useradd` e excluímos uma conta de usuário com o comando `userdel`.

Se quiséssemos criar uma nova conta de usuário chamada `frank` com uma configuração padrão, executaríamos o seguinte:

```bash
# useradd frank
```

Após criar o novo usuário, definimos uma senha usando `passwd`:

```bash
# passwd frank
Changing password for user frank.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
```

Ambos os comandos requerem autoridade de root. Quando executamos o comando `useradd`, as informações de usuário e grupo armazenadas nos bancos de dados de senha e de grupo são atualizadas para a conta de usuário recém-criada e, caso especificado, o diretório inicial do novo usuário é criado, bem como um grupo com o mesmo nome da conta de usuário.

Lembre-se de que sempre podemos usar o utilitário `grep` para filtrar os bancos de dados de senhas e grupos, exibindo apenas a entrada referente a um usuário ou grupo específico. Para o exemplo acima, usaríamos

`cat /etc/passwd | grep frank` **TIP** ou

`grep frank /etc/passwd`

para ver informações básicas sobre a conta `frank` recém-criada.

As opções mais importantes que se aplicam ao comando `useradd` são:

`-c`

Cria uma nova conta de usuário com comentários personalizados (por exemplo, nome completo)

`-d`

Cria uma nova conta de usuário com um diretório inicial personalizado.

`-e`

Cria uma nova conta de usuário com uma data específica na qual ela será desativada.

`-f`

Cria uma nova conta de usuário definindo o número de dias que o usuário tem para atualizar a senha após a expiração.

`-g`

Cria uma nova conta de usuário com um GID específico.

`-G`

Cria uma nova conta de usuário adicionando-a a diversos grupos secundários.

`-m`

Cria uma nova conta de usuário com seu diretório inicial.

`-M`

Cria uma nova conta de usuário sem seu diretório inicial.

`-s`

Cria uma nova conta de usuário com um shell de login específico.

`-u`

Cria uma nova conta de usuário com um UID específico.

Depois que a nova conta de usuário é criada, usamos os comandos `id` e `groups` para descobrir seu UID, GID e os grupos aos quais pertence.

```bash
# id frank
uid=1000(frank) gid=1000(frank) groups=1000(frank)
# groups frank
frank : frank
```

> [!tip]
> Lembre-se de verificar e, possivelmente, editar o arquivo `/etc/login.defs`, que define os parâmetros de configuração que controlam a criação de usuários e grupos. Por exemplo, você pode definir o intervalo de UIDs e GIDs que podem ser atribuídos a novas contas de usuário e grupo, especificar que não é necessário usar a opção `-m` para criar o diretório inicial do novo usuário e se o sistema deve criar automaticamente um novo grupo para cada novo usuário.

Se quiser excluir uma conta de usuário, pode usar o comando `userdel`. Esse comando atualiza, em particular, as informações armazenadas nos bancos de dados da conta, excluindo todas as entradas referentes ao usuário especificado. A opção `-r` também remove o diretório inicial do usuário e todo o seu conteúdo, juntamente com o spool de correio do usuário. Os arquivos que estiverem em outros locais deverão ser pesquisados e excluídos manualmente.

```bash
# userdel -r frank
```

Também neste caso, é preciso ter autoridade root para excluir contas de usuário.

##### O diretório de esqueleto

Quando adicionamos uma nova conta de usuário e criamos seu diretório pessoal, este é preenchido com arquivos e pastas copiados do diretório de esqueleto (por padrão, `/etc/skel`). A idéia é simples: um administrador de sistema quer que os novos usuários tenham os mesmos arquivos e diretórios em seu diretório inicial. Portanto, se você deseja personalizar os arquivos e pastas que são criados automaticamente no diretório inicial das novas contas de usuário, adicione esses novos arquivos e pastas ao diretório de esqueleto.

> [!tip]
> Note que os arquivos de perfil geralmente encontrados no diretório de esqueleto são arquivos ocultos. Portanto, se você deseja listar todos os arquivos e pastas do diretório de esqueleto que serão copiados para o diretório inicial dos usuários recém-

criados, deve usar o comando `ls -Al`.

##### Adicionando e excluindo grupos

Quanto ao gerenciamento dos grupos, os comandos `groupadd` e `groupdel` servem para adicionar e excluir grupos.

Para criar um novo grupo chamado `developer`, executaríamos o seguinte comando como root:

```bash
# groupadd -g 1090 developer
```

A opção `-g` deste comando cria um grupo com um GID específico.

Se quiser remover o grupo `developer`, você pode executar este comando:

```bash
# groupdel developer
```

> [!warning]
> Lembre-se de que quando adicionamos uma nova conta de usuário, o grupo principal e os grupos secundários aos quais ela pertence devem existir antes de se iniciar o comando `useradd`. Além disso, não é possível excluir um grupo se este for o grupo principal de uma conta de usuário.

##### O comando `passwd`

Este comando é usado principalmente para alterar a senha de um usuário. Qualquer usuário pode alterar sua senha, mas apenas o root pode alterar a senha de qualquer usuário.

Dependendo da opção de `passwd` usada, podemos controlar aspectos específicos do envelhecimento da senha:

`-d`

Exclui a senha de uma conta de usuário (definindo assim uma senha vazia, transformando-a em uma conta sem senha).

`-e`

Força a conta de usuário a alterar a senha.

`-l`

Bloqueia a conta de usuário (a senha criptografada é prefixada com um ponto de exclamação).

`-u`

Desbloqueia a conta de usuário (o ponto de exclamação é removido).

`-S`

Exibe informações sobre o status da senha de uma conta específica.

Essas opções só estão disponíveis para o root. Para ver a lista completa de opções, consulte as páginas de manual.

#### Exercícios Guiados

1. Indique a que arquivo se refere cada uma das entradas a seguir:

  - `developer:x:1010:frank,grace,dave`
  - `root:x:0:0:root:/root:/bin/bash`
  - `henry:$1$.AbCdEfGh123456789A1b2C3d4.:18015:20:90:5:30::`
  - `henry:x:1000:1000:User Henry:/home/henry:/bin/bash`
  - `staff:!:dave:carol,emma`

2. Observe esta saída para responder às sete questões a seguir:

  ```bash
  # cat /etc/passwd | tail -3
  dave:x:1050:1050:User Dave:/home/dave:/bin/bash
  carol:x:1051:1015:User Carol:/home/carol:/bin/sh
  henry:x:1052:1005:User Henry:/home/henry:/bin/tcsh
  # cat /etc/group | tail -3
  web_admin:x:1005:frank,emma
  web_developer:x:1010:grace,kevin,christian
  dave:x:1050:
  # cat /etc/shadow | tail -3
  dave:$6$AbCdEfGh123456789A1b2C3D4e5F6G7h8i9:0:20:90:7:30::
  carol:$6$q1w2e3r4t5y6u7i8AbcDeFgHiLmNoPqRsTu:18015:0:60:7:::
  henry:!$6$123456789aBcDeFgHa1B2c3d4E5f6g7H8I9:18015:0:20:5:::
  # cat /etc/gshadow | tail -3
  web_admin:!:frank:frank,emma
  web_developer:!:kevin:grace,kevin,christian
  dave:!::
  ```

  - Qual o identificador de usuário (UID) e identificador de grupo (GID) de `carol`?
  - Qual shell está configurado para `dave` e `henry`?
  - Qual o nome do grupo principal de `henry`?
  - Quem são os membros do grupo `web_developer`? Quais deles são administradores do grupo?
  - Qual usuário não pode se logar no sistema?
  - Qual usuário deverá mudar a senha na próxima vez em que fizer login no sistema?
  - Quantos dias devem se passar até que seja exigida uma alteração de senha para `carol`?

#### Exercícios Exploratórios

1. Trabalhando como root, use o comando `useradd -m dave` para adicionar uma nova conta de usuário. Quais as operações realizadas por esse comando? Suponha que `CREATE_HOME` e `USERGROUPS_ENAB` em `/etc/login.defs` estejam definidos como sim.

2. A conta de usuário `dave` foi criada; esse usuário pode fazer login no sistema?

3. Encontre o identificador de usuário (UID) e de grupo (GID) de `dave` e todos os membros do grupo `dave`.

4. Crie os grupos `sys_admin`, `web_admin` e `db_admin` e encontre seus identificadores de grupo (GIDs).

5. Adicione uma nova conta de usuário de nome `carol` com UID 1035 e defina `sys_admin` como grupo principal e `web_admin` e `db_admin` como grupos secundários.

6. Exclua as contas de usuário `dave` e `carol` e os grupos `sys_admin`, `web_admin` e `db_admin` criados anteriormente.

7. Execute o comando `ls -l /etc/passwd /etc/group /etc/shadow /etc/gshadow` e descreva a saída em termos de permissões de arquivos. Quais desses quatro arquivos estão em shadow por razões de segurança? Pressuponha que seu sistema usa senhas shadow.

8. Execute o comando `ls -l /usr/bin/passwd`. Qual bit especial é definido e o que ele significa?

#### Resumo

Nesta lição, você aprendeu:

- Noções fundamentais de gerenciamento de usuários e grupos no Linux
- Gerenciar informações de usuários e grupos armazenados nos bancos de dados de senhas e grupos
- Manter o diretório de esqueleto
- Adicionar e remover contas de usuário
- Adicionar e remover contas de grupo
- Alterar a senha das contas de usuário

Os seguintes comandos foram discutidos nesta lição:

`useradd`

Cria uma nova conta de usuário.

`groupadd`

Cria uma nova conta de grupo.

`userdel`

Exclui uma conta de usuário.

`groupdel`

Exclui uma conta de grupo.

`passwd`

Altera a senha das contas de usuário e controla todos os aspectos do envelhecimento da senha.

#### Respostas aos Exercícios Guiados

1. Indique a que arquivo se refere cada uma das entradas a seguir:

  - `developer:x:1010:frank,grace,dave`

  `/etc/group`

  - `root:x:0:0:root:/root:/bin/bash`

  `/etc/passwd`

  - `henry:$1$.AbCdEfGh123456789A1b2C3d4.:18015:20:90:5:30::`

  `/etc/shadow`

  - `henry:x:1000:1000:User Henry:/home/henry:/bin/bash`

  `/etc/passwd`

  - `staff:!:dave:carol,emma`

  `/etc/gshadow`

2. Observe esta saída para responder às sete questões a seguir:

  ```bash
  # cat /etc/passwd | tail -3
  dave:x:1050:1050:User Dave:/home/dave:/bin/bash
  carol:x:1051:1015:User Carol:/home/carol:/bin/sh
  henry:x:1052:1005:User Henry:/home/henry:/bin/tcsh
  # cat /etc/group | tail -3
  web_admin:x:1005:frank,emma
  web_developer:x:1010:grace,kevin,christian
  dave:x:1050:
  # cat /etc/shadow | tail -3
  dave:$6$AbCdEfGh123456789A1b2C3D4e5F6G7h8i9:0:20:90:7:30::
  carol:$6$q1w2e3r4t5y6u7i8AbcDeFgHiLmNoPqRsTu:18015:0:60:7:::
  henry:!$6$123456789aBcDeFgHa1B2c3d4E5f6g7H8I9:18015:0:20:5:::
  # cat /etc/gshadow | tail -3
  web_admin:!:frank:frank,emma
  web_developer:!:kevin:grace,kevin,christian
  dave:!::
  ```

  - Qual o identificador de usuário (UID) e identificador de grupo (GID) de `carol`?

  O identificador de usuário é 1051 e o de grupo é 1015 (o terceiro e o quarto campos de `/etc/passwd`).

  - Qual shell está configurado para `dave` e `henry`?

  `dave` usa /bin/bash e `henry` usa /bin/tcsh (o sétimo campo em `/etc/passwd`).

  - Qual o nome do grupo principal de `henry`?

  O nome do grupo é `web_admin` (o primeiro campo em `/etc/group`).

  - Quem são os membros do grupo `web_developer`? Quais deles são administradores do grupo?

  Os membros são `grace`, `kevin` e `christian` (o quarto campo em `/etc/group`), mas apenas `kevin` é o administrador do grupo (o terceiro campo em `/etc/gshadow`).

  - Qual usuário não pode se logar no sistema?

  A conta de usuário `henry` está bloqueada (tem um ponto de exclamação na frente dos hashes de senha em `/etc/shadow`).

  - Qual usuário deverá mudar a senha na próxima vez em que fizer login no sistema?

  Se o terceiro campo (Data da Última Mudança de Senha) de `/etc/shadow` for 0, o usuário deve alterar sua senha na próxima vez em que se logar ao sistema. Portanto, `dave` deverá trocar a senha.

  - Quantos dias devem se passar até que seja exigida uma alteração de senha para `carol`?

  60 dias (o quinto campo em `/etc/shadow`).

#### Respostas aos Exercícios Exploratórios

1. Trabalhando como root, use o comando `useradd -m dave` para adicionar uma nova conta de usuário. Quais as operações realizadas por esse comando? Suponha que `CREATE_HOME` e `USERGROUPS_ENAB` em `/etc/login.defs` estejam definidos como sim.

  O comando adiciona um novo usuário, chamado `dave`, à lista de usuários no sistema. O diretório inicial de `dave` é criado (por padrão `/home/dave`) e os arquivos e diretórios contidos no diretório esqueleto são copiados no diretório inicial. Finalmente, o novo grupo é criado com o mesmo nome da conta de usuário.

2. A conta de usuário `dave` foi criada; esse usuário pode fazer login no sistema?

  Não, porque a conta `dave` está bloqueada (como indica o ponto de exclamação em `/etc/shadow`).

  ```bash
  # cat /etc/shadow | grep dave
  dave:!:18015:0:99999:7:::
  ```

  Se você definir uma senha para `dave`, a conta será desbloquada. Faça isso usando o comando `passwd`.

  ```bash
  # passwd dave
  Changing password for user dave.
  New UNIX password:
  Retype new UNIX password:
  passwd: all authentication tokens updated successfully.
  ```

3. Encontre o identificador de usuário (UID) e de grupo (GID) de `dave` e todos os membros do grupo `dave`.

  ```bash
  # cat /etc/passwd | grep dave
  dave:x:1015:1019::/home/dave:/bin/sh
  # cat /etc/group | grep 1019
  dave:x:1019:
  ```

  O UID e GID of `dave` são 1015 e 1019, respectivamente (o terceiro e o quarto campos em `/etc/passwd`) e o grupo `dave` não tem membros (o quarto campo em `/etc/group` está vazio).

4. Crie os grupos `sys_admin`, `web_admin` e `db_admin` e encontre seus identificadores de grupo

  (GIDs).

  ```bash
  # groupadd sys_admin
  # groupadd web_admin
  # groupadd db_admin
  # cat /etc/group | grep admin
  sys_admin:x:1020:
  web_admin:x:1021:
  db_admin:x:1022:
  ```

  Os GIDs dos grupos `sys_admin`, `web_admin` e `db_admin` são 1020, 1021 e 1022, respectivamente.

5. Adicione uma nova conta de usuário de nome `carol` com UID 1035 e defina `sys_admin` como grupo principal e `web_admin` e `db_admin` como grupos secundários.

  ```bash
  # useradd -u 1035 -g 1020 -G web_admin,db_admin carol
  # id carol
  uid=1035(carol) gid=1020(sys_admin) groups=1020(sys_admin),1021(web_admin),1022(db_admin)
  ```

6. Exclua as contas de usuário `dave` e `carol` e os grupos `sys_admin`, `web_admin` e `db_admin` criados anteriormente.

  ```bash
  # userdel -r dave
  # userdel -r carol
  # groupdel sys_admin
  # groupdel web_admin
  # groupdel db_admin
  ```

7. Execute o comando `ls -l /etc/passwd /etc/group /etc/shadow /etc/gshadow` e descreva a saída em termos de permissões de arquivos. Quais desses quatro arquivos estão em shadow por razões de segurança? Pressuponha que seu sistema usa senhas shadow.

  ```bash
  # ls -l /etc/passwd /etc/group /etc/shadow /etc/gshadow
  -rw-r--r-- 1 root root    853 mag  1 08:00 /etc/group
  -rw-r----- 1 root shadow 1203 mag  1 08:00 /etc/gshadow
  -rw-r--r-- 1 root root   1354 mag  1 08:00 /etc/passwd
  -rw-r----- 1 root shadow 1563 mag  1 08:00 /etc/shadow
  ```

  Os arquivos `/etc/passwd` e `/etc/group` são legíveis por todos e estão em shadow por motivos de segurança. Quando senhas shadow são usadas, vemos um `x` no segundo campo desses arquivos, porque as senhas criptografadas de usuários e grupos são armazenadas em `/etc/shadow` e `/etc/gshadow`, legíveis apenas pelo root e, em certos sistemas, também por membros pertencentes ao grupo `shadow`.

8. Execute o comando `ls -l /usr/bin/passwd`. Qual bit especial é definido e o que ele significa?

  ```bash
  # ls -l /usr/bin/passwd
  -rwsr-xr-x 1 root root 42096 mag 17  2015 /usr/bin/passwd
  ```

  O comando `passwd` tem o bit SUID definido (o quarto caractere desta linha), o que significa que o comando é executado com os privilégios do proprietário do arquivo (ou seja, o root). É assim que os usuários comuns podem mudar sua senha.

## 5.3 Gerenciando permissões e donos de arquivos

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 5.3
- **Peso**: 2

**Áreas chave de conhecimento**

- Permissões de arquivos/diretórios e seus donos

**Partial list of the used files, terms and utilities**

- `ls -l`, `ls -a`
- `chmod`, `chown`

### 5.3 Lição 1

#### Introdução

Por ser um sistema multiusuário, o Linux precisa de uma maneira de rastrear quem é o dono de cada arquivo e se um usuário pode ou não executar ações nesse arquivo. Isso serve para garantir a privacidade dos usuários que desejam manter em sigilo o conteúdo de seus arquivos, além de permitir trabalhar em colaboração, tornando certos arquivos acessíveis a diversos usuários.

Isso é feito por meio de um sistema de permissões em três níveis: cada arquivo no disco pertence a um usuário e a um grupo de usuários e conta com três conjuntos de permissões: uma para o proprietário, uma para o grupo que possui o arquivo e outra para todos os demais. Nesta lição, você aprenderá a consultar as permissões para um arquivo e a manipulá-las.

##### Como consultar informações sobre arquivos e diretórios

O comando `ls` é usado para obter uma lista do conteúdo de qualquer diretório. Nessa forma básica, aparecem somente os nomes de arquivos:

```bash
$ ls
```

```
Another_Directory  picture.jpg  text.txt
```

Mas há muito mais informações disponíveis sobre cada arquivo, incluindo tipo, tamanho, dono e muito mais. Para visualizar essas informações, você deve solicitar a `ls` uma lista de “forma longa”, usando o parâmetro `-l`:

```bash
$ ls -l
total 536
drwxrwxr-x 2 carol carol   4096 Dec 10 15:57 Another_Directory
-rw------- 1 carol carol 539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol   1881 Dec 10 15:57 text.txt
```

Cada coluna na saída acima tem um significado:

- A *primeira* coluna da lista mostra o tipo de arquivo e as permissões.

  Por exemplo, em `drwxrwxr-x`:

  - O primeiro caractere, `d`, indica o tipo de arquivo.
  - Os três caracteres seguintes, `rwx`, indicam as permissões do proprietário do arquivo, também designado como *user* ou `u`.
  - Os três caracteres seguintes, `rwx`, indicam as permissões do *grupo* que possui o arquivo, também chamado de `g`.
  - Os três últimos caracteres, `r-x`, indicam as permissões para todos os outros, também chamados de *others* ou `o`.
- A *segunda* coluna indica o número de links fisicos apontando para aquele arquivo. No caso de um diretório, isso significa o número de subdiretórios, além de um link para si mesmo (`.`) e o diretório pai (`..`).
- A *terceira* e *quarta* colunas mostram as informações de propriedade: respectivamente o usuário e o grupo que possuem o arquivo.
- A *quinta* coluna mostra o tamanho do arquivo em bytes.
- A *sexta* coluna mostra a data e a hora exatas, ou a *marca temporal*, de quando o arquivo foi modificado pela última vez.
- A *sétima* e última coluna mostra o nome do arquivo.

Se quiser ver os tamanhos de arquivo em formato “legível por humanos”, adicione o parâmetro `-h` a `ls`. O tamanho dos arquivos com menos de um quilobyte será mostrado em bytes. Nos arquivos com mais de um quilobyte e menos de um megabyte, um `K` é adicionado depois do número, indicando que o tamanho está em quilobytes. O mesmo vale para arquivos com tamanhos em megabytes (`M`) gigabytes (`G`):

```bash
$ ls -lh
total 1,2G
drwxrwxr-x 2 carol carol 4,0K Dec 10 17:59 Another_Directory
----r--r-- 1 carol carol    0 Dec 11 10:55 foo.bar
-rw-rw-r-- 1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
-rw------- 1 carol carol 528K Dec 10 10:43 picture.jpg
---xr-xr-x 1 carol carol   33 Dec 11 10:36 test.sh
-rwxr--r-- 1 carol carol 1,9K Dec 20 18:13 text.txt
-rw-rw-r-- 1 carol carol 2,6M Dec 11 22:14 Zipped.zip
```

Para exibir somente as informações de um conjunto específico de arquivos, adicione o nome desses arquivos a `ls`:

```bash
$ ls -lh HugeFile.zip test.sh
total 1,2G
-rw-rw-r-- 1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
---xr-xr-x 1 carol carol   33 Dec 11 10:36 test.sh
```

##### E os diretórios?

Se você tentar consultar informações sobre um diretório usando `ls -l`, ele exibirá uma lista do conteúdo do diretório:

```bash
$ ls -l Another_Directory/
total 0
-rw-r--r-- 1 carol carol 0 Dec 10 17:59 another_file.txt
```

Para evitar isso e consultar informações sobre o diretório em si, adicione o parâmetro `-d` a `ls`:

```bash
$ ls -l -d Another_Directory/
drwxrwxr-x 2 carol carol 4096 Dec 10 17:59 Another_Directory/
```

##### Exibindo arquivos ocultos

A lista de diretórios que obtivemos usando `ls -l` anteriormente está incompleta:

```bash
$ ls -l
total 544
drwxrwxr-x 2 carol carol   4096 Dec 10 17:59 Another_Directory
-rw------- 1 carol carol 539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol   1881 Dec 10 15:57 text.txt
```

Há outros três arquivos nesse diretório, mas eles estão ocultos. No Linux, os arquivos cujo nome começa com um ponto (`.`) são ocultados automaticamente. Para vê-los, precisamos adicionar o parâmetro `-a` ao `ls`:

```bash
$ ls -l -a
total 544
drwxrwxr-x 3 carol carol   4096 Dec 10 16:01 .
drwxrwxr-x 4 carol carol   4096 Dec 10 15:56 ..
drwxrwxr-x 2 carol carol   4096 Dec 10 17:59 Another_Directory
-rw------- 1 carol carol 539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol   1881 Dec 10 15:57 text.txt
-rw-r--r-- 1 carol carol      0 Dec 10 16:01 .thisIsHidden
```

O arquivo `.thisIsHidden` está oculto simplesmente porque seu nome começa com `.`.

Porém, os diretórios `.` e `..` são especiais. `.` é um ponteiro para o diretório atual, enquanto `..` é um ponteiro para o diretório pai (o diretório que contém o diretório atual). No Linux, todo diretório contém pelo menos esses dois diretórios especiais.

> [!tip]
> É possível combinar diversos parâmetros no `ls` (e em muitos outros comandos do Linux). `ls -l -a`, por exemplo, pode ser escrito como `ls -la`.

##### Compreendendo os tipos de arquivos

Já mencionamos que a primeira letra da saída de `ls -l` descreve o tipo de arquivo. Os três tipos de arquivo mais comuns são:

`-` **(arquivo normal)**

Um arquivo pode conter qualquer tipo de dado. os arquivos podem ser modificados, movidos, copiados e excluídos.

`d` **(diretório)**

Um diretório contém outros arquivos e diretórios e ajuda a organizar o sistema de arquivos. Tecnicamente, os diretórios são um tipo especial de arquivo. `l` **(link simbólico)**

Este “arquivo” é um apontador para outro arquivo ou diretório em outro local do sistema de arquivos.

Além desses, existem outros três tipos de arquivos que você deve pelo menos conhecer, mas que estão fora do escopo desta lição:

`b` **(dispositivo de bloco)**

Este arquivo representa um dispositivo virtual ou físico, como os discos ou outro tipo de dispositivo de armazenamento. Por exemplo, o primeiro disco rígido do sistema pode ser representado por `/dev/sda`.

`c` **(dispositivo de caracteres)**

Este arquivo representa um dispositivo virtual ou físico. Os terminais (como o terminal principal em `/dev/ttyS0`) e portas seriais são exemplos comuns de dispositivos de caracteres.

`s` **(socket)**

Os sockets são como “dutos” que transmitem informações entre dois programas.

> [!warning]
> Não altere nenhuma das permissões dos dispositivos de bloco, de caracteres ou sockets, a menos que saiba o que está fazendo. Isso pode fazer com que o sistema pare de funcionar!

##### Entendendo as permissões

Na saída de `ls -l`, as permissões de arquivo são mostradas logo após o tipo de arquivo, na forma de três grupos de três caracteres cada, na ordem `r`, `w` e `x`. Eis o significado deles. Lembre-se de que um hífen `-` representa a ausência de uma permissão determinada.

###### Permissões de arquivos

`r`

Representa *read* (leitura) e tem valor octal `4` (não se preocupe, falaremos de octais daqui a pouquinho). Significa a permissão de abrir um arquivo e ler seu conteúdo.

`w`

Representa *write* (escrita) e tem valor octal `2`. Significa a permissão de editar ou remover um arquivo. `x`

Representa *execute* (execução) e tem valor octal `1`. Significa que o arquivo pode ser rodado como executável ou script.

Então, por exemplo, um arquivo com permissões `rw-` pode ser lido e escrito, mas não pode ser executado.

###### Permissões em diretórios

`r`

Representa *read* (leitura) e tem valor octal `4`. Significa a permissão para ler o conteúdo do diretório, como os nomes de arquivos. Mas não implica na permissão para ler os arquivos em si.

`w`

Representa *write* (escrita) e tem valor octal `2`. Significa a permissão de editar ou remover um arquivo em um diretório, além de alterar seu nome.

`x`

Representa *execute* (execução) e tem valor octal `1`. Significa a permissão de entrar em um diretório, mas não de listar seus arquivos (para isso, é necessária a permissão `r`).

A última parte sobre os diretórios é um pouco confusa. Vamos imaginar, por exemplo, que temos um diretório chamado `Another_Directory`, com as seguintes permissões:

```bash
$ ls -ld Another_Directory/
d--xr-xr-x 2 carol carol 4,0K Dec 20 18:46 Another_Directory
```

Imagine também que dentro desse diretório tem um script do shell chamado `hello.sh` com as seguintes permissões:

```
-rwxr-xr-x 1 carol carol 33 Dec 20 18:46 hello.sh
```

Se você for a usuária `carol` e tentar listar o conteúdo de `Another_Directory`, aparecerá uma mensagem de erro, pois seu usuário não tem permissão de leitura para aquele diretório:

```bash
$ ls -l Another_Directory/
ls: cannot open directory 'Another_Directory/': Permission denied
```

Todavia, a usuária `carol` *tem* permissões de execução, o que significa que ela pode entrar no diretório. Assim, a usuária `carol` pode acessar arquivos dentro do diretório, desde que tenha as permissões corretas *para o arquivo respectivo*. Neste exemplo, a usuária tem permissões totais para o script `hello.sh`, então ela *pode* executar o script, embora *não possa* ler o conteúdo do diretório que o contém. Basta dispor do nome de arquivo completo.

```bash
$ sh Another_Directory/hello.sh
Hello LPI World!
```

Como dissemos anteriormente, as permissões são especificadas em sequência: primeiro para o proprietário do arquivo, depois para o grupo proprietário e por fim para outros usuários. Sempre que alguém tenta executar uma ação no arquivo, as permissões são verificadas da mesma maneira. Primeiro, o sistema verifica se o usuário atual possui o arquivo e, se for o caso, aplica apenas o primeiro conjunto de permissões. Caso contrário, ele verifica se o usuário atual pertence ao grupo que possui o arquivo. Nesse caso, ele aplica apenas o segundo conjunto de permissões. Em qualquer outro caso, o sistema aplicará o terceiro conjunto de permissões. Isso significa que, se o usuário atual for o proprietário do arquivo, apenas as permissões do proprietário serão efetivas, mesmo que as permissões do grupo ou outras permissões sejam mais permissivas do que as permissões do proprietário.

##### Modificando as permissões de arquivo

O comando `chmod` é usado para modificar as permissões de um arquivo e emprega pelo menos dois parâmetros: o primeiro descreve quais permissões devem ser alteradas e o segundo aponta para o arquivo ou diretório em que a alteração será feita. No entanto, as permissões para alterações podem ser descritas de duas maneiras, ou “modos”, diferentes.

O primeiro, chamado *modo simbólico*, oferece um controle refinado, permitindo adicionar ou revogar uma única permissão sem modificar as de outras pessoas no conjunto de permissões. O outro modo, chamado *modo numérico*, é mais fácil de lembrar e mais rápido de usar quando queremos definir todos os valores de permissão de uma só vez.

Ambos os modos permitem o mesmo resultado final. Então, por exemplo, os comandos:

```bash
$ chmod ug+rw-x,o-rwx text.txt
```

e

```bash
$ chmod 660 text.txt
```

produzirão exatamente a mesma saída, um arquivo com as permissões definidas:

```
-rw-rw---- 1 carol carol  765 Dec 20 21:25 text.txt
```

Agora, vamos entender como cada modo funciona.

##### Modo simbólico

Ao descrever quais permissões devem ser alteradas no *modo simbólico*, o(s) primeiro(s) caractere(s) indicam as permissões que serão alteradas: permissões do usuário (`u`), do grupo (`g`), outras (`o`) e/ou as três juntas (`a`).

Em seguida, você precisa dizer ao comando o que fazer: você pode conceder uma permissão (`+`), revogar uma permissão (`-`) ou configurá-la para um valor específico (`=`).

Por fim, você especifica qual permissão deseja afetar: leitura (`r`), escrita (`w`) ou execução (`x`).

Por exemplo, imagine que temos um arquivo chamado `text.txt` com a seguinte permissão definida:

```bash
$ ls -l text.txt
-rw-r--r-- 1 carol carol 765 Dec 20 21:25 text.txt
```

Se quisermos conceder permissões de escrita aos membros do grupo proprietário arquivo, usamos o parâmetro `g+w`. Fica mais fácil entender assim: “Para o grupo (`g`), conceda (`+`) permissões de escrita (`w`)”. Assim, o comando ficaria:

```bash
$ chmod g+w text.txt
```

Vamos conferir o resultado com `ls`:

```bash
$ ls -l text.txt
-rw-rw-r-- 1 carol carol 765 Dec 20 21:25 text.txt
```

Se quisermos remover as permissões de leitura para o proprietário do mesmo arquivo, podemos raciocinar assim: “Para o usuário (`u`), revogue (`-`) as permissões de leitura (`r`)”. Assim, o parâmetro seria `u-r`, desta maneira:

```bash
$ chmod u-r text.txt
$ ls -l text.txt
--w-rw-r-- 1 carol carol 765 Dec 20 21:25 text.txt
```

E se quisermos definir as permissões exatamente como `rw-` para todos? Se for o caso, pensamos desta maneira: “Para todos (`a`), defina exatamente (`=`) leitura (`r`), escrita (`w`), mas não execução (`-` )”. Assim:

```bash
$ chmod a=rw- text.txt
$ ls -l text.txt
-rw-rw-rw- 1 carol carol 765 Dec 20 21:25 text.txt
```

Obviamente, é possível modificar várias permissões ao mesmo tempo. Nesse caso, nós as separamos com vírgula (`,`):

```bash
$ chmod u+rwx,g-x text.txt
$ ls -lh text.txt
-rwxrw-rw- 1 carol carol 765 Dec 20 21:25 text.txt
```

O exemplo acima pode ser lido como: “Para o usuário (`u`), conceda (`+`) permissões de leitura, escrita e execução (`rwx`), para o grupo (`g`) revogue (`-`) permissões de execução (`x`)”.

Quando executado em um diretório, `chmod` modifica apenas as permissões do diretório. `chmod` tem um modo recursivo, útil quando desejamos alterar as permissões para “todos os arquivos dentro de um diretório e seus subdiretórios”. Para usá-lo, adicione o parâmetro `-R` após o nome do comando e antes das permissões a alterar, da seguinte maneira:

```bash
$ chmod -R u+rwx Another_Directory/
```

Esse comando pode ser lido como: “Recursivamente (`-R`), para o usuário (`u`), conceda (`+`) permissões de leitura, escrita e execução (`rwx`)”.

> [!warning]
> Tenha cautela e pense duas vezes antes de usar a opção `-R`, pois é fácil até demais alterar as permissões de arquivos e diretórios que não desejaríamos alterar, especialmente em diretórios com um grande número de arquivos e subdiretórios.

##### Modo numérico

No *modo numérico*, as permissões são especificadas de maneira diferente: como um valor numérico de três dígitos na notação octal, um sistema numérico de base 8.

Cada permissão tem um valor correspondente e elas são especificadas na seguinte ordem: primeiro vem leitura (`r`), que é `4`, depois escrita (`w`), que é `2`, e por fim a execução (`x`), representada por `1`. Se não houver permissão, use o valor zero (`0`). Portanto, uma permissão de `rwx` seria `7` (`4+2+1`) e `r-x` seria `5` (`4+0+1`).

O primeiro dos três dígitos no conjunto de permissões representa as permissões do usuário (`u`), o segundo as do grupo (`g`) e o terceiro as do proprietário (`o`). Se desejássemos definir as permissões de um arquivo como `rw-rw----`, o valor octal seria `660`:

```bash
$ chmod 660 text.txt
$ ls -l text.txt
-rw-rw---- 1 carol carol 765 Dec 20 21:25 text.txt
```

Além disso, a sintaxe no *modo numérico* é a mesma do *modo simbólico*: o primeiro parâmetro representa as permissões que desejamos alterar e o segundo aponta para o arquivo ou diretório em que a alteração será feita.

> [!tip]
> Se o valor de uma permissão for *ímpar*, é certeza que o arquivo é executável!

Qual sintaxe usar? O *modo numérico* é recomendado quando queremos alterar as permissões para um valor específico, por exemplo `640` (`rw- r-- ---`).

O *modo simbólico* é mais útil para alterar apenas um valor específico, quaisquer que sejam as permissões atuais do arquivo. Por exemplo, posso adicionar permissões de execução para o usuário somplesmente com `chmod u+x script.sh` sem me preocupar e nem sequer tocar nas permissões atuais do grupo e outras.

##### Modificando o proprietário de um arquivo

O comando `chown` é usado para modificar o proprietário de um arquivo ou diretório. A sintaxe é bastante simples:

```
chown username:groupname filename
```

Por exemplo, vamos verificar um arquivo chamado `text.txt`:

```bash
$ ls -l text.txt
-rw-rw---- 1 carol carol 1881 Dec 10 15:57 text.txt
```

O usuário que possui o arquivo é `carol` e o grupo também é `carol`. Agora, vamos modificar o grupo proprietário do arquivo para outro grupo, como `students`:

```bash
$ chown carol:students text.txt
$ ls -l text.txt
-rw-rw---- 1 carol students 1881 Dec 10 15:57 text.txt
```

Lembre-se de que o usuário que possui um arquivo não precisa pertencer ao grupo que o possui. No exemplo acima, a usuária `carol` não precisa ser membro do grupo `Students`. No entanto, ela precisa ser membro do grupo para poder transferir a propriedade do arquivo para ele.

O usuário ou o grupo podem ser omitidos se você não quiser alterá-los. Assim, para alterar apenas o grupo que possui um arquivo, usaríamos `chown :students text.txt`. Para mudar apenas o usuário, o comando seria `chown carol text.txt`. Como alternativa, você pode usar o comando `chgrp students text.txt` para alterar apenas o grupo.

A menos que você seja o administrador do sistema (root), não poderá alterar a propriedade de um arquivo pertencente a outro usuário ou grupo ao qual você não pertença. Se tentar fazer isso, receberá a mensagem de erro `Operation not permitted` (Operação não permitida).

##### Consultando os grupos

Antes de alterar a propriedade de um arquivo, pode ser útil saber quais grupos existem no sistema, quais usuários são membros de um grupo e a quais grupos um usuário pertence. Essas tarefas podem ser realizadas com dois comandos, `groups` e `groupmems`.

Para ver quais grupos existem no seu sistema, basta digitar `groups`:

```bash
$ groups
carol students cdrom sudo dip plugdev lpadmin sambashare
```

E para saber a quais grupos um usuário pertence, adicione o nome de usuário como parâmetro:

```bash
$ groups carol
carol : carol students cdrom sudo dip plugdev lpadmin sambashare
```

Para fazer o inverso, exibindo quais usuários pertencem a um grupo, use `groupmems`. O parâmetro `-g` especifica o grupo e `-l` lista todos os seus membros:

```bash
$ sudo groupmems -g cdrom -l
carol
```

> [!tip]
> `groupmems` só pode ser executado como root, o administrador do sistema. Se você não estiver atualmente logado como root, adicione `sudo` antes do comando.

##### Permissões especiais

Além das permissões de leitura, escrita e execução para usuários, grupos e outros, cada arquivo pode ter três outras *permissões especiais* capazes de alterar a maneira como um diretório funciona ou como um programa é executado. Elas podem ser especificadas em modo simbólico ou numérico e são as seguintes:

###### Sticky Bit

O sticky bit, também chamado de *Restricted Deletion Flag*, tem o valor octal `1` e, no modo simbólico, é representado por um `t` dentro das permissões de outros. Aplica-se apenas aos diretórios e, no Linux, evita que os usuários removam ou renomeiem um arquivo em um diretório, a menos que sejam proprietários desse arquivo ou diretório.

Os diretórios com o sticky bit definido trazem um `t` no lugar do `x` nas permissões de *outros* na saída de `ls -l`:

```bash
$ ls -ld Sample_Directory/
drwxr-xr-t 2 carol carol 4096 Dec 20 18:46 Sample_Directory/
```

No modo numérico, as permissões especiais são especificadas usando uma “notação de 4 dígitos”, sendo o primeiro dígito a permissão especial para agir. Por exemplo, para definir o sticky bit (valor `1`) para o diretório `Another_Directory` no modo numérico, com permissões `755`, o comando seria:

```bash
$ chmod 1755 Another_Directory
$ ls -ld Another_Directory
drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 Another_Directory
```

###### Set GID

O Set GID, também conhecido como SGID ou bit Set Group ID, tem o valor octal `2` e, no modo simbólico, é representado por um `s` nas permissões de *grupo*. Pode ser aplicado a arquivos ou diretórios executáveis. Nos arquivos executáveis, ele concede acesso aos privilégios do grupo que possui o arquivo ao processo resultante da execução do arquivo. Quando aplicado a diretórios, ele faz com que todos os arquivos ou diretórios criados com ele herdem o grupo do diretório pai.

Os arquivos e diretórios com o bit SGID trazem um `s` no lugar do `x` nas permissões de *grupo* na saída do `ls -l`:

```bash
$ ls -l test.sh
-rwxr-sr-x 1 carol carol 33 Dec 11 10:36 test.sh
```

Para adicionar permissões SGID a um arquivo no modo simbólico, o comando seria:

```bash
$ chmod g+s test.sh
$ ls -l test.sh
-rwxr-sr-x 1 carol root     33 Dec 11 10:36 test.sh
```

O exemplo a seguir ajudará a entender melhor os efeitos do SGID em um diretório. Suponha que tenhamos um diretório chamado `Sample_Directory`, pertencente ao usuário `carol` e ao grupo `users`, com a seguinte estrutura de permissões:

```bash
$ ls -ldh Sample_Directory/
drwxr-xr-x 2 carol users 4,0K Jan 18 17:06 Sample_Directory/
```

Agora, vamos mudar para este diretório e, usando o comando `touch`, criar um arquivo vazio dentro dele. O resultado seria:

```bash
$ cd Sample_Directory/
$ touch newfile
$ ls -lh newfile
-rw-r--r-- 1 carol carol 0 Jan 18 17:11 newfile
```

Como vemos, o arquivo pertence ao usuário `carol` e ao grupo `carol`. Mas, se o diretório tivesse a permissão SGID definida, o resultado seria diferente. Primeiro, vamos adicionar o bit SGID ao `Sample_Directory` e verificar os resultados:

```bash
$ sudo chmod g+s Sample_Directory/
$ ls -ldh Sample_Directory/
drwxr-sr-x 2 carol users 4,0K Jan 18 17:17 Sample_Directory/
```

O `s` nas permissões do grupo indica que o bit SGID está definido. Agora, vamos mudar para este diretório e, novamente, criar um arquivo vazio com o comando `touch`:

```bash
$ cd Sample_Directory/
$ touch emptyfile
$ ls -lh emptyfile
-rw-r--r-- 1 carol users 0 Jan 18 17:20 emptyfile
```

Como vemos, o grupo que possui o arquivo é `users`. Isso ocorre porque o bit SGID fez o arquivo herdar o grupo proprietário do diretório pai, que é `users`.

###### Set UID

SUID, também conhecido como Set User ID, tem valor octal `4` e é representado por um `s` nas permissões de *usuário* no modo simbólico. Aplica-se apenas aos arquivos e seu comportamento é semelhante ao do bit SGID, mas o processo será executado com os privilégios do *usuário* proprietário do arquivo. Os arquivos com o bit SUID mostram um `s` no lugar do `x` nas permissões do usuário, na saída de `ls -l`:

```bash
$ ls -ld test.sh
-rwsr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
```

Podemos combinar diversas permissões especiais em um parâmetro somando-as. Assim, para definir o SGID (valor `2`) e o SUID (valor `4`) no modo numérico para o script `test.sh` com permissões `755`, digite:

```bash
$ chmod 6755 test.sh
```

E o resultado seria:

```bash
$ ls -lh test.sh
-rwsr-sr-x 1 carol carol 66 Jan 18 17:29 test.sh
```

> [!tip]
> Se o seu terminal exibe cores, como é o caso da maioria atualmente, é fácil ver se

essas permissões especiais estão definidas olhando a saída de `ls -l`. Para o sticky bit, o nome do diretório pode ser mostrado em uma fonte preta com fundo azul. O mesmo se aplica aos arquivos com os bits SGID (fundo amarelo) e SUID (fundo vermelho). As cores podem ser diferentes dependendo da distribuição do Linux e das configurações do terminal que você usa.

#### Exercícios Guiados

1. Crie um diretório chamado `emptydir` usando o comando `mkdir emptydir`. Em seguida, usando `ls`, liste as permissões do diretório `emptydir`.

2. Crie um arquivo vazio chamado `emptyfile` com o comando `touch emptyfile`. Em seguida, usando `chmod` com notação simbólica, adicione permissões de execução ao proprietário do arquivo `emptyfile` e remova as permissões de gravação e execução para todos os outros. Faça isso usando apenas um comando `chmod`.

3. Quais serão as permissões de um arquivo chamado `text.txt` depois de você executar o comando `chmod 754 text.txt`?

4. Vamos supor que um arquivo chamado `test.sh` seja um script do shell com as seguintes permissões e propriedade:

  ```
  -rwxr-sr-x 1 carol root     33 Dec 11 10:36 test.sh
  ```

  - Quais são as permissões do proprietário do arquivo?
  - Se o usuário `john` executar esse script, sob quais privilégios de usuário ele será executado?
  - Usando a notação numérica, qual deve ser a sintaxe do chmod para “desfazer” a permissão especial concedida a este arquivo?

5. Considere este arquivo:

  ```bash
  $ ls -l /dev/sdb1
  brw-rw---- 1 root disk 8, 17 Dec 21 18:51 /dev/sdb1
  ```

  Que tipo de arquivo é `sdb1`? E quem pode escrever nele?

6. Considere os 4 arquivos a seguir:

  ```
  drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 Another_Directory
  ----r--r-- 1 carol carol    0 Dec 11 10:55 foo.bar
  -rw-rw-r-- 1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
  drwxr-sr-x 2 carol users 4,0K Jan 18 17:26 Sample_Directory
  ```

  Escreva as permissões correspondentes a cada arquivo e diretório usando a notação numérica de 4 dígitos.

  `Another_Directory`

  `foo.bar`

  `HugeFile.zip`

  `Sample_Directory`

#### Exercícios Exploratórios

1. Experimente o seguinte em um terminal: crie um arquivo vazio chamado `emptyfile` com o comando `touch emptyfile`. Agora “zere” as permissões do arquivo com `chmod 000` `emptyfile`. O que acontecerá se você mudar as permissões de `emptyfile` passando apenas *um* valor de `chmod` para o modo numérico, como `chmod 4 emptyfile`? E se usarmos dois, como `chmod 44 emptyfile`? O que aprendemos sobre a maneira como `chmod` interpreta o valor numérico?

2. É possível executar um arquivo para o qual você tem permissões de execução, mas não de leitura (`--x`)? Por que ou porque não?

3. Considere as permissões do diretório temporário em um sistema Linux, `/tmp`:

  ```bash
  $ ls -ld /tmp
  drwxrwxrwt  19 root root  16K Dec 21 18:58 tmp
  ```

  Usuário, grupo e outros têm permissões totais. Mas um usuário regular pode excluir *qualquer* arquivo dentro deste diretório? Por quê?

4. Um arquivo chamado `test.sh` tem as seguintes permissões: `-rwsr-xr-x`, o que indica que o bit SUID foi definido. Agora, execute os seguintes comandos:

  ```bash
  $ chmod u-x test.sh
  $ ls -l test.sh
  -rwSr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
  ```

  O que nós fizemos? O que significa o `S` maiúsculo?

5. Como criar um diretório chamado `Box` no qual todos os arquivos pertençam automaticamente ao grupo `users` e só possam ser removidos pelo usuário que os criou?

#### Resumo

Por ser um sistema multiusuário, o Linux precisa de uma maneira de rastrear quem possui e quem pode acessar cada arquivo. Isso é feito por meio de um sistema de permissões em três níveis. Nesta lição, aprendemos como esse sistema funciona.

Nesta lição, você aprendeu como usar `ls` para obter informações sobre as permissões de arquivos, como controlar ou alterar quem pode criar, excluir ou modificar um arquivo com `chmod` nas notações *numérica* e *simbólica* e como alterar a propriedade de arquivos com `chown` e `chgrp`.

Os seguintes comandos foram discutidos nesta lição:

`ls`

Lista os arquivos, incluindo opcionalmente detalhes como permissões.

`chmod`

Altera as permissões de um arquivo ou diretório..

`chown`

Altera o usuário e/ou o grupo proprietário de um arquivo ou diretório.

`chgrp`

Altera o grupo proprietário de um arquivo ou diretório.

#### Respostas aos Exercícios Guiados

1. Crie um diretório chamado `emptydir` usando o comando `mkdir emptydir`. Em seguida, usando `ls`, liste as permissões do diretório `emptydir`.

  Adicionamos o parâmetro `-d` a `ls` para ver os atributos de arquivo de um diretório, em vez de listar seu conteúdo. Assim, a resposta é:

  ```
  ls -l -d emptydir
  ```

  Você ganha pontos extras se tiver juntado os dois parâmetros em um só, como em `ls -ld` `emptydir`.

2. Crie um arquivo vazio chamado `emptyfile` com o comando `touch emptyfile`. Em seguida, usando `chmod` com notação simbólica, adicione permissões de execução ao proprietário do arquivo `emptyfile` e remova as permissões de gravação e execução para todos os outros. Faça isso usando apenas um comando `chmod`.

  Pense desta maneira:

  - “Para o usuário que possui o arquivo (`u`) adicione (`+`) permissões de execução (`x`)”, portanto `u+x`.
  - “Para o grupo (`g`) e outros usuários (`o`), remova (`-`) permissões de escrita (`w`) e execução (`x`)”, portanto `go-wx`.

  Para combinar esses dois conjuntos de permissões, adicionamos uma virgula entre eles. Assim, o resultado final será:

  ```
  chmod u+x,go-wx emptyfile
  ```

3. Quais serão as permissões de um arquivo chamado `text.txt` depois de você executar o comando `chmod 754 text.txt`?

  Lembre-se de que em notação numérica cada dígito representa um conjunto de três permissões, cada uma com um valor respectivo: *leitura* é `4`, *escrita* é `2`, *execução* é `1` e a ausência de permissões é `0`. Obtemos o valor de um dígito somando os valores correspondentes de cada permissão. `7` é `4+2+1`, ou `rwx`, `5` é `4+0+1`, ou `r-x`, e `4` é somente leitura, ou `r--`. As permissões de `text.txt` seriam

  ```
  rwxr-xr--
  ```

4. Vamos supor que um arquivo chamado `test.sh` seja um script do shell com as seguintes permissões e propriedade:

  ```
  -rwxr-sr-x 1 carol root     33 Dec 11 10:36 test.sh
  ```

  - Quais são as permissões do proprietário do arquivo?

  As permissões do proprietário (2º ao 4 caracteres na saída de `ls -l`) são `rwx`, por isso a resposta é: “ler, escrever e executar o arquivo”.

  - Se o usuário `john` executar esse script, sob quais privilégios de usuário ele será executado?

  Preste atenção às permissões do *grupo*. Elas são `r-s`, o que significa que o bit SGID está definido. O grupo proprietário do arquivo é `root`, de modo que o script, mesmo quando iniciado por um usuário regular, será executado com privilégios de root.

  - Usando a notação numérica, qual deve ser a sintaxe do chmod para “desfazer” a permissão especial concedida a este arquivo?

  Podemos “desfazer” as permissões especiais passando um 4º dígito, `0`, para `chmod`. As permissões atuais são `755`, então o comando deve ser `chmod 0755`.

5. Considere este arquivo:

  ```bash
  $ ls -l /dev/sdb1
  brw-rw---- 1 root disk 8, 17 Dec 21 18:51 /dev/sdb1
  ```

  Que tipo de arquivo é `sdb1`? E quem pode escrever nele?

  O primeiro caractere da saída de `ls -l` mostra o tipo de arquivo. `b` é um *dispositivo de bloco*, normalmente um disco (interno ou externo), conectado à máquina. O proprietário (`root`) e todos os usuários do grupo `disk` podem escrever nele.

6. Considere os 4 arquivos a seguir:

  ```
  drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 Another_Directory
  ----r--r-- 1 carol carol    0 Dec 11 10:55 foo.bar
  -rw-rw-r-- 1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
  ```

  ```
  drwxr-sr-x 2 carol users 4,0K Jan 18 17:26 Sample_Directory
  ```

  Escreva as permissões correspondentes a cada arquivo e diretório usando a notação numérica de 4 dígitos.

  As permissões correspondentes, em notação numérica, são as seguintes:

  `Another_Directory`

  Resposta: `1755`

  `1` para o sticky bit, `755` para as permissões regulares (`rwx` para o usuário, `r-x` para grupo e outros).

  `foo.bar`

  Resposta: `0044`

  Sem permissões especiais (de modo que o primeiro dígito é `0`), sem permissões para o usuário (`---`) e somente leitura (`r--r--`) para grupo e outros.

  `HugeFile.zip`

  Resposta: `0664` +Sem permissões especiais, de modo que o primeiro dígito é `0`. `6` (`rw-`) para usuário e grupo, `4` (`r--`) para outros.

  `Sample_Directory`

  Resposta: `2755`

  `2` para o bit SGID, `7` (`rwx`) para o usuário, `5` (`r-x`) para o grupo e outros.

#### Respostas aos Exercícios Exploratórios

1. Experimente o seguinte em um terminal: crie um arquivo vazio chamado `emptyfile` com o comando `touch emptyfile`. Agora “zere” as permissões do arquivo com `chmod 000` `emptyfile`. O que acontecerá se você mudar as permissões de `emptyfile` passando apenas *um* valor de `chmod` para o modo numérico, como `chmod 4 emptyfile`? E se usarmos dois, como `chmod 44 emptyfile`? O que aprendemos sobre a maneira como `chmod` interpreta o valor numérico?

  Lembre-se de que “zeramos” as permissões de `emptyfile`. Assim, seu estado inicial seria:

  ```
  ---------- 1 carol carol    0 Dec 11 10:55 emptyfile
  ```

  Agora, vamos tentar o primeiro comando, `chmod 4 emptyfile`:

  ```bash
  $ chmod 4 emptyfile
  $ ls -l emptyfile
  -------r-- 1 carol carol 0 Dec 11 10:55 emptyfile
  ```

  As permissões de *outros* foram alteradas. E se usássemos dois dígitos, como em `chmod 44` `emptyfile`?

  ```bash
  $ chmod 44 emptyfile
  $ ls -l emptyfile
  ----r--r-- 1 carol carol 0 Dec 11 10:55 emptyfile
  ```

  Agora, as permissões de *grupo* e *outros* foram afetadas. A partir daí, podemos concluir que em notação numérica, `chmod` lê o valor “de trás pra frente”, do dígito menos significativo (*others*) para o mais significativo (*usuário*). Se você passar um só dígito, as permissões de *outros* são modificadas. Com dois dígitos modificamos *grupo* e *outros*, com três modificamos *usuário*, *grupo* e *outros* e com quatro modificamos *usuário*, *grupo*, *outros* e as permissões especiais.

2. É possível executar um arquivo para o qual você tem permissões de execução, mas não de leitura (`--x`)? Por que ou porque não?

  No início, a resposta parece óbvia: se você tem permissão de execução, o arquivo deveria poder ser executado. Isso se aplica aos programas em formato binário que são executados diretamente pelo kernel. No entanto, existem programas (por exemplo, scripts do shell) que devem antes ser lidos e interpretados. Nesses casos, a permissão de leitura (`r`) também deve ser configurada.

3. Considere as permissões do diretório temporário em um sistema Linux, `/tmp`:

  ```bash
  $ ls -ld /tmp
  drwxrwxrwt  19 root root  16K Dec 21 18:58 tmp
  ```

  Usuário, grupo e outros têm permissões totais. Mas um usuário regular pode excluir *qualquer* arquivo dentro deste diretório? Por quê?

  `/tmp` é o que chamamos um diretório *escrito por todos*, ou seja, qualquer usuário pode escrever nele. Mas não queremos que um usuário modifique arquivos criados por outros, por isso o *sticky bit* foi definido (como indicado pelo `t` nas permissões de *outros*). Graças a isso, um usuário pode excluir arquivos em `/tmp`, mas somente se tiver criado esses arquivos.

4. . Um arquivo chamado `test.sh` tem as seguintes permissões: `-rwsr-xr-x`, o que indica que o bit SUID foi definido. Agora, execute os seguintes comandos:

  ```bash
  $ chmod u-x test.sh
  $ ls -l test.sh
  -rwSr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
  ```

  O que nós fizemos? O que significa o `S` maiúsculo?

  Removemos as permissões de execução do usuário dono do arquivo. O `s` (ou `t`) toma o lugar do `x` na saída de `ls -l`, por isso o sistema precisa de uma maneira de mostrar se o usuário tem permissões de execução ou não. Para isso, ele muda a caixa do caractere especial.

  Um `s` minúsculo no primeiro grupo de permissões indica que o usuário dono do arquivo tem permissões de execução e que o bit SUID foi definido. Um `S` maiúsculo indica que o usuário dono do arquivo não tem (`-`) permissões de execução e que o bit SUID foi definido.

  Pode-se dizer o mesmo do SGID. Um `s` minúsculo no segundo grupo de permissões indica que o grupo dono do arquivo tem permissões de execução e que o bit SUID foi definido. Um `S` maiúsculo indica que o grupo dono do arquivo não tem (`-`) permissões de execução e que o bit SUID foi definido.

  Isso também vale para o sticky bit, representado pelo `t` No terceiro grupo de permissões. O `t` minúsculo indica que o sticky bit foi definido e que os outros têm permissões de execução. O `T` maiúsculo indica que o sticky bit foi definido e que os outros não têm permissões de execução.

5. Como criar um diretório chamado `Box` no qual todos os arquivos pertençam automaticamente ao grupo `users` e só possam ser removidos pelo usuário que os criou?

  Este seria um processo de vários passos. O primeiro é criar o diretório:

  ```bash
  $ mkdir Box
  ```

  Queremos que cada arquivo criado dentro deste diretório seja atribuído automaticamente ao grupo `users`. Para isso, configuramos esse grupo como proprietário do diretório, depois definimos nele o bit SGID. Também precisamos garantir que qualquer membro do grupo possa escrever nesse diretório.

  Como não precisamos nos importar com as outras permissões e queremos apenas “ligar” os bits especiais, faz sentido usar o modo simbólico:

  ```bash
  $ chown :users Box/
  $ chmod g+wxs Box/
  ```

  Note que se seu usuário atual não pertencer ao grupo `users`, será necessário usar o comando `sudo` antes dos comandos acima para fazer a alteração como root.

  Para terminar, vamos garantir que somente o usuário criador de um arquivo tem a permissão de excluí-lo. Para isso, definimos o sticky bit (representado por um `t`) no diretório. Lembre-se de que ele é configurado nas permissões de outros (`o`).

  ```bash
  $ chmod o+t Box/
  ```

  As permissões do diretório `Box` devem aparecer da seguinte maneira:

  ```
  drwxrwsr-t 2 carol users  4,0K Jan 18 19:09 Box
  ```

  Claro que também é possível especificar o bit SGID e o sticky bit usando somente um comando `chmod`:

  ```bash
  $ chmod g+wxs,o+t Box/
  ```

  Se você pensou nisso, parabéns!

## 5.4 Diretórios e arquivos especiais

- **Referência ao LPI objectivo**: Linux Essentials v1.6, Exam 010, Objective 5.4
- **Peso**: 1

**Áreas chave de conhecimento**

- Usando arquivos e diretórios temporários
- Links simbólicos

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `/tmp/`, `/var/tmp/` and Sticky Bit
- `ls -d`
- `ln -s`

### 5.4 Lição 1

#### Introdução

No Linux, tudo é tratado como um arquivo. No entanto, alguns arquivos recebem um tratamento especial, seja devido ao local em que estão armazenados, como os arquivos temporários, ou à maneira como interagem com o sistema de arquivos, como os links. Nesta lição, aprenderemos onde esses arquivos estão localizados, como funcionam e como gerenciá-los.

##### Arquivos temporários

Os arquivos temporários são arquivos usados pelos programas para armazenar dados que serão necessários apenas por um curto período de tempo — por exemplo, dados de processos em execução, logs de falhas, arquivos de rascunho de um salvamento automático, arquivos intermediários usados durante uma conversão, arquivos de cache e assim por diante.

###### Localização dos arquivos temporários

A versão 3.0 do *Filesystem Hierarchy Standard* (FHS) define locais padrão para os arquivos temporários nos sistemas Linux. Cada local tem uma finalidade e um comportamento diferentes, e é recomendável que os desenvolvedores sigam as convenções definidas pelo FHS ao gravar dados temporários no disco.

`/tmp`

De acordo com o FHS, não se deve pressupor que os arquivos escritos aqui serão preservados entre as invocações de um programa. A *recomendação* é que esse diretório seja limpo (todos os arquivos apagados) durante a inicialização do sistema, embora isso *não seja obrigatório*.

`/var/tmp`

Outro local para arquivos temporários, mas este *não deve ser limpo* durante a inicialização do sistema, ou seja, os arquivos armazenados aqui geralmente persistem entre as reinicializações.

`/run`

Este diretório contém arquivos variáveis de tempo de execução usados pelos processos ativos, como os arquivos identificadores de processo (`.pid`). Os programas que precisam de mais de um arquivo de tempo de execução podem criar subdiretórios aqui. Este local *deve ser limpo* durante a inicialização do sistema. Antigamente essa finalidade pertencia a `/var/run` e, em alguns sistemas, `/var/run` pode ser um link simbólico para `/run`.

Observe que nada impede o programa de criar arquivos temporários em outro local do sistema, mas é recomendável respeitar as convenções definidas pelo FHS.

###### Permissões em arquivos temporários

A existência de diretórios temporários que contemplam todo o sistema em um sistema multiusuário apresenta alguns desafios em relação às permissões de acesso. A princípio, poderíamos pensar que esses diretórios seriam “graváveis por todos”, ou seja, qualquer usuário poderia escrever ou excluir dados dele. Mas se assim fosse, como impedir que um usuário apagasse ou modificasse arquivos criados por outro?

A solução é uma permissão especial chamada *sticky bit*, que se aplica a diretórios e arquivos. Porém, por razões de segurança, o kernel do Linux ignora o sticky bit quando ele é aplicado a arquivos. Quando esse bit especial é definido para um diretório, ele impede que os usuários removam ou renomeiem um arquivo nesse diretório, a menos que sejam proprietários do arquivo.

Os diretórios com o sticky bit definido mostram um `t` no lugar do `x` nas permissões de *outros* na saída de `ls -l`. Por exemplo, vamos verificar as permissões dos diretórios `/tmp` e `/var/tmp`:

```bash
$ ls -ldh /tmp/ /var/tmp/
drwxrwxrwt 25 root root 4,0K Jun  7 18:52 /tmp/
```

```
drwxrwxrwt 16 root root 4,0K Jun  7 09:15 /var/tmp/
```

Como você pode ver pelo `t` no lugar do `x` na permissão para *outros*, os dois diretórios estão com o sticky bit definido.

Para definir o sticky bit em um diretório usando `chmod` no modo numérico, use a notação de quatro dígitos, sendo `1` o primeiro dígito. Por exemplo:

```bash
$ chmod 1755 temp
```

define o sticky bit para o diretório chamado `temp` e suas permissões como `rwxr-xr-t`.

Ao usar o modo simbólico, empregue o parâmetro `t`. Assim, `+t` para definir o sticky bit e `-t` para desativá-lo. Desta maneira:

```bash
$ chmod +t temp
```

##### Compreendendo os links

Já dissemos que, no Linux, tudo é tratado como um arquivo. Mas existe um tipo *especial* de arquivo chamado *link*. Há dois tipos de links em um sistema Linux:

- **Links simbólicos**: Também chamados de *soft links*, eles apontam para o caminho de outro arquivo. Se excluirmos o arquivo para o qual o link aponta (chamado *destino*), o link ainda existirá, mas “para de funcionar”, pois passará a apontar para “nada”.
- **Links físicos**: Um link físico é como como um segundo nome para o arquivo original. Eles *não* são duplicatas, mas sim uma entrada adicional no sistema de arquivos que aponta para o mesmo local (inode) no disco.

> [!tip]
> Um *inode* é uma estrutura de dados que armazena os atributos de um objeto (como um arquivo ou diretório) em um sistema de arquivos. Dentre esses atributos estão o nome de arquivo, permissões, proprietário e os blocos do disco nos quais estão armazenados os dados referentes àquele objeto. São semelhantes a um verbete em um índice; por isso o nome, que vem de “index node”.

###### Trabalhando com links físicos

**Criando links físicos**

O comando para criar um link físico no Linux é `ln`. A sintaxe básica é:

```bash
$ ln TARGET LINK_NAME
```

O `TARGET` já deve existir (trata-se do arquivo para o qual o link apontará) e, se o destino não estiver no diretório atual ou se você deseja criar o link em outro lugar, é *obrigatório* especificar o caminho completo para ele. Por exemplo, o comando

```bash
$ ln target.txt /home/carol/Documents/hardlink
```

Cria um arquivo chamado `hardlink` no diretório `/home/carol/Documents/`, vinculado ao arquivo `target.txt` no diretório atual.

Se deixarmos de fora o último parâmetro (`LINK_NAME`), será criado um link com o mesmo nome do destino no diretório atual.

**Gerenciando os links físicos**

Os links físicos são entradas no sistema de arquivos que têm nomes diferentes, mas que apontam para os mesmos dados no disco. Todos esses nomes são equivalentes e podem ser usados para se referir a um arquivo. Se você alterar o conteúdo de um dos nomes, o conteúdo de todos os outros nomes que apontam para aquele arquivo será alterado, já que todos apontam para os mesmos dados. Se você excluir um dos nomes, os outros nomes continuarão a funcionar.

Isso acontece porque quando você “exclui” um arquivo, os dados não são realmente apagados do disco. O sistema simplesmente exclui a entrada na tabela do sistema de arquivos apontando para o inode correspondente aos dados no disco. Mas se houver uma segunda entrada apontando para o mesmo inode, ainda será possível acessar os dados. É como se fossem duas estradas convergindo no mesmo ponto. Mesmo se bloquearmos ou redirecionarmos uma das estradas, ainda será possível chegar ao destino usando a outra.

Para conferir, podemos usar o parâmetro `-i` de `ls`. Considere o seguinte conteúdo de um diretório:

```bash
$ ls -li
total 224
```

```
3806696 -r--r--r-- 2 carol carol 111702 Jun  7 10:13 hardlink
3806696 -r--r--r-- 2 carol carol 111702 Jun  7 10:13 target.txt
```

O número anterior às permissões é o número inode. Percebeu que tanto o arquivo `hardlink` quanto o arquivo `target.txt` têm o mesmo número (`3806696`)? Isso ocorre porque um é o link físico do outro.

Mas qual é o original e qual é o link? Não dá pra dizer, já que, na prática, eles são a mesma coisa.

Observe que todo link físico que aponta para um arquivo aumenta a *contagem de links* do arquivo. Este é o número logo após as permissões na saída de `ls -l`. Por padrão, todo arquivo tem uma contagem de links de `1` (os diretórios têm uma contagem de `2`), e cada link físico apontando para ele aumenta a contagem em um. Por isso a contagem de links é `2` nos arquivos da lista acima.

Ao contrário dos links simbólicos, só é possível criar links físicos para arquivos, e tanto o link quanto o destino devem residir no mesmo sistema de arquivos.

**Movendo e removendo links físicos**

Como os links físicos são tratados como arquivos regulares, eles podem ser excluídos com `rm` e renomeados ou movidos no sistema de arquivos com `mv`. E como um link rígido aponta para o mesmo inode do destino, ele pode ser movido livremente, sem medo de “quebrar” o link.

###### Links simbólicos

**Criando links simbólicos**

O comando usado para criar um link simbólico também é `ln`, mas com o parâmetro `-s` adicionado. Assim:

```bash
$ ln -s target.txt /home/carol/Documents/softlink
```

Criamos assim um arquivo chamado `softlink` no diretório `/home/carol/Documents/`, apontando para o arquivo `target.txt` no diretório atual.

Como no caso dos links físicos, é possível omitir o nome do link para criar um link com o mesmo nome do destino no diretório atual.

**Gerenciando links simbólicos**

Os links simbólicos apontam para outro caminho no sistema de arquivos. Podemos criar links simbólicos para arquivos *e* diretórios, mesmo em diferentes partições. É muito fácil identificar um link simbólico na saída de `ls`:

```bash
$ ls -lh
total 112K
-rw-r--r-- 1 carol carol 110K Jun  7 10:13 target.txt
lrwxrwxrwx 1 carol carol   12 Jun  7 10:14 softlink -> target.txt
```

No exemplo acima, o primeiro caractere nas permissões para o arquivo `softlink` é `l`, indicando um link simbólico. Além disso, logo após o nome do arquivo, vemos o nome do destino para o qual o link aponta, o arquivo `target.txt`.

Note que nas listagens de arquivos e diretórios os links simbólicos sempre mostram as permissões `rwx` para o usuário, o grupo e outros, mas, na prática, as permissões de acesso para eles são as mesmas do destino.

**Movendo e removendo links simbólicos**

Como no caso dos links físicos, os links simbólicos podem ser removidos usando `rm` e movidos ou renomeados com `mv`. No entanto, deve-se tomar cuidado especial ao criá-los, para evitar “quebrar” o link se ele for movido de seu local original.

Ao criar links simbólicos, é preciso estar ciente de que, a menos que um caminho seja totalmente especificado, o local do destino será interpretado como sendo *relativo* ao local do link. Isso pode criar problemas caso o link ou o arquivo para o qual ele aponta seja movido.

É mais fácil entender isso com um exemplo. Digamos que temos um arquivo chamado `original.txt` no diretório atual e desejamos criar um link simbólico para ele chamado `softlink`. Poderíamos usar:

```bash
$ ln -s original.txt softlink
```

E aparentemente tudo correria bem. Vamos verificar com `ls`:

```bash
$ ls -lh
total 112K
-r--r--r-- 1 carol carol 110K Jun  7 10:13 original.txt
lrwxrwxrwx 1 carol carol   12 Jun  7 19:23 softlink -> original.txt
```

Observe como o link é elaborado: `softlink` aponta para (`→`) `original.txt`. Entretanto, vamos ver o que acontece se movermos o link para o diretório pai e tentarmos exibir seu conteúdo com o comando `less`:

```bash
$ mv softlink ../
$ less ../softlink
../softlink: No such file or directory
```

Como o caminho para `original.txt` não foi especificado, o sistema pressupõe que ele está no mesmo diretório que o link. Quando isso deixa de ser verdade, o link para de funcionar.

Para evitar isso, devemos sempre especificar o caminho completo para o destino ao criar o link:

```bash
$ ln -s /home/carol/Documents/original.txt softlink
```

Dessa forma, o link continuará a funcionar mesmo se for movido, porque aponta para a localização absoluta do destino. Verifique com `ls`:

```bash
$ ls -lh
total 112K
lrwxrwxrwx 1 carol carol   40 Jun  7 19:34 softlink -> /home/carol/Documents/original.txt
```

#### Exercícios Guiados

1. Imagine que um programa precisa criar um arquivo temporário de uso único, que não será novamente necessário após o encerramento do programa. Qual seria o diretório correto para criar esse arquivo?

2. Qual é o diretório temporário que *deve* ser limpo durante o processo de inicialização?

3. Qual é o parâmetro de `chmod` no modo *simbólico* para ativar o sticky bit em um diretório?

4. Imagine que existe um arquivo chamado `document.txt` no diretório `/home/carol/Documents`. Com qual comando criaríamos um link simbólico para ele chamado `text.txt` no diretório atual?

5. Explique a diferença entre um link físico para um arquivo e uma cópia desse arquivo.

#### Exercícios Exploratórios

1. Imagine que dentro de um diretório você cria um arquivo chamado `recipes.txt`. Dentro deste diretório, você também criará um link físico para este arquivo, chamado `receitas.txt`, e um link simbólico (ou *soft*) para este, chamado `rezepte.txt`.

  ```bash
  $ touch recipes.txt
  $ ln recipes.txt receitas.txt
  $ ln -s recipes.txt rezepte.txt
  ```

  O conteúdo do diretório deve aparecer assim:

  ```bash
  $ ls -lhi
  total 160K
  5388833 -rw-r--r-- 4 carol carol 77K jun 17 17:25 receitas.txt
  5388833 -rw-r--r-- 4 carol carol 77K jun 17 17:25 recipes.txt
  5388837 lrwxrwxrwx 1 carol carol  12 jun 24 10:12 rezepte.txt -> receitas.txt
  ```

  Lembre-se que, por ser um link físico, `receitas.txt` aponta para o mesmo inode que `recipes.txt`. O que aconteceria com o link `rezepte.txt` se o nome `receitas.txt` fosse excluído? Por quê?

2. Imagine que você tem um pendrive conectado ao sistema e montado em `/media/youruser/FlashA`. Você deseja criar em seu diretório pessoal um link chamado `schematics.pdf` apontando para o arquivo `esquema.pdf` no diretório raiz do pendrive. Então, você digita o comando:

  ```bash
  $ ln /media/youruser/FlashA/esquema.pdf ~/schematics.pdf
  ```

  O que aconteceria? Por quê?

3. Considere a seguinte saída de `ls -lah`:

  ```bash
  $ ls -lah
  total 3,1M
  drwxr-xr-x 2 carol carol 4,0K jun 17 17:27 .
  drwxr-xr-x 5 carol carol 4,0K jun 17 17:29 ..
  -rw-rw-r-- 1 carol carol 2,8M jun 17 15:45 compressed.zip
  -rw-r--r-- 4 carol carol  77K jun 17 17:25 document.txt
  -rw-rw-r-- 1 carol carol 216K jun 17 17:25 image.png
  ```

  ```
  -rw-r--r-- 4 carol carol  77K jun 17 17:25 text.txt
  ```

  - Quantos links apontam para o arquivo `document.txt`?
  - Trata-se de links físicos ou simbólicos?
  - Qual parâmetro você deveria passar para `ls` para ver qual inode é ocupado por cada arquivo?

4. Imagine que você tem, em seu diretório `~/Documents`, um arquivo chamado `clients.txt` contendo alguns nomes de clientes e um diretório chamado `somedir`. Dentro dele, existe um arquivo *diferente*, *também* chamado `clients.txt`, contendo nomes diferentes. Para replicar essa estrutura, use os seguintes comandos:

  ```bash
  $ cd ~/Documents
  $ echo "John, Michael, Bob" > clients.txt
  $ mkdir somedir
  $ echo "Bill, Luke, Karl" > somedir/clients.txt
  ```

  Em seguida você cria um link dentro de `somedir` chamado `partners.txt` apontando para esse arquivo, com os comandos:

  ```bash
  $ cd somedir/
  $ ln -s clients.txt partners.txt
  ```

  Assim, a estrutura do diretório é:

  ```
  Documents
  |-- clients.txt
  `-- somedir
  |-- clients.txt
  `-- partners.txt -> clients.txt
  ```

  Agora, você move `partners.txt` de `somedir` para `~/Documents`, e lista seu conteúdo.

  ```bash
  $ cd ~/Documents/
  ```

  ```bash
  $ mv somedir/partners.txt .
  $ less partners.txt
  ```

  O link ainda funciona? Se sim, qual arquivo terá seu conteúdo listado? Por quê?

5. Considere os arquivos a seguir:

  ```
  -rw-r--r-- 1 carol carol 19 Jun 24 11:12 clients.txt
  lrwxrwxrwx 1 carol carol 11 Jun 24 11:13 partners.txt -> clients.txt
  ```

  Quais são as permissões de acesso de `partners.txt`? Por quê?

#### Resumo

Nesta lição, você aprendeu:

- Onde são armazenados os arquivos temporários.
- Qual a permissão especial aplicada a eles.
- O que são links.
- A diferença entre os links *simbólicos* e *físicos*.
- Como criar links.
- Como movê-los, renomeá-los ou excluí-los.

Os seguintes comandos foram discutidos nesta lição:

- `ln`
- O parâmetro `-i` de `ls`

#### Respostas aos Exercícios Guiados

1. Imagine que um programa precisa criar um arquivo temporário de uso único, que não será novamente necessário após o encerramento do programa. Qual seria o diretório correto para criar esse arquivo?

  Como não precisamos mais do arquivo depois que o programa for encerrado, o diretório correto é `/tmp`.

2. Qual é o diretório temporário que *deve* ser limpo durante o processo de inicialização?

  O diretório é `/run` ou, em certos sistemas, `/var/run`.

3. Qual é o parâmetro de `chmod` no modo *simbólico* para ativar o sticky bit em um diretório?

  O símbolo do sticky bit no modo simbólico é `t`. Como queremos habilitar (adicionar) essa permissão no diretório, o parâmetro deve ser `+t`.

4. Imagine que existe um arquivo chamado `document.txt` no diretório `/home/carol/Documents`. Com qual comando criaríamos um link simbólico para ele chamado `text.txt` no diretório atual?

  `ln -s` é o comando para criar um link simbólico. Como é necessário especificar o caminho completo do arquivo para o qual estamos criando o link, o comando seria:

  ```bash
  $ ln -s /home/carol/Documents/document.txt text.txt
  ```

5. Explique a diferença entre um link físico para um arquivo e uma cópia desse arquivo.

  Um link físico é apenas outro nome para um arquivo. Mesmo que pareça uma duplicata do arquivo original, para todos os efeitos, o link e o original são iguais, pois apontam para os mesmos dados no disco. As alterações feitas no conteúdo do link serão refletidas no original e vice-versa. Uma cópia é uma entidade completamente independente, ocupando um lugar diferente no disco. As alterações na cópia não serão refletidas no original e vice-versa.

#### Respostas aos Exercícios Exploratórios

1. Imagine que dentro de um diretório você crie um arquivo chamado `recipes.txt`. Dentro deste diretório, você também criará um link físico para este arquivo, chamado `receitas.txt`, e um link simbólico (ou *soft*) para este chamado `rezepte.txt`.

  ```bash
  $ touch recipes.txt
  $ ln recipes.txt receitas.txt
  $ ln -s recipes.txt rezepte.txt
  ```

  O conteúdo do diretório deve aparecer assim:

  ```bash
  $ ls -lhi
  total 160K
  5388833 -rw-r--r-- 4 carol carol 77K jun 17 17:25 receitas.txt
  5388833 -rw-r--r-- 4 carol carol 77K jun 17 17:25 recipes.txt
  5388837 lrwxrwxrwx 1 carol carol  12 jun 24 10:12 rezepte.txt -> recipes.txt
  ```

  Lembre-se que, por ser um link físico, `receitas.txt` aponta para o mesmo inode que `recipes.txt`. O que aconteceria com o link `rezepte.txt` se o nome `receitas.txt` fosse excluído? Por quê?

  O link simbólico `rezepte.txt` deixaria de funcionar, porque os links simbólicos apontam para nomes, e não inodes, e o nome `receitas.txt` não existe mais, mesmo que os dados ainda estejam no disco com o nome `recipes.txt`.

2. Imagine que você tem um pendrive conectado ao sistema e montado em `/media/youruser/FlashA`. Você deseja criar em seu diretório pessoal um link chamado `schematics.pdf` apontando para o arquivo `esquema.pdf` no diretório raiz do pendrive. Então, você digita o comando:

  ```bash
  $ ln /media/youruser/FlashA/esquema.pdf ~/schematics.pdf
  ```

  O que aconteceria? Por quê?

  O comando falharia. A mensagem de erro seria `Invalid cross-device link` (Link inválido entre dispositivos), esclarecendo o motivo: os links físicos não podem apontar para um destino em uma partição ou dispositivo diferente. A única maneira de criar um link como esse é usar um link *simbólico* ou *soft*, adicionando o parâmetro `-s` a `ln`.

3. Considere a seguinte saída de `ls -lah`:

  ```bash
  $ ls -lah
  total 3,1M
  drwxr-xr-x 2 carol carol 4,0K jun 17 17:27 .
  drwxr-xr-x 5 carol carol 4,0K jun 17 17:29 ..
  -rw-rw-r-- 1 carol carol 2,8M jun 17 15:45 compressed.zip
  -rw-r--r-- 4 carol carol  77K jun 17 17:25 document.txt
  -rw-rw-r-- 1 carol carol 216K jun 17 17:25 image.png
  -rw-r--r-- 4 carol carol  77K jun 17 17:25 text.txt
  ```

  - Quantos links apontam para o arquivo `document.txt`?

  Todos os arquivos começam com `1` na contagem de links. Como a contagem de links desse arquivo é `4`, existem três links apontando para ele.

  - Trata-se de links físicos ou simbólicos?

  São links físicos, já que os links simbólicos não aumentam a contagem de links de um arquivo.

  - Qual parâmetro você deveria passar para `ls` para ver qual inode é ocupado por cada arquivo?

  O parâmetro é `-i`. O inode será mostrado na primeira coluna da saída de `ls`, como abaixo:

  ```bash
  $ ls -lahi
  total 3,1M
  5388773 drwxr-xr-x 2 rigues rigues 4,0K jun 17 17:27 .
  5245554 drwxr-xr-x 5 rigues rigues 4,0K jun 17 17:29 ..
  5388840 -rw-rw-r-- 1 rigues rigues 2,8M jun 17 15:45 compressed.zip
  5388833 -rw-r--r-- 4 rigues rigues  77K jun 17 17:25 document.txt
  5388837 -rw-rw-r-- 1 rigues rigues 216K jun 17 17:25 image.png
  5388833 -rw-r--r-- 4 rigues rigues  77K jun 17 17:25 text.txt
  ```

4. Imagine que você tem, em seu diretório `~/Documents`, um arquivo chamado `clients.txt` contendo alguns nomes de clientes e um diretório chamado `somedir`. Dentro dele, existe um arquivo *diferente*, *também* chamado `clients.txt`, contendo nomes diferentes. Para replicar essa estrutura, use os seguintes comandos:

  ```bash
  $ cd ~/Documents
  ```

  ```bash
  $ echo "John, Michael, Bob" > clients.txt
  $ mkdir somedir
  $ echo "Bill, Luke, Karl" > somedir/clients.txt
  ```

  Em seguida você cria um link dentro de `somedir` chamado `partners.txt` apontando para esse arquivo, com os comandos:

  ```bash
  $ cd somedir/
  $ ln -s clients.txt partners.txt
  ```

  Assim, a estrutura do diretório é:

  ```
  Documents
  |-- clients.txt
  `-- somedir
  |-- clients.txt
  `-- partners.txt -> clients.txt
  ```

  Agora, você move `partners.txt` de `somedir` para `~/Documents`, e lista seu conteúdo.

  ```bash
  $ cd ~/Documents/
  $ mv somedir/partners.txt .
  $ less partners.txt
  ```

  O link ainda funciona? Se sim, qual arquivo terá seu conteúdo listado? Por quê?

  Isto é quase uma “pegadinha”, mas o link funcionará e o arquivo listado será o que está em `~/Documents`, contendo os nomes `John`, `Michael`, `Bob`.

  Lembre-se de que, como não especificamos o caminho completo para o alvo `clients.txt` ao criar o link simbólico `partners.txt`, o local do destino será interpretado como sendo relativo ao local do link, que neste caso é o diretório atual.

  Quando o link é movido de `~/Documents/somedir` para `~/Documents`, ele deveria parar de funcionar, já que o destino não estava mais no mesmo diretório do link. Porém, coincidentemente existe um arquivo chamado `clients.txt` em `~/Documents`, de forma que o link apontará para esse arquivo em vez do destino original dentro de `~/somedir`.

  Para evitar isso, sempre especifique o caminho completo para o destino ao criar um link simbólico.

5. Considere os arquivos a seguir:

  ```
  -rw-r--r-- 1 rigues rigues 19 Jun 24 11:12 clients.txt
  lrwxrwxrwx 1 rigues rigues 11 Jun 24 11:13 partners.txt -> clients.txt
  ```

  Quais são as permissões de acesso de `partners.txt`? Por quê?

  As permissões de acesso de `partners.txt` são `rw-r--r--`, já que os links sempre herdam as mesmas permissões de acesso do alvo.

---
*Fonte: Linux Professional Institute, Materiais Didáticos Linux Essentials (learning.lpi.org), licença CC BY-NC-ND 4.0. Conversão do PDF para Markdown apenas para estudo pessoal.*
