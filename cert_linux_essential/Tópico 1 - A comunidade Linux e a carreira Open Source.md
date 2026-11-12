---
tags: [lpi, linux-essentials, 010-160]
topico: 1
certificacao: LPI Linux Essentials 010-160 (v1.6)
---

# Tópico 1: A comunidade Linux e a carreira Open Source

## 1.1 A evolução do Linux e sistemas operacionais populares

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 1.1
- **Peso**: 2

**Áreas chave de conhecimento**

- Distribuições
- Sistemas Embarcados
- Linux na Nuvem

**Segue uma lista parcial dos arquivos, termos e utilitários utilizados**

- Debian, Ubuntu (LTS)
- CentOS, openSUSE, Red Hat, SUSE
- Linux Mint, Scientific Linux
- Raspberry Pi, Raspbian
- Android

### 1.1 Lição 1

#### Introdução

O Linux é um dos sistemas operacionais mais populares. Linus Torvalds começou a desenvolvê-lo em 1991 inspirado no Unix, um outro sistema operacional criado nos anos 70 pelos Laboratórios AT&T. O Unix foi projetado para computadores pequenos. Na época, eram consideradas “pequenas” as máquinas que não precisavam de um cômodo inteiro com ar condicionado e que custavam menos de um milhão de dólares. Mais tarde, essa categoria passou a designar as máquinas que podiam ser erguidas por duas pessoas. Até então, o Unix não estava disponível para pequenos computadores, como os computadores de escritório, que eram baseados na plataforma x86. Assim, Linus, na época um estudante, começou a implementar um sistema operacional semelhante ao Unix, mas capaz de rodar nessa plataforma.

O Linux, em sua maior parte, lança mão dos mesmos princípios e idéias básicas do Unix, mas não contém código Unix, pois trata-se de um projeto independente. O Linux não é suportado por uma empresa individual, mas por uma comunidade internacional de programadores. Disponível gratuitamente, pode ser usado por qualquer pessoa, sem restrições.

##### Distribuições

Uma *distribuição* Linux é um pacote que consiste em um *kernel* Linux, mais uma seleção de aplicativos mantidos por uma empresa ou comunidade de usuários. O objetivo de uma distribuição é otimizar o kernel e os aplicativos que rodam no sistema operacional para um determinado tipo de uso ou grupo de usuários. As distribuições freqüentemente incluem ferramentas próprias para a instalação de software e administração do sistema. Por essa razão, certas distribuições são usadas principalmente em ambientes desktop, por serem mais fáceis de usar, enquanto outras são mais comumente instaladas em servidores para usar os recursos disponíveis da maneira mais eficiente possível.

Outra maneira de classificar as distribuições é de acordo com a *família de distribuições* a que pertencem. As distribuições da família Debian usam o gerenciador de pacotes `dpkg` para gerenciar o software executado no sistema operacional. Os pacotes que podem ser instalados com o gerenciador de pacotes são mantidos por membros voluntários da comunidade da distribuição. Os mantenedores usam o formato de pacote `deb` para especificar como o software é instalado no sistema operacional e como é configurado por padrão. Assim como uma distribuição, um pacote é constituído por um conjunto de programas, mais uma configuração e documentação correspondentes, facilitando a instalação, atualização e utilização do software pelo usuário.

O *Debian GNU/Linux* é a maior distribuição da família Debian. O Projeto Debian GNU/Linux foi lançado por Ian Murdock em 1993 e conta, hoje, com milhares de voluntários trabalhando no projeto. O objetivo do Debian GNU/Linux é fornecer um sistema operacional extremamente confiável. Ele também promove a visão de Richard Stallman de um sistema operacional que respeite as liberdades do usuário de executar, estudar, distribuir e aprimorar o software. Por essa razão, ele também não fornece nenhum programa proprietário por padrão.

O *Ubuntu* é outra distribuição baseada no Debian que merece ser mencionada. O Ubuntu foi criado por Mark Shuttleworth e sua equipe em 2004, com a missão de produzir um ambiente desktop Linux fácil de usar. A ideia do Ubuntu é fornecer um software livre para todas as pessoas ao redor do mundo, bem como reduzir o custo dos serviços profissionais. A distribuição lança uma nova versão a cada seis meses, além de uma versão com suporte de longo prazo a cada 2 anos.

O *Red Hat* é uma distribuição Linux desenvolvida e mantida pela empresa de software de mesmo nome, adquirida pela IBM em 2019. A distribuição Red Hat Linux foi iniciada em 1994 e rebatizada em 2003 como *Red Hat Enterprise Linux*, ou RHEL. É fornecida às empresas como uma solução empresarial confiável suportada pela Red Hat e vem com software destinado a facilitar o uso do Linux em ambientes de servidores profissionais. Alguns de seus componentes requerem assinaturas ou licenças pagas. O projeto *CentOS* usa o código-fonte livre do Red Hat Enterprise Linux para compilar uma distribuição inteiramente gratuita, mas que não conta com o serviço de suporte comercial.

Tanto o RHEL quanto o CentOS são otimizados para uso em ambientes de servidor. O projeto *Fedora* foi fundado em 2003 com a ideia de criar uma distribuição Linux voltada para computadores desktop. A Red Hat iniciou e ainda mantém essa distribuição. O Fedora é muito progressista e adota novas tecnologias rapidamente, sendo frequentemente considerado um banco de testes para novas tecnologias que, mais tarde, poderão ser incluídas no RHEL. Todas as distribuições baseadas em Red Hat usam o formato de pacote `rpm`.

A empresa SUSE foi fundada em 1992 na Alemanha como um provedor de serviços Unix. A primeira versão do *SUSE Linux* foi lançada em 1994. Ao longo dos anos, o SUSE Linux tornou-se mais conhecido por sua ferramenta de configuração YaST, que permite aos administradores instalar e configurar software e hardware, configurar servidores e redes. Semelhante ao RHEL, o SUSE oferece o *SUSE Linux Enterprise Server*, sua edição comercial, com lançamentos menos frequentes e adequado para a implantação em empresas e ambientes de produção. É distribuído como um servidor, bem como um ambiente desktop, com pacotes adequados para fins específicos. Em 2004, a SUSE lançou o projeto *openSUSE*, que permitia que os desenvolvedores e usuários testassem e desenvolvessem ainda mais o sistema. A distribuição openSUSE pode ser baixada gratuitamente.

Muitas distribuições independentes foram lançadas ao longo dos anos. Algumas delas se baseiam em Red Hat ou Ubuntu, outras são projetadas para aprimorar uma propriedade específica de um sistema ou hardware. Existem distribuições construídas com funcionalidades específicas, como o *QubesOS*, um ambiente de desktop extremamente seguro, ou o *Kali Linux*, que oferece um ambiente para explorar vulnerabilidades de software e é usado principalmente para testes de intrusão. Recentemente, diversas distribuições Linux minúsculas foram projetadas para rodar especificamente em containers Linux, como o Docker. Existem também distribuições construídas especificamente para componentes de sistemas embarcados e mesmo dispositivos inteligentes.

##### Sistemas embarcados

Os sistemas embarcados são uma combinação de hardware e software projetados para cumprir uma função específica dentro de um sistema maior. Normalmente fazem parte de outros dispositivos e ajudam a controlá-los. Podem ser encontrados em aplicações automotivas, médicas e até militares. Devido a essa ampla variedade de aplicações, Uma variedade de sistemas operacionais baseados no kernel do Linux foi desenvolvida para uso em sistemas embarcados. uma parte significativa dos dispositivos inteligentes usa um sistema operacional baseado no kernel do Linux.

Assim, em sistemas embarcados temos software embarcado, cujo objetivo é acessar o hardware e torná-lo utilizável. Dentre as principais vantagens do Linux sobre qualquer software embarcado proprietário estão a compatibilidade entre plataformas de diferentes fornecedores, desenvolvimento, suporte e ausência de taxas de licença. Dois dos mais populares projetos de software embarcado são o Android, usado principalmente em telefones celulares por diferentes fabricantes, e o Raspbian, que é usado principalmente no Raspberry Pi.

###### Android

O Android é um sistema operacional móvel desenvolvido principalmente pelo Google. A Android Inc. foi fundada em 2003 em Palo Alto, Califórnia. A empresa inicialmente criou um sistema operacional destinado a rodar em câmeras digitais. Em 2005, o Google comprou a Android Inc. e transformou esse sistema em um dos maiores sistemas operacionais móveis.

A base do Android é uma versão modificada do kernel do Linux junto com outros softwares de código aberto. O sistema foi desenvolvido principalmente para dispositivos touchscreen, mas o Google desenvolveu também versões para smart TVs e smartwatches. Diferentes versões do Android foram desenvolvidas para consoles de jogos, câmeras digitais e mesmo PCs.

O código do Android está disponível gratuitamente no *Android Open Source Project* (AOSP). O Google oferece uma série de componentes proprietários juntamente com o núcleo de código aberto do Android. Dentre esses componentes estão aplicativos como Google Agenda, Google Maps, Google Mail, o navegador Chrome e a Google Play Store, que facilita a instalação de aplicativos. A maioria dos usuários considera essas ferramentas como parte integrante da sua experiência no Android. Assim, praticamente todos os dispositivos móveis na Europa e na América que vêm com Android instalado incluem software proprietário do Google.

O Android oferece muitas vantagens em dispositivos embarcados. O sistema operacional é intuitivo e fácil de usar, graças à interface gráfica de usuário, e conta com uma comunidade de desenvolvedores muito ampla, sendo fácil encontrar ajuda para o desenvolvimento. Ele também é suportado pela maioria dos fabricantes de hardware com um driver Android, sendo assim fácil e econômico criar protótipos de um sistema inteiro.

###### O Raspbian e o Raspberry Pi

O Raspberry Pi é um computador de baixo custo, do tamanho de um cartão de crédito, que pode exercer o papel de um computador de mesa inteiramente funcional, mas também pode ser usado dentro de um sistema Linux embarcado. É desenvolvido pela Raspberry Pi Foundation, uma instituição educacional de caridade no Reino Unido. Sua finalidade principal é ensinar os jovens a programar e compreender a funcionalidade dos computadores. O Raspberry Pi pode ser projetado e programado para realizar tarefas e operações que fazem parte de um sistema muito mais complexo.

Dentre as particularidades do Raspberry Pi temos um conjunto de pinos GPIO (General Purpose Input-Output, ou entrada e saída de uso geral) que podem ser usados para conectar dispositivos eletrônicos e placas de expansão. Isso permite usar o Raspberry Pi como uma plataforma para desenvolvimento de hardware. Embora tenha sido criado para fins educacionais, os Raspberry Pis são utilizados atualmente em diversos projetos caseiros, bem como para prototipagem industrial no desenvolvimento de sistemas embarcados.

O Raspberry Pi emprega processadores ARM. Muitos sistemas operacionais, incluindo o Linux, rodam no Raspberry Pi. Como o Raspberry Pi não contém um disco rígido, o sistema operacional é iniciado a partir de um cartão de memória SD. Uma das distribuições Linux mais importantes para o Raspberry Pi é o *Raspbian*. Como o nome sugere, ele pertence à família de distribuição Debian. Ele é personalizado para ser instalado no hardware do Raspberry Pi e oferece mais de 35000 pacotes otimizados para esse ambiente. Além do Raspbian, existem várias outras distribuições Linux para o Raspberry Pi, como por exemplo o Kodi, que transforma o Raspberry Pi numa central de mídia.

##### O Linux e a Nuvem

O termo *cloud computing*, ou computação em nuvem, refere-se a uma forma padronizada de consumir recursos de computação, seja comprando-os de um provedor público de nuvem ou criando uma nuvem privada. Segundo relatórios de 2017, o Linux está por trás de 90% da carga de trabalho das nuvens públicas. Todos os provedores de serviços de nuvem, do *Amazon Web* *Services* (AWS) ao *Google Cloud Platform* (GCP), oferecem diferentes formas de Linux. Mesmo a Microsoft hoje oferece máquinas virtuais baseadas em Linux em sua nuvem *Azure*.

O Linux é comumente incluído nas ofertas de *Infraestrutura como Serviço* (IaaS). As instâncias de IaaS são máquinas virtuais provisionadas em poucos minutos na nuvem. Ao iniciar uma instância de IaaS, uma imagem contendo os dados é escolhida e disponibilizada para a nova instância. Os provedores de nuvem oferecem diversas imagens que contêm instalações de distribuições populares de Linux prontas para executar, além de suas próprias versões de Linux. O usuário de nuvem escolhe a imagem que contém sua distribuição preferida e ganha acesso quase imediato a uma instância da nuvem que roda aquela distribuição. A maioria dos provedores de nuvem adiciona ferramentas às imagens para adaptar a instalação a uma instância específica de nuvem. Essas ferramentas servem, por exemplo, para estender os sistemas de arquivo da imagem de modo a que se encaixem perfeitamente no disco rígido real da máquina virtual.

#### Exercicios Guiados

1. Quais as diferenças entre o Debian GNU/Linux e o Ubuntu? Cite dois aspectos.

2. Em quais os ambientes/plataformas o Linux é mais usado? Cite três ambientes/plataformas diferentes e dê o nome de uma distribuição que pode ser usada em cada um deles.

3. Você planeja instalar uma distribuição de Linux em um novo ambiente. Cite quatro coisas a se considerar na escolha de uma distribuição.

4. Cite três dispositivos que rodam Android OS, além de smartphones.

5. Explique três grandes vantagens da computação em nuvem.

#### Exercícios Exploratórios

1. Levando em conta o custo e o desempenho, quais as distribuições mais adequadas para uma empresa que tem como objetivo reduzir custos com licenças sem prejudicar o desempenho? Justifique sua resposta.

2. Quais são as principais vantagens do Raspberry Pi e quais funções ele pode realizar em um contexto empresarial?

3. Quais distribuições são propostas pelo Amazon Cloud Services e pelo Google Cloud? Cite pelo menos três mais comuns e duas diferentes.

#### Resumo

Nesta lição, você aprendeu:

- Quais distribuições de Linux existem
- O que são sistemas com Linux embarcado
- Como são usados os sistemas com Linux embarcado
- Diferentes aplicações do Android
- Diferentes usos de um Raspberry Pi
- O que é a Computação em Nuvem
- Qual o papel do Linux na computação em nuvem

#### Respostas aos Exercícios Guiados

