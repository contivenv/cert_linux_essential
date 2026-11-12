---
tags: [lpi, linux-essentials, 010-160]
topico: 4
certificacao: LPI Linux Essentials 010-160 (v1.6)
---

# Tópico 4: O Sistema Operacional Linux

## 4.1 Escolhendo um Sistema Operacional

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 4.1
- **Peso**: 1

**Áreas chave de conhecimento**

- Diferenças entre Windows, Mac, Linux
- Gerenciamento do ciclo de vida das distribuições

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- GUI versus linha de comando, configuração desktop
- Ciclos de manutenção, Beta e Stable

### 4.1 Lição 1

#### Introdução

Quer você use um computador em casa, na universidade ou dentro de uma empresa, ainda assim será necessário tomar uma decisão sobre o sistema operacional a ser usado. Claro que essa decisão pertence a você no caso do seu computador pessoal, mas talvez você também seja o responsável por fazer a escolha de um sistema para sua empresa. Como sempre, é essencial estar bem informado sobre as opções disponíveis para tomar uma decisão responsável. Nesta lição, vamos ajudá-lo a conhecer melhor as opções disponíveis de sistemas operacionais.

##### O que é um sistema operacional

Uma das primeiras coisas que precisamos deixar claro antes de começar nossa jornada pela escolha de um sistema operacional é entender o que queremos dizer com o termo. O sistema operacional reside no coração do seu computador e permite executar aplicativos dentro e por cima dele. Além disso, o sistema operacional contém drivers para acessar o hardware do computador, como discos e partições, telas, teclados, placas de rede e assim por diante. Costumamos abreviar o termo “sistema operacional” simplesmente como *SO*. Existem atualmente muitos sistemas operacionais para uso em computadores empresariais e também para uso pessoal e doméstico. Para simplificar a seleção disponível, podemos agrupar as opções da seguinte maneira:

- Sistemas operacionais baseados em Linux
  - Linux para empresas
  - Linux para o usuário comum
- UNIX
- macOS
- Sistemas operacionais baseados em Windows
  - Servidores Windows
  - Sistemas desktop Windows

##### Escolhendo uma distribuição Linux

###### O kernel do Linux e as distribuições do Linux

Quando falamos em distribuições Linux, o sistema operacional é o Linux. O Linux é o *kernel*, ou seja, o cerne de toda distribuição Linux. O software do kernel do Linux é mantido por um grupo de indivíduos liderado por Linus Torvalds. Torvalds é empregado por um consórcio de empresas chamado The Linux Foundation para trabalhar no kernel do Linux.

> [!note]
> O kernel do Linux foi desenvolvido inicialmente por Linus Torvalds, um estudante finlandês, em 1991. Em 1992, o primeiro lançamento do Kernel sob a GNU Licença Pública Geral versão 2 (GPLv2) foi a versão 0.12.

- **Kernel do Linux**: Como dissemos, todas as distribuições Linux rodam o mesmo sistema operacional, Linux.
- **Distribuição Linux**: Quando falamos de Red Hat Linux, ou Ubuntu Linux, referimo-nos à *distribuição Linux*. A distribuição Linux é fornecida com um kernel do Linux e um ambiente que nos permite interagir com ele. No mínimo, precisamos de um shell de linha de comando como o Bash e um conjunto de comandos básicos que nos permitam acessar e gerenciar o sistema. Claro que, na maioria das vezes, a distribuição Linux inclui um ambiente de desktop completo, como o Gnome ou o KDE.

Embora todas as distribuições Linux executem o sistema operacional Linux, as distribuições têm bastante variedade na versão do sistema operacional usada. Ou seja, *a versão do Kernel do Linux* *que está sendo usada* quando a distribuição é inicializada.

Se tiver acesso a uma linha de comando do Linux no momento, você pode conferir facilmente qual a versão do kernel do Linux que está usando lendo o *kernel release*:

**TIP**

```bash
$ uname -r
4.15.0-1019-aws
```

###### Tipos de distribuições Linux

Pode parecer uma escolha óbvia sempre executar a versão mais recente do kernel do Linux, mas não é tão simples assim. Podemos categorizar vagamente as distribuições do Linux em três conjuntos:

- Distribuições Linux de nível empresarial
  - Red Hat Enterprise Linux
  - CentOS
  - SUSE Linux Enterprise Server
  - Debian GNU/Linux
  - Ubuntu LTS
- Distribuições Linux para o usuário doméstico
  - Fedora
  - Ubuntu não-LTS
  - openSUSE
- Distribuições de Linux experimentais e para hackers
  - Arch
  - Gentoo

É claro que esse é apenas um subconjunto muito pequeno das distribuições possíveis, mas o mais importante é a diferença entre as distribuições *empresariais*, *de usuário* e *experimentais*, e por que cada uma delas existe.

- **Linux empresarial**: Distribuições como o CentOS (*Community Enterprise OS*) são projetadas para serem implantadas em grandes organizações usando hardware corporativo. As necessidades corporativas são muito diferentes das necessidades de pequenas empresas, amadores ou usuários domésticos. Para garantir a disponibilidade de seus serviços, os usuários corporativos

  têm requisitos mais elevados em relação à estabilidade de seu hardware e software. Portanto, as distribuições empresariais do Linux tendem a incluir versões mais antigas do kernel e de outros softwares, que funcionam de maneira confiável. Geralmente, as distribuições portam as atualizações importantes, como correções de segurança, para essas versões estáveis. Em troca, as distribuições corporativas do Linux podem não ter suporte para o hardware de consumo mais recente, além de conter versões mais antigas dos pacotes de software. No entanto, como no caso das distribuições Linux para usuários finais, as empresas tendem a escolher componentes de hardware maduros e desenvolver seus serviços em versões estáveis de software.

- **Linux para o usuário final**: Distribuições como o Ubuntu são mais direcionadas para pequenas empresas ou particulares e usuários ocasionais. Esse tipo de usuário tem mais probabilidade de estar usando o hardware mais recente do mercado. Esses sistemas precisam dos drivers mais recentes para aproveitar ao máximo o novo hardware. Assim, o kernel mais recente é ideal para os usuários domésticos, mesmo tendo sido menos testado. Os kernels Linux mais recentes trazem os drivers mais atuais para suportar o hardware moderno que provavelmente estará em uso. Dado o crescimento do Linux que tem sido constatado no mercado de jogos, é importantíssimo que os drivers mais recentes estejam disponíveis para esses usuários.

> [!note]
> Algumas distribuições, como o Ubuntu, oferecem versões para o usuário doméstico, que contêm software recente e recebem atualizações por um curto período, além das chamadas versões com suporte a longo prazo (Long Term Support ou LTS), mais adequadas para ambientes empresariais.

- **Distribuições Linux experimentais e para hackers**: Distribuições como o Arch Linux ou o Gentoo Linux vivem na vanguarda da tecnologia. Elas trazem as versões mais recentes do software, mesmo que essas versões ainda contenham erros e recursos não testados. Por outro lado, essas distribuições tendem a usar um modelo de lançamento contínuo (rolling release) que lhes permite entregar atualizações a qualquer momento. Essas distribuições são usadas por usuários avançados que desejam sempre ter acesso ao software mais recente, têm consciência de que a funcionalidade pode quebrar a qualquer momento e são capazes de reparar seu sistema quando isso acontece.

Em resumo, ao considerar o uso do Linux como sistema operacional, se você estiver usando hardware de nível corporativo em seus servidores ou computadores desktop, poderá escolher distribuições Linux de nível corporativo ou de usuário doméstico. Se você estiver usando hardware de nível doméstico e quiser aproveitar ao máximo as inovações de hardware mais recentes, provavelmente precisará de uma distribuição Linux igualmente recente para atender às necessidades do hardware.

Algumas distribuições Linux têm parentesco entre si. O Ubuntu, por exemplo, é baseado no Debian Linux e usa o mesmo sistema de empacotamento, DPKG. Já o Fedora é uma plataforma de teste para o RedHat Enterprise Linux, onde recursos potenciais de versões futuras do RHEL podem ser explorados antes de serem disponibilizados na distribuição corporativa.

Existem muitas outras distribuições Linux além das que mencionamos nesta lição. Uma vantagem de o Linux ser um software de código aberto é que muitas pessoas podem desenvolvê-lo da maneira como acham melhor. Graças a isso, existem centenas de distribuições. Para conhecer mais distribuições Linux, visite The Distro Watch Web Site. Os mantenedores desse site listam as 100 distribuições Linux mais baixadas, permitindo comparar e ver o que é popular atualmente.

###### Ciclo de vida do suporte no Linux

Como seria de se esperar, as distribuições corporativas do Linux têm uma vida útil mais longa do que as edições para o consumidor ou para a comunidade. Por exemplo, o Red Hat Enterprise Linux oferece suporte por 10 anos. O Red Hat Enterprise Linux 8 foi lançado em maio de 2019 e as atualizações e suporte ao software estarão disponíveis até maio de 2029.

As edições para o usuário doméstico geralmente só contam com o suporte da comunidade por meio de fóruns. As atualizações de software costumam ficar disponíveis por três lançamentos. Se tomarmos o Ubuntu como exemplo, no momento em que escrevemos este artigo a versão mais recente disponível era a 19.04, que foi atualizada no lançamento 19.10 e interrompida em janeiro de 2020. O Ubuntu também oferece edições com suporte a longo prazo, conhecidas como edições *LTS*, que contam com 5 anos de suporte a partir do lançamento original. A versão LTS atual é a 18.04, que terá atualizações de software até 2023. Essas versões LTS fazem do Ubuntu uma opção razoável para uso em empresas, graças ao suporte comercial disponibilizado pela Canonical (a empresa por trás da marca Ubuntu) ou por empresas de consultoria independentes.

> [!note]
> As distribuições do Ubuntu usam datas como números de versão, no formato YY.MM: Por exemplo, a versão 19.04 foi lançada em abril de 2019.

###### O Linux no desktop

A implementação do Linux como sistema desktop pode ser mais difícil em uma empresa cuja equipe de suporte técnico está mais habituada a sistemas operacionais comerciais. No entanto, não é apenas o suporte que pode causar dificuldades. Um cliente corporativo também pode ter feito grandes investimentos em soluções de software que o prendem a sistemas operacionais específicos. Dito isso, há muitos exemplos de desktops Linux sendo integrados em grandes organizações; empresas como a Amazon, por exemplo, têm sua própria distribuição Linux Amazon Linux 2. Ela é usada na plataforma de nuvem da AWS, mas também internamente, em servidores e desktops.

Usar o Linux em uma pequena empresa ou em casa é bem mais fácil e pode ser uma experiência gratificante, eliminando a necessidade de pagar por uma licença e abrindo seus olhos para o verdadeiro tesouro de programas gratuitos e de código aberto disponíveis para o Linux. Você também descobrirá que existem muitos ambientes de desktop diferentes à disposição. Os mais comuns são o Gnome e o KDE, porém existem muitos outros. A decisão só depende de sua preferência pessoal.

###### Usando o Linux em servidores

No mundo empresarial, é muito comum que o Linux seja usado como sistema operacional nos servidores. Os servidores são mantidos por engenheiros especializados em Linux. Mesmo que haja milhares de usuários, eles não precisam saber nada sobre os servidores aos quais estão se conectando. O sistema operacional do servidor não é importante para eles e, em geral, os aplicativos clientes não diferem entre o Linux e outros sistemas operacionais no backend. Também é verdade que, à medida que mais aplicativos vão sendo virtualizados ou postos em contêineres dentro de nuvens locais e remotas, o sistema operacional vai ficando mais mascarado, e há grande probabilidade de o sistema operacional embarcado ser Linux.

###### Linux na nuvem

Outra oportunidade de se familiarizar com o Linux é implantá-lo em uma das muitas nuvens públicas disponíveis. A criação de uma conta em um dos muitos provedores de nuvem permite implantar rapidamente muitas distribuições diferentes do Linux de maneira rápida e fácil.

##### Sistemas operacionais não-Linux

Sim, por incrível que pareça, existem sistemas operacionais que não são baseados no kernel do Linux. É claro que, ao longo dos anos, existiram muitos e alguns deles caíram no esquecimento, mas ainda existem opções disponíveis para você, seja em casa ou no trabalho.

###### Unix

Antes de termos o Linux como sistema operacional, havia o Unix. O Unix costumava ser vendido junto com o hardware. Ainda hoje, diversos Unixes comerciais, como o AIX e o HP-UX, estão disponíveis no mercado. Embora o Linux tenha sido altamente inspirado no Unix (e na falta de disponibilidade dele para determinado hardware), a família de sistemas operacionais BSD baseia- se diretamente nele. Hoje, o FreeBSD, o NetBSD e o OpenBSD, junto com alguns outros sistemas BSD relacionados, estão disponíveis como software livre.

O Unix costumava ser muito usado no mundo empresarial, mas sofreu um declínio com o crescimento do Linux. À medida que o Linux cresceu e as ofertas de suporte corporativo também foram aumentando, vimos o Unix lentamente começar a sumir. O Solaris, originalmente da Sun antes de se mudar para a Oracle, desapareceu recentemente. Ele era um dos maiores sistemas operacionais Unix usados pelas empresas de telecomunicações, anunciado como *Telco Grade Unix* (Unix em nível de operadora de telecomunicações).

Dentre os sistemas operacionais Linux, temos:

- AIX
- FreeBSD, NetBSD, OpenBSD
- HP-UX
- Irix
- Solaris

###### macOS

O macOS (anteriormente OS X) da Apple data de 2001. Largamente inspirado no BSD Unix e usando o shell de linha de comando Bash, trata-se um sistema amigável para quem está acostumado a usar sistemas operacionais Unix ou Linux. Se você estiver usando o macOS, pode abrir o aplicativo Terminal para acessar a linha de comando. Use o mesmo comando `uname` para verificar o sistema operacional relatado:

```bash
$ uname -s
Darwin
```

> [!note]
> Neste caso, usamos a opção `-s` para retornar o nome do sistema operacional. Anteriormente, usamos `-r` para retornar o número da versão do kernel.

###### Microsoft Windows

Ainda podemos dizer que a maioria dos desktops e laptops em circulação estão rodando Windows. Esse sistema operacional conheceu um verdadeiro sucesso, dominando o mercado de desktops há anos. Embora se trate de um software proprietário e não seja gratuito, em geral a licença do sistema operacional é incluída na compra do hardware, facilitando a escolha do usuário. Obviamente, todos os fornecedores de hardware e software oferecem amplo suporte ao Windows, além de existirem muitos aplicativos de código aberto para o sistema. O futuro para o Windows não parece tão brilhante quanto no passado. Com a diminuição nas vendas de desktops e laptops, o foco passou a ser o mercado de tablets e celulares. Esse mercado foi dominado pela Apple e pelo Android, e a Microsoft está tendo dificuldades em ganhar terreno.

Como plataforma de servidor, a Microsoft agora permite que seus clientes escolham entre uma GUI (*Graphical User Interface*, ou interface gráfica de usuário) e uma versão apenas em linha de comando. A separação entre a GUI e a linha de comando é importante. Na maioria das vezes, a GUI dos Microsoft Servers mais antigos é carregada, mas ninguém a usa. Veja, por exemplo, o controlador de domínio do Active Directory… os usuários o usam o tempo todo para se autenticar no domínio, mas ele é gerenciado remotamente nas estações de trabalho dos administradores e não no servidor.

#### Exercícios Guiados

1. Qual projeto forma o componente comum de todas as distribuições Linux?

  CentOS

  Red Hat

  Ubuntu

  Kernel do Linux

  CoreOS

2. Qual sistema operacional é relatado como estando em uso no macOS da Apple?

  OS X

  OSX

  Darwin

  MacOS

3. Qual a diferença entre uma distribuição Linux e o kernel do Linux?

  O kernel é parte de uma distribuição e a distribuição reúne aplicativos em volta do kernel, tornando-o útil

  O kernel é a distribuição Linux

  Todas as distribuições que usam o mesmo kernel são iguais

4. Qual destes é um ambiente de desktop no Linux?

  Mint

  Elementary

  Zorin

  Gnome

5. Qual componente de um sistema operacional permite o acesso ao hardware?

  Drivers

  Shells

  Serviços

  Aplicativos

#### Exercícios Exploratórios

1. Se tiver acesso à linha de comando, encontre a lançamento atual do Kernel de seu sistema.

2. Usando seu mecanismo de pesquisa preferido, localize e identifique os provedores de nuvem pública disponíveis para você. Dentre eles existe o AWS, o Google Cloud, o Rackspace e muitos outros. Escolha um e veja quais sistemas operacionais estão disponíveis para implementação.

#### Resumo

Nesta seção, você aprendeu como diferenciar entre os diferentes sistemas operacionais mais comuns. Nós falamos de:

- Sistemas operacionais baseados em Linux
- UNIX
- macOS
- Sistemas operacionais baseados em Windows

Dentro da categoria Linux, podemos dividir ainda mais a seleção entre as distribuições com suporte a longo prazo e aquelas com um ciclo de suporte mais curto. As versões LTS são mais adequadas para empresas; o suporte de curto prazo é mais direcionado aos usuários domésticos e ocasionais.

- Distribuições Linux de nível empresarial
  - Red Hat Enterprise Linux
  - CentOS
  - SUSE Linux Enterprise Server
  - Debian GNU/Linux
  - Ubuntu LTS
- Distribuições Linux para o usuário doméstico
  - Fedora
  - Ubuntu não-LTS
  - openSUSE
- Distribuições de Linux experimentais e para hackers
  - Arch
  - Gentoo

#### Respostas aos Exercícios Guiados

1. Qual projeto forma o componente comum de todas as distribuições Linux?

| CentOS |  |
|---|---|
| Red Hat |  |
| Ubuntu |  |
| Kernel do Linux | X |
| CoreOS |  |

2. Qual sistema operacional é relatado como estando em uso no macOS da Apple?

