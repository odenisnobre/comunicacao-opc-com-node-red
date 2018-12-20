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