1. Quais as diferenças entre o Debian GNU/Linux e o Ubuntu? Cite dois aspectos.

  O Ubuntu baseia-se em um instantâneo do Debian, e por isso existem muitas semelhanças entre eles. Todavia, eles não deixam de apresentar diferenças significativas. A primeira delas seria a usabilidade para os iniciantes. O Ubuntu é recomendado aos iniciantes devido à sua facilidade de uso; já o Debian é recomendado para usuários mais avançados. A principal diferença reside na complexidade da configuração de usuário, que o Ubuntu não exige durante o processo de instalação.

  Outra diferença seria a estabilidade de cada distribuição. O Debian é considerado mais estável em comparação com o Ubuntu. Isso acontece porque ele recebe menos atualizações, que são testadas em detalhe, e o sistema operacional como um todo tem mais estabilidade. Por outro lado, o Ubuntu permite que o usuário utilize os lançamentos mais recentes de software e todas as novas tecnologias.

2. Em quais os ambientes/plataformas o Linux é mais usado? Cite três ambientes/plataformas diferentes e dê o nome de uma distribuição que pode ser usada em cada um deles.

  Dentre os ambientes/plataformas mais comuns poderíamos citar smartphone, desktop e servidor. Nos smartphones, ele pode ser empregado em distribuições como o Android. Para desktop e servidores, é possível escolher qualquer distribuição que pareça adequada à funcionalidade da máquina em questão, como Debian ou Ubuntu, ou ainda CentOS e Red Hat Enterprise Linux.

3. Você planeja instalar uma distribuição de Linux em um novo ambiente. Cite quatro coisas a se considerar na escolha de uma distribuição.

  Ao escolher uma distribuição, alguns elementos importantes a considerar são custo, desempenho, escalabilidade, estabilidade e as exigências de hardware do sistema.

4. Cite três dispositivos que rodam Android OS, além de smartphones.

  Dentre os outros dispositivos que usam Android estão as smart TVs, tablets, Android Auto e smartwatches.

5. Explique três grandes vantagens da computação em nuvem.

  As principais vantagens da computação em nuvem são flexibilidade, facilidade de recuperação e baixo custo. Os serviços baseados na nuvem são fáceis de implementar e escalar, dependendo das necessidades da empresa. Eles são mais vantajosos para as soluções de backup e recuperação, já que permitem que uma empresa se recupere rapidamente e sem grandes repercussões após um incidente. Além disso, reduzem os custos operacionais, pois é possível pagar apenas pelos recursos usados pela empresa em um modelo baseado em assinatura.

#### Respostas aos Exercícios Exploratórios

1. Levando em conta o custo e o desempenho, quais as distribuições mais adequadas para uma empresa que tem como objetivo reduzir custos com licenças sem prejudicar o desempenho? Justifique sua resposta.

  Uma das distribuições mais adequadas ao uso empresarial é o CentOS. Ela incorpora todos os produtos do Red Hat, que também são usados no sistema operacional comercial dessa empresa, sem deixar de ser gratuita. Da Mesma maneira, os lançamentos do Ubuntu LTS garantem o suporte por períodos mais longos. As versões estáveis de Debian GNU/Linux também são frequentemente usadas em ambientes empresariais.

2. Quais são as principais vantagens do Raspberry Pi e quais funções ele pode realizar em um contexto empresarial?

  O Raspberry Pi, embora pequeno, funciona como um computador normal. Além disso, custa pouco e pode lidar com tráfego web e muitas outras funcionalidades. Pode ser usado como servidor ou firewall, como placa principal de um robô e muitos outros pequenos dispositivos.

3. Quais distribuições são propostas pelo Amazon Cloud Services e pelo Google Cloud? Cite pelo menos três mais comuns e duas diferentes.

  As distribuições em comum entre o Amazon e o Google Cloud Services são Ubuntu, CentOS e Red Hat Enterprise Linux. Cada um desses provedores de serviços na nuvem propõe distribuições específicas. A Amazon tem o Amazon Linux e o Kali Linux, ao passo que o Google oferece o uso de FreeBSD e Windows Servers.

## 1.2 Principais Aplicações Open Source

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 1.2
- **Peso**: 2

**Áreas chave de conhecimento**

- Aplicações Desktop
- Aplicações em Servidores
- Linguagens de desenvolvimento
- Ferramentas de gerenciamento de pacotes e repositórios

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- OpenOffice.org, LibreOffice, Thunderbird, Firefox, GIMP
- Nextcloud, ownCloud
- Apache HTTPD, NGINX, MariaDB, MySQL, NFS, Samba
- C, Java, JavaScript, Perl, shell, Python, PHP
- dpkg, apt-get, rpm, yum

### 1.2 Lição 1

#### Introdução

Um aplicativo é um programa de computador cuja função não está diretamente ligada ao funcionamento interno da máquina, mas sim a tarefas realizadas pelo usuário. As distribuições Linux oferecem muitas opções de aplicativos para executar uma variedade de tarefas, como programas de escritório, navegadores web, programas de reprodução e edição de mídia etc. Frequentemente existe mais de um aplicativo ou ferramenta para executar um determinado trabalho. Cabe ao usuário escolher o aplicativo que melhor se adapta às suas necessidades.

##### Pacotes de software

Quase todas as distribuições Linux vêm com um conjunto pré-instalado de aplicativos por padrão. Além desses aplicativos, as distribuições têm um repositório de pacotes com uma vasta coleção de programas disponíveis para instalação através de seu *gerenciador de pacotes*. Embora as diversas distribuições ofereçam mais ou menos os mesmos aplicativos, há vários sistemas diferentes de gerenciamento de pacotes de acordo com as distribuições. Por exemplo, Debian, Ubuntu e Linux Mint usam as ferramentas `dpkg`, `apt-get` e `apt` para instalar pacotes de software chamados geralmente de *pacotes DEB*. Já distribuições como Red Hat, Fedora e CentOS usam os comandos `rpm`, `yum` e `dnf`, que por sua vez instalam *pacotes RPM*. Como o empacotamento de aplicativos é diferente para cada família de distribuições, é fundamental instalar pacotes do repositório correto de cada distribuição. O usuário final normalmente não precisa se preocupar com esses detalhes, já que o gerenciador de pacotes da distribuição escolhe os pacotes corretos, as dependências solicitadas e as atualizações futuras. As dependências são os pacotes auxiliares de que os programas necessitam. Por exemplo, se uma biblioteca oferece funções para gerenciar imagens no formato JPEG que são usadas por diversos programas, ela estará muito provavelmente em um pacote próprio, do qual dependerão todos os aplicativos que usarem a biblioteca em questão.

Os comandos `dpkg` e `rpm` operam em arquivos empacotados individuais. Na prática, quase todas as tarefas de gerenciamento de pacotes são executadas pelos comandos `apt-get` ou `apt` em sistemas que usam pacotes DEB, ou por `yum` ou `dnf` em sistemas que usam pacotes RPM. Esses comandos funcionam com catálogos de pacotes, podem baixar novos pacotes e suas dependências e verificar se existem novas versões dos pacotes instalados.

##### Instalação do pacote

Suponha que você tenha ouvido falar de um comando chamado `figlet`, que mostra um texto ampliado no terminal, e quer experimentá-lo. No entanto, aparece a seguinte mensagem após a execução do comando `figlet`:

```bash
$ figlet
-bash: figlet: command not found
```

Isso provavelmente indica que o pacote não está instalado em seu sistema. Se sua distribuição funciona com pacotes DEB, você pode procurar os repositórios adequados usando `apt-cache` `search package_name` ou `apt search package_name`. O comando `apt-cache` é usado para procurar por pacotes e listar informações sobre os pacotes disponíveis. O seguinte comando procura por quaisquer ocorrências do termo “figlet” nos nomes e descrições dos pacotes:

```bash
$ apt-cache search figlet
figlet - Make large character ASCII banners out of ordinary text
```

A pesquisa identificou um pacote chamado *figlet* que corresponde ao comando ausente. A instalação e a remoção de um pacote requerem permissões especiais concedidas somente ao administrador do sistema: o usuário chamado `root`. Em sistemas desktop, usuários comuns podem instalar ou remover pacotes prefixando o comando `sudo` aos comandos de instalação/remoção. Esse comando exige sua senha para ser executado. Para pacotes DEB, a instalação é realizada com o comando `apt-get install package_name` ou `apt install` `package_name`:s

```bash
$ sudo apt-get install figlet
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
figlet
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
```

Nesse momento, o pacote será baixado e instalado no sistema. Quaisquer dependências de que o pacote eventualmente precise também serão baixadas e instaladas:

```
Need to get 184 kB of archives.
After this operation, 741 kB of additional disk space will be used.
Get:1 http://archive.raspbian.org/raspbian stretch/main armhf figlet armhf 2.2.5-2 [184 kB]
Fetched 184 kB in 0s (213 kB/s)
Selecting previously unselected package figlet.
(Reading database ... 115701 files and directories currently installed.)
Preparing to unpack .../figlet_2.2.5-2_armhf.deb ...
Unpacking figlet (2.2.5-2) ...
Setting up figlet (2.2.5-2) ...
update-alternatives: using /usr/bin/figlet-figlet to provide /usr/bin/figlet (figlet) in
auto mode
Processing triggers for man-db (2.7.6.1-2) ...
```

Após o download ser concluído, todos os arquivos são copiados para os locais apropriados, qualquer configuração adicional é executada e o comando se torna disponível:

```bash
$ figlet Awesome!
_                                         _
/ \__      _____  ___  ___  _ __ ___   ___| |
/ _ \ \ /\ / / _ \/ __|/ _ \| '_ ` _ \ / _ \ |
/ ___ \ V  V /  __/\__ \ (_) | | | | | |  __/_|
/_/   \_\_/\_/ \___||___/\___/|_| |_| |_|\___(_)
```

Nas distribuições baseadas em pacotes RPM, as pesquisas são feitas usando `yum search` `package_name` ou `dnf search package_name`. Digamos que você queira exibir um texto de uma forma mais irreverente, seguido por um desenho de vaquinha, mas não sabe bem qual pacote é capaz de executar essa tarefa. Como no caso dos pacotes DEB, os comandos de busca RPM aceitam termos descritivos:

```bash
$ yum search speaking cow
Last metadata expiration check: 1:30:49 ago on Tue 23 Apr 2019 11:02:33 PM -03.
==================== Name & Summary Matched: speaking, cow ====================
cowsay.noarch : Configurable speaking/thinking cow
```

Após encontrar um pacote adequado no repositório, ele pode ser instalado com `yum install` `package_name` ou `dnf install package_name`:

```bash
$ sudo yum install cowsay
Last metadata expiration check: 2:41:02 ago on Tue 23 Apr 2019 11:02:33 PM -03.
Dependencies resolved.
==============================================================================
Package         Arch           Version               Repository         Size
==============================================================================
Installing:
cowsay          noarch         3.04-10.fc28          fedora             46 k

Transaction Summary
==============================================================================
Install  1 Package

Total download size: 46 k
Installed size: 76 k
Is this ok [y/N]: y
```

Mais uma vez, o pacote desejado e todas as suas possíveis dependências serão baixados e instalados:

```
Downloading Packages:
cowsay-3.04-10.fc28.noarch.rpm                    490 kB/s |  46 kB     00:00
==============================================================================
Total                                              53 kB/s |  46 kB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Preparing        :                                                          1/1
Installing       : cowsay-3.04-10.fc28.noarch                               1/1
```

```
Running scriptlet: cowsay-3.04-10.fc28.noarch                               1/1
Verifying        : cowsay-3.04-10.fc28.noarch                               1/1

Installed:
cowsay.noarch 3.04-10.fc28

Complete!
```

O comando `cowsay` faz exatamente o que seu nome implica:

```bash
$ cowsay "Brought to you by yum"
_______________________
< Brought to you by yum >
-----------------------
\   ^__^
\  (oo)\_______
(__)\       )\/\
||----w |
||     ||
```

Embora possam parecer inúteis, os comandos `figlet` e `cowsay` oferecem uma maneira de chamar a atenção de outros usuários para informações relevantes.

##### Remoção de Pacotes

Os mesmos comandos usados para instalar pacotes são usados para removê-los. Todos os comandos aceitam a palavra-chave `remove` para desinstalar um pacote instalado: `apt-get` `remove package_name` ou `apt remove package_name` para pacotes DEB e `yum remove` `package_name` ou `dnf remove package_name` para pacotes RPM. O comando `sudo` também é necessário para executar a remoção. Por exemplo, para remover o pacote *figlet* previamente instalado em uma distribuição baseada em DEB:

```bash
$ sudo apt-get remove figlet
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages will be REMOVED:
figlet
0 upgraded, 0 newly installed, 1 to remove and 0 not upgraded.
After this operation, 741 kB disk space will be freed.
```

```
Do you want to continue? [Y/n] Y
```

Depois de confirmar a operação, o pacote é removido do sistema:

```
(Reading database ... 115775 files and directories currently installed.)
Removing figlet (2.2.5-2) ...
Processing triggers for man-db (2.7.6.1-2) ...
```

Nos sistemas baseados em RPM, o procedimento é semelhante. Por exemplo, para remover o pacote *cowsay* instalado anteriormente em uma distribuição baseada em RPM:

```bash
$ sudo yum remove cowsay
Dependencies resolved.
==================================================================================
Package          Arch             Version                Repository         Size
==================================================================================
Removing:
cowsay           noarch           3.04-10.fc28           @fedora            76 k

Transaction Summary
==================================================================================
Remove  1 Package

Freed space: 76 k
Is this ok [y/N]: y
```

Da mesma forma, uma confirmação é solicitada e o pacote é apagado do sistema:

```
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Preparing        :                                                          1/1
Erasing          : cowsay-3.04-10.fc28.noarch                               1/1
Running scriptlet: cowsay-3.04-10.fc28.noarch                               1/1
Verifying        : cowsay-3.04-10.fc28.noarch                               1/1