| OS X |  |
|---|---|
| OSX |  |
| Darwin | X |
| MacOS |  |

3. Qual a diferença entre uma distribuição Linux e o kernel do Linux?

| O kernel é parte de uma distribuição, a | X |
|---|---|
| distribuição reúne aplicativos em volta do |  |
| kernel, tornando-o útil |  |
| O kernel é a distribuição Linux |  |
| Todas as distribuições que usam o mesmo |  |
| kernel são iguais |  |

4. Qual destes é um ambiente de desktop no Linux?

| Mint |  |
|---|---|
| Elementary |  |
| Zorin |  |
| Gnome | X |

5. Qual componente de um sistema operacional permite o acesso ao hardware?

| Drivers | X |
|---|---|
| Shells |  |
| Serviços |  |
| Aplicativos |  |

#### Respostas aos Exercícios Exploratórios

1. Se tiver acesso à linha de comando, encontre a lançamento atual do Kernel de seu sistema.

  ```bash
  $ uname -r
  4.15.0-47-generic
  ```

2. Usando seu mecanismo de pesquisa preferido, localize e identifique os provedores de nuvem pública disponíveis para você. Dentre eles existe o AWS, o Google Cloud, o Rackspace e muitos outros. Escolha um e veja quais sistemas operacionais estão disponíveis para implementação.

  O AWS, por exemplo, permite implementar várias distribuições Linux como Debian, Red Hat, SUSE ou Ubuntu, além do Windows.

## 4.2 Entendendo o Hardware do Computador

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 4.2
- **Peso**: 2

**Áreas chave de conhecimento**

- Hardware

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- Placas-mãe, processadores, fontes, drives ópticos, periféricos
- Discos-rígidos e partições, /dev/sd\*
- Drivers

### 4.2 Lição 1

#### Introdução

Sem o hardware, o software nada mais é do que outra forma de literatura. O hardware processa os comandos descritos pelo software e fornece mecanismos para armazenamento, entrada e saída de dados. Até mesmo a nuvem está escorada em hardware.

Em seu papel como sistema operacional, uma das responsabilidades do Linux é fornecer software com interfaces que permitem acessar o hardware de um sistema. A maioria das especificações de configuração está além do escopo desta lição. No entanto, os usuários geralmente precisam se preocupar com o desempenho, a capacidade e outros fatores relacionados ao hardware, pois são eles que permitem que um sistema seja capaz de suportar adequadamente aplicativos específicos. Esta lição discute o hardware como itens físicos separados usando conectores e interfaces padrão. Os padrões são relativamente estáticos. Mas a forma, o desempenho e as características de capacidade do hardware estão em constante evolução. Mesmo que essas evoluções afetem as distinções físicas, os aspectos conceituais do hardware descritos nesta lição permanecem válidos.

> [!note]
> Em vários pontos desta lição, usamos exemplos na linha de comando para demonstrar maneiras de acessar informações sobre o hardware. A maioria dos exemplos vem de um Raspberry Pi B +, mas aplica-se à maioria dos sistemas. Não é

necessário entender esses comandos para compreender este material.

##### Fontes de alimentação

Todos os componentes ativos de um sistema de computação requerem eletricidade para operar. Infelizmente, a maioria das fontes de eletricidade não é apropriada. O hardware de um sistema de computação requer tensões elétricas específicas com tolerâncias relativamente estreitas. Não é bem o que a tomada da parede da sua casa pode oferecer.

As fontes de alimentação normalizam o fornecimento de energia disponível. Os requisitos de tensão padronizados permitem que os fabricantes criem componentes de hardware que podem ser usados em sistemas de qualquer lugar do mundo. As fontes de alimentação de computadores pessoais costumam usar a eletricidade das tomadas como suprimento. As fontes de alimentação de um servidor são cruciais para seu funcionamento, e portanto costumam ser conectadas a várias fontes de fornecimento para garantir que continuem operando se uma delas falhar.

O consumo de energia gera calor. O calor excessivo pode fazer com que os componentes do sistema operem lentamente ou até parem de funcionar. A maioria dos sistemas possui algum tipo de ventoinha para promover um resfriamento mais eficiente. Componentes como os processadores geralmente produzem um calor que o fluxo de ar por si só não é capaz de dissipar. Esses componentes quentes vêm com aletas especiais, conhecidas como dissipadores de calor, para ajudar a expulsar o calor que geram. Os dissipadores de calor geralmente têm sua própria ventoinha para garantir um fluxo de ar adequado.

##### Placa-mãe

Todo o hardware de um sistema precisa ser interconectado. A placa-mãe normaliza essa interconexão usando conectores padronizados e fatores de forma. Ela também fornece suporte para a configuração e as necessidades elétricas desses conectores.

Existem muitas configurações possíveis para a placa-mãe. Elas suportam diferentes processadores e sistemas de memória, trazem diferentes combinações de conectores padronizados e se adaptam aos diferentes tamanhos de acondicionamento. Tirando, talvez, a capacidade de conectar dispositivos externos específicos, a configuração da placa-mãe não tem muito segredo para os usuários. Os administradores do sistema precisam entender a configuração da placa-mãe quando é necessário identificar dispositivos específicos.

Logo que uma fonte de energia é aplicada pela primeira vez, é necessário configurar e inicializar um hardware específico à placa-mãe antes que o sistema possa operar. Para isso, as placas-mãe usam a programação armazenada na memória não-volátil, conhecida como firmware. A forma original do firmware da placa-mãe era conhecida como BIOS (*Basic Input/Output System*, ou

Sistema Básico de Entrada/Saída). Além das definições básicas de configuração, a BIOS era a principal responsável pela identificação, carregamento e transferência da operação para um sistema operacional, como o Linux. À medida que o hardware foi evoluindo, o firmware foi expandido para suportar discos maiores, diagnósticos, interfaces gráficas, rede e outros recursos avançados, independentemente do sistema operacional carregado. As primeiras tentativas de fazer avançar o firmware para além da BIOS básica eram frequentemente específicas a um fabricante de placas-mãe. A Intel definiu o padrão EFI (*Extensible Firmware Interface*) para o firmware avançado. Mais tarde, a empresa forneceu a EFI para um organismo de normalização como base para a criação da UEFI (*Unified Extensible Firmware Interface*). Hoje, a maioria das placas-mãe usa UEFI. É raro encontrar BIOS ou EFI em sistemas recentes. Apesar disso, a maioria das pessoas ainda se refere ao firmware da placa-mãe como BIOS.

Pouquíssimas configurações de firmware são de interesse para os usuários comuns, e assim, geralmente apenas os responsáveis pela configuração do hardware do sistema precisam lidar com o firmware e suas configurações. Uma das poucas opções comumente alteradas é a ativação das extensões de virtualização nas CPUs modernas.

##### Memória

A memória do sistema conserva os dados e o código do programa dos aplicativos em execução no momento. Quando falamos na memória do computador, em geral nos referimos a essa memória do sistema. Outro termo comum usado para a memória do sistema é a sigla RAM (*Random Access* *Memory*) ou alguma variação dela. Às vezes, também são usadas referências ao acondicionamento físico da memória do sistema, como DIMM, SIMM ou DDR.

Fisicamente, a memória do sistema costuma ser acondicionada em módulos de placas de circuito individuais que são conectados à placa-mãe. Atualmente, os módulos de memória individuais variam de 2 GB a 64 GB. Para a maioria das aplicações de uso geral, 4 GB é o mínimo de memória do sistema que os usuários devem considerar. Para estações de trabalho individuais, 16 GB normalmente são mais do que suficientes. No entanto, mesmo 16 GB podem ser limitantes para usuários que executam jogos, vídeos ou aplicativos de áudio de última geração. Os servidores geralmente exigem 128 GB ou até 256 GB de memória para oferecer um suporte eficiente a todos os usuários.

Na maioria dos casos, o Linux permite que os usuários tratem a memória do sistema como uma caixa preta. Um aplicativo é iniciado e o Linux trata de alocar a memória do sistema necessária a ele. Quando o aplicativo é encerrado, o Linux libera a memória para uso de outros aplicativos. Mas e se um aplicativo exigir mais do que a memória do sistema disponível? Nesse caso, o Linux move os aplicativos inativos da memória do sistema para uma área especial do disco conhecida como espaço de troca (swap space). O Linux move os aplicativos inativos do espaço de troca de volta para a memória do sistema quando eles precisam ser executados.

Os sistemas sem hardware de vídeo dedicado costumam usar uma parte da memória do sistema (geralmente 1 GB) como armazenamento para exibição de vídeo. Isso reduz a memória efetiva do sistema. O hardware de vídeo dedicado possui normalmente sua própria memória separada, que não está disponível como memória do sistema.

Existem várias maneiras de obter informações sobre a memória do sistema. Para o usuário, os valores mais interessantes são a quantidade total de memória disponível e em uso. Uma fonte de informação seria executar o comando `free` junto com o parâmetro `-m` para gerar uma saída em megabytes:

```bash
$ free -m
total        used        free      shared  buff/cache   available
Mem:            748          37          51          14         660         645
Swap:            99           0          99
```

A primeira linha especifica a memória total disponível para o sistema (`total`), a memória em uso (`used`) e a memória livre (`free`). A segunda linha exibe as informações correspondentes ao espaço de troca. A memória indicada como `shared` e `buff/cache` está sendo empregada atualmente para outras funções do sistema, embora a quantidade indicada em `available` possa ser usada para aplicação.

##### Processadores

A palavra “processador” implica que algo está sendo processado. Nos computadores, a maior parte desse processamento refere-se a sinais elétricos. Normalmente, esses sinais são tratados como tendo um dos valores binários de 1 ou 0.

Quando falamos em computadores, costumamos usar o termo processador de forma intercambiável com a sigla CPU (*Central Processing Unit*, ou Unidade de Processamento Central). Isso não é tecnicamente correto. Todo computador de uso geral possui uma CPU que processa os comandos binários especificados pelo software. Portanto, é compreensível que as pessoas confundam processador e CPU. No entanto, além de uma CPU, os computadores modernos geralmente incluem outros processadores de tarefas específicos. O processador adicional mais conhecido é provavelmente a GPU (*Graphical Processing Unit*, ou Unidade de Processamento Gráfico). Assim, embora uma CPU seja um processador, nem todos os processadores são CPUs.

Para a maioria das pessoas, a arquitetura da CPU é uma referência às instruções que o processador suporta. Embora a Intel e a AMD produzam processadores que suportam as mesmas instruções, é importante diferenciá-los por fornecedor devido às diferenças específicas de acondicionamento, desempenho e consumo de energia. As distribuições de software geralmente usam as seguintes designações para especificar o conjunto mínimo de instruções necessárias para operar:

- **i386**: Referencia o conjunto de instruções de 32 bits associado ao Intel 80386.
- **x86**: Referencia tipicamente os conjuntos de instruções de 32 bits associados aos sucessores do 80386, como 80486, 80586 e Pentium.
- **x64 / x86-64**: Referencia os processadores que suportam as instruções de 32 e 64 bits da família x86.
- **AMD**: Uma referência ao suporte do x86 pelos processadores AMD.
- **AMD64**: Uma referência ao suporte do x64 pelos processadores AMD.
- **ARM**: Referencia uma CPU *Reduced Instruction Set Computer* (RISC) que não se baseia no conjunto de instruções x86. Geralmente usado por dispositivos embarcados e móveis, tablets e dispositivos operados por bateria. Uma versão do Linux para ARM é usada pelo Raspberry Pi.

O arquivo `/proc/cpuinfo` contém informações detalhadas sobre o processador de um sistema. Infelizmente, os detalhes não são amigáveis para os usuários comuns. Um resultado mais geral pode ser obtido com o comando `lscpu`. Eis a saída de um Raspberry Pi B +:

```bash
$ lscpu
Architecture:          armv7l
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    1
Core(s) per socket:    4
Socket(s):             1
Model:                 4
Model name:            ARMv7 Processor rev 4 (v7l)
CPU max MHz:           1400.0000
CPU min MHz:           600.0000
BogoMIPS:              38.40
Flags:                 half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32
```

```
lpae evtstrm crc32
```

Para a maioria das pessoas, a infinidade de fornecedores, famílias de processadores e fatores de especificação representam uma variedade desconcertante de opções. Apesar disso, há vários fatores associados a CPUs e processadores que mesmo os usuários comuns e administradores precisam levar em consideração quando precisam especificar ambientes operacionais:

- **Tamanho do bit**: Para as CPUs, esse número refere-se ao tamanho nativo dos dados que ele manipula e à quantidade de memória que pode acessar. A maioria dos sistemas modernos são de 32 ou 64 bits. Se um aplicativo precisar acessar mais de 4 gigabytes de memória, ele deverá ser executado em um sistema de 64 bits, pois 4 gigabytes é o número máximo que pode ser representado usando 32 bits. E, embora aplicativos de 32 bits normalmente possam ser executados em sistemas de 64 bits, aplicativos de 64 bits não podem ser executados em sistemas de 32 bits.
- **Velocidade de clock**: Geralmente expressa em megahertz (MHz) ou gigahertz (GHz). Relaciona-se à rapidez com que um processador processa instruções. Mas a velocidade do processador é apenas um dos fatores que afetam os tempos de resposta, tempos de espera e taxa de transferência do sistema. Mesmo ao realizarmos várias tarefas ao mesmo tempo, é raro que a CPU de um PC de mesa comum esteja ativa mais de 2 ou 3% do tempo. Ainda assim, se você costuma lançar aplicativos exigentes, que envolvem atividades como criptografia ou renderização de vídeo, a velocidade da CPU pode ter um impacto significativo na taxa de transferência e no tempo de espera.
- **Cache**: As CPUs exigem um fluxo constante de instruções e dados para operar. O custo e o consumo de energia de uma memória de sistema rica em gigabytes que pudesse ser acessada na velocidade do clock da CPU seriam proibitivos. A memória cache da CPU é integrada ao chip do processador e fornece um buffer de alta velocidade entre as CPUs e a memória do sistema. A cache é separada em várias camadas, comumente chamadas de L1, L2, L3 e até L4. Em geral, no caso da cache, quanto mais, melhor.
- **Núcleos**: Chamamos de núcleo uma CPU individual. Além do núcleo que representa uma CPU física, a *Hyper-Threading* *Technology* (HTT) permite que uma única CPU física processe simultaneamente múltiplas instruções, atuando virtualmente como várias CPUs físicas. Na maioria dos casos, múltiplos núcleos físicos são empacotados como um único processador físico. No entanto, existem placas-mãe que suportam múltiplos processadores físicos. Em teoria, um número maior de núcleos deveria proporcionar um melhor rendimento do sistema.

  Infelizmente, os aplicativos de desktop geralmente mantêm as CPUs ocupadas 2 ou 3% do tempo e, portanto, adicionar mais CPUs ociosas provavelmente resultaria em uma melhoria mínima na taxa de transferência. É mais adequado dispor de mais núcleos para a execução de aplicativos que são criados para ter vários segmentos de operação independentes, como renderização de frames de vídeo, renderização de página web ou ambientes de máquina virtual multiusuário.

##### Armazenamento

Os dispositivos de armazenamento são um método de preservar programas e dados. As *Unidades* *de Disco Rígido* (Hard Disk Drives ou HDDs) e as *Unidades de Estado Sólido* (Solid State Drives ou SSDs) são a forma mais comum de dispositivo de armazenamento para servidores e desktops. Também usamos cartões de memória USB e dispositivos óticos, como os DVDs, mas raramente como dispositivo primário.

Como o nome indica, uma unidade de disco rígido armazena informações em um ou mais discos rígidos físicos. Os discos físicos são cobertos com um material magnético que possibilita o armazenamento. Os discos estão contidos em um acondicionamento lacrado, pois a poeira, pequenas partículas e até impressões digitais interferem na capacidade do HDD de ler e gravar na mídia magnética.

Os SSDs são, grosso modo, versões mais sofisticadas de dispositivos de memória USB com capacidade significativamente maior. Os SSDs armazenam informações em microchips em que não há partes móveis.

Embora a tecnologia por trás dos HDDs e SSDs seja diferente, é possível compará-los em uma série de fatores importantes. A capacidade do disco rígido baseia-se no dimensionamento dos componentes físicos, enquanto a capacidade do SSD depende do número de microchips. Os SSDs custam entre 3 e 10 vezes mais que um HDD por gigabyte. Para ler ou gravar, um HDD deve esperar que um ponto do disco gire até um local conhecido, ao passo que os SSDs são de acesso aleatório. As velocidades de acesso do SSD são tipicamente de 3 a 5 vezes maiores que nos dispositivos HDD. Como não têm partes móveis, os SSDs consomem menos energia e são mais confiáveis do que os HDDs.

A capacidade de armazenamento dos HDDs e SSDs está aumentando constantemente. Atualmente, HDDs de 5 terabytes e SSDs de 1 terabyte são facilmente encontrados no mercado. Apesar disso, uma maior capacidade de armazenamento nem sempre é melhor. Quando um dispositivo de armazenamento falha, todas as informações são perdidas. E, é claro, o backup leva mais tempo quando há mais informações para salvar. Para aplicativos que leem e gravam uma grande quantidade de dados, a latência e o desempenho podem ser mais importantes do que a capacidade.

Os sistemas modernos usam SCSI (*Small Computer System Interface*) ou SATA (*Serial AT* *Attachment*) para conectar-se aos dispositivos de armazenamento. Essas interfaces são tipicamente suportadas pelo conector apropriado na placa-mãe. O carregamento inicial do sistema vem de um dispositivo de armazenamento conectado à placa-mãe. As configurações de firmware definem a ordem em que os dispositivos são acessados para esse carregamento inicial.

