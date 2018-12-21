# Teste de Comunicação entre um servidor OPC e NodeRed


## Objetivo

> *O projeto tem como objetivo documentar os testes de comunicação realizado entre um servidor OPC e o NodeRed.*

## Desenvolvimento

O primeiro passo para iniciar os testes foi definir qual OPC utilizar. Após análise chegamos em dois servidor:

1. KEPServer
	+ Utilizado a versão Enterprise V5
2. Prosys OPC UA Simulation Server
	+ Utilizado a versão [3.1.6-192](https://downloads.prosysopc.com/opc-ua-simulation-server-downloads.php)
	
O nosso [Nodered](https://nodered.org/) está na versão 0.19.5.

O node **OPC** que utilizamos foi [node-red-contrib-iiot-opcua](https://flows.nodered.org/node/node-red-contrib-iiot-opcua).

Após configurado os servidores OPCs e instalado o node OPC, vamos às configurações:

## Kepserver

1. **Configuração**
	* Foi configurado um canal e um dispositivo de teste(modo simulador) no Kepserver conforme imagens:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-03.jpg"/></br>
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-04.jpg"/></br>
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-05.jpg"/></br>
	* Abrindo o modo **Client** do Kepserver temos as informações e estrutura que utilizaremos no NodeRed:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-06.jpg"/></br>
		+ 1(a). **Kepware.KEPServerEnterprise.V5**: este é o nome que deverá ser configurado no node do NodeRed.
		+ 2(b). Mostra o nome do canal com o dispositivo.
		+ 3(c). Identifica o caminho completo da *tag* OPC que será linkado no NodeRed para leitura ou escrita.
	* As configurações de comunicação e acesso a sistemas externos são configurados conforme imagem abaixo:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-10.jpg"/></br>
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-11.jpg"/></br>
		
		Com essas configurações de acesso que podem ser local ou remoto, conforme mostrado acima, temos condições de configurar o NodeRed.
		
2. **Uso**
	* Com o *node OPC* devidamente instalado prosseguiremos com as configurações do NodeRed.
		- arsfasfsaf