Removed:
cowsay.noarch 3.04-10.fc28
```

```
Complete!
```

Os arquivos de configuração dos pacotes removidos são mantidos no sistema e podem ser utilizados novamente se o pacote for reinstalado no futuro.

##### Aplicativos de escritório

Os aplicativos de escritório são utilizados para editar arquivos de texto, apresentações, planilhas e outros formatos comumente utilizados num ambiente de escritório. Esses aplicativos são normalmente organizados em coleções chamadas *office suites*, ou suíte de escritório.

Durante muito tempo, a suíte de escritório mais usada no Linux foi o *OpenOffice.org*. O OpenOffice.org era uma versão open source da *StarOffice suite*, produzida pela *Sun Microsystems*. Alguns anos depois, a Sun foi adquirida pela *Oracle Corporation*, que por sua vez transferiu o projeto para a *Apache Foundation*, e o OpenOffice.org foi rebatizado como *Apache OpenOffice*. Nesse meio tempo, outra suíte de escritório baseada no mesmo código fonte foi lançada pela *Document Foundation*, que a batizou de *LibreOffice*.

Os dois projetos têm as mesmas características básicas e são compatíveis com os formatos de documentos do *Microsoft Office*. No entanto, o formato de documento preferido é o *Open* *Document Format*, um formato de arquivo totalmente aberto e padrão ISO. A utilização de arquivos ODF garante que os documentos possam ser transferidos entre sistemas operacionais e aplicativos de diferentes fornecedores, como o Microsoft Office. Os principais aplicativos oferecidos pelo OpenOffice/LibreOffice são:

- **Writer**: Editor de texto
- **Calc**: Planilhas
- **Impress**: Apresentações
- **Draw**: Desenho vetorial
- **Math**: Fórmulas matemáticas
- **Base**: Banco de dados

Tanto o LibreOffice quanto o Apache OpenOffice são softwares de código aberto, mas o LibreOffice é licenciado sob a LGPLv3 e o Apache OpenOffice traz a licença Apache License 2.0. A distinção de licenciamento implica que o LibreOffice pode incorporar melhorias feitas pelo Apache OpenOffice, mas o Apache OpenOffice não pode incorporar melhorias feitas pelo LibreOffice. Essa, junto com uma comunidade mais ativa de desenvolvedores, é a razão pela qual a maioria das distribuições adota o LibreOffice como seu conjunto padrão de aplicativos de escritório.

##### Navegadores web

Para a maioria dos usuários, o principal objetivo de um computador é fornecer acesso à Internet. Hoje em dia, as páginas web podem funcionar como um aplicativo completo, com a vantagem de serem acessíveis de qualquer lugar, sem a necessidade de instalar software extra. Isso faz do navegador web o aplicativo mais importante do sistema operacional, pelo menos para o usuário médio.

> [!tip]
> Uma das melhores fontes para aprender mais sobre desenvolvimento web é o MDN Web Docs, disponível em https://developer.mozilla.org/. Mantido pela Mozilla, o site está repleto de tutoriais para iniciantes e materiais de referência sobre as mais modernas tecnologias web.

Os principais navegadores web no ambiente Linux são o *Google Chrome* e o *Mozilla Firefox*. O Chrome é um navegador web mantido pelo Google, mas baseado no navegador de código aberto *Chromium*, que pode ser instalado através do gerenciador de pacotes da distribuição e é totalmente compatível com o Chrome. Mantido pela Mozilla, uma organização sem fins lucrativos, o Firefox é um navegador cujas origens estão ligadas ao Netscape, o primeiro navegador web popular a adotar o modelo open source. A Fundação Mozilla está profundamente envolvida com o desenvolvimento dos padrões abertos subjacentes à web moderna.

A Mozilla também desenvolve outros aplicativos, como o cliente de email *Thunderbird*. Muitos usuários optam por usar webmail em vez de um programa de email dedicado, mas um cliente como o Thunderbird oferece funcionalidades extras e integra-se melhor com outras aplicações no desktop.

##### Multimídia

Comparado com os aplicativos web disponíveis, os aplicativos para desktop ainda são a melhor opção para a criação de conteúdo multimídia. As atividades relacionadas a multimídia, como a renderização de vídeo, frequentemente exigem quantidades elevadas de recursos do sistema, que podem ser mais bem administrados por um aplicativo desktop local. Listamos abaixo alguns dos aplicativos multimídia mais populares do ambiente Linux e seus usos.

- **Blender**: Um renderizador 3D para criar animações. O Blender também pode ser usado para exportar objetos 3D para serem impressos em uma impressora 3D.
- **GIMP**: Um editor de imagens completo, que pode ser comparado com o *Adobe Photoshop*, mas com seus próprios conceitos e ferramentas para trabalhar com imagens. O GIMP pode ser usado para criar, editar e salvar a maioria dos arquivos bitmap, como JPEG, PNG, GIF, TIFF e muitos outros.
- **Inkscape**: Um editor de gráficos vetoriais, semelhante ao *Corel Draw* ou ao *Adobe Illustrator*. O formato padrão do Inkscape é SVG, um padrão aberto para gráficos vetoriais. Os arquivos SVG podem ser abertos por qualquer navegador web e, devido à sua natureza de gráfico vetorial, podem ser usados em layouts flexíveis de páginas web.
- **Audacity**: Um editor de áudio. O Audacity pode ser usado para filtrar, aplicar efeitos e converter entre diferentes formatos de áudio, como MP3, WAV, OGG, FLAC etc.
- **ImageMagick**: O ImageMagick é uma ferramenta de linha de comando usada para converter e editar a maioria dos tipos de arquivos de imagem. Também pode ser usado para criar documentos PDF a partir de arquivos de imagem e vice-versa.

Também existem muitos aplicativos dedicados à reprodução de mídia. O programa mais popular para a reprodução de vídeo é o *VLC*, mas alguns usuários preferem outras alternativas, como o *smplayer*. A reprodução de música local também traz muitas opções, como o *Audacious*, o *Banshee* e o *Amarok*, que também podem gerenciar uma coleção local de arquivos de áudio.

##### Programas de servidor

Quando um navegador web carrega uma página de um site, na verdade ele se conecta a um computador remoto e pede uma informação específica. Nesse cenário, o computador que executa o navegador web é chamado de *cliente*, e o computador remoto, *servidor*.

O computador servidor, que pode ser um computador desktop comum ou hardware especializado, necessita de um programa específico para gerenciar cada tipo de informação que irá fornecer. No que tange ao envio de páginas web, a maioria dos servidores ao redor do mundo lança mão de programas de servidor de código aberto. Esse programa de servidor em particular é chamado de *HTTP server* (HTTP significa *Hyper Text Transfer Protocol*, ou Protocolo de Transferência de Hipertexto), e os mais populares são *Apache*, *Nginx* e *lighttpd*.

Mesmo as páginas web mais simples podem ter muitas solicitações, que vão desde arquivos comuns — o que se chama conteúdo estático — até o conteúdo dinâmico renderizado a partir de diversas fontes. O papel de um servidor HTTP é coletar e enviar todos os dados solicitados de volta para o navegador, que então organiza o conteúdo conforme definido pelo documento HTML recebido (HTML significa *Hyper Text Markup Language*, ou Linguagem de Marcação de Hipertexto) e outros arquivos anexos. Portanto, a renderização de uma página web envolve operações executadas no lado do servidor e operações executadas no lado do cliente. Ambos os lados podem usar scripts personalizados para realizar tarefas específicas. No lado do servidor HTTP, a linguagem de scripts PHP é comumente usada. Já no lado do cliente usa-se o JavaScript.

Os programas de servidor podem fornecer todo tipo de informação. Não é incomum que um programa de servidor solicite informações fornecidas por outros programas servidores. Esse é o caso quando um servidor HTTP pede informações fornecidas por um servidor de banco de dados.

Por exemplo, quando uma página dinâmica é solicitada, o servidor HTTP normalmente consulta um banco de dados para coletar todas as informações necessárias e envia o conteúdo dinâmico de volta para o cliente. De maneira semelhante, quando um usuário se inscreve em um site, o servidor HTTP reúne os dados enviados pelo cliente e os armazena em um banco de dados.

Um banco de dados é um conjunto organizado de informações. Um servidor de banco de dados armazena conteúdos de maneira formatada, tornando possível ler, escrever e vincular grandes quantidades de dados com alta velocidade. Os servidores de banco de dados de código aberto são usados em muitas aplicações, não apenas na Internet. Mesmo os aplicativos locais podem armazenar dados, conectando-se a um servidor de banco de dados local. O tipo mais comum de banco de dados é o *banco de dados relacional*, no qual os dados são organizados em tabelas predefinidas. Os bancos de dados relacionais de código aberto mais populares são *MariaDB* (derivado do *MySQL*) e *PostgreSQL*.

##### Compartilhamento de dados

Em redes locais, como as encontradas em escritórios e casas, é desejável que os computadores não somente possam acessar a Internet, como também sejam capazes de se comunicar uns com os outros. Às vezes um computador age como um servidor, outras vezes o mesmo computador age como um cliente, o que é necessário quando se quer acessar arquivos em outro computador na rede — por exemplo, acessar um arquivo armazenado em um computador desktop a partir de um dispositivo portátil — sem o incômodo de copiá-lo para um drive USB ou algo do tipo.

Entre máquinas com Linux, usa-se frequentemente o *NFS* (*Network File System*, ou Sistema de Arquivos de Rede). O protocolo NFS é a forma padrão de compartilhar sistemas de arquivos em redes equipadas apenas com máquinas Unix/Linux. Com o NFS, um computador pode compartilhar um ou mais diretórios com computadores específicos na rede, permitindo que eles leiam e escrevam arquivos nesses diretórios. O NFS pode ser usado inclusive para compartilhar a árvore de diretórios inteira de um sistema operacional com clientes que podem assim inicializar a partir dela. Esses computadores, chamados *thin clients* ou "clientes magros", são geralmente usados em grandes redes para evitar a manutenção de cada sistema operacional individual em uma rede.

Se existem outros tipos de sistemas operacionais ligados à rede, recomenda-se a utilização de um protocolo de compartilhamento de dados que possa ser compreendido por todos eles. O *Samba* cumpre esse requisito. O Samba implementa um protocolo de compartilhamento de arquivos na rede originalmente pensado para o sistema operacional Windows, mas hoje é compatível com todos os principais sistemas operacionais. Com o Samba, os computadores na rede local não só podem compartilhar arquivos, como também impressoras.

Em algumas redes locais, a autorização dada pelo login em uma estação de trabalho é concedida por um servidor central, chamado *controlador de domínio*, que gerencia o acesso a vários recursos locais e remotos. O controlador de domínio é um serviço fornecido pelo *Active Directory* da Microsoft. As estações de trabalho Linux podem ser associadas a um controlador de domínio usando Samba ou um subsistema de autenticação chamado *SSSD*. A partir da versão 4, o Samba também pode funcionar como controlador de domínio em redes heterogêneas.

Se o objetivo é implementar uma solução de computação em nuvem capaz de fornecer diversos métodos de compartilhamento de dados baseados na web, duas alternativas devem ser consideradas: *ownCloud* e *Nextcloud*. Os dois projetos são muito semelhantes porque o Nextcloud é um derivado do ownCloud, o que não é incomum entre projetos open source. Esses derivados são geralmente chamados de *fork* (bifurcação ou ramificação). Ambos oferecem os mesmos recursos básicos: compartilhamento e sincronização de arquivos, espaços de trabalho colaborativos, calendário, contatos e email, tudo através de interfaces para desktop, celular e web. O Nextcloud oferece também conferência em áudio e vídeo, ao passo que o ownCloud concentra- se mais em compartilhamento de arquivos e integração com software de terceiros. Há muito mais recursos disponíveis na forma de plugins que podem ser ativados no momento em que forem necessários.

Tanto o ownCloud quanto o Nextcloud oferecem uma versão paga com recursos extras e suporte estendido. O que os torna diferentes de outras soluções comerciais é a possibilidade de instalar o NextCloud ou o ownCloud em um servidor privado, gratuitamente, evitando assim que se mantenham dados confidenciais em um servidor desconhecido. Como todos os serviços dependem de comunicação HTTP e são escritos em PHP, a instalação deve ser realizada em um servidor web previamente configurado, como o Apache. Se você estiver pensando em instalar o ownCloud ou o Nextcloud em seu próprio servidor, não se esqueça de habilitar também o HTTPS para criptografar todas as conexões à sua nuvem.

##### Administração de redes

A comunicação entre computadores só é possível se a rede estiver funcionando corretamente. Normalmente, a configuração da rede é feita por um conjunto de programas executados no roteador, responsáveis por configurar e verificar a disponibilidade da rede. Para isso, dois serviços de rede básicos são usados: *DHCP* (*Dynamic Host Configuration Protocol*, ou Protocolo de Configuração Dinâmica de Host) e *DNS* (*Domain Name System*, ou Sistema de Nomes de Domínio).

O DHCP é responsável por atribuir um endereço IP ao host quando um cabo de rede está conectado ou quando o dispositivo entra em uma rede sem fio. Quando nos conectamos à Internet, o servidor DHCP do provedor de acesso fornece um endereço IP ao dispositivo solicitante. Um servidor DHCP é muito útil também em redes locais, para fornecer endereços IP automaticamente a todos os dispositivos conectados. Se o DHCP não estiver configurado ou se não estiver funcionando corretamente, será necessário configurar manualmente o endereço IP de cada dispositivo conectado à rede. Não é prático definir manualmente os endereços IP em redes grandes ou mesmo em redes pequenas, e por essa razão a maioria dos roteadores de rede vem com um servidor DHCP pré-configurado por padrão.

O endereço IP é necessário para possibilitar a comunicação com um outro dispositivo em uma rede IP, mas nomes de domínio como `www.lpi.org` são muito mais fáceis de lembrar do que um número IP como `203.0.113.165`. O nome de domínio sozinho, entretanto, não basta para estabelecer a comunicação através da rede. Assim, o nome de domínio precisa ser traduzido em forma de endereço IP por um servidor DNS. O endereço IP do servidor DNS é fornecido pelo servidor DHCP do provedor de acesso e é usado por todos os sistemas conectados para traduzir nomes de domínio como endereços IP.

As configurações do DHCP e do DNS podem ser modificadas através da interface web do roteador. Por exemplo, é possível restringir a atribuição de IP apenas a dispositivos conhecidos ou associar um endereço IP fixo a máquinas específicas. Também é possível alterar o servidor DNS padrão fornecido pelo provedor de acesso. Alguns servidores DNS de terceiros, como os fornecidos pelo Google ou OpenDNS, podem ter um tempo de resposta mais rápido e funcionalidades adicionais.

##### Linguagens de programação

Todos os programas de computador (programas de cliente e servidor, aplicativos para desktop e o próprio sistema operacional) são feitos a partir de uma ou mais linguagens de programação. Os programas podem ser um único arquivo ou um sistema complexo de centenas de arquivos, que o sistema operacional trata como uma seqüência de instruções a ser interpretada e executada pelo processador e outros dispositivos.

Existem inúmeras linguagens de programação para diferentes finalidades, e os sistemas Linux fornecem muitas delas. Como o software de código aberto também inclui as fontes dos programas, os sistemas Linux oferecem aos desenvolvedores condições perfeitas para entender, modificar ou criar software de acordo com suas próprias necessidades.

Cada programa começa como um arquivo de texto, chamado *código fonte*. Esse código fonte é escrito em uma linguagem mais ou menos amigável que descreve o que o programa está fazendo. Um processador de computador não pode executar diretamente esse código. Assim, nas *linguagens compiladas*, o código fonte é convertido em um *arquivo binário*, que pode por sua vez ser executado pelo computador. Um programa chamado *compilador* é responsável por fazer a conversão do código fonte para a forma executável. Como o arquivo binário é compilado para um modelo específico de processador, o programa pode ter de ser recompilado para rodar em outro tipo de computador.

Nas *linguagens interpretadas*, o programa não precisa ser compilado previamente. Em vez disso, um *interpretador* lê o código fonte e executa suas instruções toda vez que o programa é executado. Isso torna o desenvolvimento mais fácil e rápido, mas, ao mesmo tempo, os programas interpretados tendem a ser mais lentos do que os programas compilados.

Eis algumas das linguagens de programação mais populares:

- **JavaScript**: O JavaScript é uma linguagem de programação usada principalmente em páginas web. No início, os aplicativos em JavaScript eram muito simples, como rotinas de validação de formulários. Hoje em dia, o JavaScript é considerado uma linguagem de primeira classe e é usado para criar aplicações muito complexas não só na web, mas também em servidores e dispositivos móveis.
- **C**: A linguagem de programação C está intimamente relacionada com os sistemas operacionais, particularmente o Unix, mas é usada para escrever qualquer tipo de programa para quase qualquer tipo de dispositivo. As grandes vantagens do C são a flexibilidade e a velocidade. O mesmo código fonte escrito em C pode ser compilado para rodar em diferentes plataformas e

  sistemas operacionais, com pouca ou nenhuma modificação. Após ser compilado, porém, o programa só roda no sistema alvo.

- **Java**: O aspecto principal do Java é que os programas escritos nessa linguagem são portáteis, o que significa que o mesmo programa pode ser executado em diferentes sistemas operacionais. Apesar do nome, o Java não tem relação com o JavaScript.
- **Perl**: O Perl é uma linguagem de programação mais usada para processar conteúdo de texto. Tem uma forte ênfase em expressões regulares, o que faz do Perl uma linguagem adequada para filtragem e análise de texto.
- **Shell**: O shell, particularmente o Bash shell, não é apenas uma linguagem de programação, mas uma interface interativa para executar outros programas. Os programas em Shell, conhecidos como *shell scripts*, podem automatizar tarefas complexas ou repetitivas no ambiente de linha de comando.
- **Python**: O Python é uma linguagem de programação muito popular entre estudantes e profissionais não diretamente envolvidos com ciência da computação. Apesar de ter recursos avançados, o Python é uma boa maneira de começar a aprender programação devido à sua facilidade de uso.
- **PHP**: O PHP é mais usado como uma linguagem de script do lado do servidor para gerar conteúdo para a web. A maioria das páginas HTML online não são arquivos estáticos, mas conteúdo dinâmico gerado pelo servidor a partir de várias fontes, como bancos de dados. Os programas em PHP — às vezes chamados apenas de páginas PHP ou scripts PHP — são freqüentemente usados para gerar esse tipo de conteúdo. O termo LAMP vem da combinação de um sistema operacional Linux, um servidor Apache HTTP, um banco de dados MySQL (ou MariaDB) e programação em PHP. Os servidores LAMP são uma solução muito popular para rodar servidores web. Além do PHP, todas as linguagens de programação descritas anteriormente podem ser usadas para implementar esse tipo de aplicação.

C e Java são linguagens compiladas. A fim de ser executado pelo sistema, o código fonte escrito em C é convertido em código de máquina binário, enquanto o código fonte em Java é convertido em *bytecode* executado em um ambiente de software especial chamado *Java Virtual Machine*. JavaScript, Perl, Shell script, Python e PHP são linguagens interpretadas, também chamadas de *linguagens de script*.

#### Exercícios Guiados

1. Para cada um dos seguintes comandos, identifique se ele está associado ao *sistema de* *empacotamento Debian* ou ao *sistema de empacotamento Red Hat*:

| `dpkg` |  |
|---|---|
| `rpm` |  |
| `apt-get` |  |
| `yum` |  |
| `dnf` |  |

2. Qual comando poderia ser usado para instalar o Blender no Ubuntu? Após a instalação, como o programa pode ser executado?

3. Qual aplicativo da suíte LibreOffice pode ser usado para trabalhar com planilhas eletrônicas?

4. Qual navegador web de código aberto foi usado como base para o desenvolvimento do Google Chrome?

5. O SVG é um padrão aberto para gráficos vetoriais. Qual é o aplicativo mais popular para editar arquivos SVG em sistemas Linux?

6. Para cada um dos seguintes formatos de arquivo, escreva o nome de um aplicativo capaz de abrir e editar o arquivo correspondente:

  `png`

  `doc`

  `xls`

  `ppt`

  `wav`

7. Que pacote de software permite o compartilhamento de arquivos entre máquinas Linux e Windows através da rede local?

#### Exercícios Exploratórios

1. Você sabe que os arquivos de configuração são preservados mesmo que o pacote associado seja removido do sistema. Como seria possível remover automaticamente o pacote chamado *cups* e seus arquivos de configuração de um sistema baseado em DEB?

2. Suponha que você tem muitos arquivos de imagem TIFF e quer convertê-los para JPEG. Qual pacote de software poderia ser usado para converter esses arquivos diretamente na linha de comando?

3. Qual pacote de software você precisa instalar para poder abrir documentos do Microsoft Word enviados a você por um usuário do Windows?

4. Todos os anos, o site linuxquestions.org promove uma pesquisa sobre os aplicativos Linux mais populares. Visite https://www.linuxquestions.org/questions/2018-linuxquestions-org-members- choice-awards-128/ e descubra quais são os aplicativos de desktop mais populares entre os utilizadores experientes de Linux.

#### Sumário

Nesta lição, você aprendeu:

- Os sistemas de gerenciamento de pacotes usados nas principais distribuições Linux
- Aplicativos de código aberto capazes de editar formatos de arquivos populares
- Os programas de servidor subjacentes a muitos serviços importantes de Internet e rede local
- Linguagens de programação comuns e seus usos

#### Respostas aos Exercícios Guiados

1. Para cada um dos seguintes comandos, identifique se ele está associado ao sistema de empacotamento \_Debian ou ao sistema de empacotamento \_Red Hat:

| `dpkg` | sistema de empacotamento Debian |
|---|---|
| `rpm` | sistema de empacotamento Red Hat |
| `apt-get` | sistema de empacotamento Debian |
| `yum` | sistema de empacotamento Red Hat |
| `dnf` | sistema de empacotamento Red Hat |

2. Qual comando poderia ser usado para instalar o Blender no Ubuntu? Após a instalação, como o programa pode ser executado?

  O comando `apt-get install blender`. O nome do pacote deve ser especificado em minúsculas. O programa pode ser executado diretamente do terminal com o comando `blender` ou escolhendo-o no menu de aplicativos.

3. Qual aplicativo da suíte LibreOffice pode ser usado para trabalhar com planilhas eletrônicas?

  Calc

4. Qual navegador web de código aberto foi usado como base para o desenvolvimento do Google Chrome?

  Chromium

5. O SVG é um padrão aberto para gráficos vetoriais. Qual é o aplicativo mais popular para editar arquivos SVG em sistemas Linux?

  Inkscape

6. Para cada um dos seguintes formatos de arquivo, escreva o nome de um aplicativo capaz de abrir e editar o arquivo correspondente:

| `png` | Gimp |
|---|---|
| `doc` | LibreOffice Writer |
| `xls` | LibreOffice Calc |
| `ppt` | LibreOffice Impress |

  `wav` Audacity

7. Que pacote de software permite o compartilhamento de arquivos entre máquinas Linux e Windows através da rede local?

  Samba

#### Respostas aos Exercícios Exploratórios

1. Você sabe que os arquivos de configuração são preservados mesmo que o pacote associado seja removido do sistema. Como seria possível remover automaticamente o pacote chamado *cups* e seus arquivos de configuração de um sistema baseado em DEB?

  `apt-get purge cups`

2. Suponha que você tem muitos arquivos de imagem TIFF e quer convertê-los para JPEG. Qual pacote de software poderia ser usado para converter esses arquivos diretamente na linha de comando?

  ImageMagick

3. Qual pacote de software você precisa instalar para poder abrir documentos do Microsoft Word enviados a você por um usuário do Windows?

  LibreOffice ou OpenOffice

4. Todos os anos, o site linuxquestions.org promove uma pesquisa sobre os aplicativos Linux mais populares. Visite https://www.linuxquestions.org/questions/2018-linuxquestions-org-members- choice-awards-128/ e descubra quais são os aplicativos de desktop mais populares entre os utilizadores experientes de Linux.

  Navegador: Firefox. Cliente de email: Thunderbird. Reprodução de mídia: VLC. Editor de imagens rasterizadas: GIMP.

## 1.3 Entendendo o Software Open Source e suas Licenças

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 1.3
- **Peso**: 1

**Áreas chave de conhecimento**

- Filosofia do Código Aberto
- Licenciamento
- Free Software Foundation (FSF), Open Source Initiative (OSI)

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- GPL, BSD, Creative Commons, Copyleft, Permissive
- Free Software, Open Source Software, FOSS, FLOSS
- Modelos de negócios Open Source

### 1.3 Lição 1

#### Introdução

Embora os termos *software livre* e *software de código aberto* sejam amplamente utilizados, ainda existem alguns equívocos sobre seu significado. Em particular, o conceito de “liberdade” precisa ser examinado mais de perto. Vamos começar com a definição dos dois termos.

##### Definição de Software Livre e de Código Aberto

###### Critérios do Software Livre

Antes de mais nada, “livre”, no contexto de software livre, não tem nada a ver com “gratuito”, ou, como resume o fundador da *Free Software Foundation* (FSF), Richard Stallman:

Para entender o conceito, você deve pensar em “livre” como em “livre expressão”, não como em “cerveja grátis”.

> — Richard Stallman, What is free software? (O que é software livre?)

Independentemente de você ter de pagar ou não pelo software, existem quatro critérios que definem um software livre. Richard Stallman descreve estes critérios como “as quatro liberdades essenciais”, cuja contagem começa em zero:

- “A liberdade de executar o programa como você deseja, para qualquer finalidade (liberdade 0).”

  Onde, como e para qual propósito o software é usado não é algo que possa ser estipulado e nem restringido.

- “A liberdade de estudar como o programa funciona e de alterá-lo para que ele compute seus dados da maneira como você deseja (liberdade 1). O acesso ao código fonte é um pré-requisito para isso.”

  Qualquer pessoa pode alterar o software de acordo com suas idéias e necessidades, o que por sua vez pressupõe que o chamado *código fonte*, ou seja, todos os arquivos que compõem um software, devem estar disponíveis em um formato legível pelos programadores. E, é claro, esse direito se aplica a um único usuário que pode querer adicionar um único recurso, mas também a empresas de software que constroem sistemas complexos, como sistemas operacionais de smartphones ou firmware de roteadores.

- “A liberdade de redistribuir cópias para que você possa ajudar os outros (liberdade 2).”

  Esta liberdade encoraja explicitamente cada usuário a compartilhar o software com outras pessoas. Trata-se, portanto, da mais ampla distribuição possível e, portanto, da maior comunidade possível de usuários e desenvolvedores que, com base nestas liberdades, desenvolvem e aprimoram ainda mais o software para o benefício de todos.

- “A liberdade de distribuir cópias de suas versões modificadas para outras pessoas (liberdade 3). Ao fazer isso, você está dando a toda a comunidade a chance de se beneficiar de suas alterações. O acesso ao código fonte é um pré-requisito para isso.”

  Não se trata apenas da distribuição de software livre, mas da distribuição de software livre *modificado*. Qualquer pessoa que fizer alterações em um software livre tem o direito de disponibilizar as alterações para outros. Se o fizer, é obrigada a fazê-lo também livremente, ou seja, não deve restringir as liberdades originais ao distribuir o software, mesmo que ele tenha sido modificado ou ampliado. Por exemplo, se um grupo de desenvolvedores tiver ideias diferentes dos criadores originais sobre a direção que um software específico deve tomar, podem criar sua própria ramificação de desenvolvimento (chamada também de *bifurcação*) e continuar a desenvolvê-lo como um novo projeto. Mas, obviamente, todas as obrigações associadas a essa liberdade continuam vigentes.

A ênfase na idéia de liberdade também é consistente com o fato de que todo movimento libertário é dirigido *contra* algo; no caso, um oponente que refuta as liberdades postuladas, considera o software como propriedade e deseja mantê-lo guardado a sete chaves. Em contraste com o software livre, esse software é chamado *proprietário*.

###### Software de Código Aberto versus Software Livre

Para muitos, *software livre* e *software de código aberto* são sinônimos. A abreviação freqüentemente usada *FOSS*, para *Software Livre e de Código Aberto* (em inglês, Free and Open Source Software), enfatiza essa aproximação. FLOSS para *Software Livre/Libre e de Código Aberto* (Free/Libre and Open Source Software) é outro termo popular, que enfatiza inequivocamente a idéia de liberdade também para outros idiomas que não o inglês. No entanto, se considerarmos a origem e o desenvolvimento de ambos os termos, vale a pena diferenciá-los.

O termo *software livre* com a definição das quatro liberdades descritas remonta a Richard Stallman e ao projeto GNU fundado por ele em 1985 — quase 10 anos antes do surgimento do Linux. O nome “GNU não é Unix” descreve a intenção com um toque de humor: o GNU começou como uma iniciativa para desenvolver uma solução tecnicamente convincente — no caso, o sistema operacional Unix — do zero, torná-la disponível para o público em geral e melhorá-la continuamente junto ao público em geral. O fato de o código fonte ser aberto representava simplesmente uma necessidade técnica e organizacional para atingir esse objetivo, mas em sua auto-imagem o movimento do software livre ainda é um movimento *social* e *político* - e, segundo certas fontes, também ideológico.

Com o sucesso do Linux, as possibilidades colaborativas da Internet e os milhares de projetos e empresas que surgiram nesse novo cosmos do software, o aspecto social cada vez mais recuou para o segundo plano. A abertura do código fonte deixou de ser um requisito técnico para se tornar uma característica determinante: quando o código fonte era visível, o software era considerado “de código aberto”. Os motivos sociais deram lugar a uma abordagem mais pragmática no desenvolvimento de software.

O software livre e o software de código aberto trabalham na mesma coisa, com os mesmos métodos e em uma comunidade global de indivíduos, projetos e empresas. Mas por serem oriundos de diferentes direções — uma social e uma pragmática-técnica — às vezes ocorrem conflitos. Eles surgem quando os resultados do trabalho conjunto não correspondem aos objetivos originais de ambos os movimentos. Isso ocorre sobretudo quando o software abre suas fontes, mas não respeita as quatro liberdades do software livre ao mesmo tempo, por exemplo quando há restrições à divulgação, à alteração ou às conexões com outros componentes do software.

A *licença* sob a qual o software é disponibilizado determina a condições a que um software está sujeito em relação ao seu uso, distribuição e modificação. E como os requisitos e motivos podem ser muito diferentes, inúmeras licenças diferentes foram criadas na área de FOSS. Devido à abordagem muito mais fundamental do movimento do software livre, não é de surpreender que ele não reconheça muitas licenças de código aberto como “livres” e, assim, as rejeite. Inversamente, esse raramente é o caso na abordagem muito mais pragmática do código aberto.

Analisamos abaixo, em poucas palavras, o intricadíssimo campo das licenças.

##### Licenças

Ao contrário de uma geladeira ou um carro, o software não é um produto *físico*, mas *digital*. Assim, uma empresa não pode de fato transferir a propriedade desse produto vendendo-o e transferindo a posse física — em vez disso, ela transfere os direitos de uso daquele produto e o usuário concorda contratualmente com esses direitos de uso. A definição do que são esses direitos de uso e, principalmente, do que eles *não* são é registrado na licença do software e, assim, é fácil entender a importância das regulações ali contidas.

Ao passo que os grandes fornecedores de software proprietário, como a Microsoft ou a SAP, têm suas próprias licenças feitas sob medida para seus produtos, os defensores do software livre e de código aberto desde o início buscaram a clareza e a universalidade em suas licenças, já que, afinal, todo usuário deve poder compreendê-las e, se necessário, usá-las ele próprio para seus próprios desenvolvimentos.

No entanto, não se deve esconder que esse ideal de simplicidade dificilmente pode ser alcançado, pois é preciso enfrentar demasiados requisitos específicos e entendimentos legais nem sempre compatíveis internacionalmente. Para dar apenas um exemplo: a legislação alemã e a americana são fundamentalmente diferentes em matéria de direitos autorais. De acordo com a legislação alemã, existe uma *pessoa* como *autor* (mais precisamente: *Urheber*), cuja obra é sua *propriedade* *intelectual*. Embora o autor possa autorizar a utilização da sua obra, ele não pode atribuir ou renunciar à sua autoria. Esta última especificidade não existe na legislação americana. Também aqui existe um autor (que, porém, também pode ser uma empresa ou instituição), mas ele só possui os direitos de exploração, os quais podem ser transferidos totalmente ou em parte, possibilitando que o autor se dissocie completamente de sua obra. Uma licença válida internacionalmente precisa ser interpretada levando-se em conta as diferentes legislações.

Como consequência, existem muitas licenças FOSS que, frequentemente, são bem diferentes. Pior ainda são as diferentes versões de uma mesma licença, ou ainda uma mistura de licenças (dentro de um projeto, ou até ao se conectar vários projetos), que podem causar confusão ou mesmo disputas legais.

Tanto os representantes do software livre quanto os defensores do movimento de código aberto (que tem uma orientação predominantemente econômica) criaram suas próprias organizações, que hoje são decisivamente responsáveis pela formulação das licenças de software de acordo com seus princípios e apoiam seus membros em sua aplicação.

###### Copyleft

A já mencionada *Free Software Foundation* (FSF) formulou a *GNU General Public License* (GPL), uma das mais importantes licenças de software livre, usada por muitos projetos, como o kernel do Linux. Além disso, ela lançou licenças que podem ser personalizadas para um determinado projeto, como a *GNU Lesser General Public License* (LGPL), que rege a combinação de software livre com modificações cujo código-fonte não precisa ser divulgada ao público, a *GNU Affero* *General Public License* (AGPL), que cobre a venda de acesso a software hospedado, ou a *GNU Free* *Documentation License* (FDL), que estende os princípios da liberdade à documentação do software. Além disso, a FSF faz recomendações pró ou contra licenças de terceiros, e projetos afiliados como o GPL-Violations.org investigam suspeitas de violação de licenças livres.

A FSF chama o princípio segundo o qual uma licença livre também se aplica a variantes modificadas do software de *copyleft* — em contraste com o princípio de direitos autorais restritivos que ela rejeita. A idéia, portanto, é transferir os princípios generosos de uma licença de software da forma mais irrestrita possível para futuras variantes do software, a fim de evitar restrições subseqüentes.

O que parece óbvio e simples, no entanto, leva a complicações consideráveis na prática, razão pela qual os críticos muitas vezes chamam o princípio copyleft de “viral”, já que ele é transmitido para as versões posteriores.

Do que foi dito, pode-se depreender, por exemplo, que dois componentes de software licenciados sob diferentes licenças copyleft podem não ser combináveis entre si, uma vez que ambas as licenças não podem ser transferidas para o produto subsequente ao mesmo tempo. Isso pode se aplicar até mesmo a versões diferentes da mesma licença!

Por essa razão, as licenças ou versões de licenças mais recentes já não abraçam o copyleft com tanto rigor. A já mencionada *GNU Lesser General Public License* (LGPL) é, nesse sentido, uma concessão que permite conectar software livre com componentes “não livres”, como ocorre freqüentemente com as chamadas *bibliotecas*. As bibliotecas contêm subrotinas ou rotinas, que por sua vez são usadas por vários outros programas. Isso leva à situação comum na qual um software proprietário faz apelo à subrotina de uma biblioteca livre.

Outro modo de evitar conflitos de licença é a *licença dual*, na qual um software é licenciado sob diferentes licenças, por exemplo uma licença livre e uma licença proprietária. Um caso típico de uso é uma versão livre de um software que só pode ser usado quando se respeitam as restrições de copyleft e a alternativa de se adquirir o software sob uma licença diferente, que libera o licenciado de certas restrições em troca de uma taxa que pode ser usada para financiar o desenvolvimento do software.

Portanto, deve ficar claro que a escolha da licença para projetos de software deve ser feita com muita cautela, uma vez que a cooperação com outros projetos, a possibilidade de combinação com outros componentes e também o design futuro do próprio produto dependem disso. O copyleft apresenta desafios especiais aos desenvolvedores nesse aspecto.

###### Definição de Código Aberto e licenças permissivas

Do lado do código aberto, é principalmente a *Open Source Initiative* (OSI), fundada em 1998 por Eric S. Raymond e Bruce Perens, que trata das questões de licenciamento. Ela também desenvolveu um procedimento padronizado para verificar as licenças de software quanto à conformidade com sua *Definição de Código Aberto*. Atualmente, mais de 80 licenças reconhecidas de código aberto podem ser encontradas no site da OSI.

Há também licenças como a “OSI-approved”, que contradizem explicitamente o princípio do copyleft, especialmente o grupo de *licenças BSD*. O *Berkeley Software Distribution* (BSD) é uma variante do sistema operacional Unix originalmente desenvolvido na Universidade de Berkeley, que mais tarde deu origem a projetos livres como *NetBSD*, *FreeBSD* e *OpenBSD*. As licenças subjacentes a esses projetos são freqüentemente consideradas *permissivas*. Em contraste com as licenças copyleft, elas não têm o objetivo de estabelecer os termos de uso das variantes modificadas. Em vez disso, a liberdade irrestrita tem o papel de ajudar o software a ser tão amplamente distribuído quanto possível, concedendo aos seus editores o poder único de decisão sobre o que fazer com as edições — se, por exemplo, elas também serão lançadas ou se serão tratadas como produtos de código fechado e distribuídas comercialmente.

A *Licença BSD de 2 Cláusulas*, também chamada *Licença BSD Simplificada* ou *Licença FreeBSD*, demonstra o quanto essas licenças permissivas podem ser sucintas. Além da cláusula padrão de responsabilidade, que protege os desenvolvedores contra pedidos de indenização decorrentes de danos causados pelo software, a licença consiste apenas nas duas regras a seguir:

Redistribuição e uso em formas fonte e binária, com ou sem modificação, são permitidos desde que as seguintes condições sejam atendidas:

1. Redistribuições de código fonte devem manter o aviso de direitos autorais acima, esta lista de condições e o seguinte aviso legal.

2. Redistribuições em forma binária devem reproduzir o aviso de direitos autorais acima, esta lista de condições e o seguinte aviso legal na documentação e/ou outros materiais fornecidos com a distribuição.

###### Creative Commons

O bem-sucedido conceito de desenvolvimento do FLOSS e o progresso tecnológico associado levaram a tentativas de transferir o princípio do código aberto para outras áreas não técnicas. A preparação e a disponibilização de conhecimentos, bem como a cooperação criativa na resolução de tarefas complexas, são agora considerados como prova do princípio do código aberto, ampliado e relacionado ao conteúdo.

Isso levou à necessidade de criar bases sólidas igualmente nessas áreas, permitindo que os resultados do trabalho pudessem ser compartilhados e processados. Como as licenças de software disponíveis não eram adequadas a isso, houve inúmeras tentativas de converter em licenças igualmente úteis os requisitos específicos de áreas que vão desde a produção científica até obras de arte digitalizadas “no espírito do código aberto”.

Atualmente, a iniciativa mais importante desse tipo é de longe a *Creative Commons* (CC), que resume as suas preocupações da seguinte forma:

A Creative Commons é uma organização global sem fins lucrativos que permite o compartilhamento e a reutilização da criatividade e do conhecimento através da disponibilização de ferramentas legais gratuitas.

> — https://creativecommons.org/faq/#what-is-creative-commons-and-what-do-you-do

Com a Creative Commons, o foco da atribuição de direitos deixa de ser o distribuidor e volta a ser o autor. Um exemplo: no processo editorial tradicional, um autor normalmente transfere todos os direitos de publicação (impressão, tradução etc.) para um editor, que por sua vez assegura a melhor distribuição possível da obra. Atualmente, os novos canais de distribuição possibilitados pela internet colocam o autor em posição de exercer ele próprio muitos desses direitos editoriais e de decidir por si mesmo como seu trabalho pode ser utilizado. A Creative Commons oferece a oportunidade de determinar isso de forma simples e legalmente confiável, mas ela quer mais: os autores são encorajados a tornar suas obras disponíveis como contribuição para um processo generalizado de troca e cooperação. Ao contrário do copyright tradicional, que dá ao autor todos os direitos que ele pode transferir para outras pessoas caso necessário, a Creative Commons adota a postura oposta: o autor disponibiliza sua obra à comunidade, mas pode escolher, dentre vários aspectos, aqueles que precisam ser levados em consideração quando a obra for utilizada — quanto mais aspectos forem escolhidos, mais restritiva será a licença.

E assim, o princípio “Escolha uma Licença” da CC pede que o autor defina passo a passo as propriedades individuais para gerar a licença recomendada, que o autor pode então incorporar à sua obra na forma de texto e ícone.

Para entender melhor, eis uma visão geral das seis possíveis combinações e licenças oferecidas pela CC:

- **CC BY (“Atribuição”)**: A licença livre que permite a qualquer pessoa editar e distribuir a obra, desde que cite o autor.
- **CC BY-SA (“Atribuição-CompartilhaIgual”)**: Como a CC BY, exceto porque a obra modificada só pode ser distribuída sob a mesma licença. O princípio do copyleft permanece, porque a licença também é “herdada” aqui.
- **CC BY-ND (“Atribuição-SemDerivações”)**: Como a CC BY, exceto porque a obra só pode ser repassada sem modificações.
- **CC BY-NC (“Atribuição-NãoComercial”)**: A obra pode ser editada e distribuída com citação do autor, mas somente para fins não comerciais.
- **CC BY-NC-SA (“Atribuição-NãoComercial-CompartilhaIgual”)**: Como a BY-NC, exceto porque a obra só pode ser compartilhada sob as mesmas condições (ou seja, uma licença semelhante à copyleft).
- **CC BY-NC-ND (“Atribuição-NãoComercial-SemDerivações”)**: A licença mais restritiva de todas: a distribuição da obra é permitida com citação do autor, mas somente inalterada e para fins não comerciais.

##### Modelos de negócios em Open Source

Em retrospectiva, o trunfo da FLOSS é representar um movimento popular de tecnófilos idealistas que, livres de restrições econômicas e dependências monetárias, põem seu trabalho a serviço do público em geral. Ao mesmo tempo, empresas que valem bilhões foram criadas no ambiente FLOSS; poderíamos citar como exemplo a empresa americana *Red Hat*, fundada em 1993 com vendas anuais de mais de 3 bilhões de dólares (2018) e assumida pela gigante de TI IBM em 2018.

Então, vamos dar uma olhada na tensão entre a distribuição livre e quase sempre gratuita de software de alta qualidade e os modelos de negócios para seus criadores, porque uma coisa deve ficar clara: os inúmeros desenvolvedores altamente qualificados de software livre também precisam ganhar dinheiro, e o ambiente FLOSS original, puramente não-comercial, deve, portanto, desenvolver modelos de negócios sustentáveis para preservar seu próprio cosmos.

Uma abordagem comum, especialmente em projetos maiores em fase inicial, é o chamado *crowdfunding*, ou seja, a coleta de doações monetárias através de uma plataforma como o *Kickstarter*. Em troca, os doadores recebem um bônus predefinido dos desenvolvedores no caso de sucesso, ou seja, se os objetivos previamente definidos forem alcançados, seja um acesso ilimitado ao produto ou recursos exclusivos.

Outra abordagem é a *licença dual*: o software livre é oferecido em paralelo sob uma licença mais restritiva ou mesmo proprietária, o que por sua vez garante ao cliente serviços mais extensos (tempos de resposta em caso de erros, atualizações, versões para certas plataformas etc.). Um exemplo dentre muitos é o *ownCloud*, que está sendo desenvolvido sob a GPL e oferece aos clientes empresariais uma “Business Edition” sob uma licença proprietária.

Tomemos também o ownCloud como exemplo de outro modelo de negócio amplamente difundido de FLOSS: serviços profissionais. Muitas empresas carecem do conhecimento técnico interno necessário para configurar e operar softwares complexos e críticos de forma confiável e, sobretudo, segura. Assim, elas contratam serviços profissionais, como consultoria, manutenção ou assistência técnica, diretamente do fabricante. As questões de responsabilidade também têm seu papel nessa decisão, já que a empresa transfere os riscos da operação para o fabricante.

Se um software consegue se tornar bem-sucedido e popular em seu campo, existem possibilidades periféricas de monetização, como o merchandising ou certificados adquiridos pelos clientes para indicar seu status especial no uso daquele software. A plataforma de aprendizagem *Moodle* oferece a certificação de instrutores, oficializando seus conhecimentos para clientes potenciais, por exemplo, e este é apenas um exemplo dentre inúmeros outros.

O *Software como Serviço* (Software as a Service ou SaaS) é outro modelo de negócios, especialmente para tecnologias baseadas na web. Aqui, um provedor de nuvem executa um software como uma Gestão de Relacionamento com o Cliente (Customer Relationship Management ou CRM) ou um Sistema de Gerenciamento de Conteúdo (Content Management System ou CMS) em seus servidores e oferece aos seus clientes acesso ao aplicativo instalado. Isso evita que o cliente precise se preocupar com a instalação e a manutenção do software. Em contrapartida, o cliente paga pelo uso do software de acordo com diversos parâmetros, como por exemplo o número de usuários. A disponibilidade e a segurança têm um papel importante, sendo fatores críticos no mundo empresarial.

Por último, mas não menos importante, o modelo de desenvolvimento por encomenda de extensões específicas em software livre para um cliente é particularmente comum em projetos menores. Normalmente, cabe ao cliente decidir o que fazer com essas extensões, ou seja, se ele também as libera ou se as mantêm privadas como parte de seu próprio modelo de negócios.

Uma coisa deve ficar clara: embora o software livre esteja geralmente disponível gratuitamente, muitos modelos de negócios foram criados nesse ambiente, e eles são constantemente modificados e ampliados por inúmeros freelancers e empresas em todo o mundo de maneira muito criativa, o que, em última análise, também garante a continuidade da existência de todo o movimento FLOSS.

#### Exercícios Guiados

1. Quais são — de forma resumida — as “quatro liberdades” definidas por Richard Stallman e a Free Software Foundation?

  liberdade 0

  liberdade 1

  liberdade 2

  liberdade 3

2. O que significa a abreviatura FLOSS?

3. Você desenvolveu um software livre e quer garantir que o software em si, mas também todas as futuras criações que se baseiem nele, também sejam livres. Qual licença deve escolher?

  CC BY

  GPL versão 3

  Licença BSD de 2 Cláusulas

  LGPL

4. Quais das seguintes licenças você considera permissivas e quais considera copyleft?

  Licença BSD Simplificada

  GPL versão 3

  CC BY

  CC BY-SA

5. Você escreveu um aplicativo web e o publicou sob uma licença livre. Como você pode ganhar dinheiro com seu produto? Cite três possibilidades.

#### Exercícios Exploratórios

1. Sob qual licença (incluindo a versão) estão disponíveis os seguintes aplicativos?

  Apache HTTP Server

  MySQL Community Server

  Artigos da Wikipedia

  Mozilla Firefox

  GIMP

2. Você deseja publicar seu software sob a GNU GPL v3. Qual o procedimento a seguir?

3. Você escreveu software proprietário e gostaria de combiná-lo com software livre sob a GPL versão 3. Existe essa possibilidade? O que deve ser levado em conta?

4. Por que a Free Software Foundation lançou a *GNU Affero General Public License* (GNU AGPL) como suplemento à GNU GPL?

5. Dê três exemplos de software livre que também é oferecido em “Edição Empresarial”, ou seja, em versão paga.

#### Sumário

Nesta lição você aprendeu:

- Semelhanças e diferenças entre software livre e de código aberto (FLOSS)
- Licenças FLOSS, sua importância e problemas
- Copyleft versus licenças permissivas
- Modelos de negócio FLOSS

#### Respostas aos Exercícios Guiados

1. Quais são — de forma resumida — as “quatro liberdades” definidas por Richard Stallman e a Free Software Foundation?

| liberdade 0 | executar o software |
|---|---|
| liberdade 1 | estudar e modificar o software (código fonte) |
| liberdade 2 | distribuir o software |
| liberdade 3 | distribuir o software modificado |

2. O que significa a abreviatura FLOSS?

  Free/Libre Open Source Software

3. Você desenvolveu um software livre e quer garantir que o software em si, mas também todas as futuras criações que se baseiem nele, também sejam livres. Qual licença deve escolher?

| CC BY |  |
|---|---|
| GPL versão 3 | X |
| Licença BSD de 2 Cláusulas |  |
| LGPL |  |

4. Quais das seguintes licenças você considera permissivas e quais considera copyleft?

| Licença BSD Simplificada | permissiva |
|---|---|
| GPL versão 3 | copyleft |
| CC BY | permissiva |
| CC BY-SA | copyleft |

5. Você escreveu um aplicativo web e o publicou sob uma licença livre. Como você pode ganhar dinheiro com seu produto? Cite três possibilidades.

  - Licença dual, ou seja, oferecendo uma “Edição Empresarial” paga
  - Oferecendo hospedagem, serviços e suporte
  - Desenvolvendo extensões proprietárias para os clientes

#### Respostas aos Exercícios Exploratórios

1. Sob qual licença (incluindo a versão) estão disponíveis os seguintes aplicativos?

| Apache HTTP Server | Apache License 2.0 |
|---|---|
| MySQL Community Server | GPL 2 |
| Wikipedia articles (English) | Creative Commons Attribution Share-Alike license (CC-BY-SA) |
| Mozilla Firefox | Mozilla Public License 2.0 |
| GIMP | GPL 3 |

2. Você deseja publicar seu software sob a GNU GPL v3. Qual o procedimento a seguir?

  - Se necessário, proteger-se contra o empregador com uma renúncia aos direitos autorais, por exemplo, para poder especificar a licença.
  - Adicionar um aviso de direitos autorais a cada arquivo.
  - Adicionar um arquivo chamado `COPYING` com o texto completo da licença de seu software.
  - Adicionar uma referência à licença a cada arquivo.

3. Você escreveu software proprietário e gostaria de combiná-lo com software livre sob a GPL versão 3. Existe essa possibilidade? O que deve ser levado em conta?

  As Questões Frequentes da Free Software Foundation trazem essa informação: Desde que seu software proprietário e o software livre permaneçam separados, a combinação é possível. Porém, você deve garantir que essa separação seja tecnicamente assegurada e reconhecível pelos usuários. Se você integrar o software livre de tal maneira que ele se torne parte integrante de seu produto, deve publicar também o produto sob a GPL de acordo com o princípio do copyleft.

4. Por que a Free Software Foundation lançou a *GNU Affero General Public License* (GNU AGPL) como suplemento à GNU GPL?

  A GNU AGPL vem preencher uma lacuna de licenciamento que ocorre especialmente com software livre hospedado em um servidor: se um desenvolvedor fizer alterações no software, ele não é obrigado, sob a GPL, a tornar essas alterações acessíveis, já que ele permite acesso ao programa, mas não “redistribui” o programa no sentido definido pela GPL. A GNU AGPL, por outro lado, estipula que o software deve ser disponibilizado para download com todas as alterações.

5. Dê três exemplos de software livre que também é oferecido em “Edição Empresarial”, ou seja, em versão paga.

  MySQL, Zammad, Nextcloud

## 1.4 ICT Habilidades ICT e trabalhando no Linux

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 1.4
- **Peso**: 2

**Áreas chave de conhecimento**

- Habilidades no Desktop
- Chegando à linha de comando
- Usos industriais para Linux, computação em nuvem e virtualização

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- Usando um navegador, questões de privacidade, opções de configuração, procurando na web e salvando conteúdo
- Terminal e Console
- Senhas
- Questões e ferramentas relacionadas à privacidade
- Uso de aplicações Open Source populares em apresentações e projetos

### 1.4 Lição 1

#### Introdução

Houve um tempo em que trabalhar com Linux no desktop era considerado difícil, já que o sistema carecia de muitos dos aplicativos e ferramentas de configuração mais elaborados oferecidos por outros sistemas operacionais. Dito isso, era mais simples começar pelo desenvolvimento dos aplicativos mais essenciais em linha de comando e deixar as ferramentas gráficas mais complexas para mais tarde. No início, como o Linux foi inicialmente pensado para usuários mais avançados, isso não era um grande problema. Mas esses dias terminaram. Hoje em dia, os ambientes de desktop Linux estão bem mais maduros, não deixando nada a desejar no que diz respeito aos recursos e à facilidade de uso. Ainda assim, a linha de comando ainda é considerada uma ferramenta poderosa, empregada diariamente pelos usuários avançados. Nesta lição, vamos apresentar alguns conhecimentos básicos de desktop necessários para você saber escolher a melhor ferramenta para cada tarefa, começando com o acesso à linha de comando.

##### Interfaces de usuário Linux

Ao usar um sistema Linux, você interage com uma linha de comando ou com interfaces gráficas de usuário. Ambas as opções oferecem acesso a diversos aplicativos capazes de executar praticamente qualquer tarefa no computador. Embora o objetivo 1.2 já tenha apresentado uma série de aplicativos comumente usados, vamos começar esta lição com um olhar mais atento para os ambientes desktop, as formas de acessar o terminal e as ferramentas usadas para apresentações e gerenciamento de projetos.

###### Ambientes desktop

A abordagem do Linux é modular, ou seja, diferentes partes do sistema são desenvolvidas por diferentes projetos e desenvolvedores, que dão conta de uma necessidade ou de um objetivo específico. Por essa razão, existem várias opções de ambientes desktop para escolher, bem como diversos gerenciadores de pacotes, e por isso o ambiente desktop padrão pode variar bastante entre as muitas distribuições existentes. Ao contrário dos sistemas operacionais proprietários, como Windows e MacOS, nos quais os usuários ficam restritos ao ambiente desktop que vem com o SO, existe a possibilidade de se instalar diversos ambientes e escolher aquele que mais se adapta a você e a suas necessidades.

Basicamente, existem dois ambientes de trabalho principais no mundo Linux: *Gnome* e *KDE*. Ambos são bem completos, contam com uma grande comunidade e visam o mesmo propósito, mas com abordagens ligeiramente divergentes. Para resumir, o Gnome busca seguir o princípio KISS (“keep it simple stupid”, ou “mantenha simples, estúpido”, em português), com aplicações simplificadas e limpas. Por sua vez, o KDE tem outra perspectiva, oferecendo um leque maior de aplicativos e oferecendo ao usuário a possibilidade de alterar cada uma das configurações do ambiente.

Enquanto os aplicativos Gnome baseiam-se no kit de ferramentas GTK (escrito na linguagem C), os aplicativos KDE utilizam a biblioteca Qt (escrita em C++). Um dos aspectos mais práticos de se escrever programas usando o mesmo kit de ferramentas gráficas é que eles ficam com uma aparência e usabilidade semelhantes, o que proporciona um sentido de coesão ao usuário durante sua experiência. Outra característica importante é que, quando empregamos a mesma biblioteca gráfica compartilhada em diversos aplicativos de uso frequente, economizamos espaço na memória, além de reduzirmos o tempo de carregamento depois de a biblioteca ter sido carregada pela primeira vez.

###### Como abrir a linha de comando

Para nós, um dos aplicativos mais importantes é o emulador de terminal gráfico. São chamados de emuladores de terminal porque realmente emulam, em um ambiente gráfico, os antigos terminais seriais (muitas vezes máquinas de teletipo) que eram na verdade clientes conectados a uma máquina remota na qual a computação acontecia de fato. Essas máquinas eram, na verdade, computadores muito simples e sem gráficos, usados nas primeiras versões do Unix.

No Gnome, esse aplicativo se chama *Gnome Terminal*, enquanto no KDE ele é conhecido como *Konsole*. Mas há muitas outras opções disponíveis, tais como o *Xterm*. Estes aplicativos são uma forma de termos acesso a um ambiente de linha de comando e, assim, podermos interagir com um shell.

Assim, procure o aplicativo de terminal no menu de programas da distribuição de sua escolha. Tirando pequenas diferenças entre eles, todos esses aplicativos oferecem o necessário para você ganhar confiança no uso da linha de comando.

Outra maneira de entrar no terminal é usar o TTY virtual. Para encontrá-lo, pressione `Ctrl` + `Alt` + `F#` . Leia `F#` como uma das teclas de função de 1 a 7, por exemplo. É provável que algumas das combinações iniciais estejam associadas ao gerenciador de sessão ou ao ambiente gráfico. As outras irão exibir um prompt pedindo seu nome de login, como no exemplo abaixo:

