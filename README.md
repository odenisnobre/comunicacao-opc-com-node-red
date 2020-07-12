<h1 align="center">
<br>
Comunicação OPC com Node-Red
</h1>

<p align="center">O projeto tem como objetivo documentar os testes de comunicação realizado entre um servidor OPC e o Node-Red.</p>

<p align="center">
  <a href="https://www.apache.org/licenses/LICENSE-2.0">
    <img src="https://img.shields.io/badge/apache-2.0-blue" alt="License Apache">
  </a>
</p>
<hr />

## Desenvolvimento

O primeiro passo para iniciar os testes foi definir qual OPC utilizar. Após análise chegamos em dois servidor:

1. KEPServer
	+ Utilizado a versão Enterprise V5
2. Prosys OPC UA Simulation Server
	+ Utilizado a versão [3.1.6-192](https://downloads.prosysopc.com/opc-ua-simulation-server-downloads.php)
	
O nosso [Node-red](https://nodered.org/) está na versão 0.19.5.

O node **OPC** que utilizamos foi [node-red-contrib-iiot-opcua](https://flows.nodered.org/node/node-red-contrib-iiot-opcua).

Após configurado os servidores OPCs e instalado o node OPC, vamos às configurações:

## Kepserver

1. **Configuração**
	+ Foi configurado um canal e um dispositivo de teste(modo simulador) no Kepserver conforme imagens:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-03.jpg"/>
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-04.jpg"/>
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-05.jpg"/>
	+ Abrindo o modo **Client** do Kepserver temos as informações e estrutura que utilizaremos no Node-Red:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-06.jpg"/></br>
		1. **Kepware.KEPServerEnterprise.V5**: este é o nome que deverá ser configurado no node do Node-Red.
		2. Mostra o nome do canal com o dispositivo.
		3. Identifica o caminho completo da *tag* OPC que será linkado no Node-Red para leitura ou escrita.
	+ As configurações de comunicação e acesso a sistemas externos são configurados conforme imagem abaixo:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-10.jpg"/></br>
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-11.jpg"/></br>
		
		Com essas configurações de acesso que podem ser local ou remoto, conforme mostrado acima, temos condições de configurar o Node-Red.
		No meu caso irei usar as configurações 	```opc.tcp://192.168.50.130:49370```
		
2. **Uso**  
	+ Com o *node OPC* devidamente instalado prosseguiremos com as configurações do Node-Red.  
	+ **Leitura**:  
		+ Para fazer a leitura de um valor vamos usar a seguinte estrutura:  
			<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-12.jpg"/></br>
			* (1) determina a frequência de leitura da tag OPC. Além disso, na outra aba temos o caminho completo da tag.  
				<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-15.jpg"/></br>
			* (2.1) este node é o que faz a leitura OPC. Em connector temos que configurar o servidor OPC:
				<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-18.jpg"/></br>
			* (2.2) configuração do servidor OPC. Onde é definido o Endpoint, que no nosso caso é ```opc.tcp://192.168.50.130:49370/Kepware.KEPServerEnterprise.V5```. Estas configurações estão
				conforme mostrado anteriormente. O campo **Name** é bom preencher com o nome da fonte de dados para ficar mais facil identificar caso tenha mais de um conexão OPC.  
				<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-17.jpg"/></br>
			* (3) resposta da comunicação.
			* (4) retorna o valor recebido no console do Node-Red(debug).
			* (5) como vimos no item 1, podemos listar quais tag iremos ler. Estes valores retorna um *array* de x posições. Então para usá-lo temos que 'pegar' o índice do array que necessitamos.
				A estrutura de retorno que vai, por exemplo, pro *debug* é a seguinte ```msg.payload[0].value```. Está desta forma porque selecionamos somente um item para leitura.
				O componente trend do dashboard não tem como personalizar a mensagem que é recebida, então ele recebe os dados somente no msg.payload. Este node converte ```msg.payload[0].value```
				para ```msg.payload```.
			* (6) trend para dashboard.
	+ **Escrita**
		+ Para fazer a escrita de um valor vamos usar a seguinte estrutura: 
			<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-13.jpg"/></br>
			* (1) determina a frequência de leitura da tag OPC. Além disso, na outra aba temos o caminho completo da tag. A terceira opção logo após o caminho completo da tag é o tipo de dados
				da tag que deve ser preenchido, quando é uma escrita de dados. No meu caso deixei como ```double```.
				<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-15.jpg"/></br>  
			* (2) é o node de escrita OPC.  
				<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-19.jpg"/></br>
				
## Prosys OPC UA Simulation Server

1. **Configuração**
	+ O Prosys por ser um simulador já possui sua estrutura de tag e configuração já definida ficando pronto pra uso.  
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-07.jpg"/></br>
	+ Como foi dito anteriormente o que tem que se atentar é o caminho de conexão do OPC, neste caso é ```OPCUA/SimulationServer```:  
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-08.jpg"/></br>
	+ Os tag são definidos na configuração abaixo:  
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-09.jpg"/></br>
		
2. **Uso**
	+ A forma de uso de leitura e escrita do simulador segue o mesmo padrão do Kepserver, visto que as tags já estão mapeadas.
	+ Só tem que se atentar na configuração do servidor OPC no Node-Red ficando o Endpoint ```opc.tcp://192.168.50.130:53530/OPCUA/SimulationServer```:
		<img src="https://github.com/dedynobre/comunicacao-opc-com-node-red/blob/master/images/nodered-opc-20.jpg"/></br>  
	+ As configurações do nodes são iguais.
	
## Conclusão

Com este testes de uso do node OPC chegamos a conclusão que o Node-Red atende super bem a demandas e configurações que envolvem *automação industrial*. Com isto se torna um aliado nas demandas
da indútria 4.0 e conceito de **iiot**.
Em ambientes de automação existem vários protocolos de ocmunicação e entre ele o que mais estã difundido nos ambientes industriais são basicamenteo o Modbus, seja TCP ou Serial, e o OPC. O Node-Red
tendo interface com estes protocolos abre um mundo de possibilidades de conectividade com várias aplicações.


## Help

Caso precisem te ajuda ou tenham alguma sugestão, deixe seu comentário [Aqui](https://github.com/dedynobre/comunicacao-opc-com-node-red/issues).
	
	
				
					
