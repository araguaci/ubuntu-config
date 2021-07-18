#Asterisk 17 no Ubuntu 20.04 | 18.04

Asterisk é livre framework open source coral gergelim aplicações de comunicações de construção para pequenas empresas e grandes casos de uso. Asterisk é uma solução baseada em software que transforma um computador antigo em um servidor de comunicação alimentado por um sistema IP PBX, gateway VoIP, servidor de conferência e outras soluções personalizadas. A solução é construída pelo Asterisk para fornecer energia a centrais de atendimento, operadoras e agências governamentais em todo o mundo.

Esta postagem do blog cobre a instalação do Asterisk 17 no servidor Ubuntu 20.04 | 18.04. No momento em que este artigo foi escrito, a versão mais recente do Asterisk era 17. Além disso, não é uma versão de lançamento de longo prazo e não deve ser usada em implantações de produção que requerem suporte de longo prazo para Digium.

Os pontos principais do asterisco são:

- Escrito em linguagem de programação C
- Criado para rodar em Linux e outros tipos de Unix
- Sistema de telefone comercial aprimorado
- Conecte muitos protocolos telefônicos diferentes
- Ferramentas para a construção de pacotes IP PBX tem muitos aplicativos poderosos , gateways VoIP e sistemas de conferência
- Os telefones VoIP também suportam a rede telefônica pública e POTS
- Está sendo usado o sip , a telefonia via Internet mais comum em acordo particular

## Instale o Asterisk 17 no Ubuntu 20.04 | 18.04
Siga as etapas na próxima seção para instalar o Asterisk 17 em seu sistema Linux Ubuntu 20.04 | 18.04. O asterisco é modular, portanto, não é difícil adicionar outros recursos após a instalação. Você pode facilmente.

### Etapa 1: atualize seu sistema Ubuntu
Para iniciar a instalação, atualize o índice de pacotes APT e atualize todos os pacotes instalados no sistema. Recomendamos que você execute esta instalação em um novo sistema para evitar problemas ao executar o serviço.

```
sudo apt update
sudo apt -y upgrade
```
Se o processo de atualização for bem-sucedido, você pode reiniciar o sistema.

```
sudo systemctl reboot
```

### Etapa 2: instalar dependências de compilação
Após reiniciar o sistema, faça o login e instale todas as dependências necessárias para construir o Asterisk na máquina Ubuntu 20.04 | 18.04 Linux.

```
sudo apt update
sudo add-apt-repository universe
sudo apt -y install git curl wget libnewt-dev libssl-dev libncurses5-dev subversion  libsqlite3-dev build-essential libjansson-dev libxml2-dev  uuid-dev
```

Com uma boa conexão à Internet, a instalação leva apenas alguns minutos.

### Etapa 3: Baixe o arquivo compactado do Asterisk 17
A última versão do Asterisk não pode ser encontrada no repositório oficial do sistema. Você deve baixar manualmente o pacote compactado e construir o aplicativo a partir do código-fonte.

Para Ubuntu 20.04, a versão disponível no repositório APT é 16.

```bash
sudo apt policy asterisk
```

```output
asterisk:
  Installed: (none)
  Candidate: 1:16.2.1~dfsg-2ubuntu1
  Version table:
     1:16.2.1~dfsg-2ubuntu1 500
        500 http://archive.ubuntu.com/ubuntu focal/universe amd64 Packages
        500 http://mirror.hetzner.de/ubuntu/packages focal/universe amd64 Packages
```
Use o comando wget para fazer download do arquivo compactado.

```
cd ~
wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-17-current.tar.gz
```

Descompacte o arquivo com tar.

```
tar xvf asterisk-17-current.tar.gz
```

Execute o seguinte comando para baixar a biblioteca do decodificador mp3 para a árvore do código-fonte.

```
cd asterisk-17*/
contrib/scripts/get_mp3_source.sh
```

Saída de execução de comando esperada:

```output
A    addons/mp3
A    addons/mp3/MPGLIB_README
A    addons/mp3/common.c
A    addons/mp3/huffman.h
A    addons/mp3/tabinit.c
A    addons/mp3/Makefile
A    addons/mp3/README
A    addons/mp3/decode_i386.c
A    addons/mp3/dct64_i386.c
A    addons/mp3/MPGLIB_TODO
A    addons/mp3/mpg123.h
A    addons/mp3/layer3.c
A    addons/mp3/mpglib.h
A    addons/mp3/decode_ntom.c
A    addons/mp3/interface.c
Exported revision 202.
```