```
Ubuntu 18.10 arrelia tty3
arrelia login:
```

O `arrelia`, neste caso, é o hostname da máquina, e `tty3` é o terminal disponível a partir da combinação de teclas descrita acima, mais a tecla `F3` , como em `Ctrl` + `Alt` + `F3` .

Depois de inserir seu login e senha, você finalmente entrará em um terminal, mas sem nenhum ambiente gráfico, de modo que não será possível usar o mouse ou executar aplicações gráficas sem antes iniciar uma sessão X, ou Wayland. Mas isso está além do escopo desta lição.

###### Apresentações e projetos

A ferramenta mais importante para apresentações no Linux é o *LibreOffice Impress*. Ele faz parte do pacote de escritório *LibreOffice*. Pense no LibreOffice como um substituto de código aberto para o *Microsoft Office*. Ele pode inclusive abrir e salvar arquivos PPT e PPTX, nativos do *Powerpoint*. Mas apesar disso, é recomendável dar preferência ao formato nativo ODP Impress. O ODP é parte do *Open Document Format*, um padrão internacional para esse tipo de arquivo. Isso é especialmente importante se você deseja manter seu documento acessível por muitos anos sem se preocupar com problemas de compatibilidade. Por se tratar de um padrão aberto, qualquer pessoa pode implementar esse formato sem pagar royalties ou licenças. Isso também permite que você possa experimentar outros softwares de apresentação sem perder o acesso aos seus arquivos, já que há grande probabilidade de que eles sejam compatíveis com programas mais recentes.

