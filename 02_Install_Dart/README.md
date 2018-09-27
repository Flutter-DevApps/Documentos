# Guia de instalação do SDK Dart

Olá galera do Flutter-DevApps!

Há um mês atrás eu criei um guia para iniciantes em Flutter que ensinava a criar um ambiente para começar a criar seus App (pode ser consultado em [01_Install_Flutter/README.md](../01_Install_Flutter/README.md). E como vocês já sabem, para criar os aplicativos usando a SDK Flutter, precisamos codificar a aplicação em Dart… Ops, eu não ensinei a instalar o Dart antes, e como nossa aplicação de exemplo funcionou? 

Simplesmente porque no SDK do Flutter, vem embutida o pacote do SDK Dart!
Se observar no passo que uso o comando “flutter doctor -v” é exibido um check de OK na verificação do sdk do Dart

```
    ➜  v0.7.0 git:(dev) flutter doctor -v
    [!] Flutter (Channel dev, v0.7.0, on Linux, locale pt_BR.UTF-8)
        • Flutter version 0.7.0 at /home/hendi/desenv/sdk/flutter/v0.7.0
        • Framework revision 09fe34708f (2 days ago), 2018-08-22 10:20:51 -0700
        • Engine revision 4b271b2e02
        • Dart version 2.1.0-dev.1.0.flutter-69fce633b7
        ✗ Downloaded executables cannot execute on host.
            See https://github.com/flutter/flutter/issues/6207 for more information
            On Debian/Ubuntu/Mint: sudo apt-get install lib32stdc++6
            On Fedora: dnf install libstdc++.i686
            On Arch: pacman -S lib32-libstdc++5
```

Observem que a versão da época era a Dart version 2.1.0-dev.1.0.flutter-69fce633b7, e você pode consultar essa verão no diretório $FLUTTER_HOME/bin/cache/dart-sdk!

E podemos usar essa versão para construir nossas aplicações em Dart? Opa! Claro!!!

Mas observem só um detalhe… o Flutter é um SDK que depende de versões específicas do Dart. A tendência natural é que o Flutter sempre caminhe para uma versão mais atual e estável do Dart, mas hoje eles são projetos separados e o Dart sempre caminha mais à frente do Flutter.

Também não sei se notaram, mas nossa variável de ambiente $FLUTTER_HOME aponta para uma versão específica do SDK Flutter.

    FLUTTER_HOME=/home/<seu usuário>/desenv/sdk/flutter/v0.7.0
    export FLUTTER_HOME

    PATH=$FLUTTER_HOME/bin:$PATH

Ou seja, amanhã pode surgir uma 3 do Dart que quebre a compatibilidade com o Flutter v0.7.0 e force a equipe do Flutter a ter que criar uma versão v1.0.0 com o novo Dart.

Mas isso não afetaria minha aplicação e ela deixaria de funcionar? Não se você continuar na versão v0.7.0 do Flutter e usando o Dart embutido nele que está na versão 2.1.0! E provavelmente a equipe do Fluuter ainda dará suporte por um tempo nesta versão e um prazo para que todos migrem para a nova versão. Isso é normal de ocorrer em qualquer ambiente e linguagem de programação, então não fique apreensivo!

Bom, então sempre vou usar a versão embutida no Flutter pra criar minhas aplicações em Dart e isso vai resolver todos os meus problemas! Opa, também não é bem assim… Se você estivar usando aplicações em Flutter eu também recomendo isso, porém o Dart é uma linguagem de programação e não serve apenas pra criar seus Apps, não é? 

![Plataformas](../_images/plataformas.jpg "Plataformas que rodam Dart!")
Plataformas onde podemos rodar aplicações escritas em Dart.


## Onde vamos usar Dart?

Uma das perguntas que surgiu no nosso grupo, foi se usaríamos Dart também pra criar os serviços no backend em nossas aplicações de estudo aqui na nossa organização do Github, e pelos comentários isso ficou decidido quem sim!

Então vamos fazer nosso passo a passo para a instalação do Dart.


## Formas de instalação do Dart

Atualmente a equipe do Dart libera dois tipos de releases, um estável (**stable**) com atualizações não muito frequentes, mas que pode ocorre num prazo mínimo de 6 semanas e outra versão de desenvolvimento (**dev**), essa sim com atualizações bem frequentes que pode ocorrer a cada semana.

### 1. Instalação no Windows
	
#### 1.1. Utilizando o Chocolatey

    C:\> choco install dart-sdk # instalação da versão stable
    C:\> choco install dart-sdk –pre # instalação da versão dev
    C:\> choco upgrade dart-sdk # upgrade da versão

#### 1.2. Utilizando o bom e velho wizard

	Acessa o endereço http://www.gekorm.com/dart-windows/, faz o download do exe e manda bala!

	
### 2. Instalação no Debian e derivados (como Ubunut, Mint e etc)

#### 2.1. Utilizando o apt-get

**Versão stable**

    $ sudo apt-get update
    $ sudo apt-get install apt-transport-https
    $ sudo sh -c 'curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -'
    $ sudo sh -c 'curl https://storage.googleapis.com/download.dartlang.org/linux/debian/dart_stable.list > /etc/apt/sources.list.d/dart_stable.list'
    $ sudo apt-get update
    $ sudo apt-get install dart

**Versão dev**

    $ sudo sh -c 'curl https://storage.googleapis.com/download.dartlang.org/linux/debian/dart_unstable.list > /etc/apt/sources.list.d/dart_unstable.list'
    $ sudo apt-get update
    $ sudo apt-get install dart

#### 2.2. Utilizando o bom e velho .deb

    Acessa o endereço https://storage.googleapis.com/dart-archive/channels/stable/release/latest/linux_packages/dart_2.0.0-1_amd64.deb (stable) ou https://storage.googleapis.com/dart-archive/channels/dev/release/latest/linux_packages/dart_2.1.0-dev.5.0-1_amd64.deb (dev), faz o download do .deb do 2.x e manda bala!


### 3. Instalação no Mac (peço sua ajuda para contribuir com esse trecho)

    Aguardando contribuição.


### 4. Instalação no formato Zip

	Acesse o endereço https://www.dartlang.org/tools/sdk/archive, faça o download do zip stable ou dev para a arquitetura correta do seu ambiente.
	No meu caso, selecionei no Dev channel:
		Versão 2.1.0-dev.5.0
		OS: Linux (para meu Fedora 28)
		Arch: 64-bit
		Link: https://storage.googleapis.com/dart-archive/channels/dev/release/2.1.0-dev.5.0/sdk/dartsdk-linux-x64-release.zip
    
    Descompacta no local preferido (nos próximos passos, vou detalhar esse modo de instalação).

## Configurando o ambiente Dart (Detalhando o mode zip de instalação - Meu preferido!)

### Configuração do local de instalação

Para facilitar o desenvolvimento, vou sugerir criar alguns diretórios para melhor organização do ambiente local. Vou usar essa convenção nos comandos abaixo, se não quiser seguir essa convenção faça adaptações nos comandos a serem executado.

    $ mkdir -p ~/desenv/sdk/dart/2.1.0-dev.5.0; # Local de descompactação do Dart 2.1.0


### Instalação do SDK Dart

Acesse o endereço https://storage.googleapis.com/dart-archive/channels/dev/release/2.1.0-dev.5.0/sdk/dartsdk-linux-x64-release.zip, baixe o arquivo no diretório informado abaixo e depois descompacte-o.

    $ mv ~/Downloads/dartsdk-linux-x64-release.zip ~/desenv/sdk/dart/2.1.0-dev.5.0
    $ cd ~/desenv/sdk/dart/2.1.0-dev.5.0
    $ unzip dartsdk-linux-x64-release.zip
    $ rm dartsdk-linux-x64-release.zip
    $ mv dart-sdk/* .
    $ rm dart-sdk -rf
    
Obs: Certifique-se que o diretório do java ficou assim ~/desenv/sdk/dart/2.1.0-dev.5.0

E no final do arquivo ~/.bash_profile ou ~/.profile (vai depender de sua distro linux), coloque os trechos abaixo: (após edição do arquivo refazer login no linux)

    DART_HOME=/home/<seu usuário>/desenv/sdk/dart/2.1.0-dev.5.0
    export DART_HOME

    PATH=$DART_HOME/bin:$PATH

### Testando a instalação


Listando os arquivos do local de instalação do Dart

    $ ls $DART_HOME      
    drwxrwxr-x  5 hendi hendi      4096 set 26 23:46 .
    drwxrwxr-x  3 hendi hendi      4096 set 26 23:35 ..
    drwx------  3 hendi hendi      4096 set 19 14:48 bin
    -rw-r--r--  1 hendi hendi        47 jun 11 10:48 dartdoc_options.yaml
    drwxr-xr-x  2 hendi hendi      4096 set 19 14:47 include
    drwxr-xr-x 27 hendi hendi      4096 set 19 14:48 lib
    -rw-r--r--  1 hendi hendi      2500 ago  9  2017 LICENSE
    -rw-r--r--  1 hendi hendi       936 ago  9  2017 README
    -rw-r--r--  1 hendi hendi        41 set 19 14:47 revision
    -rw-r--r--  1 hendi hendi        14 set 19 14:47 version


Verificando a versão instalada    

    $ dart --version
    Dart VM version: 2.1.0-dev.5.0 (Wed Sep 19 19:15:19 2018 +0200) on "linux_x64"


## O que tem no SDK?

O SDK Dart contém um diretório **lib** que contém as bibliotecas do Dart e um diretório **bin** que contém as seguintes comandos:

    $ ls $DART_HOME/bin

    dart - A VM standalone (runtime)
    dart2js - O compilador Dart para JavaScript (usado apenas para o desenvolvimento para web browsers)
    dartanalyzer - O analizador estático de código
    dartdevc - O compilador Dart para geração de módulos JavaScript (amd, common ou es6) (usado apenas para o desenvolvimento para web browsers)
    dartdoc - Gerador de documentantação de API
    dartfmt - Formatador de código Dart
    pub - O gerenciador de pacotes Dart


Aguardem mais novidades...

O próximo passo será falar um pouco sobre a VM do Dart e sobre o pub (gerenciador de pacotes)