Certifique-se de que todas as dependências sejam resolvidas.

```
sudo contrib/scripts/install_prereq install
```

Finalmente, uma mensagem de sucesso é exibida.

```output
#############################################
## instalação concluída com sucesso
#############################################
```

### Etapa 4: compilar e instalar o Asterisk 17 no Ubuntu 20.04 | 18.04

Depois de instalar as dependências, você pode construir o Asterisk 17 a partir das fontes baixadas.

Farei as definições de configuração para atender às dependências do script de construção.

```
./configure
```
Se for bem-sucedido, você verá uma saída semelhante a esta:

```output
configure: creating ./config.status
config.status: creating makeopts
config.status: creating autoconfig.h
configure: Menuselect build configuration successfully completed

               .$$$$$$$$$$$$$$$=..
            .$7$7..          .7$$7:.
          .$$:.                 ,$7.7
        .$7.     7$$$$           .$$77
     ..$$.       $$$$$            .$$$7
    ..7$   .?.   $$$$$   .?.       7$$$.
   $.$.   .$$$7. $$$$7 .7$$$.      .$$$.
 .777.   .$$$$$$77$$$77$$$$$7.      $$$,
 $$$~      .7$$$$$$$$$$$$$7.       .$$$.
.$$7          .7$$$$$$$7:          ?$$$.
$$$          ?7$$$$$$$$$$I        .$$$7
$$$       .7$$$$$$$$$$$$$$$$      :$$$.
$$$       $$$$$$7$$$$$$$$$$$$    .$$$.
$$$        $$$   7$$$7  .$$$    .$$$.
$$$$             $$$$7         .$$$.
7$$$7            7$$$$        7$$$
 $$$$$                        $$$
  $$$$7.                       $$  (TM)
   $$$$$$$.           .7$$$$$$  $$
     $$$$$$$$$$$$7$$$$$$$$$.$$$$$$
       $$$$$$$$$$$$$$$$.

configure: Package configured for:
configure: OS type  : linux-gnu
configure: Host CPU : x86_64
configure: build-cpu:vendor:os: x86_64 : pc : linux-gnu :
configure: host-cpu:vendor:os: x86_64 : pc : linux-gnu :
```

Execute o seguinte comando para definir as opções do menu:

```
make menuselect
```

Use as setas do teclado para mover para a chave selecionada.

Selecione o complemento e ative-o.

Habilite o módulo de som central a ser usado.

Como instalar o Asterisk 17 no Ubuntu 20.04 | 18.04

Você também pode adicionar o pacote de software MOH que deseja usar.

Como instalar o Asterisk 17 no Ubuntu 20.04 | 18.04

Faça o mesmo para Pacotes de Som Extra.

Como instalar o Asterisk 17 no Ubuntu 20.04 | 18.04

Você também pode usar os outros menus para selecionar a opção que melhor se adapta ao seu caso de uso.

Quando terminar, execute o seguinte comando para construir o Asterisk 17 no Ubuntu 20.04 | 18.04.

```
make
```

Esta é a minha saída de compilação de sucesso:

```output
.....
TROLEnc.o ooh323cDriver.o -> chan_ooh323.so
   [CC] format_mp3.c -> format_mp3.o
   [CC] mp3/common.c -> mp3/common.o
   [CC] mp3/dct64_i386.c -> mp3/dct64_i386.o
   [CC] mp3/decode_ntom.c -> mp3/decode_ntom.o
   [CC] mp3/layer3.c -> mp3/layer3.o
   [CC] mp3/tabinit.c -> mp3/tabinit.o
   [CC] mp3/interface.c -> mp3/interface.o
   [LD] format_mp3.o mp3/common.o mp3/dct64_i386.o mp3/decode_ntom.o mp3/layer3.o mp3/tabinit.o mp3/interface.o -> format_mp3.so
   [CC] res_config_mysql.c -> res_config_mysql.o
   [LD] res_config_mysql.o -> res_config_mysql.so
Building Documentation For: third-party channels pbx apps codecs formats cdr cel bridges funcs tests main res addons
 +--------- Asterisk Build Complete ---------+
 + Asterisk has successfully been built, and +
 + can be installed by running:              +
 +                                           +
 +                make install               +
 +-------------------------------------------+
```