Mas se você prefere código em vez de interfaces gráficas, tem um punhado de ferramentas à escolha. O *Beamer* é uma classe *LaTeX* capaz de criar apresentações de slides a partir de código LaTeX. O LaTeX em si é um sistema de composição de texto amplamente utilizado para escrever documentos científicos acadêmicos, sobretudo por sua capacidade de lidar com símbolos matemáticos complexos, que causam dificuldades para outros softwares. Se você está na universidade e precisa lidar com equações e outros problemas relacionados à matemática, o Beamer pode lhe poupar um tempo precioso.

A outra opção é o *Reveal.js*, um incrível pacote NPM (NPM é o gerenciador de pacotes padrão do NodeJS) que permite criar belas apresentações usando a web. Assim, se você entende de HTML e CSS, o Reveal.js contribuirá com a maior parte do JavaScript necessário para criar apresentações bonitas e interativas que se adaptam bem a qualquer resolução e tamanho de tela.

Por fim, se você procura um substituto para o *Microsoft Project*, sugerimos o *GanttProject* ou o *ProjectLibre*. Ambos são muito semelhantes ao seu equivalente proprietário e compatíveis com arquivos do Project.

##### Usos do Linux na indústria

O Linux é muito utilizado nas indústrias de software e internet. Sites como W3Techs relatam que cerca de 68% dos servidores de websites na Internet são alimentados por Unix, a maioria deles com Linux.

