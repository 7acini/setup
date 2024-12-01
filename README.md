# Configuração Desktop (Ubuntu 24.04 + I3WM)

No inicio da construção do setup após a instalação minima do Ubuntu Server, primeiramente veremos se estamos conectados, pois durante a instalação ativei minha conexão com o Wifi.

```bash
$ ip addr
...
2: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
...
```
Após detectar que minha placa se encontra "DOWN", tentaremos modifica-la para que a mesma fique "UP", para isso, utilizamos o comando:
```bash
$ ip link set wlp2s0 UP
```
A "wlp2s0" é o nome da minha interface, modifique  o comando de acordo com a sua.
Caso o comando não retorne nada, e você já consegue ver que se conectou OK, porém nessa tentativa de conexão o mesmo retornou o erro:
```bash
RTNETLINK answers: Operation not possible due to RF-kill
```
Para essa solução tenho outro `paper` explicando passo-passo essa solução.

Com isso, seguiremos com a configuração base de nosso ambiente, instalando os softwares base:

```bash
$ apt update && apt upgrade
$ apt install i3 polybar rofi
```
## I3
Para o inicio da configuração do I3, digite o comando `startx`, assim iniciando o Window Manager, a partir de agora, todas as configurações do mesmo e os softwares que o redeiam serão serão feitas no arquivo:
```bash
~/.config/i3/config
```
## Rofi
para iniciação o configuração do Rofi vamos primeiro inicializa-lo, para isso utilizaremos o comando:
```bash
$ rofi -show drun
```
Para a integração do Rofi com o I3 iremos modificar a linha **58** do arquivo `~/.config/i3/config` subistituindo:

```bash
bindsym $mod+d exec dmenu_drun
```
Por
```bash
bindsym $mod+d exec --no-startup-id rofi -show drun
```
## Polybar
Para a integração do Polybar com o I3 seguiremos o mesmo padrão, onde adicionaremos ao arquivo de configuração do I3 o seguinte comando:
```bash
exec --no-startup-id polybar
```
## Alacritty

Assim como fizemos na configuração do Rofi, aqui no Alacritty, também subistituiremos uma linha no arquivo do I3, sendo ela a linha **52** onde substituiremos:
```bash
bindsym $mod+Return exec i3-sensible-terminal
```
Por
```bash
bindsym $mod+Return exec alacritty
```
