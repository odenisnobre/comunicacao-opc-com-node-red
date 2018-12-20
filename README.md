# Teste de Comunicação entre um servidor OPC e NodeRed


## Objetivo

O projeto tem como objetivo documentar os testes de comunicação realizado entre um servidor OPC e o NodeRed.

## Desenvolvimento

O primeiro passo para iniciar os testes foi definir qual OPC utilizar. Após análise chegamos em dois servidor:

1. KEPServer
	+ Utilizado a versão Enterprise V5
2. Prosys OPC UA Simulation Server
	+ Utilizado a versão [3.1.6-192](https://downloads.prosysopc.com/opc-ua-simulation-server-downloads.php)
	
O nosso [Nodered](https://nodered.org/) está na versão 0.19.5.

O node **OPC** que utilizamos foi [node-red-contrib-iiot-opcua](https://flows.nodered.org/node/node-red-contrib-iiot-opcua).

Após configurado os servidores OPCs e instalado o node OPC, vamos às configurações:

1. Configuração/uso Kepserver
	+ Foi configurado um canal e um dispositivo de teste(modo simulador) no Kepserver conforme imagens:
	+ <img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-03.jpg"/></br>
	+ <img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-04.jpg"/></br>
	+ <img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-05.jpg"/></br>