Essa grande proporção se deve não somente à natureza livre do Linux (tanto no sentido de grátis quanto no de liberdade de expressão), mas também por sua estabilidade, flexibilidade e desempenho. Essas características permitem que os fornecedores ofereçam seus serviços com menor custo e maior escalabilidade. Uma porção significativa dos sistemas Linux atualmente é executada na nuvem, seja no modelo IaaS (Infraestrutura como Serviço), PaaS (Plataforma como Serviço) ou SaaS (Software como Serviço).

O IaaS é uma maneira de compartilhar os recursos de um grande servidor oferecendo acesso a máquinas virtuais que são, na verdade, múltiplos sistemas operacionais rodando como convidados em uma máquina hospedeira sobre um importante software chamado *hipervisor*. O hipervisor é responsável por permitir que os SOs convidados possam rodar, segregando e gerenciando os recursos disponíveis na máquina hospedeira para esses convidados. Isso é o que nós chamamos *virtualização*. No modelo IaaS, você paga apenas pela fração de recursos usados por sua infraestrutura.

O Linux tem três hipervisores de código aberto bastante conhecidos: *Xen*, *KVM* e *VirtualBox*. O Xen é provavelmente o mais antigo deles. O KVM superou o Xen como o hipervisor Linux mais relevante. Seu desenvolvimento é patrocinado pela RedHat e ele é usado também por outros atores da indústria, tanto em serviços de nuvem pública quanto em configurações de nuvem privada. O VirtualBox pertence à Oracle desde que esta adquiriu a Sun Microsystems e é geralmente escolhido pelos usuários finais devido à sua facilidade de uso e de administração.