Este é o comando que você deseja instalar o Asterisk 17 no Ubuntu 20.04.
```
sudo make install
```

Saída de amostra:
```output
....
make[1]: Entering directory '/home/jkmutai/asterisk-17.6.0/sounds'
make[1]: Leaving directory '/home/jkmutai/asterisk-17.6.0/sounds'
find rest-api -name "*.json" | while read x; do 
	/usr/bin/install -c -m 644 $x "/var/lib/asterisk/rest-api" ; 
done
 +---- Asterisk Installation Complete -------+
 +                                           +
 +    YOU MUST READ THE SECURITY DOCUMENT    +
 +                                           +
 + Asterisk has successfully been installed. +
 + If you would like to install the sample   +
 + configuration files (overwriting any      +
 + existing config files), run:              +
 +                                           +
 + For generic reference documentation:      +
 +    make samples                           +
 +                                           +
 + For a sample basic PBX:                   +
 +    make basic-pbx                         +
 +                                           +
 +                                           +
 +-----------------  or ---------------------+
 +                                           +
 + You can go ahead and install the asterisk +
 + program documentation now or later run:   +
 +                                           +
 +               make progdocs               +
 +                                           +
 + **Note** This requires that you have      +
 + doxygen installed on your local system    +
 +-------------------------------------------+
```
Você pode optar por instalar o documento:

```
sudo make progdocs
```
Finalmente, instale a configuração e os exemplos.

```
sudo make samples
sudo make config
sudo ldconfig
```

### Etapa 5: iniciar o serviço Asterisk no Ubuntu 20.04 | 18.04

Crie outro usuário e grupo que executará o serviço Asterisk e atribua as permissões corretas a ele.

```
sudo groupadd asterisk
sudo useradd -r -d /var/lib/asterisk -g asterisk asterisk
sudo usermod -aG audio,dialout asterisk
sudo chown -R asterisk.asterisk /etc/asterisk
sudo chown -R asterisk.asterisk /var/{lib,log,spool}/asterisk
sudo chown -R asterisk.asterisk /usr/lib/asterisk
```

O asterik como usuário padrão :

```
sudo vim /etc/default/asterisk

AST_USER="asterisk"
AST_GROUP="asterisk"
```

```
sudo vim /etc/asterisk/asterisk.conf
runuser = asterisk ; The user to run as.
rungroup = asterisk ; The group to run as.
```

Depois de fazer as alterações, reinicie o serviço Asterisk.

```
sudo systemctl start asterisk
```

Quando o sistema é iniciado, o serviço Asterisk pode iniciar.

```
sudo systemctl enable asterisk
```

Verifique o status do serviço para ver se ele está em execução.

```
systemctl status asterisk
```

```output
● asterisk.service - LSB: Asterisk PBX
     Loaded: loaded (/etc/init.d/asterisk; generated)
     Active: active (running) since Fri 2020-08-14 12:04:41 CEST; 9s ago
       Docs: man:systemd-sysv-generator(8)
      Tasks: 82 (limit: 4567)
     Memory: 44.6M
     CGroup: /system.slice/asterisk.service
             └─54142 /usr/sbin/asterisk -U asterisk -G asterisk
```

Certifique-se de que você pode se conectar à interface de linha de comando do Asterisk.

```
sudo asterisk -rvv
```

```output
Asterisk 17.6.0, Copyright (C) 1999 - 2018, Digium, Inc. and others.
Created by Mark Spencer <[email protected]>
Asterisk comes with ABSOLUTELY NO WARRANTY; type 'core show warranty' for details.
This is free software, with components licensed under the GNU General Public
License version 2 and other licenses; you are welcome to redistribute it under
certain conditions. Type 'core show license' for details.
=========================================================================
Running as user 'asterisk'
Running under group 'asterisk'
Connected to Asterisk 17.6.0 currently running on ubuntu (pid = 54142)
ubuntu*CLI>
```

Se você tiver um firewall ufw ativo, abra a porta http e a porta 5060,5061.

```
sudo ufw allow proto tcp from any to any port 5060,5061
```

Agora para inicar o serviço  Asterisk 17 no servidor Linux Ubuntu 20.04 | 18.04.

```
sudo service asterisk start
```

```output
 * Starting Asterisk PBX: asterisk                                                                                                          [ OK ]
```