Os sistemas de armazenamento conhecidos como RAID (*Redundant Array of Independent Disks*) são uma implementação comum para evitar a perda de informações. Uma matriz RAID consiste em vários dispositivos físicos que contêm cópias duplicadas das informações. Se um desses dispositivos falhar, todas as informações ainda estarão disponíveis nos outros. As diferentes configurações físicas de RAID são conhecidas como 0, 1, 5, 6 e 10. Cada designação oferece diferentes tamanhos de armazenamento, características de desempenho e maneiras de armazenar dados redundantes ou somas de verificação para recuperação de dados. Tirando um pequeno trabalho extra de configuração do administrador, a existência de um RAID passa despercebida para os usuários.

Os dispositivos de armazenamento geralmente leem e gravam dados na forma de blocos de bytes. O comando `lsblk` pode ser usado para listar os dispositivos de bloco disponíveis para um sistema. O exemplo a seguir foi executado em um Raspberry Pi usando um cartão SD como dispositivo de armazenamento. Os detalhes da saída serão abordado nas lições sobre *Partições* e *Drivers* a seguir:

```bash
$ lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
mmcblk0     179:0    0 29.7G  0 disk
+-mmcblk0p1 179:1    0 43.9M  0 part /boot
+-mmcblk0p2 179:2    0 29.7G  0 part /
```

##### Partições

Um dispositivo de armazenamento é, na verdade uma longa sequência de locais de armazenamento. O particionamento é o mecanismo que informa ao Linux se ele deve tratar esses locais de armazenamento como uma única sequência ou como diversas sequências independentes. Cada partição é tratada como se fosse um dispositivo individual. Na maioria das vezes, as partições são criadas quando um sistema é configurado pela primeira vez. Se for preciso mudar alguma coisa, existem ferramentas administrativas que permitem gerenciar o particionamento de dispositivos.

Mas qual seria o interesse de se configurar diversas partições? Alguns usos comuns de partições incluem gerenciar o espaço de armazenamento disponível, isolar a sobrecarga de criptografia ou oferecer suporte a diferentes sistemas de arquivos. As partições possibilitam inicializar um único dispositivo de armazenamento em diferentes sistemas operacionais.

Embora o Linux seja capaz de reconhecer a sequência de armazenamento de um dispositivo bruto, um dispositivo bruto não pode ser usado do jeito que chega da loja. Antes, ele deve ser formatado. A formatação determina um sistema de arquivos para o dispositivo e o prepara para as operações de arquivo. Sem um sistema de arquivos, um dispositivo não pode ser usado para operações relacionadas a arquivos.

Os usuários veem as partições como se fossem dispositivos individuais. Dessa maneira, é fácil esquecer que só existe um único dispositivo físico. Particularmente, as operações de dispositivo para dispositivo - que na verdade são operações de partição para partição - não terão o desempenho esperado. Um único dispositivo é um mecanismo físico com um conjunto de hardware de leitura/gravação. Mas o mais importante a se lembrar é que não é possível usar as partições de um único dispositivo físico como um design à prova de falhas. Se o dispositivo falhar, todas as partições falharão ao mesmo tempo.

> [!note]
> O *Gerenciador de Volume Lógico* (Logical Volume Manager ou LVM) é um recurso de software que permite aos administradores combinar discos individuais e partições de disco e tratá-los como uma única unidade.

##### Periféricos

Servidores e estações de trabalho precisam de uma combinação de CPU, memória do sistema e armazenamento para operar. Mas esses componentes fundamentais não se relacionam diretamente com o mundo externo. Os periféricos são os dispositivos que fornecem aos sistemas entradas, saídas e acesso ao resto do mundo real.

A maioria das placas-mãe possui conectores externos integrados e suporte em firmware para interfaces periféricas legadas comuns, suportando dispositivos como teclado, mouse, som, vídeo e rede. As placas-mãe recentes geralmente incluem um conector Ethernet para as redes, um conector HDMI para atender às necessidades gráficas básicas e um ou mais conectores USB (*Universal Serial Bus*) para quase todo o resto. Existem várias versões do USB, com velocidades e características físicas diferentes. É comum haver diversas versões de portas USB em uma única placa-mãe.

As placas-mãe também podem ter um ou mais slots de expansão. Os slots de expansão permitem que os usuários adicionem placas de circuito especiais, conhecidas como placas de expansão, que suportam periféricos personalizados, legados e não-padrão. As interfaces gráficas, de som e de rede são placas de expansão comuns. As placas de expansão também suportam RAID e interfaces legadas de formato especial envolvendo conexões seriais e paralelas.

As configurações do tipo *System on a Chip* (SoC) são mais vantajosas no consumo de energia, desempenho, espaço e confiabilidade em comparação com as configurações de placa-mãe, por reunirem processadores, memória do sistema, SSD e hardware para controlar periféricos em um único pacote de circuitos integrados. Os periféricos suportados pelas configurações de SoC são limitados pelos componentes incluídos. Assim, as configurações de SoC tendem a ser desenvolvidas para usos específicos. Telefones, tablets e outros dispositivos portáteis geralmente são baseados na tecnologia SoC.

Alguns sistemas já vêm com periféricos incorporados. Os laptops são semelhantes às estações de trabalho, mas incluem periféricos de exibição, teclado e mouse por padrão. Os sistemas Tudo-Em- Um são semelhantes aos laptops, mas requerem periféricos de mouse e teclado. Em geral os controladores da placa-mãe ou do SoC são fornecidos com periféricos integrados apropriados para um uso específico.

##### Drivers e arquivos de dispositivo

Até agora, esta lição apresentou informações sobre processadores, memória, discos, particionamento, formatação e periféricos. Mas se os usuários comuns precisassem lidar com os detalhes específicos de cada um dos dispositivos que decidissem conectar à sua máquina, esses sistemas seriam praticamente inutilizáveis. Da mesma forma, os desenvolvedores de software precisariam modificar seu código para cada dispositivo novo ou modificado que precisassem suportar.

A solução para este problema de “lidar com os detalhes” existe na forma de um driver de dispositivo. Os drivers de dispositivo aceitam um conjunto padrão de solicitações, convertendo essas solicitações nas atividades de controle apropriadas ao dispositivo. Os drivers de dispositivo permitem que você e os aplicativos executados leiam o arquivo `/home/carol/stuff` sem se preocupar em saber se esse arquivo está em um disco rígido, uma unidade de estado sólido, um cartão de memória, um armazenamento criptografado ou outro dispositivo .

Os arquivos de dispositivos são encontrados no diretório `/dev` e identificam os dispositivos físicos, o acesso aos dispositivos e os drivers suportados. Por convenção, nos sistemas modernos que usam dispositivos de armazenamento baseados em SCSI ou SATA, o nome do arquivo de especificação começa com o prefixo `sd`. O prefixo é seguido por uma letra como `a` ou `b`, indicando um dispositivo físico. Após o prefixo e o identificador do dispositivo, vem um número que indica uma partição no dispositivo físico. Portanto, `/dev/sda` se refere ao primeiro dispositivo de armazenamento inteiro, enquanto `/dev/sda3` se refere à partição 3 do primeiro dispositivo de armazenamento. Há uma convenção de nomenclatura apropriada ao arquivo do dispositivo para cada tipo de dispositivo. Embora não seja possível tratar de todas as convenções de nomenclatura possíveis nesta lição, é importante lembrar que essas convenções são essenciais para a administração do sistema.

O conteúdo do diretório `/dev` está além do escopo desta lição, mas ainda assim é informativo olhar para a entrada referente a um dispositivo de armazenamento. Os arquivos de dispositivos para cartões SD tipicamente usam `mmcblk` como prefixo:

```bash
$ ls -l mmcblk*
brw-rw---- 1 root disk 179, 0 Jun 30 01:17 mmcblk0
brw-rw---- 1 root disk 179, 1 Jun 30 01:17 mmcblk0p1
brw-rw---- 1 root disk 179, 2 Jun 30 01:17 mmcblk0p2
```

Os detalhes da lista para um arquivo de dispositivo são diferentes dos detalhes típicos de um arquivo:

- Ao contrário de um arquivo ou diretório, a primeira letra do campo de permissões é `b`. Isso indica que os blocos são lidos e gravados no dispositivo em blocos, e não em caracteres individuais.
- O campo tamanho tem dois valores separados por vírgula, em vez de um único valor. O primeiro valor geralmente indica um driver específico dentro do kernel e o segundo valor especifica um dispositivo específico operado pelo driver.
- O nome do arquivo usa um número para o dispositivo físico, portanto a convenção de nomenclatura se adapta especificando o sufixo da partição como um `p` seguido de um dígito.

> [!note]
> Cada dispositivo do sistema deve ter uma entrada em `/dev`. Como o conteúdo do diretório `/dev` é criado na instalação, costumam existir entradas para todos os drivers e dispositivos possíveis, mesmo que não haja nenhum dispositivo físico presente.

#### Exercícios Guiados

1. Descreva estes termos:

  Processador

  CPU

  GPU

2. Ao executar principalmente aplicativos de edição de vídeo (uma atividade intensiva em termos de computação), quais componentes e características normalmente teriam o maior impacto na usabilidade do sistema:

  CPU cores - CPU speed - Available system memory - Storage system - GPU - Video display

3. Qual seria o nome do arquivo de dispositivo `/dev` para a partição 3 do terceiro drive SATA de um sistema:

| `sd3p3` |  |
|---|---|
| `sdcp3` |  |
| `sdc3` |  |

#### Exercícios Exploratórios

1. Rode o comando `lsblk` em seu sistema. Identifique os parâmetros abaixo. Caso não tenha um sistema à disposição, analise a lista `lsblk -f` do sistema Raspberry Pi mencionada na seção “Armazenamento”, acima:

  ```bash
  $ lsblk -f
  NAME        FSTYPE LABEL  UUID                                 MOUNTPOINT
  mmcblk0
  +-mmcblk0p1 vfat   boot   9304-D9FD                            /boot
  +-mmcblk0p2 ext4   rootfs 29075e46-f0d4-44e2-a9e7-55ac02d6e6cc /
  ```

  - Tipos de dispositivo e quantos são
  - A estrutura de partições de cada dispositivo
  - O tipo de sistema de arquivos e a montagem de cada partição

#### Resumo

Um sistema é a soma de seus componentes. Diferentes componentes afetam o custo, o desempenho e a usabilidade de diferentes maneiras. Embora existam configurações comuns para estações de trabalho e servidores, não há uma configuração que seja melhor que as outras.

#### Respostas aos Exercícios Guiados

1. Descreva estes termos:

  **Processador**

  Um termo geral que se aplica a qualquer tipo de processador. Muitas vezes usado incorretamente como sinônimo de CPU.

  **CPU**

  Unidade Central de Processamento. Uma unidade de processamento que suporta as tarefas computacionais de uso geral.

  **GPU**

  Unidade de Processamento Gráfico. Uma unidade de processamento otimizada para suportar atividades relacionadas à apresentação de imagens.

2. Ao executar principalmente aplicativos de edição de vídeo (uma atividade intensiva em termos de computação), quais componentes e características normalmente teriam o maior impacto na usabilidade do sistema:

  **Núcleos da CPU**

  Sim. Uma configuração com múltiplos núcleos suporta as tarefas concorrentes de apresentação e renderização exigidas pela edição de vídeo.

  **Velocidade da CPU**

  Sim. A renderização de vídeo requer uma dose significativa de atividade computacional.

  **Memória disponível do sistema**

  Provavelmente. O vídeo não-compactado usado na edição é grande. Os sistemas de uso geral costumam vir com 8 gigabytes de memória. Uma memória de 16 ou mesmo 32 gigabytes permitiria que o sistema operasse mais quadros de vídeo não compactado, aumentando a eficácia das atividades de edição.

  **Sistema de armazenamento**

  Sim. Os arquivos de vídeo são grandes. A sobrecarga de um drive SSD local suporta uma transferência mais eficiente. Drives de rede mais lentos seriam contraproducentes.

  **GPU**

  Não. A GPU teria um impacto principalmente na apresentação do vídeo renderizado.

  **Exibição de vídeo**

  Não. A exibição de vídeo teria um impacto principalmente na apresentação do vídeo renderizado.

3. Qual seria o nome do arquivo de dispositivo `/dev` para a partição 3 do terceiro drive SATA de um sistema:

| `sd3p3` | Incorreto. O Drive 3 seria `sdc` e não `sd3` |
|---|---|
| `sdcp3` | Incorreto. A Partição 3 seria `3` e não `p3` |
| `sdc3` | Correto |

#### Respostas aos Exercícios Exploratórios

1. Rode o comando `lsblk` em seu sistema. Identifique os parâmetros abaixo. Caso não tenha um sistema à disposição, analise a lista `lsblk -f` do sistema Raspberry Pi mencionada na seção “Armazenamento”, acima:

  ```bash
  $ lsblk -f
  NAME        FSTYPE LABEL  UUID                                 MOUNTPOINT
  mmcblk0
  +-mmcblk0p1 vfat   boot   9304-D9FD                            /boot
  +-mmcblk0p2 ext4   rootfs 29075e46-f0d4-44e2-a9e7-55ac02d6e6cc /
  ```

  As respostas a seguir baseiam-se na lista `lsblk -f` do sistema Raspberry Pi mostrado anteriormente. Suas respostas podem ser diferentes:

  **Tipos de dispositivo e quantos são**

  Há um só dispositivo: `mmcblk0`. Por convenção, sabemos que `mmcblk` seria um cartão de memória USB.

  **A estrutura de partições de cada dispositivo**

  Existem duas partições: `mmcblk0p1` e `mmcblk0p2`.

  **O tipo de sistema de arquivos e a montagem de cada partição**

  A Partição 1 usa o sistema de arquivos `vfat`. Ele é usado para inicializar o sistema e está montado como `/boot`. A Partição 2 usa o sistema de arquivos `ext4`. Ele é usado como o sistema de arquivos principais e está montado como `/`.

## 4.3 Onde os dados são armazenados

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 4.3
- **Peso**: 3

**Áreas chave de conhecimento**

- Programas e configuração, pacotes e banco de dados de pacotes
- Processos, endereços de memória, mensagens do sistema; logando-se.

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `ps`, `top`, `free`
- `syslog`, `dmesg`
- `/etc/`, `/var/log/`
- `/boot/`, `/proc/`, `/dev/`, `/sys/`

### 4.3 Lição 1

#### Introdução

Um sistema operacional considera que tudo são dados. Para o Linux, tudo é considerado como um arquivo: programas, arquivos regulares, diretórios, dispositivos de bloco (como os discos rígidos), dispositivos de caracteres (como os consoles), processos do kernel, sockets, partições, links etc. A estrutura de diretórios do Linux , começando com o *root* `/`, é uma coleção de arquivos que contêm dados. Essa redução de tudo a arquivos é um recurso poderoso do Linux, pois permite refinar praticamente todos os aspectos do sistema.

Nesta lição, discutiremos os diferentes locais em que dados importantes são armazenados, conforme estabelecido pelo Linux Filesystem Hierarchy Standard (FHS). Alguns desses locais são diretórios reais que armazenam dados de maneira permanente em discos, enquanto outros são pseudo-sistemas de arquivos carregados na memória que nos dão acesso aos dados do subsistema do kernel, como processos em execução, uso de memória, configuração de hardware e assim por diante. Os dados armazenados nesses diretórios virtuais são usados por uma série de comandos que nos permitem monitorar e manipular esses dados.

##### Programas e suas configurações

Sem a menor dúvida, os dados importantes de um sistema Linux são seus programas e os arquivos de configuração correspondentes. Os primeiros são arquivos executáveis que contêm conjuntos de instruções a serem executadas pelo processador do computador, ao passo que os últimos geralmente consistem em documentos de texto que controlam a operação de um programa. Os arquivos executáveis podem ser arquivos binários ou de texto. Os arquivos de texto executáveis são chamados de scripts. Os dados de configuração no Linux também são tradicionalmente armazenados em arquivos de texto, embora existam diversos estilos de representação de dados de configuração.

###### Onde os arquivos binários são armazenados

Como qualquer outro arquivo, os arquivos executáveis vivem em diretórios vinculados a `/`. Mais especificamente, os programas são distribuídos em uma estrutura de três camadas: a primeira camada (`/`) inclui os programas que podem ser necessários no modo de usuário único, a segunda camada (`/usr`) contém a maioria dos programas multiusuários e a terceira camada (`/usr/local`) é usada para armazenar o software que não é fornecido pela distribuição e foi compilado localmente.

Tipicamente, os programas estão nestes locais:

`/sbin`

Contém binários essenciais para a administração do sistema, como `parted` ou `ip`.

`/bin`

Contém binários essenciais para todos os usuários, como `ls`, `mv` ou `mkdir`.

`/usr/sbin`

Armazena binários para administração do sistema, como `deluser` ou `groupadd`.

`/usr/bin`

Inclui a maioria dos arquivos executáveis - como `free`, `pstree`, `sudo` or `man` — que podem ser acessados por todos os usuários.

`/usr/local/sbin`

Usado para armazenar programas instalados localmente para a administração do sistema e que não são gerenciados pelo gerenciador de pacotes do sistema.

`/usr/local/bin`

Tem a mesma finalidade de `/usr/local/sbin`, mas para programas comuns de usuário.

Recentemente, algumas distribuições começaram a substituir `/bin` e `/sbin` por links simbólicos para `/usr/bin` e `/usr/sbin`.

> [!note]
> O diretório `/opt` às vezes é usado para armazenar aplicativos opcionais de terceiros.

Além desses diretórios, os usuários comuns podem ter seus próprios programas em:

- `/home/$USER/bin`
- `/home/$USER/.local/bin`

> [!tip]
> Para descobrir quais diretórios estão disponíveis para executar binários, referencie a variável `PATH` com `echo $PATH`. Para saber mais sobre o `PATH`, reveja as lições sobre variáveis e customização do shell.

Podemos encontrar o local dos programas com o comando `which`:

```bash
$ which git
/usr/bin/git
```

###### Onde os arquivos de configuração são armazenados

**O Diretório** `/etc`