Já o PaaS e o SaaS incrementam o modelo IaaS, tanto tecnicamente quanto conceitualmente. No PaaS, em vez de uma máquina virtual, os usuários têm acesso a uma plataforma na qual é possível implantar e executar seu aplicativo. A ideia é aliviar a carga de se lidar com tarefas de administração de sistema e atualizações de sistema operacional. O Heroku é um exemplo comum de PaaS no qual o código do programa pode ser simplesmente executado sem que seja preciso cuidar dos containers subjacentes e máquinas virtuais.

E finalmente, o SaaS é o modelo em que geralmente se paga por uma assinatura para simplesmente usar um software sem se preocupar com mais nada. O\_Dropbox\_ e o *Salesforce* são dois bons exemplos de SaaS. A maioria desses serviços é acessada através de um navegador web.

Um projeto como o *OpenStack* é uma coleção de software de código aberto que pode fazer uso de diferentes hipervisores e outras ferramentas a fim de oferecer um ambiente de nuvem IaaS completo no local, aproveitando o poder do cluster de computadores em seu próprio centro de processamento de dados. No entanto, a configuração dessa infraestrutura não é uma tarefa trivial.

##### Problemas de privacidade ao se usar a internet

O navegador web é um programa fundamental em qualquer desktop de nossa época, mas algumas pessoas ainda não sabem como utilizá-los de maneira segura. Embora mais e mais serviços sejam acessados através de um navegador, quase todas as ações feitas no navegador são rastreadas e analisadas por diferentes intermediários. Proteger o acesso aos serviços de Internet e evitar o rastreamento são aspectos importantes para um uso seguro da Internet.

###### Rastreamento de cookies

Vamos supor que você visitou uma loja virtual, selecionou um produto que queria e o colocou em seu carrinho. Mas, no último segundo, decidiu tirar um tempo para refletir e decidir se realmente precisava daquilo. Depois de um tempinho, você começa a ver anúncios daquele mesmo produto em todos os cantos da web. Ao clicar nesses anúncios, você é imediatamente encaminhado à página do produto naquela mesma loja. Não é incomum que os produtos colocados no carrinho ainda estejam lá, esperando que você se decida a adquiri-los. Já se perguntou como eles fazem isso? Como mostram o anúncio certo em outra página web? A resposta a essas questões está no *rastreamento de cookies*.

Os Cookies são pequenos arquivos que um site pode salvar em seu computador para armazenar e recuperar algum tipo de informação que possa ser útil em sua navegação. Eles existem há muitos anos e são uma das maneiras mais antigas de armazenar dados no lado do cliente. Um bom exemplo de seu uso são as identidades únicas para os carrinhos de compras. Dessa forma, se você voltar ao mesmo site em poucos dias, a loja pode lembrar-lhe os produtos que você colocou em seu carrinho durante a última visita e poupar-lhe o tempo de procurá-los novamente.

Até aí tudo bem, já que o site está oferecendo um recurso útil e não compartilhando seus dados com terceiros. Mas e quanto aos anúncios exibidos enquanto você navega em outras páginas da web? É aí que entram as redes de anúncios. As redes de anúncios são empresas que oferecem anúncios para lojas virtuais como a do nosso exemplo, de um lado, e monetização para websites, do outro. Os criadores de conteúdo, como blogueiros, por exemplo, podem disponibilizar espaço para essas redes de anúncios em seu blog em troca de uma comissão relacionada às vendas geradas pelo anúncio.

Mas como eles sabem qual produto exibir no anúncio? Isso normalmente é feito com um cookie da rede de anúncios que também é salvo no momento em que você visitou ou buscou um produto determinado na loja virtual. Ao fazer isso, a rede consegue recuperar as informações desse cookie nos sites em que a rede anuncia, fazendo a correlação com os produtos em que você se mostrou interessado. Essa é uma das maneiras mais comuns de se rastrear alguém pela Internet. Usamos o exemplo de uma loja online para dar uma explicação mais tangível, mas as plataformas de mídia social fazem o mesmo com seus botões de “Curtir” ou “Compartilhar”.

Uma maneira de se livrar desse efeito é não permitir que sites de terceiros armazenem cookies em seu navegador. Dessa forma, somente o site que você visita pode armazenar seus cookies. Mas esteja ciente de que alguns recursos “legítimos” podem não funcionar bem se você fizer isso, já que muitos sites atualmente dependem de serviços de terceiros para funcionar. Então, você pode procurar por um gerenciador de cookies no repositório de complementos do seu navegador, a fim de ter um controle fino sobre os cookies que serão armazenados em sua máquina.

###### Não Rastrear (DNT)

Outro equívoco comum está relacionado a uma determinada configuração de browser conhecida como DNT. Esse é um acrônimo de “Do Not Track” (Não Rastrear) e pode ser ativado basicamente em qualquer navegador atual. Como no caso do modo privado, não é difícil encontrar pessoas que acreditam que não serão rastreadas se ativarem essa configuração. Infelizmente, isso nem sempre é verdade. Atualmente, o DNT é apenas uma forma de dizer aos websites visitados que você não quer que eles o rastreiem, mas na verdade são eles que vão decidir se vão respeitar sua escolha ou não. Em outras palavras, o DNT é uma maneira de pedir para ser excluído do rastreamento dos websites, mas não há garantia de que esse pedido será atendido.

Tecnicamente, isso é feito simplesmente emitindo uma flag extra no cabeçalho do protocolo da requisição HTTP (`DNT: 1`) ao se requisitar dados de um servidor web. Se quiser saber mais sobre este tópico, o site https://allaboutdnt.com é um bom ponto de partida.

###### Janelas “anônimas”

Você deve ter notado as aspas no título acima. Isso porque essas janelas não são tão anônimas quanto a maioria das pessoas pensa. Os nomes podem variar: elas podem ser chamadas de “modo privado”, “incógnito” ou “anônimo”, dependendo do navegador que você estiver usando.

No Firefox, é fácil ativar esse modo pressionando as teclas `Ctrl` + `Shift` + `P` . No Chrome, basta pressionar `Ctrl` + `Shift` + `N` . O que ele realmente faz é abrir uma nova sessão, a qual normalmente não compartilha nenhuma configuração ou dados do seu perfil padrão. Quando você fecha a janela privada, o navegador exclui automaticamente todos os dados gerados por essa sessão, não deixando vestígios no computador usado. Assim, nenhum dado pessoal, como histórico, senhas ou cookies, serão armazenados nesse computador.

Porém, muita gente interpreta erroneamente esse conceito, acreditando que é possível navegar na internet de forma anônima, o que não é inteiramente verdade. Uma das coisas que o modo privado ou incógnito faz é evitar aquilo que chamamos de rastreamento de cookies. Quando você visita um site, ele pode armazenar um pequeno arquivo em seu computador contendo um identificador que pode ser usado para rastreá-lo. A menos que você configure seu navegador para não aceitar cookies de terceiros, as redes de anúncios ou outras empresas podem armazenar e recuperar esse identificador e rastrear sua navegação na web. Mas como os cookies armazenados em uma sessão de modo privado são excluídos logo após o encerramento da sessão, essas informações são perdidas para sempre.

Além disso, os sites e outros agentes da internet ainda podem usar muitas outras técnicas para rastrear suas atividades. Portanto, o modo privado permite um certo nível de anonimato, mas é completamente privado apenas no computador que está sendo utilizado. Se você precisa acessar sua conta de email ou site bancário a partir de um computador público, por exemplo em um aeroporto ou hotel, não deve deixar de utilizar o modo privado do navegador. Em outras situações, pode haver benefícios, mas é preciso saber exatamente quais riscos estão sendo evitados e quais permanecem. Sempre que utilizar um computador acessível ao público, esteja ciente de que outras ameaças à segurança, como malware ou keyloggers, podem estar presentes. Seja prudente sempre que inserir informações pessoais, como nomes de usuário e senhas, nesses computadores, ou quando baixar ou copiar dados confidenciais.

###### Escolha a senha certa

Uma das situações mais difíceis enfrentadas por um usuário é ter de escolher uma senha segura para os serviços que utiliza. Você certamente já ouviu dizer que não se deve usar combinações comuns como `qwerty`, `123456` ou `654321`, nem números fáceis de adivinhar como seu aniversário (ou de um parente) ou código postal. A razão para isso é que essas combinações são muito óbvias, certamente as primeiras que um invasor vai experimentar a fim de ganhar acesso à sua conta.

Existem técnicas conhecidas para criar uma senha segura. Uma das mais famosas é inventar uma frase que lembre aquele serviço e pegar as primeiras letras de cada palavra. Vamos supor que eu quero criar uma boa senha para o Facebook, por exemplo. Nesse caso, eu poderia criar uma frase como "Eu ficaria feliz se tivesse 1000 amigos como o Claudemir". Pegamos a primeira letra de cada palavra e a senha final seria "Effst1000acoC". Isso resultaria em uma senha de 13 caracteres, longa o suficiente para ser difícil de adivinhar e, ao mesmo tempo, fácil de decorar (desde que eu seja capaz de me lembrar da frase e do “algoritmo” para recuperar a senha).

Frases são mais fáceis de lembrar do que senhas, mas até esse método tem suas limitações. Temos de criar senhas para uma porção de serviços hoje em dia, e como as usamos com frequências diferentes, acaba ficando muito difícil lembrar de todas as frases no momento em que precisamos delas. Então, o que podemos fazer? Você pode responder que a coisa mais sábia a fazer neste caso é criar um punhado de boas senhas e reutilizá-las em serviços similares, certo?

Infelizmente, essa também não é uma boa ideia. Você provavelmente também já ouviu dizer que não deve reutilizar a mesma senha para diferentes serviços. O problema de se fazer isso é que um serviço específico pode vazar sua senha (sim, acontece bastante) e qualquer pessoa que tenha acesso a ela tentará usar a mesma combinação de email e senha em outros serviços populares da Internet, na esperança de que você tenha feito exatamente isso: reciclado senhas. E adivinhe? Caso esse palpite esteja certo, você acabará tendo um problema não apenas em um serviço, mas em vários. E pode acreditar: sempre achamos que não vai acontecer conosco, até ser tarde demais.

Então, o que podemos fazer para nos proteger? Uma das abordagens mais seguras disponíveis hoje é usar um *gerenciador de senhas*. Os gerenciadores de senhas são programas que essencialmente armazenam todas as suas senhas e nomes de usuário em um formato criptografado que pode ser descriptografado por uma senha mestra. Dessa forma, você só precisa se lembrar de uma boa senha, já que o gerenciador cuidará de manter todas as outras em segurança.

O *KeePass* é um dos gerenciadores de senha open source mais famosos e ricos em recursos do mercado. Ele armazena suas senhas em um arquivo criptografado dentro de seu sistema de arquivos. O fato de ser open source é uma questão importante para este tipo de software, pois isso garante que não haverá um uso espúrio de seus dados, já que qualquer desenvolvedor pode auditar o código e saber exatamente como funciona. Isso proporciona um nível de transparência impossível de alcançar com código proprietário. O KeePass tem versões para a maioria dos sistemas operacionais, incluindo Windows, Linux e macOS, bem como para os sistemas móveis, como iOS e Android. Também inclui um sistema de plugins capaz de estender sua funcionalidade para bem além do padrão.

O *Bitwarden* é outra solução de código aberto com uma abordagem semelhante, mas em vez de armazenar seus dados em um arquivo, ele lança mão de um servidor na nuvem. Dessa forma, é mais fácil manter todos os seus dispositivos sincronizados e suas senhas facilmente acessíveis através da web. O *Bitwarden* é um dos poucos projetos em que não só os clientes, mas também o servidor na nuvem estão disponíveis como software de código aberto. Isso significa que é possível hospedar sua própria versão do Bitwarden e torná-la disponível para qualquer pessoa, como a sua família ou os funcionários da sua empresa. Isso lhe dará flexibilidade, mas também total controle sobre como essas senhas são armazenadas e utilizadas.

Uma das coisas mais importantes a se ter em mente ao usar um gerenciador de senhas é criar uma senha aleatória para cada serviço diferente, uma vez que você não precisará decorá-las. Seria inútil usar um gerenciador de senhas para armazenar senhas recicladas ou facilmente adivinháveis. Assim, a maioria deles inclui um gerador de senhas aleatórias que cria senhas fortíssimas para você.

##### Criptografia

Sempre que fazemos transferências ou armazenamos dados, é preciso tomar precauções para garantir que terceiros não possam ter acesso a eles. Os dados transferidos pela internet passam por uma série de roteadores e redes que podem ser acessados por terceiros. Do mesmo modo, os dados armazenados em meios físicos podem ser lidos por qualquer pessoa que entre em posse deles. Para evitar esse tipo de acesso, as informações confidenciais devem ser criptografadas antes de sair de um dispositivo informático.

###### TLS

O *Transport Layer Security* (TLS) é um protocolo que aumenta a segurança das conexões de rede por meio da criptografia. O TLS é o sucessor do *Secure Sockets Layer* (SSL), que se tornou obsoleto devido a falhas graves. O TLS também evoluiu algumas vezes para se adaptar e tornar-se mais seguro, por isso a versão mais atual é a 1.3. Ele garante tanto a privacidade quanto a autenticidade, graças ao uso de criptografia simétrica e de chave pública. Isso significa que, uma vez em uso, é possível ter certeza de que ninguém será capaz de interceptar ou alterar sua comunicação com aquele servidor durante aquela sessão.

A lição mais importante aqui é saber reconhecer se um website é confiável. Procure sempre pelo símbolo de “cadeado” na barra de endereços do navegador. Se desejar, você pode clicar nele para inspecionar o certificado, que desempenha um papel importante no protocolo HTTPS.

O TLS é usado no protocolo HTTPS (*HTTP sobre TLS*) para possibilitar o envio de dados confidenciais (como o número do seu cartão de crédito) através da web. O funcionamento do TLS vai muito além do objetivo deste artigo, mas você pode encontrar mais informações em Wikipedia e em Mozilla wiki.

###### Criptografia de arquivos e emails com GnuPG

Existem muitas ferramentas para proteger emails, mas uma das mais importantes é certamente o *GnuPG*. GnuPG significa *GNU Privacy Guard*; trata-se de uma implementação open source do *OpenPGP*, um padrão internacional codificado no RFC 4880.

O GnuPG pode ser usado para assinar, criptografar e descriptografar textos, emails, arquivos, diretórios e até mesmo partições de disco inteiras. Ele utiliza criptografia de chave pública e está amplamente disponível. Em poucas palavras, o GnuPG cria um par de arquivos que contêm suas chaves públicas e privadas. Como o nome indica, a chave pública pode ser disponibilizada para qualquer pessoa e a chave privada precisa ser mantida em segredo. As pessoas usam sua chave pública para criptografar dados que somente sua chave privada será capaz de decodificar.

A chave privada também pode ser usada para assinar qualquer arquivo ou email, que poderão ser validados com a chave pública correspondente. Essa assinatura digital funciona de forma análoga a uma assinatura do mundo real. A partir do momento em que você é o único a conhecer sua chave privada, o receptor pode ter a certeza de você é o autor. Ao lançar mão da funcionalidade de hash criptográfico, o GnuPG também garante que não foram feitas alterações após a assinatura, já que qualquer mudança no conteúdo a invalidaria.

O GnuPG é uma ferramenta muito poderosa e, em certa medida, também complexa. Para saber mais, visite website e Archlinux wiki (a wiki Archlinux é uma boa fonte de informação, mesmo que você não use Archlinux).

###### Criptografia de disco

Uma boa maneira de garantir a segurança de seus dados é criptografar inteiramente o disco ou partição. Existem muitos softwares open source que podem ser usados com esse fim. Seu funcionamento e o nível de criptografia que oferecem também varia bastante. Existem dois métodos básicos: criptografia de dispositivos *empilhada* e *de bloco*.

As soluções de criptografia empilhada no sistema de arquivos são implementadas por cima do sistema de arquivos existente. Ao usar esse método, os arquivos e diretórios são criptografados antes de serem armazenados no sistema de arquivos e descriptografados depois de lidos. Isso significa que os arquivos são armazenados no sistema de arquivos hospedeiro em um formato criptografado (ou seja, seu conteúdo, e geralmente também os nomes de arquivos/pastas, são substituídos por dados aparentemente aleatórios), mas tirando isso, eles ainda existem no sistema de arquivos sem criptografia, como arquivos normais, links simbólicos, hardlinks etc.

Por outro lado, a criptografia de dispositivos de bloco ocorre abaixo da camada do sistema de arquivos, garantindo que tudo o que é escrito num dispositivo de bloco é criptografado. Se olharmos para o bloco offline, ele vai parecer uma grande massa de dados aleatórios, e não será nem mesmo possível dizer qual é o tipo de sistema de arquivos sem antes descriptografá-lo. Ou seja, não dá para saber o que é um arquivo ou diretório, nem seu tamanho e de que tipo de dados se trata, porque os metadados, a estrutura de diretórios e as permissões também são criptografados.

Ambos os métodos têm seus pontos positivos e negativos. Dentre todas as opções disponíveis, sugerimos dar uma olhada no *dm-crypt*, que é o padrão de fato para a criptografia de bloco em sistemas Linux, sendo nativo no kernel. Pode ser usado com a extensão *LUKS* (*Linux Unified Key* *Setup*), uma especificação que implementa um padrão independente de plataforma, para uso com diversas ferramentas.

Se quiser experimentar um método de criptografia empilhada, sugerimos o *EncFS*, que é provavelmente a maneira mais simples de proteger dados no Linux, já que não requer privilégios de root para ser implementado e pode rodar em um sistema de arquivos existente sem modificações.

Finalmente, se você precisa acessar dados em várias plataformas, confira o Veracrypt. Ele é o sucessor do Truecrypt e permite a criação de mídia e arquivos criptografados, que podem ser usados no Linux, bem como em macOS e Windows.

#### Exercícios Guiados

1. Você deve usar uma “janela anônima” em seu navegador quando quer:

  Navegar na internet de maneira completamente anônima

  Não deixar traços no computador que está usando

  Ativar o TLS para evitar o rastreamento de cookies

  Para usar o DNT

  Para usar criptografia durante a transmissão de dados

2. O que é OpenStack?

  Um projeto que permite a criação de um IaaS privado

  Um projeto que permite a criação de um PaaS privado

  Um projeto que permite a criação de um SaaS privado

  Um hipervisor

  Um gerenciador de senhas de código aberto

3. Quais das opções abaixo são softwares válidos para criptografia de discos?

  RevealJS, EncFS e dm-crypt

  dm-crypt e KeePass

  EncFS e Bitwarden

  EncFS e dm-crypt

  TLS e dm-crypt

4. Selecione verdadeiro ou falso para a criptografia de dispositivos com dm-crypt:

  Os arquivos são criptografados antes de serem escritos no disco

  O sistema de arquivos inteiro se torna uma massa criptografada

  Apenas os arquivos e diretórios são criptografados, e não os links simbólicos

  Não requer acesso de root

  É uma criptografia de dispositivo de bloco

5. O Beamer é:

  Um mecanismo de criptografia

  Um hipervisor

  Um programa de virtualização

  Um componente do OpenStack

  Uma ferramenta de apresentações em LaTeX

#### Exercícios Exploratórios

1. A maioria das distribuições vem com o Firefox instalado por padrão (se não for o seu caso, será preciso instalá-lo antes). Vamos instalar uma extensão para o Firefox chamada *Lightbeam*. Para isso, você pode pressionar `Ctrl` + `Shift` + `A` e buscar por “Lightbeam” no campo de busca que aparece na aba aberta, ou visitar a página da extensão com o Firefox e clicar no botão “Instalar”: https://addons.mozilla.org/en-GB/firefox/addon/lightbeam-3-0/. Em seguida, inicie a extensão clicando no ícone e comece a visitar páginas web em outras abas para ver o que acontece.

2. Qual a coisa mais importante ao se usar um gerenciador de senhas?

3. Use seu navegador para visitar https://haveibeenpwned.com/. Descubra qual a finalidade do site e confira se seu endereço de email foi incluído em algum vazamento de dados.

#### Sumário

O terminal é uma maneira poderosa de interagir com o sistema e existem muitas ferramentas úteis e maduras para se usar nesse tipo de ambiente. Para abrir o terminal, procure no menu de seu ambiente de desktop ou pressione `Ctrl` + `Alt` + `F#` .

O Linux é amplamente usado na indústria da tecnologia para oferecer serviços de IaaS, PaaS e SaaS. Existem três hipervisores principais que desempenham um papel importante no suporte desses serviços: Xen, KVM e Virtualbox.

O navegador é um programa essencial para a computação atualmente, mas é necessário entender como utilizá-lo com segurança. O DNT é somente uma maneira de informar ao site que você não deseja ser rastreado, mas não há garantia de que ele obedeça. As janelas anônimas são privadas somente em relação ao computador que você está usando, mas graças a isso elas podem ajudar a evitar o rastreamento de cookies.

O TLS pode criptografar suas comunicações na internet, mas você precisa ser capaz de reconhecer quando está sendo usado. Escolher senhas fortes também é importantíssimo para manter sua segurança, e por isso a melhor ideia é delegar essa responsabilidade a um gerenciador de senhas e permitir que o software crie senhas aleatórias para qualquer site em que você se logar.

Outra maneira de proteger suas comunicações é assinar e criptografar suas pastas de arquivos e emails com o GnuPG. dm-crypt e EncFS são duas alternativas para criptografar discos inteiros ou partições; eles usam, respectivamente, métodos de criptografia de bloco e empilhada.

Finalmente, o LibreOffice Impress é uma alternativa open source completa ao Microsoft Powerpoint, mas também existe o Beamer e o RevealJS para quem prefere criar apresentações usando código ao invés de interfaces gráficas. O ProjectLibre e o GanttProject podem ser boas escolhas para quem busca um substituto ao Microsoft Project.

#### Respostas aos Exercícios Guiados

1. Você deve usar uma “janela anônima” em seu navegador quando quer:

| Navegar na internet de maneira |  |
|---|---|
| completamente anônima |  |
| Não deixar traços no computador que está | X |
| usando |  |
| Ativar o TLS para evitar o rastreamento de |  |
| cookies |  |
| Para usar o DNT |  |
| Para usar criptografia durante a transmissão |  |
| de dados |  |

2. O que é OpenStack?

| Um projeto que permite a criação de um IaaS | X |
|---|---|
| privado |  |
| Um projeto que permite a criação de um PaaS |  |
| privado |  |
| Um projeto que permite a criação de um SaaS |  |
| privado |  |
| Um hipervisor |  |
| Um gerenciador de senhas de código aberto |  |

3. Quais das opções abaixo são softwares válidos para criptografia de discos?

| RevealJS, EncFS e dm-crypt |  |
|---|---|
| dm-crypt e KeePass |  |
| EncFS e Bitwarden |  |
| EncFS e dm-crypt | X |
| TLS e dm-crypt |  |

4. Selecione verdadeiro ou falso para a criptografia de dispositivos com dm-crypt:

| Os arquivos são criptografados antes de serem | V |
|---|---|
| escritos no disco |  |
| O sistema de arquivos inteiro se torna uma | V |
| massa criptografada |  |
| Apenas os arquivos e diretórios são | F |
| criptografados, e não os links simbólicos |  |
| Não requer acesso de root | F |
| É uma criptografia de dispositivo de bloco | V |

5. O Beamer é:

| Um mecanismo de criptografia |  |
|---|---|
| Um hipervisor |  |
| Um programa de virtualização |  |
| Um componente do OpenStack |  |
| Uma ferramenta de apresentações em LaTeX | X |

#### Respostas aos Exercícios Exploratórios

1. A maioria das distribuições vem com o Firefox instalado por padrão (se não for o seu caso, será preciso instalá-lo antes). Vamos instalar uma extensão para o Firefox chamada *Lightbeam*. Para isso, você pode pressionar `Ctrl` + `Shift` + `A` e buscar por “Lightbeam” no campo de busca que aparece na aba aberta, ou visitar a página da extensão com o Firefox e clicar no botão “Instalar”: https://addons.mozilla.org/en-GB/firefox/addon/lightbeam-3-0/. Em seguida, inicie a extensão clicando no ícone e comece a visitar páginas web em outras abas para ver o que acontece.

  Lembra dos cookies que podem compartilhar seus dados com diferentes serviços quando você visita um website? É exatamente isso o que esta extensão vai lhe mostrar. O Lightbeam é uma experiência da Mozilla para tentar revelar os sites principais e de terceiros com os quais você interage ao visitar uma única URL. Esse conteúdo normalmente não está visível para o usuário médio e mostra que, às vezes, um único website interage com mais de uma dúzia de serviços.

2. Qual a coisa mais importante ao se usar um gerenciador de senhas?

  Ao usar um gerenciador de senhas, o mais importante a se ter em mente é memorizar sua senha mestre e usar uma senha aleatória única para cada serviço.

3. Use seu navegador para visitar https://haveibeenpwned.com/. Descubra qual a finalidade do site e confira se seu endereço de email foi incluído em algum vazamento de dados.

  O site mantém um banco de dados de informações de login cujas senhas foram afetadas por um vazamento de senhas. Ele permite buscar por um endereço de email e mostra se esse endereço estava incluído em um banco de dados público de credenciais roubadas. Há grandes chances de que seu endereço de email tenha sido afetado por um vazamento ou outro. Se for o caso, é melhor que suas senhas tenham sido atualizadas recentemente. Se você ainda não usa um gerenciador de senhas, dê uma olhada nas opções que recomendamos nesta lição.

---
*Fonte: Linux Professional Institute, Materiais Didáticos Linux Essentials (learning.lpi.org), licença CC BY-NC-ND 4.0. Conversão do PDF para Markdown apenas para estudo pessoal.*