Nos primeiros dias do Unix, havia uma pasta para cada tipo de dados, como `/bin` para binários e `/boot` para o(s) kernel(s). No entanto, `/etc` (que significa literalmente *et cetera*) foi criado como um diretório abrangente para armazenar todos os arquivos que não pertenciam às outras categorias. A maioria deles eram arquivos de configuração. Com o passar do tempo, mais e mais arquivos de configuração foram adicionados, de modo que o `/etc` se tornou a pasta principal dos arquivos de configuração dos programas. Como já explicamos, um arquivo de configuração geralmente é um arquivo local de texto puro sem formatação (diferente de um arquivo binário) que controla a operação de um programa.

No `/etc`, encontramos diferentes padrões para os nomes dos arquivos de configuração:

- Arquivos com extensão *ad hoc* ou sem extensão, como por exemplo

  `group`

  Banco de dados de grupo do sistema. `hostname`

  Nome do computador na rede.

  `hosts`

  Lista de endereços IP com sua tradução em nomes de computadores na rede.

  `passwd`

  Banco de dados do usuário do sistema — composto por sete campos separados por dois pontos, fornecendo informações sobre o usuário.

  `profile`

  Arquivo de configuração de todo o sistema para o Bash.

  `shadow`

  Arquivo criptografado para as senhas de usuário.

- Arquivos de inicialização terminados em `rc`:

  `bash.bashrc`

  Arquivo `.bashrc` de todo o sistema para shells bash interativos.

  `nanorc`

  Exemplo de arquivo de inicialização para o GNU nano (um editor de texto simples que normalmente é fornecido com qualquer distribuição).

- Arquivos terminados em `.conf`:

  `resolv.conf`

  Arquivo de configuração do resolvedor — que fornece acesso ao DNS (Internet Domain Name System).

  `sysctl.conf`

  Arquivo de configuração para definir variáveis de sistema para o kernel.

- Diretórios com sufixo `.d`:

  Alguns programas com um arquivo de configuração exclusivo (`*.conf` ou outro) trazem um diretório `*.d` dedicado que ajuda a criar configurações modulares e mais robustas. Por exemplo, para configurar o logrotate, encontramos o diretório `logrotate.conf`, mas também os diretórios `logrotate.d`.

  Esse tratamento é útil nos casos em que aplicativos diferentes precisam de configurações para um mesmo serviço específico. Se, por exemplo, um pacote de servidor web contiver uma configuração de logrotate, essa configuração poderá ser posta em um arquivo dedicado no diretório `logrotate.d`. Esse arquivo pode ser atualizado pelo pacote do servidor web sem interferir na configuração restante de logrotate. Da mesma forma, os pacotes podem adicionar tarefas específicas colocando arquivos no diretório `/etc/cron.d` em vez de modificar `/etc/crontab`.

  No Debian - e derivados do Debian - essa abordagem foi aplicada à lista de fontes confiáveis lidas pela ferramenta de gerenciamento de pacotes `apt`: além do clássico `/etc/apt/sources.list`, agora encontramos o diretório `/etc/apt/sources.list.d`:

  ```bash
  $ ls /etc/apt/sources*
  /etc/apt/sources.list
  /etc/apt/sources.list.d:
  ```

**Arquivos de configuração em** `HOME` **(Dotfiles)**

No nível do usuário, os programas armazenam suas configurações e arquivos em arquivos ocultos no diretório inicial do usuário (também representado como `~`). Lembre-se de que os arquivos ocultos começam com um ponto (`.`), donde o nome: *dotfiles*.

Alguns desses dotfiles são scripts Bash que personalizam a sessão de shell do usuário, originados assim que o usuário faz login no sistema:

`.bash_history`

Armazena o histórico da linha de comando.

`.bash_logout`

Inclui comandos a executar quando o usuário sai do shell de login.

`.bashrc`

Script de inicialização do Bash para shells não-login.

`.profile`

Script de inicialização do Bash para shells de login.

> [!note]
> Consulte a lição “As bases da linha de comando” para aprender mais sobre o Bash e seus arquivos de inicialização.

Outros arquivos de configuração específicos ao usuário são obtidos na inicialização dos programas respectivos: `.gitconfig`, `.emacs.d`, `.ssh` etc.

##### O kernel do Linux

Antes que qualquer processo possa ser executado, o kernel deve ser carregado em uma área protegida da memória. Depois disso, o processo com o PID `1` (quase sempre o `systemd` hoje em dia) desencadeia a cadeia de processos, ou seja, um processo inicia outro(s) e assim por diante. Uma vez que os processos estão ativos, o kernel do Linux é encarregado de alocar recursos para eles (teclado, mouse, discos, memória, interfaces de rede etc.).

> [!note]
> Antes do `systemd`, o primeiro processo em um sistema Linux sempre era `/sbin/init`, como parte do gerenciador de sistemas *System V Init*. Na verdade, `/sbin/init`, ainda podemos encontrar o mas vinculado a `/lib/systemd/systemd`.

###### Onde os Kernels estão armazenados: `/boot`

O kernel reside em `/boot`, junto com outros arquivos relacionados à inicialização. A maioria desses arquivos inclui os componentes do número da versão do kernel em seu nome (versão do kernel, revisão principal, revisão secundária e número do patch).

O diretório `/boot` inclui os seguintes tipos de arquivos, com nomes correspondentes à respectiva versão do kernel:

`config-4.9.0-9-amd64`

Definições de configuração do kernel, como opções e módulos que foram compilados junto com o kernel.

`initrd.img-4.9.0-9-amd64`

Imagem de disco RAM inicial que ajuda no processo de inicialização, carregando um sistema de arquivos root temporário na memória.

`System-map-4.9.0-9-amd64`

O arquivo\` System-map\` (em certos sistemas, `System.map`) contém localizações de endereços de memória para nomes de símbolos do kernel. Cada vez que um kernel é reconstruído, o conteúdo do arquivo muda, pois as localizações da memória podem ser diferentes. O kernel usa este arquivo para procurar localizações de endereços de memória para um símbolo do kernel determinado, ou vice-versa.

`vmlinuz-4.9.0-9-amd64`

O kernel propriamente dito, em um formato compactado de extração automática (vem daí o `z` in `vmlinuz`; `vm` significa memória virtual e começou a ser usado quando o kernel começou a ter suporte a memória virtual).

`grub`

Diretório de configuração do gerenciador de inicialização `grub2`.

> [!tip]
> Por se tratar de um recurso crítico do sistema operacional, mais de um kernel e seus arquivos associados são mantidos em `/boot`, caso o kernel padrão apresente algum defeito e seja preciso voltar a uma versão anterior para — pelo menos — ser possível inicializar o sistema e repará-lo.

###### O diretório `/proc`

O diretório `/proc` é um dos chamados sistemas de arquivos virtuais ou pseudo-sistemas de arquivos, pois seu conteúdo não é gravado no disco, mas carregado na memória. Ele é preenchido de forma dinâmica sempre que o computador é inicializado e reflete constantemente o estado atual do sistema. O `/proc` inclui informações sobre:

- Processos em execução
- Configuração do kernel
- Hardware do sistema

Além de todos os dados referentes aos processos que veremos na próxima lição, esse diretório também armazena arquivos com informações sobre o hardware do sistema e as definições de configuração do kernel. Alguns desses arquivos são:

`/proc/cpuinfo`

Armazena informações sobre a CPU do sistema:

```bash
$ cat /proc/cpuinfo
processor   : 0
vendor_id   : GenuineIntel
cpu family  : 6
model       : 158
model name  : Intel(R) Core(TM) i7-8700K CPU @ 3.70GHz
stepping    : 10
cpu MHz     : 3696.000
cache size  : 12288 KB
(...)
```

`/proc/cmdline`

Armazena as strings passadas para o kernel na inicialização:

```bash
$ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-4.9.0-9-amd64 root=UUID=5216e1e4-ae0e-441f-b8f5-8061c0034c74 ro
quiet
```

`/proc/modules`

Mostra a lista de módulos carregados no kernel:

```bash
$ cat /proc/modules
nls_utf8 16384 1 - Live 0xffffffffc0644000
isofs 40960 1 - Live 0xffffffffc0635000
udf 90112 0 - Live 0xffffffffc061e000
crc_itu_t 16384 1 udf, Live 0xffffffffc04be000
fuse 98304 3 - Live 0xffffffffc0605000
vboxsf 45056 0 - Live 0xffffffffc05f9000 (O)
joydev 20480 0 - Live 0xffffffffc056e000
vboxguest 327680 5 vboxsf, Live 0xffffffffc05a8000 (O)
hid_generic 16384 0 - Live 0xffffffffc0569000
(...)
```

###### O diretório `/proc/sys`

Este diretório inclui as definições de configuração do kernel em arquivos classificados em categorias por subdiretório:

```bash
$ ls /proc/sys
abi  debug  dev  fs  kernel  net  user  vm
```

A maioria desses arquivos funciona como um interruptor e — portanto — só contém um dentre dois valores possíveis: `0` ou `1` (“ligado” ou “desligado”). Por exemplo:

`/proc/sys/net/ipv4/ip_forward`

O valor que habilita ou desabilita a máquina para atuar como roteador (capaz de encaminhar pacotes):

```bash
$ cat /proc/sys/net/ipv4/ip_forward
0
```

Porém, há algumas exceções:

`/proc/sys/kernel/pid_max`

O PID máximo permitido:

```bash
$ cat /proc/sys/kernel/pid_max
32768
```

> [!warning]
> Tenha muito cuidado ao alterar as configurações do kernel, pois o valor errado pode causar instabilidade no sistema.

##### Dispositivos de hardware

Lembre-se, no Linux “tudo é arquivo”. Ou seja, as informações sobre o hardware do dispositivo, bem como as próprias configurações do kernel, são todas armazenadas em arquivos especiais que residem em diretórios virtuais.

###### O diretório `/dev`

O diretório *device* (dispositivo) `/dev` contém arquivos (ou nós) de dispositivos para todos os dispositivos de hardware conectados. Esses arquivos de dispositivo são usados como interface entre os dispositivos e os processos que os utilizam. Cada arquivo de dispositivo se enquadra em uma destas duas categorias:

- **Dispositivos de bloco**: São aqueles em que os dados são lidos e gravados em blocos que podem ser endereçados individualmente. Podemos dar como exemplo os discos rígidos (e suas partições, como `/dev/sda1`), as unidades flash USB, CDs, DVDs etc.
- **Dispositivos de caracteres**: são aqueles em que os dados são lidos e gravados sequencialmente, um caractere de cada vez, como é o caso dos teclados, console de texto (`/dev/console`), portas seriais (como `/dev/ttyS0` e outras) etc.

Ao listar os arquivos do dispositivo, use `ls` com a opção `-l` para diferenciar os dois. Podemos — por exemplo — verificar discos rígidos e partições:

```bash
# ls -l /dev/sd*
brw-rw---- 1 root disk 8, 0 may 25 17:02 /dev/sda
brw-rw---- 1 root disk 8, 1 may 25 17:02 /dev/sda1
```

```
brw-rw---- 1 root disk 8, 2 may 25 17:02 /dev/sda2
(...)
```

Ou para terminais seriais (TeleTYpewriter):

```bash
# ls -l /dev/tty*
crw-rw-rw- 1 root tty     5,  0 may 25 17:26 /dev/tty
crw--w---- 1 root tty     4,  0 may 25 17:26 /dev/tty0
crw--w---- 1 root tty     4,  1 may 25 17:26 /dev/tty1
(...)
```

Observe que o primeiro caractere é `b` para dispositivos de bloco e `c` para dispositivos de caracteres.

> [!tip]
> O asterisco (`*`) é um caractere de globbing que significa 0 ou mais caracteres. Por isso, ele é importante nos comandos `ls -l /dev/sd*` e `ls -l /dev/tty*` mostrados acima. Para saber mais sobre esses caracteres especiais, consulte a lição sobre globbing.

Além disso, `/dev` inclui alguns arquivos especiais bastante úteis para diferentes finalidades de programação:

`/dev/zero`

Fornece tantos caracteres nulos quantos solicitados.

`/dev/null`

Também chamado de *balde de bits*. Descarta todas as informações enviadas para ele.

`/dev/urandom`

Gera números pseudo-aleatórios.

###### O diretório `/sys`

O *sistema de arquivos sys* (`sysfs`) é montado em `/sys`. Foi introduzido com a chegada do kernel 2.6 e representou um grande progresso em `/proc/sys`.

Os processos têm de interagir com os dispositivos em `/dev` e, portanto, o kernel precisa de um diretório que contenha informações sobre esses dispositivos de hardware. Esse diretório é o `/sys`, e seus dados são organizados em categorias. Por exemplo, para verificar o endereço MAC da sua placa de rede (`enp0s3`), aplicaríamos `cat` no seguinte arquivo:

```bash
$ cat /sys/class/net/enp0s3/address
08:00:27:02:b2:74
```

##### Memória e tipos de memória

Basicamente, para um programa começar a rodar, ele precisa ser carregado na memória. De modo geral, quando falamos de memória, nos referimos à *Memória de Acesso Randômico* (RAM), que — quando comparada aos discos rígidos mecânicos — tem a vantagem de ser muito mais rápida. Pelo lado negativo, ela é volátil (ou seja, quando o computador é desligado, os dados desaparecem).

Não obstante o mencionado acima, quando se trata de memória, podemos diferenciar dois tipos principais em um sistema Linux:

- **Memória física**: Também conhecida como *RAM*, vem na forma de chips compostos de circuitos integrados contendo milhões de transistores e capacitores. Estes, por sua vez, formam células de memória (o componente básico da memória do computador). Cada uma dessas células tem um código hexadecimal associado — um endereço de memória — que pode ser referenciado quando necessário.
- **Swap**: Também conhecida como *memória de troca*, é a parte da memória virtual que fica no disco rígido e é usada quando não há mais RAM disponível.

Por outro lado, existe o conceito de *memória virtual*, que é uma abstração da quantidade total de memória utilizável, incluindo a memória (a RAM, mas também o espaço em disco) tal como é vista pelos aplicativos.

`free` **analisa** `/proc/meminfo` **e exibe a quantidade de memória livre e usada no sistema de**

**maneira bem clara**

```bash
$ free
total        used        free      shared  buff/cache   available
Mem:        4050960     1474960     1482260       96900     1093740     2246372
Swap:       4192252           0     4192252
```

Vamos entender melhor as diferentes colunas: `total`

Quantidade total de memória física e de troca instalada.

`used`

Quantidade de memória física e de troca atualmente em uso.

`free`

Quantidade de memória física e de troca que não está atualmente em uso.

`shared`

Quantidade de memória física usada — principalmente — por `tmpfs`.

`buff/cache`

Quantidade de memória física atualmente em uso pelos buffers do kernel, a cache e as slabs.

`available`

Estimativa da memória física disponível para novos processos.

Por padrão, `free` mostra valores em kibibytes, mas permite uma variedade de opções para exibir os resultados em diferentes unidades de medida. Algumas dessas opções são:

`-b`

Bytes.

`-m`

Mebibytes.

`-g`

Gibibytes.

`-h`

Formato legível por humanos.

`-h` sempre é confortável de ler:

```bash
$ free -h
total        used        free      shared  buff/cache   available
Mem:           3,9G        1,4G        1,5G         75M        1,0G        2,2G
Swap:          4,0G          0B        4,0G
```

> [!note]
> Um kibibyte (KiB) é igual a 1.024 bytes, enquanto um kilobyte (KB) é igual a 1000

bytes. O mesmo se aplica, respectivamente, a mebibytes, gibibytes etc.

#### Exercícios Guiados

1. Use o comando `which` para descobrir a localização dos seguintes programas e preencha a tabela:

| **Programa** | **comando** `which` | **Caminho para o** **executável (saída)** | **O usuário precisa de** **privilégios de** `root`**?** |
|---|---|---|---|
| `swapon` |  |  |  |
| `kill` |  |  |  |
| `cut` |  |  |  |
| `usermod` |  |  |  |
| `cron` |  |  |  |
| `ps` |  |  |  |

2. Onde se encontram os arquivos a seguir?

| **Arquivo** | `/etc` | `~` |
|---|---|---|
| `.bashrc` |  |  |
| `bash.bashrc` |  |  |
| `passwd` |  |  |
| `.profile` |  |  |
| `resolv.conf` |  |  |
| `sysctl.conf` |  |  |

3. Explique o significado dos elementos numéricos no arquivo do kernel `vmlinuz-4.15.0-50-` `generic` encontrado em `/boot`:

| **Elemento numérico** |  |  | **Significado** |
|---|---|---|---|
| `4` |  |  |  |
| `15` |  |  |  |
| `0` |  |  |  |
| `50` |  |  |  |

4. Qual comando você usaria para listar todos os discos rígidos e partições em `/dev`?

#### Exercícios Exploratórios

1. Os arquivos de dispositivo para discos rígidos são representados com base nos controladores que eles usam — vimos `/dev/sd*` para unidades que usam SCSI (Small Computer System Interface) e SATA (Serial Advanced Technology Attachment), mas

  - Como as antigas unidades IDE (Integrated Drive Electronics) eram representadas?
  - E as unidades NVMe (Non-Volatile Memory Express) modernas?

2. Analise o arquivo `/proc/meminfo`. Compare o conteúdo desse arquivo com a saída do comando `free` e identifique qual chave de `/proc/meminfo` corresponde aos campos seguintes na saída de `free`:

| **saída de** `free` | **campo** `/proc/meminfo` |
|---|---|
| `total` |  |
| `free` |  |
| `shared` |  |
| `buff/cache` |  |
| `available` |  |

#### Resumo

Nesta lição, você aprendeu sobre a localização dos programas e seus arquivos de configuração em um sistema Linux. O que é importante lembrar:

- Basicamente, os programas são encontrados em uma estrutura de diretórios em três níveis: `/`, `/usr` e `/usr/local`. Cada um desses níveis pode conter diretórios `bin` e `sbin`.
- Os arquivos de configuração são armazenados em `/etc` e `~`.
- Os dotfiles são arquivos ocultos que começam com um ponto (`.`).

Também falamos sobre o kernel do Linux. Conceitos importantes:

- Para o Linux, tudo é arquivo.
- O kernel do Linux mora em `/boot`, junto com outros arquivos relacionados à inicialização.
- Para os processos começarem a rodar, o kernel precisa ser carregado primeiro em uma área protegida da memória.
- O trabalho do kernel é alocar recursos do sistema aos processos.
- O sistema de arquivos virtual (ou pseudo) `/proc` armazena dados importantes do kernel e do sistema de forma volátil.

Da mesma forma, exploramos os dispositivos de hardware e aprendemos o seguinte:

- O diretório `/dev` armazena arquivos especiais (também chamados de nós) para todos os dispositivos de hardware conectados: *dispositivos de bloco* ou *dispositivos de caracteres*. Os primeiros transferem os dados em blocos; os outros, um caractere de cada vez.
- O diretório `/dev` também contém outros arquivos especiais como `/dev/zero`, `/dev/null` ou `/dev/urandom`.
- O diretório `/sys` armazena informações sobre dispositivos de hardware, organizadas em categorias.

Finalmente, falamos um pouco da memória. Nós aprendemos que:

- Um programa roda quando é carregado na memória.
- O que é RAM (Memória de Acesso Randômico).
- O que é Swap ou troca.
- Como exibir o uso da memória.

Comandos usados nesta lição: `cat`

Concatena/imprime o conteúdo do arquivo.

`free`

Exibe a quantidade de memória livre e usada no sistema.

`ls`

Lista o conteúdo do diretório.

`which`

Mostra a localização do programa.

#### Respostas aos Exercícios Guiados

1. Use o comando `which` para descobrir a localização dos seguintes programas e preencha a tabela:

| **Programa** | **comando** `which` | **Caminho para o** **executável (saída)** | **O usuário precisa de** **privilégios de** `root`**?** |
|---|---|---|---|
| `swapon` | `which swapon` | `/sbin/swapon` | Sim |
| `kill` | `which kill` | `/bin/kill` | Não |
| `cut` | `which cut` | `/usr/bin/cut` | Não |
| `usermod` | `which usermod` | `/usr/sbin/usermod` | Sim |
| `cron` | `which cron` | `/usr/sbin/cron` | Sim |
| `ps` | `which ps` | `/bin/ps` | Não |

2. Onde se encontram os arquivos a seguir?

| **Arquivo** | `/etc` | `~` |
|---|---|---|
| `.bashrc` |  | X |
| `bash.bashrc` | X |  |
| `passwd` | X |  |
| `.profile` |  | X |
| `resolv.conf` | X |  |
| `sysctl.conf` | X |  |

3. Explique o significado dos elementos numéricos no arquivo do kernel `vmlinuz-4.15.0-50-` `generic` encontrado em `/boot`:

| **Elemento numérico** | **Significado** |
|---|---|
| `4` | Versão do kernel |
| `15` | Revisão importante |
| `0` | Revisão secundária |
| `50` | Número do patch |

4. Qual comando você usaria para listar todos os discos rígidos e partições em `/dev`? `ls /dev/sd*`

#### Respostas aos Exercícios Exploratórios

1. Os arquivos de dispositivo para discos rígidos são representados com base nos controladores que eles usam — vimos `/dev/sd*` para unidades que usam SCSI (Small Computer System Interface) e SATA (Serial Advanced Technology Attachment), mas

  `/dev/hd*`

  - E as unidades NVMe (Non-Volatile Memory Express) modernas?

  `/dev/nvme*`

2. Analise o arquivo `/proc/meminfo`. Compare o conteúdo desse arquivo com a saída do comando `free` e identifique qual chave de `/proc/meminfo` corresponde aos campos seguintes na saída de `free`:

| **saída de** `free` | **campo** `/proc/meminfo` |
|---|---|
| `total` | `MemTotal` / `SwapTotal` |
| `free` | `MemFree` / `SwapFree` |
| `shared` | `Shmem` |
| `buff/cache` | `Buffers`, `Cached` and `SReclaimable` |
| `available` | `MemAvailable` |

### 4.3 Lição 2

#### Introdução

Depois de explorar os programas e seus arquivos de configuração, vamos aprender como os comandos são executados como processos. Da mesma forma, trataremos das mensagens do sistema, do uso do buffer de anel do kernel e de como a chegada do `systemd` e seu daemon de diário  — `journald` —  mudou a maneira como as coisas eram feitas até então com relação aos registros do sistema.

##### Processos

Sempre que um usuário emite um comando, um programa é executado e um ou mais processos são gerados.

Os processos existem dentro de uma hierarquia. Depois que o kernel é carregado na memória durante a inicialização, é iniciado o primeiro processo que — por sua vez — inicia outros processos, os quais também podem iniciar outros processos. Cada processo possui um identificador exclusivo (`PID`) e um identificador do processo pai (`PPID`). Estes são números inteiros positivos atribuídos em ordem sequencial.

###### Explorando os processos dinamicamente: `top`

Para obter uma lista dinâmica de todos os processos em execução, usamos o comando `top`:

```bash
$ top

top - 11:10:29 up  2:21,  1 user,  load average: 0,11, 0,20, 0,14
Tasks:  73 total,   1 running,  72 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0,0 us,  0,3 sy,  0,0 ni, 99,7 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
KiB Mem :  1020332 total,   909492 free,    38796 used,    72044 buff/cache
KiB Swap:  1046524 total,  1046524 free,        0 used.   873264 avail Mem

PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
436 carol     20   0   42696   3624   3060 R  0,7  0,4   0:00.30 top
4 root      20   0       0      0      0 S  0,3  0,0   0:00.12 kworker/0:0
399 root      20   0   95204   6748   5780 S  0,3  0,7   0:00.22 sshd
1 root      20   0   56872   6596   5208 S  0,0  0,6   0:01.29 systemd
2 root      20   0       0      0      0 S  0,0  0,0   0:00.00 kthreadd
3 root      20   0       0      0      0 S  0,0  0,0   0:00.02 ksoftirqd/0
5 root       0 -20       0      0      0 S  0,0  0,0   0:00.00 kworker/0:0H
6 root      20   0       0      0      0 S  0,0  0,0   0:00.00 kworker/u2:0
7 root      20   0       0      0      0 S  0,0  0,0   0:00.08 rcu_sched
8 root      20   0       0      0      0 S  0,0  0,0   0:00.00 rcu_bh
9 root      rt   0       0      0      0 S  0,0  0,0   0:00.00 migration/0
10 root       0 -20       0      0      0 S  0,0  0,0   0:00.00 lru-add-drain
(...)
```

Como vimos acima, `top` também fornece informações sobre o consumo de memória e CPU do sistema em geral, bem como sobre cada processo.

O `top` permite uma certa interação do usuário.

Por padrão, a saída é classificada pela porcentagem de tempo da CPU usada por cada processo em ordem decrescente. Esse comportamento pode ser modificado pressionando as seguintes teclas de dentro de `top`:

`M`

Classifica por uso da memória.

`N`

Classifica pelo número de identificação do processo.

`T`

Classifica pelo tempo de execução.

`P`

Classifica pela porcentagem de uso da CPU.

Para alternar entre ordem crescente e decrescente, pressione `R`.

> [!tip]
> Uma versão mais sofisticada e amigável do `top` é `htop`. Outra alternativa — talvez mais exaustiva — é `atop`. Se eles ainda não estiverem instalados em seu sistema, use seu gerenciador de pacotes para instalá-los e experimentá-los.

###### Um instantâneo dos processos: `ps`

Outro comando muito útil para obter informações sobre processos é o `ps`. Enquanto `top` fornece informações dinâmicas, as do `ps` são estáticas.

Se invocado sem opções, a saída do `ps` é bastante específica e se refere apenas aos processos vinculados ao shell atual:

```bash
$ ps
PID TTY          TIME CMD
2318 pts/0    00:00:00 bash
2443 pts/0    00:00:00 ps
```

As informações exibidas relacionam-se ao identificador do processo (`PID`), ao terminal no qual o processo está sendo executado (`TTY`), ao tempo de CPU usado pelo processo (`TIME`) e ao comando que iniciou o processo (`CMD`).

Uma opção útil para o `ps` é `-f`, que mostra a listagem em formato completo:

```bash
$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
carol     2318  1682  0 08:38 pts/1    00:00:00 bash
carol     2443  2318  0 08:46 pts/1    00:00:00 ps -f
```

Em combinação com outras opções, `-f` mostra a relação entre os processos pai e filho:

```bash
$ ps -uf
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
```

```
carol       2318  0.0  0.1  21336  5140 pts/1    Ss   08:38   0:00 bash
carol       2492  0.0  0.0  38304  3332 pts/1    R+   08:51   0:00  \_ ps -uf
carol       1780  0.0  0.1  21440  5412 pts/0    Ss   08:28   0:00 bash
carol       2291  0.0  0.7 305352 28736 pts/0    Sl+  08:35   0:00  \_ emacs index.en.adoc
-nw
(...)
```

Da mesma forma, o `ps` pode exibir a porcentagem de memória usada quando invocado com a opção `-v`:

```bash
$ ps -v
PID TTY      STAT   TIME  MAJFL   TRS   DRS   RSS %MEM COMMAND
1163 tty2     Ssl+   0:00      1    67 201224 5576  0.1 /usr/lib/gdm3/gdm-x-session (...)
(...)
```

> [!note]
> Um outro comando visualmente atraente para exibir a hierarquia de processos é o `pstree`. Ele está incluído em todas as principais distribuições.

###### Informações sobre processos no diretório `/proc`

Já vimos o sistema de arquivos `/proc`. O `/proc` inclui um subdiretório numerado para cada processo em execução no sistema (o número é o `PID` do processo):

```
carol@debian:~# ls /proc
1    108  13   17   21   27   354  41   665  8    9
10   109  14   173  22   28   355  42   7    804  915
103  11   140  18   23   29   356  428  749  810  918
104  111  148  181  24   3    367  432  75   811
105  112  149  19   244  349  370  433  768  83
106  115  15   195  25   350  371  5    797  838
107  12   16   2    26   353  404  507  798  899
(...)
```

Assim, todas as informações sobre um processo específico são incluídas dentro de seu diretório. Vamos listar o conteúdo do primeiro processo — aquele cujo `PID` é `1` (a saída foi truncada para facilitar a leitura):

```bash
# ls /proc/1/
attr        cmdline          environ  io        mem       ns
autogroup   comm             exe      limits    mountinfo numa_maps
```

```
auxv        coredump_filter  fd       loginuid  mounts    oom_adj
...
```

Você pode verificar — por exemplo — o executável do processo:

```bash
# cat /proc/1/cmdline; echo
/sbin/init
```

Como vemos, o binário que iniciou a hierarquia de processos era `/sbin/init`.

> [!note]
> Podemos concatenar comandos com ponto e vírgula (`;`). A razão para usar o comando `echo` acima é fornecer uma nova linha. Experimente executar simplesmente `cat /proc/1/cmdline` para ver a diferença.

###### A carga do sistema

Potencialmente, cada processo em um sistema consome recursos. A chamada carga do sistema tenta agregar a carga geral do sistema em um único indicador numérico. Podemos ver a carga atual com o comando `uptime`:

```bash
$ uptime
22:12:54 up 13 days, 20:26,  1 user,  load average: 2.91, 1.59, 0.39
```

Os três últimos dígitos indicam a média de carga do sistema para o último minuto (`2,91`), os últimos cinco minutos (`1.59`) e os últimos quinze minutos (`0.39`), respectivamente.

Cada um desses números indica quantos processos estavam aguardando recursos da CPU ou a conclusão das operações de entrada/saída. Isso significa que esses processos estavam prontos para a execução quando recebessem os respectivos recursos.

##### Registro do sistema e mensagens do sistema

Quando o kernel e os processos começam ser executados e a se comunicar entre si, muitas informações são produzidas. A maior parte é enviada para arquivos — os chamados arquivos de registro ou, simplesmente, *logs*.

Sem esses registros, a busca por um evento que ocorreu em um servidor seria uma verdadeira dor de cabeça para os administradores de sistemas, daí a importância de ter uma maneira padronizada e centralizada de acompanhar os eventos do sistema. Além disso, os logs são claros e determinantes para a solução de problemas e questões de segurança, além de serem fontes de dados confiáveis para entender as estatísticas do sistema e prever tendências.

###### Registros com o Daemon syslog

Tradicionalmente, as mensagens do sistema são gerenciadas pelo recurso de registro padrão — syslog — ou um de seus derivados — syslog-ng ou rsyslog. O daemon de log coleta mensagens de outros serviços e programas e as armazena em arquivos de log, normalmente em `/var/log`. No entanto, alguns serviços cuidam de seus próprios logs (por exemplo, o servidor web Apache HTTPD). Da mesma forma, o kernel do Linux usa um buffer de anel na memória para armazenar suas mensagens de log.

**Arquivos de registro em** `/var/log`

Como os registros são dados que variam ao longo do tempo, normalmente eles são encontrados em `/var/log`.

Se você explorar `/var/log`, perceberá que os nomes dos logs são — até certo ponto — bastante auto-explicativos. Eis alguns exemplos:

`/var/log/auth.log`

Armazena informações sobre a autenticação.

`/var/log/kern.log`

Armazena informações do kernel.

`/var/log/syslog`

Armazena informações do sistema.

`/var/log/messages`

Armazena dados do sistema e aplicativos.

> [!note]
> O nome exato e o conteúdo dos arquivos de log podem variar nas diferentes distribuições Linux.

###### Acessando arquivos de log

Ao explorar arquivos de log, você precisa ser root (se não tiver permissões de leitura) e usar um paginador como `less`:

```bash
# less /var/log/messages
Jun  4 18:22:48 debian liblogging-stdlog:  [origin software="rsyslogd" swVersion="8.24.0" x-
```

```
pid="285" x-info="http://www.rsyslog.com"] rsyslogd was HUPed
Jun 29 16:57:10 debian kernel: [    0.000000] Linux version 4.9.0-8-amd64 (debian-
kernel@lists.debian.org) (gcc version 6.3.0 20170516 (Debian 6.3.0-18+deb9u1) ) #1 SMP
Debian 4.9.130-2 (2018-10-27)
Jun 29 16:57:10 debian kernel: [    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-
8-amd64 root=/dev/sda1 ro quiet
```

Outra alternativa é usar `tail` com a opção `-f` para ler as mensagens mais recentes do arquivo e exibir dinamicamente as novas linhas conforme elas são incluídas:

```bash
# tail -f /var/log/messages
Jul  9 18:39:37 debian kernel: [    2.350572] RAPL PMU: hw unit of domain psys 2^-0 Joules
Jul  9 18:39:37 debian kernel: [    2.512802] input: VirtualBox USB Tablet as
/devices/pci0000:00/0000:00:06.0/usb1/1-1/1-1:1.0/0003:80EE:0021.0001/input/input7
Jul  9 18:39:37 debian kernel: [    2.513861] Adding 1046524k swap on /dev/sda5.  Priority:-
1 extents:1 across:1046524k FS
Jul  9 18:39:37 debian kernel: [    2.519301] hid-generic 0003:80EE:0021.0001:
input,hidraw0: USB HID v1.10 Mouse [VirtualBox USB Tablet] on usb-0000:00:06.0-1/input0
Jul  9 18:39:37 debian kernel: [    2.623947] snd_intel8x0 0000:00:05.0: white list rate for
1028:0177 is 48000
Jul  9 18:39:37 debian kernel: [    2.914805] IPv6: ADDRCONF(NETDEV_UP): enp0s3: link is not
ready
Jul  9 18:39:39 debian kernel: [    4.937283] e1000: enp0s3 NIC Link is Up 1000 Mbps Full
Duplex, Flow Control: RX
Jul  9 18:39:39 debian kernel: [    4.938493] IPv6: ADDRCONF(NETDEV_CHANGE): enp0s3: link
becomes ready
Jul  9 18:39:40 debian kernel: [    5.315603] random: crng init done
Jul  9 18:39:40 debian kernel: [    5.315608] random: 7 urandom warning(s) missed due to
ratelimiting
```

A saída aparecerá no seguinte formato:

- Registro de data e hora
- Nome do host do qual a mensagem veio
- Nome do programa/serviço que gerou a mensagem
- PID do programa que gerou a mensagem
- Descrição da ação que ocorreu

A maioria dos arquivos de registro é gravada em texto simples; no entanto, alguns podem conter dados binários, como é o caso de `/var/log/wtmp` — que armazena dados relevantes para logins bem-sucedidos. Você pode usar o comando `file` para determinar qual é o caso:

```bash
$ file /var/log/wtmp
/var/log/wtmp: dBase III DBT, version number 0, next free block index 8
```

Esses arquivos são normalmente lidos usando comandos especiais. `last` é usado para interpretar os dados em `/var/log/wtmp`:

```bash
$ last
carol    tty2         :0               Thu May 30 10:53   still logged in
reboot   system boot  4.9.0-9-amd64    Thu May 30 10:52   still running
carol    tty2         :0               Thu May 30 10:47 - crash  (00:05)
reboot   system boot  4.9.0-9-amd64    Thu May 30 09:11   still running
carol    tty2         :0               Tue May 28 08:28 - 14:11  (05:42)
reboot   system boot  4.9.0-9-amd64    Tue May 28 08:27 - 14:11  (05:43)
carol    tty2         :0               Mon May 27 19:40 - 19:52  (00:11)
reboot   system boot  4.9.0-9-amd64    Mon May 27 19:38 - 19:52  (00:13)
carol    tty2         :0               Mon May 27 19:35 - down   (00:03)
reboot   system boot  4.9.0-9-amd64    Mon May 27 19:34 - 19:38  (00:04)
```

> [!note]
> Assim como `/var/log/wtmp`, `/var/log/btmp` armazena informações sobre tentativas malsucedidas de login. O comando especial para ler seu conteúdo é `lastb`.

**Rotação do log**

Os arquivos de log podem crescer muito em algumas semanas ou meses e ocupar todo o espaço livre em disco. Para resolver isso, usamos o utilitário `logrotate`. Ele implementa a rotação ou ciclo de log, que implica ações como mover arquivos de log para um novo nome, arquivando-os e/ou compactando-os, às vezes enviando-os por email para o administrador do sistema e, eventualmente, excluindo-os à medida que envelhecem. Há várias convenções usadas para nomear esses arquivos de log rotacionados (por exemplo, adicionando um sufixo com a data); no entanto, o mais comum é adicionar um sufixo com um número inteiro:

```bash
# ls /var/log/apache2/
access.log  error.log  error.log.1  error.log.2.gz  other_vhosts_access.log
```

Note que `error.log.2.gz` já foi compactado com o `gzip` (daí o sufixo `.gz`).

###### O buffer do anel do kernel

O buffer de anel do kernel é uma estrutura de dados de tamanho fixo que registra as mensagens de inicialização do kernel. A função desse buffer — importantíssima — é registrar todas as mensagens do kernel produzidas na inicialização — quando o `syslog` ainda não está disponível. O comando `dmesg` imprime na tela o buffer de anel do kernel (que também costumava ser armazenado em `/var/log/dmesg`). Devido à extensão do buffer de anel, este comando é normalmente usado em combinação com o utilitário de filtragem de texto `grep` ou um paginador como o `less`. Por exemplo, para procurar mensagens de inicialização:

```bash
$ dmesg | grep boot
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-9-amd64 root=UUID=5216e1e4-ae0e-
441f-b8f5-8061c0034c74 ro quiet
[    0.000000] smpboot: Allowing 1 CPUs, 0 hotplug CPUs
[    0.000000] Kernel command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-9-amd64
root=UUID=5216e1e4-ae0e-441f-b8f5-8061c0034c74 ro quiet
[    0.144986] AppArmor: AppArmor disabled by boot time parameter
(...)
```

> [!note]
> Conforme o buffer de anel do kernel vai crescendo com novas mensagens, as mais antigas desaparecem.

###### O diário do sistema: systemd-journald

A partir de 2015, o systemd substituiu o SysV Init como gerenciador de sistemas e serviços na maioria das principais distribuições Linux. Como conseqüência, o daemon do diário — journald — tornou-se o componente de registro padrão, sobrepondo-se ao syslog na maioria dos aspectos. Os dados não são mais armazenados em texto simples, mas em formato binário. Assim, o utilitário `journalctl` é necessário para ler os logs. Além disso, o journald é compatível com syslog e pode ser integrado ao syslog.

`journalctl` é o utilitário usado para ler e consultar o banco de dados do diário do systemd. Quando invocado sem opções, ele imprime o diário inteiro:

```bash
# journalctl
-- Logs begin at Tue 2019-06-04 17:49:40 CEST, end at Tue 2019-06-04 18:13:10 CEST. --
jun 04 17:49:40 debian systemd-journald[339]: Runtime journal (/run/log/journal/) is 8.0M,
max 159.6M, 151.6M free.
jun 04 17:49:40 debian kernel: microcode: microcode updated early to revision 0xcc, date =
2019-04-01
Jun 04 17:49:40 debian kernel: Linux version 4.9.0-8-amd64 (debian-kernel@lists.debian.org)
```

```
(gcc version 6.3.0 20170516 (Debian 6.3.0-18+deb9u1) )
Jun 04 17:49:40 debian kernel: Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-8-amd64
root=/dev/sda1 ro quiet
(...)
```

No entanto, se chamado com as opções `-k` ou `--dmesg`, será equivalente ao uso do comando `dmesg`:

```bash
# journalctl -k
[    0.000000] Linux version 4.9.0-9-amd64 (debian-kernel@lists.debian.org) (gcc version
6.3.0 20170516 (Debian 6.3.0-18+deb9u1) ) #1 SMP Debian 4.9.168-1+deb9u2 (2019-05-13)
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-4.9.0-9-amd64 root=UUID=5216e1e4-ae0e-
441f-b8f5-8061c0034c74 ro quiet
(...)
```

Dentre as outras opções interessantes para o `journalctl` estão:

`-b`**,** `--boot`

Mostra informações de inicialização.

`-u`

Mostra mensagens sobre uma unidade especificada. Grosso modo, uma unidade pode ser definida como qualquer recurso tratado pelo systemd. Por exemplo, `journalctl -u` `apache2.service` é usado para ler mensagens sobre o servidor web `apache2`.

`-f`

Mostra as mensagens mais recentes do diário e segue imprimindo novas entradas à medida que elas são incluídas no diário — a exemplo de `tail -f`.

#### Exercícios Guiados

1. Analise esta lista de `top` e responda às questões a seguir:

  ```
  carol@debian:~$ top

  top - 13:39:16 up 31 min,  1 user,  load average: 0.12, 0.15, 0.10
  Tasks:  73 total,   2 running,  71 sleeping,   0 stopped,   0 zombie
  %Cpu(s):  1.1 us,  0.4 sy,  0.0 ni, 98.6 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
  KiB Mem :  1020332 total,   698700 free,   170664 used,   150968 buff/cache
  KiB Swap:  1046524 total,  1046524 free,        0 used.   710956 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
  605 nobody    20   0 1137620 132424  34256 S  6.3 13.0   1:47.24 ntopng
  444 www-data  20   0  364780   4132   2572 S  0.3  0.4   0:00.44 apache2
  734 root      20   0   95212   7004   6036 S  0.3  0.7   0:00.36 sshd
  887 carol     20   0   46608   3680   3104 R  0.3  0.4   0:00.03 top
  1 root      20   0   56988   6688   5240 S  0.0  0.7   0:00.42 systemd
  2 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kthreadd
  3 root      20   0       0      0      0 S  0.0  0.0   0:00.09 ksoftirqd/0
  4 root      20   0       0      0      0 S  0.0  0.0   0:00.87 kworker/0:0
  (...)
  ```

  - Quais processos foram iniciados pelo usuário `carol`?
  - Qual diretório virtual de `/proc` você deve visitar para encontrar dados relacionados ao comando `top`?
  - Qual processo foi executado primeiro? Como você descobriu?
  - Complete a tabela especificando em qual área da saída de `top` encontramos as seguintes informações:

| **Informações sobre …** | **Área de resumo** | **Área de tarefas** |
|---|---|---|
| Memória |  |  |
| Swap |  |  |
| PID |  |  |

| **Informações sobre …** | **Área de resumo** | **Área de tarefas** |
|---|---|---|
| Tempo da CPU |  |  |
| Comandos |  |  |

2. Qual comando é usado para ler os registros binários a seguir?

  - `/var/log/wtmp`
  - `/var/log/btmp`
  - `/run/log/journal/2a7d9730cd3142f4b15e20d6be631836/system.journal`

3. Em combinação com `grep`, quais comandos você usaria para descobrir as seguintes informações sobre seu sistema Linux?

  - Data da última reinicialização do sistema (`wtmp`)
  - Quais são os discos rígidos instalados (`kern.log`)
  - Quando foi feito o último login (`auth.log`)

4. Quais dois comandos você usaria para exibir o buffer de anel do kernel?

5. Indique o local a que pertencem as seguintes mensagens de log:

  - `Jul 10 13:37:39 debian dbus[303]: [system] Successfully activated service` `'org.freedesktop.nm_dispatcher'`

| `/var/log/auth.log` |  |
|---|---|
| `/var/log/kern.log` |  |
| `/var/log/syslog` |  |
| `/var/log/messages` |  |

  - `Jul 10 11:23:58 debian kernel: [ 1.923349] usbhid: USB HID core driver`

  `/var/log/auth.log`

  `/var/log/kern.log`

  `/var/log/syslog`

  `/var/log/messages`

  - `Jul 10 14:02:53 debian sudo: pam_unix(sudo:session): session opened for` `user root by carol(uid=0)`

  `/var/log/auth.log`

  `/var/log/kern.log`

  `/var/log/syslog`

  `/var/log/messages`

  - `Jul 10 11:23:58 debian NetworkManager[322]: <info> [1562750638.8672]` `NetworkManager (version 1.6.2) is starting…`

  `/var/log/auth.log`

  `/var/log/kern.log`

  `/var/log/syslog`

  `/var/log/messages`

6. Use `journalctl` para encontrar informações sobre as seguintes unidades:

| **Unidade** |  |  |  |  | **Comando** |
|---|---|---|---|---|---|
| `ssh` |  |  |  |  |  |
| `networking` |  |  |  |  |  |
| `rsyslog` |  |  |  |  |  |
| `cron` |  |  |  |  |  |

#### Exercícios Exploratórios

1. Retome a saída de `top` dos exercícios guiados e responda às seguintes questões:

  - Quais são as duas etapas a seguir para eliminar o servidor web *apache*?
  - Na área de resumo, como seria possivel exibir as informações sobre a memória física e a memória swap usando barras de progresso?
  - Agora, classifique os processos pelo uso da memória:
  - Agora que as informações sobre a memória estão sendo exibidas em barras de progresso e os processos classificados pelo uso da memória, salve essas configurações para torná-las padrão na próxima vez que você usar o `top`:
  - Qual arquivo armazena as configurações de `top`? Onde ele fica? Como você pode verificar sua existência?

2. Aprenda sobre o comando `exec` no Bash. Tente demonstrar sua funcionalidade iniciando uma sessão do Bash e encontrando o processo do Bash com `ps`. Depois, execute `exec /bin/sh` e busque novamente pelo processo com o mesmo PID.

3. Siga estes passos para explorar os eventos do kernel e o gerenciamento dinâmico de dispositivos do udev:

  - Conecte um drive USB ao seu computador. Rode o `dmesg` e preste atenção às últimas linhas. Qual a linha mais recente?
  - Tendo em mente a saída do comando anterior, execute `ls /dev/sd*` e verifique se seu drive USB aparece na lista. Qual a saída?
  - Agora, remova o drive USB e execute `dmesg` outra vez. O que diz a linha mais recente?
  - Execute `ls /dev/sd*` novamente e verifique se o dispositivo sumiu da lista. Qual a saída?

#### Resumo

No contexto do armazenamento de dados, os seguintes tópicos foram discutidos nesta lição: gerenciamento de processos e registros e mensagens do sistema.

Em relação ao gerenciamento de processos, aprendemos o seguinte:

- Os programas geram processos e os processos existem numa hierarquia.
- Cada processo tem um identificador único (`PID`) e um identificador do processo pai (`PPID`).
- `top` é um comando muito útil para explorar de maneira dinâmica e interativa os processos em execução no sistema.
- `ps` pode ser usado para obter um instantâneo dos processos atualmente em execução no sistema.
- O diretório `/proc` inclui diretórios para cada um dos processos em execução no sistema, nomeados de acordo com o PID de cada um.
- O conceito de carga média do sistema — utilíssimo para conferir a utilização/sobrecarga da CPU.

Em relação ao log do sistema, devemos lembrar que:

- Um log é um arquivo em que os eventos do sistema são registrados. Os logs são inestimáveis para a solução de problemas.
- O log tradicionalmente é tratado por serviços especiais como syslog, syslog-ng ou rsyslog. No entanto, alguns programas usam seus próprios daemons de registro.
- Como os logs são dados variáveis, eles são mantidos em `/var` e — às vezes — seus nomes dão uma pista sobre o conteúdo (`kern.log`, `auth.log` etc.).
- A maioria dos logs é escrita em texto simples e pode ser lida com qualquer editor de texto, desde que você tenha as permissões corretas. No entanto, alguns deles são binários e devem ser lidos usando comandos especiais.
- Para evitar problemas com espaço em disco, uma *rotação do log* é realizada pelo utilitário logrotate.
- Quanto ao kernel, ele usa uma estrutura circular de dados — o buffer de anel — na qual as mensagens de inicialização são mantidas (as mensagens antigas desaparecem com o tempo).
- O gerenciador de sistema e serviços systemd substituiu o init do System V em praticamente todas as distros, tendo o journald se tornado o serviço de registro padrão.
- Para ler o diário do systemd, é necessário o utilitário `journalctl`.

Comandos usados nesta lição:

`cat`

Concatena/imprime o conteúdo do arquivo.

`dmesg`

Imprime o buffer do anel do kernel.

`echo`

Exibe uma linha de texto ou uma nova linha.

`file`

Determina o tipo de arquivo.

`grep`

Imprime linhas de acordo com um padrão.

`last`

Mostra uma lista dos últimos usuários conectados.

`less`

Exibe o conteúdo do arquivo uma página de cada vez.

`ls`

Lista o conteúdo do diretório.

`journalctl`

Consulta o diário `systemd`.

`tail`

Exibe as últimas linhas de um arquivo.

#### Respostas aos Exercícios Guiados

1. Analise esta lista de `top` e responda às questões a seguir:

  ```
  carol@debian:~$ top

  top - 13:39:16 up 31 min,  1 user,  load average: 0.12, 0.15, 0.10
  Tasks:  73 total,   2 running,  71 sleeping,   0 stopped,   0 zombie
  %Cpu(s):  1.1 us,  0.4 sy,  0.0 ni, 98.6 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
  KiB Mem :  1020332 total,   698700 free,   170664 used,   150968 buff/cache
  KiB Swap:  1046524 total,  1046524 free,        0 used.   710956 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
  605 nobody    20   0 1137620 132424  34256 S  6.3 13.0   1:47.24 ntopng
  444 www-data  20   0  364780   4132   2572 S  0.3  0.4   0:00.44 apache2
  734 root      20   0   95212   7004   6036 S  0.3  0.7   0:00.36 sshd
  887 carol     20   0   46608   3680   3104 R  0.3  0.4   0:00.03 top
  1 root      20   0   56988   6688   5240 S  0.0  0.7   0:00.42 systemd
  2 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kthreadd
  3 root      20   0       0      0      0 S  0.0  0.0   0:00.09 ksoftirqd/0
  4 root      20   0       0      0      0 S  0.0  0.0   0:00.87 kworker/0:0
  (...)
  ```

  - Quais processos foram iniciados pelo usuário `carol`?

  Resposta: apenas um: `top`.

  - Qual diretório virtual de `/proc` você deve visitar para encontrar dados relacionados ao comando `top`?

  Resposta: `/proc/887`

  - Qual processo foi executado primeiro? Como você descobriu?

  Resposta: `systemd`. Porque ele tem o `PID` \#1.

  - Complete a tabela especificando em qual área da saída de `top` encontramos as seguintes informações:

| **Informações sobre …** | **Área de resumo** | **Área de tarefas** |
|---|---|---|
| Memória | Sim | Sim |

| **Informações sobre …** | **Área de resumo** | **Área de tarefas** |
|---|---|---|
| Swap | Sim | Não |
| `PID` | Não | Sim |
| Tempo da CPU | Sim | Sim |
| Comandos | Não | Sim |

2. Qual comando é usado para ler os registros binários a seguir?

  - `/var/log/wtmp`

  Resposta: `last`

  - `/var/log/btmp`

  Resposta: `lastb`

  - `/run/log/journal/2a7d9730cd3142f4b15e20d6be631836/system.journal`

  Resposta: `journalctl`

3. Em combinação com `grep`, quais comandos você usaria para descobrir as seguintes informações sobre seu sistema Linux?

  - Data da última reinicialização do sistema (`wtmp`)

  Resposta: `last`

  - Quais são os discos rígidos instalados (`kern.log`)

  Resposta: `less /var/log/kern.log`

  - Quando foi feito o último login (`auth.log`)

  Resposta: `less /var/log/auth.log`

4. Quais dois comandos você usaria para exibir o buffer de anel do kernel?

  `dmesg` e `journalctl -k` (e também `journalctl --dmesg`).

5. Indique o local a que pertencem as seguintes mensagens de log:

  - `Jul 10 13:37:39 debian dbus[303]: [system] Successfully activated service` `'org.freedesktop.nm_dispatcher'`

| `/var/log/auth.log` |  |  |  |
|---|---|---|---|
| `/var/log/kern.log` |  |  |  |
| `/var/log/syslog` |  |  | X |
| `/var/log/messages` |  |  |  |

  - `Jul 10 11:23:58 debian kernel: [ 1.923349] usbhid: USB HID core driver`

| `/var/log/auth.log` |  |  |  |
|---|---|---|---|
| `/var/log/kern.log` |  |  | X |
| `/var/log/syslog` |  |  |  |
| `/var/log/messages` |  |  | X |

  `Jul 10 14:02:53 debian sudo: pam_unix(sudo:session): session opened for` `user root by carol(uid=0)`

| `/var/log/auth.log` |  |  | X |
|---|---|---|---|
| `/var/log/kern.log` |  |  |  |
| `/var/log/syslog` |  |  |  |
| `/var/log/messages` |  |  |  |

  - `Jul 10 11:23:58 debian NetworkManager[322]: <info> [1562750638.8672]` `NetworkManager (version 1.6.2) is starting…`

| `/var/log/auth.log` |  |  |  |
|---|---|---|---|
| `/var/log/kern.log` |  |  |  |
| `/var/log/syslog` |  |  |  |
| `/var/log/messages` |  |  | X |

6. Use `journalctl` para encontrar informações sobre as seguintes unidades:

| **Unidade** | **Comando** |
|---|---|
| `ssh` | `journalctl -u ssh.service` |
| `networking` | `journalctl -u networking.service` |
| `rsyslog` | `journalctl -u rsyslog.service` |

| **Unidade** | **Comando** |
|---|---|
| `cron` | `journalctl -u cron.service` |

#### Respostas aos Exercícios Exploratórios

1. Retome a saída de `top` dos exercícios guiados e responda às seguintes questões:

  - Quais são as duas etapas a seguir para eliminar o servidor web *apache*?

  Primeiro, pressionar `k`; depois fornecer um valor `kill`.

  - Na área de resumo, como seria possivel exibir as informações sobre a memória física e a memória swap usando barras de progresso?

  Pressionando `m` uma ou duas vezes.

  - Agora, classifique os processos pelo uso da memória:

  `M`

  - Agora que as informações sobre a memória estão sendo exibidas em barras de progresso e os processos classificados pelo uso da memória, salve essas configurações para torná-las padrão na próxima vez que você usar o `top`:

  `W`

  - Qual arquivo armazena as configurações de `top`? Onde ele fica? Como você pode verificar sua existência?

  O arquivo é `~/.config/procps/toprc` e ele fica no diretório inicial do usuário (`~`). Como se trata de um arquivo oculto (reside em um diretório cujo nome começa com um ponto), podemos verificar sua existência com `ls -a` (listar todos os arquivos). Esse arquivo pode ser gerado pressionando `Shift` + `W` enquanto estamos em `top`.

2. Aprenda sobre o comando `exec` no Bash. Tente demonstrar sua funcionalidade iniciando uma sessão do Bash e encontrando o processo do Bash com `ps`. Depois, execute `exec /bin/sh` e busque novamente pelo processo com o mesmo PID.

  `exec` substitui um processo por outro comando. No exemplo a seguir vemos que o processo do Bash é substituído por `/bin/sh` (em vez de `/bin/sh` se tornar um processo filho):

  ```bash
  $ echo $$
  19877
  $ ps auxf | grep 19877 | head -1
  carol  19877  0.0  0.0   7448  3984 pts/25   Ss   21:17   0:00  \_ bash
  $ exec /bin/sh
  ```

  ```
  sh-5.0$ ps auxf | grep 19877 | head -1
  carol  19877  0.0  0.0   7448  3896 pts/25   Ss   21:17   0:00  \_ /bin/sh
  ```

3. Siga estes passos para explorar os eventos do kernel e o gerenciamento dinâmico de dispositivos do udev:

  - Conecte um drive USB ao seu computador. Rode o `dmesg` e preste atenção às últimas linhas. Qual a linha mais recente?

  Deve aparecer algo semelhante a `[ 1967.700468] sd 6:0:0:0: [sdb] Attached SCSI` `removable disk`.

  - Tendo em mente a saída do comando anterior, execute `ls /dev/sd*` e verifique se seu drive USB aparece na lista. Qual a saída?

  Dependendo do número de dispositivos conectados ao sistema, deve aparecer algo semelhante a `/dev/sda /dev/sda1 /dev/sdb /dev/sdb1 /dev/sdb2`. Em nosso caso, encontramos nosso drive USB (`/dev/sdb`) e suas duas partições (`/dev/sdb1` e `/dev/sdb2`).

  - Agora, remova o drive USB e execute `dmesg` outra vez. O que diz a linha mais recente?

  Deve aparecer algo semelhante a `[ 2458.881695] usb 1-9: USB disconnect, device` `number 6`.

  - Execute `ls /dev/sd*` novamente e verifique se o dispositivo sumiu da lista. Qual a saída?

  Em nosso caso, `/dev/sda /dev/sda1`.

## 4.4 Seu Computador na Rede

- **Referência ao LPI objectivo**: Linux Essentials version 1.6, Exam 010, Objective 4.4
- **Peso**: 2

**Áreas chave de conhecimento**

- Internet, rede, roteadores
- Consultando configuração do cliente DNS
- Consultando configuração da rede

**Segue uma lista parcial de arquivos, termos e utilitários utilizados**

- `route`, `ip route show`
- `ifconfig`, `ip addr show`
- `netstat`, `ss`
- `/etc/resolv.conf`, `/etc/hosts`
- IPv4, IPv6
- `ping`
- `host`

### 4.4 Lição 1

#### Introdução

No mundo de hoje, qualquer tipo de dispositivo de computação troca informações por meio de redes. No cerne do conceito das redes de computadores estão as conexões físicas entre um dispositivo e seus pares. Essas conexões são chamadas *links* e constituem a conexão mais básica entre dois dispositivos diferentes. Os links podem ser estabelecidos através de vários meios, como cabos de cobre, fibras óticas, ondas de rádio ou lasers.

Cada link está conectado a uma interface de um dispositivo. Cada dispositivo pode ter múltiplas interfaces e, portanto, estar conectado a diversos links. Através desses links, os computadores podem formar uma rede: uma pequena comunidade de dispositivos capazes de se conectar diretamente. Há inúmeros exemplos dessas redes no mundo. Para poder se comunicar além do alcance de uma camada de link, os dispositivos usam roteadores. Pense nas redes da camada de link como ilhas conectadas entre si por roteadores — assim como pontes que as informações precisam atravessar para chegar a um dispositivo que faz parte de uma ilha remota.

Esse modelo leva a diversas camadas de rede diferentes:

- **Camada de link**: Responsável pela comunicação entre dispositivos conectados diretamente.
- **Camada de rede**: Gerencia o roteamento para fora das redes individuais e o endereçamento único de dispositivos além de uma única camada de link.
- **Camada de aplicativo**: Permite que programas individuais se conectem uns aos outros.

Quando foram inventadas, as redes de computadores usavam os mesmos métodos de comunicação que os telefones, ou seja, eram comutadas por circuitos. Isso significa que um link dedicado e direto tinha de ser formado entre dois nós para que eles pudessem se comunicar. Esse método funcionava bem, mas exigia todo o espaço em um determinado link para que apenas dois hosts se comunicassem.

Depois de algum tempo, as redes de computadores passaram a usar a *comutação de pacotes*. Nesse método, os dados são agrupados com um cabeçalho contendo informações sobre a origem e o destino das informações. As informações do conteúdo estão contidas nessa estrutura e são enviadas pelo link para o destinatário indicado no cabeçalho. Isso permite que diversos dispositivos compartilhem um único link e se comuniquem quase simultaneamente.

##### Comunicação na camada de link

A função de qualquer pacote é transportar informações da origem até o destino através de um link que conecta os dois dispositivos. Esses dispositivos precisam de uma maneira de se identificar. Esse é o objetivo de um *endereço de camada de link*. Em uma rede Ethernet, os endereços de *Controle de Acesso de Mídia* (Media Access Control ou MAC) são usados para identificar dispositivos individuais. Um endereço MAC consiste em 48 bits. Eles não são necessariamente únicos globalmente e não podem ser usados para endereçar pontos externos ao link atual. Portanto, esses endereços não podem ser usados para rotear pacotes para outros links. O destinatário de um pacote verifica se o endereço de destino corresponde à sua própria camada de link e, se for o caso, processa o pacote. Caso contrário, o pacote será descartado. A exceção a essa regra são *pacotes de broadcast* (um pacote enviado a todos em uma determinada rede local), que sempre são aceitos.

O comando `ip link show` exibe uma lista de todas as interfaces de rede disponíveis e seus endereços da camada de link, além de outras informações sobre o tamanho máximo do pacote:

```bash
$ ip link show
```

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group
default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT
group default qlen 1000
link/ether 00:0c:29:33:3b:25 brd ff:ff:ff:ff:ff:ff
```

A saída acima mostra que o dispositivo tem duas interfaces, `lo` e `ens33`. `lo` é o *dispositivo de* *loopback* e tem o endereço MAC `00:00:00:00:00:00`, ao passo que `ens33` é uma interface Ethernet com o endereço MAC `00:0c:29:33:3b:25`.

##### Rede IPv4

Para visitar sites como o Google ou o Twitter, verificar emails ou permitir que empresas se conectem entre si, os pacotes precisam ser capazes de passar de uma camada de link para outra. Freqüentemente, essas redes são conectadas indiretamente, com diversas camadas de link intermediárias que os pacotes devem atravessar para alcançar seu destino real.

Os endereços de camada de link de uma interface de rede não podem ser usados fora da rede específica em que está a camada de link. Como esse endereço não tem significado para os dispositivos de camada de link de outras redes, é necessária uma forma de endereços globalmente exclusivos para implementar o roteamento. Esse esquema de endereçamento, juntamente com o conceito geral de roteamento, é implementado pelo *Protocolo de Internet* (Internet Protocol ou IP).

> [!note]
> Um *protocolo* é um conjunto de procedimentos que permite que todas as partes que seguem o protocolo sejam compatíveis entre si. Um protocolo pode ser visto como a definição de um padrão. Em computação, o Internet Protocol é um padrão aceito por todos para que diferentes dispositivos produzidos por diferentes fabricantes possam se comunicar.

###### Endereços IPv4

Os endereços IP, como os endereços MAC, são uma maneira de indicar de onde vem um pacote de dados e para onde ele está indo. IPv4 era o protocolo original. Os endereços IPv4 têm 32 bits de largura, fornecendo um número máximo teórico de 4.294.967.296 endereços. No entanto, o número desses endereços que são utilizáveis pelos dispositivos é muito menor, pois alguns intervalos são reservados para casos de uso especiais, como endereços de broadcast (usados para alcançar todos os participantes de uma rede específica), endereços multicast (semelhantes aos endereços de broadcast, mas o dispositivo deve sintonizá-lo, como um rádio) ou endereços reservados para uso privado.

Em seu formato legível para humanos, os endereços IPv4 são representados como quatro grupos de dígitos separados por um ponto. Cada grupo pode variar de `0` a `255`. Por exemplo, veja o seguinte endereço IP:

```
192.168.0.1
```

Tecnicamente, cada um desses grupos de dígitos representa oito bits individuais. Assim, esse endereço também pode ser escrito desta maneira:

```
11000000.10101000.00000000.00000001
```

Na prática, usamos uma notação decimal como a mostrada acima. No entanto, a representação bit a bit ainda é importante para entender as sub-redes.

###### Sub-redes IPv4

Para oferecer suporte ao roteamento, os endereços IP podem ser divididos em duas partes: uma parte da rede e uma do host. A parte da rede identifica a rede na qual o dispositivo está e é usada para rotear pacotes para essa rede. A parte do host é usada para identificar especificamente um determinado dispositivo em uma rede e para entregar o pacote ao seu destinatário específico, uma vez atingida a sua camada de link.

Os endereços IP podem ser divididos em partes de sub-rede e host em qualquer ponto. A chamada *máscara de sub-rede* define onde essa divisão acontece. Vamos reconsiderar a representação binária do endereço IP do exemplo anterior:

```
11000000.10101000.00000000.00000001
```

Para esse endereço IP, a máscara de sub-rede define cada bit que pertence à parte da rede como `1` e cada bit que pertence à parte do host como `0`:

```
11111111.11111111.11111111.00000000
```

Na prática, a máscara de rede é escrita na notação decimal:

```
255.255.255.0
```

Isso significa que essa rede varia de `192.168.0.0` a `192.168.0.255`. Note que os três primeiros números, que possuem todos os bits definidos na máscara de rede, permanecem inalterados nos endereços IP.

Por fim, existe uma notação alternativa para a máscara de sub-rede, chamada *Classless Inter-* *Domain Routing* (CIDR). Essa notação indica somente quantos bits estão definidos na máscara de sub-rede e adiciona esse número ao endereço IP. No exemplo, 24 dos 32 bits são definidos como `1` na máscara de sub-rede. Isso pode ser expresso na notação CIDR como `192.168.0.1/24`

###### Endereços IPv4 privados

Como mencionado anteriormente, determinadas seções do endereço IPv4 são reservadas para casos de uso especiais. Um desses casos de uso são atribuições de endereços privados. As seguintes sub-redes estão reservadas para endereçamento privado:

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

Os endereços dessas sub-redes podem ser usados por qualquer pessoa. No entanto, essas sub- redes não podem ser roteadas na internet pública, pois são potencialmente usadas por várias redes ao mesmo tempo.

Hoje, a maioria das redes usa esses endereços internos. Eles permitem a comunicação interna sem a necessidade de qualquer atribuição de endereço externo. A maioria das conexões à Internet atualmente vem apenas com um único endereço IPv4 externo. Ao encaminhar pacotes para a Internet, os roteadores mapeiam todos os endereços internos para esse único endereço IP externo. Esse processo se chama *Network Address Translation* (NAT). O caso especial do NAT, em que um roteador mapeia endereços internos para um único endereço IP externo, às vezes é chamado de *masquerading*. Ele permite que qualquer dispositivo na rede interna estabeleça novas conexões com qualquer endereço IP global na internet.

> [!note]
> Com o masquerading, os dispositivos internos não podem ser referenciados na Internet, pois não possuem um endereço válido globalmente. No entanto, esse não é um recurso de segurança. Mesmo ao usar masquerading, um firewall permanece necessário.

###### Configuração do endereço IPv4

Existem duas maneiras principais de configurar endereços IPv4 em um computador: atribuir os endereços manualmente ou usar o protocolo de configuração dinâmica de host (*Dynamic Host* *Configuration Protocol* ou DHCP) para configuração automática.

Ao usar o DHCP, um servidor central controla quais endereços são entregues a quais dispositivos. O servidor também pode fornecer aos dispositivos outras informações sobre a rede, como os endereços IP dos servidores DNS, o endereço IP do roteador padrão ou, no caso de configurações mais complicadas, iniciar um sistema operacional a partir da rede. O DHCP está ativado por padrão em muitos sistemas; portanto, você provavelmente já terá um endereço IP quando estiver conectado a uma rede.

Também é possível adicionar endereços IP manualmente a uma interface usando o comando `ip` `addr add`. Aqui, adicionamos o endereço `192.168.0.5` à interface `ens33`. A rede usa a máscara de rede `255.255.255.0`, que equivale a `/24` em notação CIDR:

```bash
$ sudo ip addr add 192.168.0.5/255.255.255.0 dev ens33
```

Agora, podemos verificar se o endereço foi adicionado, usando o comando `ip addr show`:

```bash
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
25: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen
1000
link/ether 00:0c:29:33:3b:25 brd ff:ff:ff:ff:ff:ff
inet 192.168.0.5/24 192.168.0.255 scope global ens33
valid_lft forever preferred_lft forever
inet6 fe80::010c:29ff:fe33:3b25/64 scope link noprefixroute
valid_lft forever preferred_lft forever
```

A saída acima mostra a interface `lo` e a interface `ens33` com seu endereço atribuído com o comando acima.

Para verificar se um dispositivo está acessível, usamos o comando `ping`. Ele envia um tipo especial de mensagem chamado *echo request* (solicitação de eco), na qual o remetente solicita uma resposta ao destinatário. Se a conexão entre os dois dispositivos puder ser estabelecida com sucesso, o destinatário retornará uma resposta de eco, confirmando a conexão:

```bash
$ ping -c 3 192.168.0.1
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=2.16 ms
```

```
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=1.85 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=3.41 ms

--- 192.168.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 5ms
rtt min/avg/max/mdev = 1.849/2.473/3.410/0.674 ms
```

O parâmetro `-c 3` faz com que o `ping` pare de ser executado após o envio de três solicitações de eco. Caso contrário, o `ping` continua a rodar para sempre e precisa ser interrompido pressionando `Ctrl` + `C` .

###### Roteamento IPv4

O roteamento é o processo no qual um pacote passa da rede de origem para a rede de destino. Cada dispositivo mantém uma tabela de roteamento contendo informações sobre qual rede IP pode ser acessada diretamente através do vínculo do dispositivo com a camada de link e qual rede IP pode ser alcançada com a transmissão de pacotes para um roteador. Por fim, uma *rota padrão* define um roteador que recebe todos os pacotes que não correspondem a nenhuma outra rota.

Ao estabelecer uma conexão, o dispositivo procura o endereço IP do destino em sua tabela de roteamento. Se uma entrada corresponder ao endereço, o pacote será enviado à camada de link respectiva ou repassado ao roteador indicado na tabela de roteamento.

Os próprios roteadores também mantêm tabelas de roteamento. Ao receber um pacote, um roteador procura o endereço de destino em sua própria tabela e envia o pacote para o roteador seguinte. Isso é repetido até que o pacote chegue ao roteador na rede de destino. Cada roteador envolvido nessa jornada é chamado de *hop*. O último roteador encontra um link conectado direto para o endereço de destino em sua tabela de roteamento e envia os pacotes para a interface do destino.

A maioria das redes domésticas conta com apenas uma saída, o roteador enviado pelo *provedor de* *internet* (ISP). Nesse caso, o dispositivo apenas encaminha todos os pacotes que não são para a rede interna diretamente para o roteador doméstico, que o envia então ao roteador do provedor para encaminhamento adicional. Esse é um exemplo de rota padrão.

O comando `ip route show` lista a tabela atual de roteamento IPv4:

```bash
$ ip route show
127.0.0.0/8 via 127.0.0.1 dev lo0
192.168.0.0/24 dev ens33 scope link
```

Para adicionar uma rota padrão, basta ter o endereço interno do roteador que será o gateway padrão. Se, por exemplo, o roteador tiver o endereço `192.168.0.1`, o seguinte comando o configurará como uma rota padrão:

```bash
$ sudo ip route add default via 192.168.0.1
```

Para confirmar, execute `ip route show` novamente:

```bash
$ ip route show
default via 192.168.0.1 dev ens33
127.0.0.0/8 via 127.0.0.1 dev lo0
192.168.0.0/24 dev ens33 scope link
```

##### Rede IPv6

O IPv6 foi projetado para colmatar as deficiências do IPv4, principalmente a falta de endereços conforme mais e mais dispositivos iam sendo postos online. No entanto, o IPv6 também inclui outros recursos, como novos protocolos para a configuração automática de redes. Em vez de 32 bits por endereço, o IPv6 usa 128. Isso permite aproximadamente 2 128 endereços. No entanto, como o IPv4, o número de endereços utilizáveis globalmente exclusivos é muito menor porque algumas seções da alocação são reservadas para outros usos. Esse grande número de endereços significa que existem endereços públicos mais do que suficientes para todos os dispositivos atualmente conectados à Internet, mais muitos outros, reduzindo assim a necessidade de masquerading e os problemas gerados por ele, como o atraso na tradução e a impossibilidade de conectar-se diretamente a dispositivos mascarados.

###### Endereços IPv6

Quando escritos, os endereços usam 8 grupos de 4 dígitos hexadecimais, separados por dois pontos:

```
2001:0db8:0000:abcd:0000:0000:0000:7334
```

> [!note]
> Os dígitos hexadecimais vão de `0` a `f`, de forma que cada dígito pode conter um dentre 16 valores diferentes.

Para facilitar, os zeros à esquerda de cada grupo podem ser removidos quando escritos, mas cada grupo deve conter pelo menos um dígito:

```
2001:db8:0:abcd:0:0:0:7334
```

Quando diversos grupos contendo apenas zeros aparecem diretamente um após o outro, podem ser substituídos por '::':

```
2001:db8:0:abcd::7334
```

Todavia, isso só pode ser feito uma vez em cada endereço.

###### Prefixo IPv6

Os primeiros 64 bits de um endereço IPv6 são conhecidos como o *prefixo de roteamento*. O prefixo é usado pelos roteadores para determinar a qual rede um dispositivo pertence e, portanto, em qual caminho os dados precisam ser enviados. A sub-rede sempre acontece dentro do prefixo. Os provedores de internet geralmente distribuem prefixos /48 ou /58 aos seus clientes, deixando 16 ou 8 bits para sua sub-rede interna.

Existem três tipos principais de prefixos no IPv6:

- **Endereço Global Unicast**: Nele, o prefixo é atribuído a partir dos blocos reservados aos endereços globais. Esses endereços são válidos em toda a internet.
- **Endereço Local Unicast**: Pode não ser roteado na internet. No entanto, pode ser roteado internamente dentro de uma organização. Esses endereços são usados dentro de uma rede para garantir que os dispositivos tenham um endereço mesmo quando não houver conexão com a Internet. Equivalem aos intervalos de endereços privados do IPv4. Os primeiros 8 bits são sempre `fc` ou `fd`, seguidos por 40 bits gerados aleatoriamente.
- **Endereço Link-Local**: São válidos somente em um link específico. Toda interface de rede compatível com IPv6 possui um desses endereços, começando com `fe80`. Esses endereços são usados internamente pelo IPv6 para solicitar endereços adicionais usando a configuração automática e para encontrar outros computadores na rede usando o protocolo Neighbor Discovery.

###### Identificador da interface IPv6

Enquanto o prefixo determina em qual rede um dispositivo reside, o identificador de interface é usado para enumerar os dispositivos em uma rede. Os últimos 64 bits de um endereço IPv6 formam o identificador da interface, assim como os últimos bits de um endereço IPv4.

Quando um endereço IPv6 é atribuído manualmente, o identificador da interface é definido como parte do endereço. Ao usar a configuração automática de endereço, o identificador de interface é escolhido aleatoriamente ou derivado do endereço da camada de link do dispositivo. Isso faz com que uma variação do endereço da camada de link apareça no endereço IPv6.

###### Configuração do endereço IPv6

Como o IPv4, o endereço IPv6 pode ser atribuído manualmente ou automaticamente. No entanto, o IPv6 possui dois tipos diferentes de configuração automatizada: DHCPv6 e *Stateless Address* *Autoconfiguration* (SLAAC).

O SLAAC é o mais fácil dos dois métodos automatizados, sendo incorporado no padrão IPv6. As mensagens usam o novo *Neighbor Discovery Protocol*, que permite que os dispositivos se encontrem e solicitem informações a respeito de uma rede. Essas informações são enviadas pelos roteadores e podem conter prefixos IPv6 que os dispositivos podem usar combinando-os com um identificador de interface de sua escolha, desde que o endereço resultante ainda não esteja em uso. Os dispositivos não fornecem feedback ao roteador sobre os endereços criados.

O DHCPv6, por outro lado, é o DHCP atualizado para funcionar com as alterações do IPv6. Ele permite um controle mais preciso das informações entregues aos clientes, como permitir que o mesmo endereço seja sempre entregue ao mesmo cliente e enviar mais opções para o cliente do que o SLAAC. Com o DHCPv6, os clientes precisam obter o consentimento explícito de um servidor DHCP para usar um endereço.

O método para atribuir manualmente um endereço IPv6 a uma interface é o mesmo do IPv4:

```bash
$ sudo ip addr add 2001:db8:0:abcd:0:0:0:7334/64 dev ens33
```

Para confirmar se a atribuição funcionou, usamos o mesmo comando, `ip addr show`:

```bash
$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host
valid_lft forever preferred_lft forever
25: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen
```

```
1000
link/ether 00:0c:29:33:3b:25 brd ff:ff:ff:ff:ff:ff
inet 192.168.0.5/24 192.168.0.255 scope global ens33
valid_lft forever preferred_lft forever
inet6 fe80::010c:29ff:fe33:3b25/64 scope link noprefixroute
valid_lft forever preferred_lft forever
inet6 2001:db8:0:abcd::7334/64 scope global
valid_lft forever preferred_lft forever
```

Aqui também vemos o endereço link-local `fe80::010c:29ff:fe33:3b25/64`.

Como no caso do IPv4, o comando `ping` também pode ser usado para confirmar a acessibilidade dos dispositivos através do IPv6:

```bash
$ ping 2001:db8:0:abcd::1
PING 2001:db8:0:abcd::1(2001:db8:0:abcd::1) 56 data bytes
64 bytes from 2001:db8:0:abcd::1: icmp_seq=1 ttl=64 time=0.030 ms
64 bytes from 2001:db8:0:abcd::1: icmp_seq=2 ttl=64 time=0.040 ms
64 bytes from 2001:db8:0:abcd::1: icmp_seq=3 ttl=64 time=0.072 ms

--- 2001:db8:0:abcd::1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 43ms
rtt min/avg/max/mdev = 0.030/0.047/0.072/0.018 ms
```

> [!note]
> Em certos sistemas Linux, o `ping` não suporta IPv6. Esses sistemas incluem um comando dedicado `ping6` para isso.

Para confirmar o endereço link-local, use `ping` novamente. Mas como todas as interfaces usam o prefixo `fe80::/64`, a interface correta deve ser especificada junto com o endereço:

```bash
$ ping6 -c 1 fe80::010c:29ff:fe33:3b25%ens33
PING fe80::010c:29ff:fe33:3b25(fe80::010c:29ff:fe33:3b25) 56 data bytes
64 bytes from fe80::010c:29ff:fe33:3b25%ens33: icmp_seq=1 ttl=64 time=0.049 ms

--- fe80::010c:29ff:fe33:3b25 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.049/0.049/0.049/0.000 ms
```

##### DNS

Os endereços IP são difíceis de memorizar e não são lá muito atraentes quando estamos tentando comercializar um serviço ou produto. É aqui que o *Domain Name System* (sistema de nomes de domínio) entra em ação. Em sua forma mais simples, o DNS é uma lista telefônica que mapeia nomes de domínio memoráveis e amigáveis, como `exemplo.com`, para endereços IP. Quando, por exemplo, um usuário navega até um site, ele insere o nome do host DNS como parte da URL. O navegador web envia o nome de DNS para o resolvedor DNS configurado. Esse resolvedor de DNS, por sua vez, descobrirá o endereço relacionado àquele domínio. O resolvedor responde com essa informação e o navegador tenta acessar o servidor web nesse endereço IP.

Os resolvedores usados pelo Linux para procurar dados DNS estão no arquivo de configuração `/etc/resolv.conf`:

```bash
$ cat /etc/resolv.conf
search lpi
nameserver 192.168.0.1
```

Quando o resolvedor realiza uma pesquisa de nome, ele primeiro verifica o arquivo `/etc/hosts` para ver se encontra um endereço para o nome solicitado. Se for o caso, ele retorna esse endereço e não entra em contato com o DNS. Isso permite que os administradores de rede forneçam a resolução de nomes sem a necessidade de configurar um servidor DNS completo. Cada linha desse arquivo contém um endereço IP seguido por um ou mais nomes:

```
127.0.0.1          localhost.localdomain   localhost
::1                localhost.localdomain   localhost
192.168.0.10       server
2001:db8:0:abcd::f server
```

Para realizar uma pesquisa no DNS, use o comando `host`:

```bash
$ host learning.lpi.org
learning.lpi.org has address 208.94.166.198
```

O comando `dig` oferece informações mais detalhadas:

```bash
$ dig learning.lpi.org
; <<>> DiG 9.14.3 <<>> learning.lpi.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21525
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
```

```
;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 2ac55879b1adef30a93013705d3306d2128571347df8eadf (bad)
;; QUESTION SECTION:
;learning.lpi.org.      IN  A

;; ANSWER SECTION:
learning.lpi.org.   550 IN  A   208.94.166.198

;; Query time: 3 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Sat Jul 20 14:20:21 EST 2019
;; MSG SIZE  rcvd: 89
```

Aqui também vemos o nome dos tipos de registro DNS, neste caso `A` para IPv4.

##### Sockets

Um *socket* é um terminal de comunicação para dois programas conversando entre si. Se o socket estiver conectado por uma rede, os programas poderão ser executados em dispositivos diferentes, como um navegador web no laptop de um usuário e um servidor web no data center de uma empresa.

Existem três tipos principais de sockets:

- **Sockets Unix**: Conecta os processos em execução no mesmo dispositivo.
- **Sockets UDP (User Datagram Protocol)**: Conectam aplicativos usando um protocolo rápido, mas pouco resistente.
- **Sockets TCP (Transmission Control Protocol)**: Mais confiáveis que os sockets UDP; por exemplo, eles confirmam a recepção de dados.

Os sockets Unix só podem conectar aplicativos em execução no mesmo dispositivo. Já os sockets TCP e UDP podem se conectar através de uma rede. O TCP permite um fluxo de dados que sempre chegam na ordem exata em que foram enviados. O UDP meio que se guia sozinho; o pacote é enviado, mas a forma de entrega na outra extremidade não é garantida. No entanto, o UDP não tem a mesma sobrecarga do TCP, sendo assim perfeito para aplicações de baixa latência, como videogames online.

O TCP e o UDP usam portas para endereçar vários sockets no mesmo endereço IP. Embora a porta de origem de uma conexão geralmente seja aleatória, as portas de destino são padronizadas para um serviço específico. O HTTP, por exemplo, geralmente é hospedado na porta 80; o HTTPS é executado na porta 443. O SSH, um protocolo para fazer login com segurança em um sistema Linux remoto, escuta na porta 22.

O comando `ss` permite que um administrador investigue todos os sockets em um computador Linux. Ele mostra tudo, desde o endereço de origem até o endereço de destino e o tipo. Um de seus melhores recursos é o uso de filtros que permitem monitorar os sockets em qualquer estado de conexão que se queira. O `ss` pode ser executado com um conjunto de opções, além de uma expressão de filtro para limitar as informações mostradas.

Quando executado sem nenhuma opção, o comando exibe uma lista de todos os sockets estabelecidos. A opção `-p` inclui informações sobre o processo que está usando cada socket. A opção `-s` mostra um resumo dos sockets. Há muitas outras opções disponíveis para esta ferramenta, mas algumas das principais são `-4` e `-6` para restringir o protocolo IP a IPv4 ou IPv6 respectivamente; `-t` e `-u` permitem que o administrador selecione sockets TCP ou UDP e `-l` exibe apenas o socket que está atento às novas conexões.

O comando a seguir, por exemplo, lista todos os sockets TCP atualmente em uso:

```bash
$ ss -t
State       Recv-Q  Send-Q    Local Address:Port      Peer Address:Port
ESTAB       0       0           192.168.0.5:49412      192.168.0.1:https
ESTAB       0       0           192.168.0.5:37616      192.168.0.1:https
ESTAB       0       0           192.168.0.5:40114      192.168.0.1:https
ESTAB       0       0           192.168.0.5:54948      192.168.0.1:imap
...
```

#### Exercícios Guiados

1. Um engenheiro de rede precisa atribuir dois endereços IP à interface `ens33` de um host, um endereço IPv4 (`192.168.10.10/24`) e um endereço IPv6 (`2001:0:0:abcd:0:8a2e:0370:7334/64`). Quais comandos ele deve usar para fazer isso?

2. Quais endereços da lista abaixo são privados?

  `192.168.10.1`

  `120.56.78.35`

  `172.16.57.47`

  `10.100.49.162`

  `200.120.42.6`

3. Qual item você adicionaria ao arquivo de hosts para atribuir `192.168.0.15` a `example.com`?

4. Que efeito teria o comando a seguir?

  ```
  sudo ip -6 route add default via 2001:db8:0:abcd::1
  ```

#### Exercícios Exploratórios

1. Cite o tipo de registro de DNS usado para atender às seguintes solicitações:

  - Dados textuais
  - Pesquisa reversa de endereço IP
  - Um domínio que não tem endereço próprio e precisa de outro domínio para obter essas informações
  - Servidor de email

2. O Linux tem um recurso chamado bridging, o que ele faz e qual sua utilidade?

3. Qual opção precisa ser fornecida ao comando `ss` para visualizar todos os sockets UDP estabelecidos?

4. Qual comando exibe um resumo de todos os sockets em execução em um dispositivo Linux?

5. A saída a seguir foi gerada pelo comando do exercício anterior. Quantos sockets TCP e UDP estão ativos?

  ```
  Total: 978 (kernel 0)
  TCP:   4 (estab 0, closed 0, orphaned 0, synrecv 0, timewait 0/0), ports 0

  Transport Total     IP        IPv6
  *     0         -         -
  RAW   1         0         1
  UDP   7         5         2
  TCP   4         3         1
  INET      12        8         4
  FRAG      0         0         0
  ```

#### Resumo

Este tópico trata do uso de redes em seu computador Linux. Primeiro, aprendemos sobre os vários níveis de rede:

- A camada de link, que conecta os dispositivos diretamente.
- A camada de rede, que faz o roteamento entre as redes e um espaço de endereço global.
- A camada de aplicativo, na qual os aplicativos se conectam.

Vimos como o IPv4 e o IPv6 são usados para endereçar computadores individuais e como o TCP e o UDP enumeram os sockets usados pelos aplicativos para se conectar. Também aprendemos como o DNS é usado para resolver nomes para endereços IP.

Comandos usados nos exercícios:

`dig`

Consulta informações de DNS e fornece dados detalhados sobre as consultas e respostas de DNS.

`host`

Consulta informações de DNS e fornece uma saída condensada.

`ip`

Configura o uso da rede no Linux, incluindo interfaces de rede, endereços e roteamento.

`ping`

Testa a conectividade com um dispositivo remoto.

`ss`

Mostra informações sobre sockets.

#### Respostas aos Exercícios Guiados

1. Um engenheiro de rede precisa atribuir dois endereços IP à interface `ens33` de um host, um endereço IPv4 (`192.168.10.10/24`) e um endereço IPv6 (`2001:0:0:abcd:0:8a2e:0370:7334/64`). Quais comandos ele deve usar para fazer isso?

  ```
  sudo ip addr add 192.168.10.10/24 dev ens33
  sudo ip addr add 2001:0:0:abcd:0:8a2e:0370:7334/64 dev ens33
  ```

2. Quais endereços da lista abaixo são privados?

| `192.168.10.1` |  |  | X |
|---|---|---|---|
| `120.56.78.35` |  |  |  |
| `172.16.57.47` |  |  | X |
| `10.100.49.162` |  |  | X |
| `200.120.42.6` |  |  |  |

3. Qual item você adicionaria ao arquivo de hosts para atribuir `192.168.0.15` a `example.com`?

  ```
  192.168.0.15  example.com
  ```

4. Que efeito teria o comando a seguir?

  ```
  sudo ip -6 route add default via 2001:db8:0:abcd::1
  ```

  Ele adicionaria à tabela uma rota padrão que envia todo o tráfego IPv6 ao roteador com o endereço interno `2001:db8:0:abcd::1`.

#### Respostas aos Exercícios Exploratórios

1. Cite o tipo de registro de DNS usado para atender às seguintes solicitações:

  - Dados textuais

  TXT

  - Pesquisa reversa de endereço IP

  PTR

  - Um domínio que não tem endereço próprio e precisa de outro domínio para obter essas informações

  CNAME

  - Servidor de email

  MX

2. O Linux tem um recurso chamado bridging, o que ele faz e qual sua utilidade?

  Um bridge conecta múltiplas interfaces de rede. Todas as interfaces conectadas a um bridge podem se comunicar como se estivessem conectadas à mesma camada de link: Todos os dispositivos usam endereços IP da mesma sub-rede e não requerem um roteador para se conectar entre si.

3. Qual opção precisa ser fornecida ao comando `ss` para visualizar todos os sockets UDP estabelecidos?

  A opção `-u` mostra todos os sockets UDP estabelecidos.

4. Qual comando exibe um resumo de todos os sockets em execução em um dispositivo Linux?

  O comando `ss -s` mostra um resumo de todos os sockets

5. A saída a seguir foi gerada pelo comando do exercício anterior. Quantos sockets TCP e UDP estão ativos?

  ```
  Total: 978 (kernel 0)
  TCP:   4 (estab 0, closed 0, orphaned 0, synrecv 0, timewait 0/0), ports 0

  Transport Total     IP        IPv6
  ```

  ```
  *     0         -         -
  RAW   1         0         1
  UDP   7         5         2
  TCP   4         3         1
  INET      12        8         4
  FRAG      0         0         0
  ```

  11 sockets TCP e UDP estão ativos.

---
*Fonte: Linux Professional Institute, Materiais Didáticos Linux Essentials (learning.lpi.org), licença CC BY-NC-ND 4.0. Conversão do PDF para Markdown apenas para estudo pessoal.*
