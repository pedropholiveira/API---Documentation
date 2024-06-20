<div id ='Nio' >
<h2>NioBox</h2> 
    O módulo de automação IP Niobox é um dispositivo projetado para facilitar a automação de ambientes através da rede local. Ele permite o controle remoto de dispositivos, agendamento de tarefas automatizadas, monitoramento em tempo real e integração com sistemas de monitoramento existentes. É ideal para otimizar operações em residências e ambientes comerciais, oferecendo facilidade de configuração e uso via navegador web, tanto por DNS local quanto por IP padrão.
</div>
</br>

# API---Documentation

* [Modo de Configuração do Dispositivo](#config)
    * [Configuração por IP Fixo](#ipFixo)
    * [Configuração em Rede](#dns_local)
*  [Rotas de Configuração](#config_routes)
    * [Configuração do Endereço de ip](#set_ip)
    * [Alteração do Endereço de DNS local](#chenge_name)
    * [Requisitando Endereço de IP](#get_ip)
    * [Requisitando Informações do Dispositivo](#device_info)
    * [Apagando as Configurações de IP do Dispositivo](#rese_ip)
    * [Apagando as Configurações de Automação](#reset_automation)
    * [Restaurando o Dispositivo para as Configurações de Fabrica](#factory_reset)
* [Rotas de Acionamento e Leitura](#input_output)
    * [Acionamento de Saidas](#set_output)
    * [Leitura de Entradas](#get_input)
    * [Leitura de Saidas](#get_output)
    * [Leitura de Entradas e Saidas](#get_io_status)
* [Rotas de Interfaces](#interface)
    * [Interface Inicial](#incial_interface)
    * [Interface de Automação](#automation_interface)
    * [Interface de Configuração do Endereço de IP](#ip_interface)
    * [Interface de Controle](#table_interface)
    * [Interface de Monitoramento de Entradas](#read_input)
    * [Interface de Monitoramento de Saidas](#write_output)
* [Rotas de Desenvolvimento](#dev)
    * [Apagar as configuraçoes de Automação](#reset_automation)
    * [Salvar Configurações de IP](#save_form_ip)
    * [Salvar Tabela de Automação 4x4](#save_table_4x4)
    * [Salvar Tabela de Automação 8x8](#save_table_8x8)
    * [Salvar Tabela de Automação](#save_table)
     * [Retornar Dados de Automação Salvos no Dispositivo](#return_automation_epprom)
    * [Inverter Estado de Saidas](#or_out)
    * [Obter o Estado Atual das Entradas e Saidas](#get_io)
	

<div id ='ipFixo' >
<h2> Modo de Configuração usando IP Fixo</h2> 
   Neste modo, você pode configurar a Niobox utilizando o endereço IP padrão fornecido no guia de instalação rápida. Para isso, siga as etapas abaixo:

* Conecte o dispositivo de automação IP à fonte de energia.
* Com o auxilio de um cabo de rede conecte o Dispositivo ao seu computador.  
* Aguarde até que a luz indicadora do dispositivo esteja estável.
* Abra um navegador da web e digite o endereço IP padrão (192.168.1.100) fornecido no guia de instalação rápida.
* Siga as instruções na tela para concluir o processo de configuração.
* Após configurado conecte o dispositivo a sua rede. 
<br>

<font color='red'><i>obs: talvez seja necessario configurar o ip do computador utilizado para a mesma faixa do dispositivo, no caso .1. Lembre-se de escolher um endereço de IP valido em sua rede. </i></font>
</div>


<div id ='dns_local' >
<h2> Configuração em Rede</h2> 
   Neste modo, você pode configurar a Niobox diretamente na rede utilizando o endereço de DNS local fornecido no guia de instalação rápida. Siga as instruções fornecidas no guia para realizar a configuração usando esta opção. Para isso, siga as etapas abaixo:

* Conecte o cabo de rede ao dispositivo..
* Conecte o dispositivo de automação IP à fonte de energia.  
* Aguarde até que a luz indicadora do dispositivo comece a piscar.
* Utilizando um computador conectado a MESMA rede abra seu navegador de internet (chrome, microsoft edge, etc) pesquise por “niobox.local”.
*Caso você esteja utilizando a versão mais recente, basta acessar o menu “configurar endereço de IP”.
* Siga as instruções na tela para concluir o processo de configuração. 
<br>

<font color='red'><i>obs: dependendo das configurações de sua rede pode ser que demore cerca de 10 minutos para que o endereço de dns local esteja disponivel para o usuario. Dependendo das configurações de segurança de sua rede o endereço de dns local pode falhar.  Lembre-se de escolher um endereço de IP valido em sua rede. </i></font>
</div>


<div id ='config_routes' >
<h2>Rotas de Configuração</h2> 
   Rotas Utilizadas para configurar os parametros do dispositivo.
</div>

<div id ='set_ip' >
<h2>Configuração do entdereço de IP: GET</h2> 
  
* Rota: "niobox.local/set_ip_config" ou "<b/>ip_niobox</b>/set_ip_config"</br>
* Método: GET. </br>
* Função: Rota utilizada para configurar o endereço de IP do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* ip: - > endereço de IP que o dispositivo ira adquirir <b/>obrigatório.</b>
	* gateway: -> endereço de IP do gateway da rede <b/>obrigatório.</b>
	* mask: -> endereço da mascara de rede <b/>obrigatorio.</b>
	</br>
	
* Exemplo de requisição: 
	
		niobox.local/set_ip_config?ip=192.168.88.121&mask=255.255.255.0&gateway=192.168.88.1
	* <b/>ip</b>: endereço de ip que o usuario deseja configurar no dispositivo.
	* <b/>mask</b>: endereço da mascara de rede do local onde o dispositivo sera instalado.<br>
	* <b/>gateway</b>: endereço de ip do gateway da rede onde o dispositivo sera instalado.<br>
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>
	
* Retorno Esperado: </br>

		 {
			"result": "success",
			"info": {
				"ip": "192.168.88.121",
				"gateway": "192.168.88.1",
				"mask": "255.255.255.0",
				"device_name": "niobox"
			}
		}
		
	* <i/>"result"</i>: campo que retorna o status da requisição.
	* <i/>"info"</i>: campo referente ao conteudo da requisição.
	* <i/>"ip"</i>: endereço de IP salvo no dispositivo. 
	* <i/>"gateway"</i>: endereço dE IP do gateway salvo no dispositivo. 
	* <i/>"mask"</i>: endereço da mascara de rede salvo no dispositivo.
	* <i/>"device_name"</i>: DNS local do dispositivo.

<h2>Configuração do entdereço de IP: POST</h2> 
* Rota: "niobox.local/set_ip_config" ou "<b/>ip_niobox</b>/set_ip_config"</br>
* Método: POST. </br>
* Função: Rota utilizada para configurar o endereço de IP do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* ip: - > endereço de IP que o dispositivo ira adquirir <b/>obrigatório.</b>
	* gateway: -> endereço de IP do gateway da rede <b/>obrigatório.</b>
	* mask: -> endereço da mascara de rede <b/>obrigatorio.</b>
	</br>
	
* Exemplo de requisição: 
	* Rota utilizada: <br>
		
				niobox.local/set_ip_config
		<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>
	
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações: 

			{
				"ip": "192.168.88.120",
				"mask": "255.255.255.0",
				"gateway": "192.168.88.1"
			}
	
	* <b/>ip</b>: endereço de ip que o usuario deseja configurar no dispositivo.
	* <b/>mask</b>: endereço da mascara de rede do local onde o dispositivo sera instalado.<br>
	* <b/>gateway</b>: endereço de ip do gateway da rede onde o dispositivo sera instalado.<br>
	
* Retorno Esperado: </br>

		 {
			"result": "success",
			"info": {
				"ip": "192.168.88.120",
				"gateway": "192.168.88.1",
				"mask": "255.255.255.0",
				"device_name": "niobox"
			}
		}
	* <i/>"result"</i>: campo que retorna o status da requisição.
	* <i/>"info"</i>: campo referente ao conteudo da requisição.
	* <i/>"ip"</i>: endereço de IP salvo no dispositivo. 
	* <i/>"gateway"</i>: endereço dE IP do gateway salvo no dispositivo. 
	* <i/>"mask"</i>: endereço da mascara de rede salvo no dispositivo.
	* <i/>"device_name"</i>: DNS local do dispositivo.
<br>
</div>


<div id ='chenge_name' >
<h2>Alteração do endereço de DNS local: GET</h2> 
  * Rota: "niobox.local/set_ip_config" ou "<b/>ip_niobox</b>/set_ip_config"</br>
* Método: GET. </br>
* Função: Rota utilizada para configurar o endereço de IP do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* ip: - > endereço de IP que o dispositivo ira adquirir <b/>obrigatório.</b>
	* gateway: -> endereço de IP do gateway da rede <b/>obrigatório.</b>
	* mask: -> endereço da mascara de rede <b/>obrigatorio.</b>
	</br>
	
* Exemplo de requisição: 
	
		niobox.local/set_ip_config?ip=192.168.88.121&mask=255.255.255.0&gateway=192.168.88.1
	* <b/>ip</b>: endereço de ip que o usuario deseja configurar no dispositivo.
	* <b/>mask</b>: endereço da mascara de rede do local onde o dispositivo sera instalado.<br>
	* <b/>gateway</b>: endereço de ip do gateway da rede onde o dispositivo sera instalado.<br>
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>
	
* Retorno Esperado: </br>

		 {
			"result": "success",
			"info": {
				"ip": "192.168.88.121",
				"gateway": "192.168.88.1",
				"mask": "255.255.255.0",
				"device_name": "niobox"
			}
		}
		
	* <i/>"result"</i>: campo que retorna o status da requisição.
	* <i/>"info"</i>: campo referente ao conteudo da requisição.
	* <i/>"ip"</i>: endereço de IP salvo no dispositivo. 
	* <i/>"gateway"</i>: endereço dE IP do gateway salvo no dispositivo. 
	* <i/>"mask"</i>: endereço da mascara de rede salvo no dispositivo.
	* <i/>"device_name"</i>: DNS local do dispositivo.

<h2>Alteração do endereço de DNS local: POST</h2> 

* Rota: "niobox.local/set_ip_config" ou "<b/>ip_niobox</b>/set_ip_config"</br>
* Método: GET. </br>
* Função: Rota utilizada para configurar o endereço de IP do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* ip: - > endereço de IP que o dispositivo ira adquirir <b/>obrigatório.</b>
	* gateway: -> endereço de IP do gateway da rede <b/>obrigatório.</b>
	* mask: -> endereço da mascara de rede <b/>obrigatorio.</b>
	</br>
	
* Exemplo de requisição: 
	
		niobox.local/set_ip_config?ip=192.168.88.121&mask=255.255.255.0&gateway=192.168.88.1
	* <b/>ip</b>: endereço de ip que o usuario deseja configurar no dispositivo.
	* <b/>mask</b>: endereço da mascara de rede do local onde o dispositivo sera instalado.<br>
	* <b/>gateway</b>: endereço de ip do gateway da rede onde o dispositivo sera instalado.<br>
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>
	
* Retorno Esperado: </br>

		 {
			"result": "success",
			"info": {
				"ip": "192.168.88.121",
				"gateway": "192.168.88.1",
				"mask": "255.255.255.0",
				"device_name": "niobox"
			}
		}
		
	* <i/>"result"</i>: campo que retorna o status da requisição.
	* <i/>"info"</i>: campo referente ao conteudo da requisição.
	* <i/>"ip"</i>: endereço de IP salvo no dispositivo. 
	* <i/>"gateway"</i>: endereço dE IP do gateway salvo no dispositivo. 
	* <i/>"mask"</i>: endereço da mascara de rede salvo no dispositivo.
	* <i/>"device_name"</i>: DNS local do dispositivo.
</div>

<div id ='get_ip' >
<h2>Requisitando endereço de IP</h2> 
   * Rota: "niobox.local/get_ip_config" ou "<b/>ip_niobox</b>/get_ip_config"</br>
* Método: GET. </br>
* Função: Rota utilizada para obter o endereço de IP do dispositivo. </br>
* Parametros: <b/> *Não requer* </b>.</br>
* Resposta Esperada:<br>

* Exemplo de requisição: 
	
		niobox.local/get_ip_config
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i> 
	
* Retorno Esperado: </br>

		 {
			"result": "success",
			"info": {
				"ip": "192.168.88.121",
				"gateway": "192.168.88.1",
				"mask": "255.255.255.0",
				"device_name": "niobox"
			}
		}
		
	* <i/>"result"</i>: campo que retorna o status da requisição.
	* <i/>"info"</i>: campo referente ao conteudo da requisição.
	* <i/>"ip"</i>: endereço de IP salvo no dispositivo. 
	* <i/>"gateway"</i>: endereço dE IP do gateway salvo no dispositivo. 
	* <i/>"mask"</i>: endereço da mascara de rede salvo no dispositivo.
	* <i/>"device_name"</i>: DNS local do dispositivo.

</div>

<div id ='device_info' >
<h2>Requisitando informações do dispositivo</h2> 
* Rota: "niobox.local/get_device_info" ou "<b/>ip_niobox</b>/get_device_info".</br>
* Método: GET. </br>
* Função: Rota utilizada para obter as informações/configurações do dispositivo. </br>
* Parametros: <b/> *Não requer*.</b></br>
* Exemplo de Requisição: 

		niobox.local/get_device_info
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

		 {
			"result": "success",
			"info": {
				"ip": "192.168.88.43",
				"gateway": "192.168.88.1",
				"mask": "255.255.255.0",
				"device_name": "niobox"
			}
		}
	
	* <i/>"result"</i>: campo que retorna o status da requisição.
	* <i/>"info"</i>: campo referente ao conteudo da requisição.
	* <i/>"ip"</i>: endereço de IP salvo no dispositivo. 
	* <i/>"gateway"</i>: endereço dE IP do gateway salvo no dispositivo. 
	* <i/>"mask"</i>: endereço da mascara de rede salvo no dispositivo.
	* <i/>"device_name"</i>: DNS local do dispositivo.
</div>


<div id ='rese_ip' >
<h2>Apagando as configurações de IP do Dispositivo</h2> 
* Rota: "niobox.local/reset_ip" ou "<b/>ip_niobox</b>/reset_ip".</br>
* Método: GET. </br>
* Parametros: <b/> *Não requer* </b>.</br>
* Função: Rota utilizada para apagar as configurações de IP do dispositivo, restaurando-o as configurações de IP de fabrica. (olhar manual). </br>
* Exemplo de Requisição: 

		niobox.local/reset_ip
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

		  {"result": "success"}
	* <i/>"result"</i>: resultado da requisição.   
</div>
  
  <div id ='reset_automation' >
<h2>Apagando as Configurações de Automação</h2> 
  * Rota: "niobox.local/reset_ip" ou "<b/>ip_niobox</b>/reset_ip".</br>
* Método: GET. </br>
* Parametros: <b/> *Não requer* </b>.</br>
* Função: Rota utilizada para apagar as configurações de IP do dispositivo, restaurando-o as configurações de IP de fabrica. (olhar manual). </br>
* Exemplo de Requisição: 

		niobox.local/reset_ip
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

		  {"result": "success"}
	* <i/>"result"</i>: resultado da requisição.
</div>
  
    
<div id ='factory_reset' >
<h2>Restaurando o dispositivo para as configurações de Fabrica</h2> 
  * Rota: "niobox.local/factory_reset" ou "<b/>ip_niobox</b>/factory_reset".</br>
* Método: GET. </br>
* Parametros: <b/> *Não requer* </b>.</br>
* Função: Rota utilizada para apagar as configurações de IP e Automação salvas no dispositivo, restaurando-o as configurações de fabrica. (olhar manual). </br>
* Exemplo de Requisição: 

		niobox.local/factory_reset
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

		  {"result": "success"}
	* <i/>"result"</i>: resultado da requisição.
</div>
    
 <div id ='input_output' >
<h2>Rotas de Acionamento e Leitura</h2> 
   Rotas Utilizadas para acionamento de saidas e leitura de entradas.
</div>

 <div id ='set_output' >
<h2>Acionamento de Saidas: GET</h2> 
   * Rota: "niobox.local/set_output" ou "<b/>ip_niobox</b>/set_output".</br>
* Método: GET. </br>
* Função: Rota utilizada para alterar o estado das saidas do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* address: - > Rele a ser atuado (1 - n° maximo de reles da niobox consultar manual<!--([consultar manual)](https://zionstech.com/))--> <b/>obrigatório.</b>
	* state: -> Estado que o rele referenciado pelo address devera assumir (1 = ligado e 0 = desligado) <b/>obrigatório.</b>
	* time_1: -> Valor de tempo que o rele permanecera no estado definido pelo parametro state <b/>opcional.</b>
	* time_2: -> Valor de tempo que o rele permanecera no estado inverso definido pelo parametro state  <b/>opcional.</b>
	* n_cycles: -> Quantidade de ciclos que irao ocorrer <b/>opcional.</b>
	* time_interval: -> Tempo de intervalo entre ciclos de pulso <b/>opcional.</b> 
	</br>
	</br>
MODOS DE OPERAÇÃO:
* 1. Alterar o estado de um rele:

			niobox.local/set_output?address=1&state=1
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera assumir (1 = acionado e 0 = desacionado).
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
</br>

* 2. Gerador de pulso: 

				niobox.local/set_output?address=1&state=1&time_1=1000
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera assumir (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em milissegundos que o rele devera assumir o estado definido pelo parametro state.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
</br> 

* 3. Repetir um pulso por tempo inderteminado: 

			niobox.local/set_output?address=1&state=1&time_1=1000&time_2=1000
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro state.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
</br>

* 4. Repetir ciclo de pulsos pela quantidade de vezes definida: 

			niobox.local/set_output?address=1&state=1&time_1=1000&time_2=1000&n_cycles=5
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro.
		* <b/>n_cycles</b>: numero de vezes que o ciclo devera ocorrer.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		

</br>

* 5. Repetir um pulso por um tempo definido: 

			niobox.local/set_output?address=1&state=1&time_1=1000&time_2=1000&time_total=100000
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro state.
		* <b/>time_total</b>: tempo total em millissegungos que a operação devera ocorrer.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
</br>

* 6. Repetir um ciclo de pulsos, com intervalo por tempo inderteminado: 

			niobox.local/set_output?address=1&state=1&time_1=1000&time_2=1000&n_cycles=5&time_interval=100000
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro state.
		* <b/>n_cycles</b>: numero de pulsos por ciclo.
		* <b/>time_interval</b>: tempo de espera em milissegundos entre os ciclos.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
	
	<br>
		
* FORMATO DE RESPOSTA ESPERADO :

		{
			"result": "success",
			"data": {
				"output": {
					"state": [
						true,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					]
				}
			}
		}

* <i/>"result"</i>: campo que informa o status da requisição. 
* <i/>"data"</i>: campo que contem as informações da requisição. 
* <i/>"output"</i>: campo referente a solicitação da requisição. 
* <i/>"state"</i>: campo que informa o estado atual das entradas do dispositivo. 

<h2>Acionamento de Saidas: POST</h2> 
* Rota: "niobox.local/set_output" ou "<b/>ip_niobox</b>/set_output".</br>
* Método: POST. </br>
* Função: Rota utilizada para alterar o estado das saidas do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* address: - > Rele a ser atuado (1 - n° maximo de reles da niobox consultar manual<!--([consultar manual)](https://zionstech.com/))-->  <b/>obrigatório.</b>
	* state: -> Estado que o rele referenciado pelo address devera assumir (1 = ligado e 0 = desligado) <b/>obrigatório.</b>
	* time_1: -> Valor de tempo que o rele permanecera no estado definido pelo parametro state <b/>opcional.</b>
	* time_2: -> Valor de tempo que o rele permanecera no estado inverso definido pelo parametro state  <b/>opcional.</b>
	* n_cycles: -> Quantidade de ciclos que irão ocorrer <b/>opcional.</b>
	* time_interval: -> Tempo de intervalo entre ciclos de pulso <b/>opcional.</b> 
	</br>
	</br>
MODOS DE OPERAÇÃO:
* 1. Alterar o estado de um rele:
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações: 

			{
			"address":1,
			"state":1
			}
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera assumir (1 = acionado e 0 = desacionado).
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
</br>

* 2. Gerador de pulso: 
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações:

			{
			"address":1,
			"state":1,
			"time_1":1000
			}
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera assumir (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em milissegundos que o rele devera assumir o estado setado pelo parametro state.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
</br> 

* 3. Repetir um pulso por tempo inderteminado: 
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações:

			{
			"address":1,
			"state":1,
			"time_1":1000,
			"time_2":1000
			}
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo paramtero state.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
</br>

* 4. Repetir ciclo de pulsos pela quantidade de vezes definida: 
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações:

			{
			"address":1,
			"state":1,
			"time_1":1000,
			"time_2":1000,
			"n_cycles":5
			}
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro state.
		* <b/>n_cycles</b>: numero de vezes que o ciclo devera ocorrer.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		

</br>

* 5. Repetir um pulso por um tempo definido: 
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações:

			{
			"address":1,
			"state":1,
			"time_1":1000,
			"time_2":1000,
			"time_total":1000
			}
		
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro state.
		* <b/>time_total</b>: tempo total em millissegungos que a operação devera ocorrer.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
</br>

* 6. Repetir um ciclo de pulsos, com intervalo por tempo inderteminado: 
	* Como é utilizado um metodo POST para realizar o acionamento devemos enviar um json contendo as seguintes informações:

			{
			"address":1,
			"state":1,
			"time_1":1000,
			"time_2":1000,
			"n_cycles":5,
			"time_interval":5000,
			"time_total":1000
			}
			
		* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		* <b/>state</b>: estado que o rele devera acionar no primeiro ciclo (1 = acionado e 0 = desacionado).
		* <b/>time_1</b>: tempo em que o rele devera assumir estado definido pelo parametro state. 
		* <b/>time_2</b>: tempo em que o rele devera assumir o estado inverso definido pelo parametro state.
		* <b/>n_cycles</b>: numero de pulsos por ciclo.
		* <b/>time_interval</b>: tempo de espera em milissegundos entre os ciclos.
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
<br>

* FORMATO DE RESPOSTA ESPERADO :

		{
			"result": "success",
			"data": {
				"output": {
					"state": [
						true,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					]
				}
			}
		}

* <i/>"result"</i>: campo que informa o status da requisição. 
* <i/>"data"</i>: campo que contem as informações da requisição. 
* <i/>"output"</i>: campo referente a solicitação da requisição. 
* <i/>"state"</i>: campo que informa o estado atual das entradas do dispositivo. 
</div>

 <div id ='get_input' >
<h2>Leitura de Entradas</h2> 
   * Rota: "niobox.local/get_input_status" ou "<b/>ip_niobox</b>/get_input_status".</br>
* Método: GET. </br>
* Função: Rota utilizada para consultar o estado das entradas do dispositivo. </br>
* Parametros: <b/> *Não requer.* </b></br>
* Exemplo de Requisição: <br>

		niobox.local/get_input_status
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

		 {
			"result": "success",
			"data": {
				"input": {
					"state": [
						true,
						true,
						true,
						true,
						false,
						false,
						false,
						false
					],
					"transition": [
						false,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					]
				}
			}
		}


* <i/>"result"</i>: campo que informa o status da requisição. 
* <i/>"data"</i>: campo que contem as informações da requisição. 
* <i/>"input"</i>: campo referente a solicitação da requisição. 
* <i/>"state"</i>: campo que informa o estado atual das entradas do dispositivo. 
* <i/>"transition"</i>: campo que informa se houve transição de estado nas entradas do dispositivo. 

</div>

<div id ='get_output' >
<h2>Leitura de Saidas</h2> 
   * Rota: "niobox.local/get_output_status" ou "<b/>ip_niobox</b>/get_output_status".</br>
* Método: GET. </br>
* Função: Rota utilizada para consultar o estado das saidas do dispositivo. </br>
* Parametros: <b/> *Não requer.* </b></br>
* Exemplo de Requisição: 

		niobox.local/get_output_status
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>
* Resposta Esperada:<br>

		 {
			"result": "success",
			"data": {
				"output": {
					"state": [
						false,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					],
					"transition": [
						false,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					]
				}
			}
		}		
* <i/>"result"</i>: campo que informa o status da requisição. 
* <i/>"data"</i>: campo que contem as informações da requisição. 
* <i/>"output"</i>: campo referente a solicitação da requisição. 
* <i/>"state"</i>: campo que informa o estado atual das saidas do dispositivo. 
* <i/>"transition"</i>: campo que informa se houve transição de estado nas saidas do dispositivo. 

</div>

<div id ='get_io_status' >
<h2>RLeitura de Entradas e Saidas</h2> 
   * Rota: "niobox.local/get_io_status" ou "<b/>ip_niobox</b>/get_io_status".</br>
* Método: GET. </br>
* Função: Rota utilizada verificar o estados das entras e saidas do dispositivo. </br>
* Parametros: <b/> *Não requer.* </b></br>
* Exemplo de Requisição: 

		niobox.local/get_io_status
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

		 {
			"result": "success",
			"data": {
				"output": {
					"state": [
						false,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					],
					"transition": [
						false,
						false,
						false,
						false,
						false,
						false,
						false,
						false
					]
				},
				"input": {
					"state": [
						true,
						true,
						true,
						true,
						false,
						false,
						false,
						false
					],
					"transition": [
						true,
						true,
						true,
						true,
						false,
						false,
						false,
						false
					]
				}
			}
		}		
* <i/>"result"</i>: campo que informa o status da requisição. 
* <i/>"data"</i>: campo que contem as informações da requisição. 
* <i/>"input"</i>: campo referente as informações das entradas. 
* <i/>"state"</i>: campo que informa o stado atual das entradas do dispositivo. 
* <i/>"transition"</i>: campo que informa se houve transição de estado nas entradas do dispositivo. 
* <i/>"output"</i>: campo referente as informações das saidas. 
* <i/>"state"</i>: campo que informa o estado atual das saidas do dispositivo. 
* <i/>"transition"</i>: campo que informa se houve transição de estado das saidas do dispositivo. 
</div>

<div id ='interface' >
<h2>Rotas de Interfaces</h2> 
   Rotas Utilizadas para acessar as interfaces de usuario.
</div>

<div id ='incial_interface' >
<h2>Interface Inicial</h2> 
   * Rota: "niobox.local/" ou "<b/>ip_niobox</b>/"</br>
* Método: GET. </br>
* Função: Rota utilizada para acessar a tela inicial do dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
</div>



<div id ='automation_interface' >
<h2>Interface de Automação</h2> 
    * Rota: "niobox.local/automation" ou "<b/>ip_niobox</b>/automation"</br>
* Método: GET. </br>
* Função: Rota utilizada para acessar a tela de configuração do modo automação do dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/automation
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
</div>


<div id ='ip_interface' >
<h2>Interface de Configuração do Endereço de IP</h2> 
   * Rota: "niobox.local/ip_config" ou "<b/>ip_niobox</b>/ip_config"</br>
* Método: GET. </br>
* Função: Rota utilizada para acessar a tela de configuração dos parametros de rede do dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/ip_config
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
</div>

<div id ='table_interface' >
<h2>Interface de Controle</h2> 
   * Rota: "niobox.local/table" ou "<b/>ip_niobox</b>/table"</br>
* Método: GET. </br>
* Função: Rota utilizada para acessar a tela da mesa de controle do dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/table
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
</div>

<div id ='read_input' >
<h2>Interface de Monitoramento de Entradas</h2> 
   * Rota: "niobox.local/read_input" ou "<b/>ip_niobox</b>/read_input"</br>
* Método: GET. </br>
* Função: Rota utilizada para acessar a tela de monitoramento das entradas do dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/read_input
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
</div>

<div id ='write_output' >
<h2>Interface de Monitoramento de Saidas</h2> 
   * Rota: "niobox.local/write_output" ou "<b/>ip_niobox</b>/write_output"</br>
* Método: GET. </br>
* Função: Rota utilizada para acessar a tela de  acionamento/monitoramento das saidas do dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/write_output
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
</div>

<div id ='reset_automatio' >
<h2>Apagar as Configuraçoes de Automação</h2> 
   * Rota: "niobox.local/reset_automation" ou "<b/>ip_niobox</b>/reset_automation"</br>
* Método: GET. </br>
* Função: Rota utilizada para apagar todas as informações de automação salvas no dispositivo. </br>
* <b/>PARAMETROS:</b> Não requer. </br>
* Exemplo de requisição: 
	
		niobox.local/reset_automation	
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
* Retorno Esperado: </br>

		 {
		"result": "success"
		}
	* <i/>"result"</i>: campo que retorna o status da requisição.
</div>

<div id ='save_form_ip' >
<h2>Salvar Configurações de IP</h2> 
   * Rota: "niobox.local/form_input" ou "<b/>ip_niobox</b>/form_input"</br>
* Método: POST. </br>
* Função: Rota utilizada para salvar todas as informações inseridas no formulario. </br>
* <b/>PARAMETROS:</b>
	* ip: - > Endereço de IP que o dispositivo ira adquirir <b/>obrigatorio.</b>
	* gateway: - > Endereço de IP do gateway da rede <b/>obrigatorio.</b>
	* mask: - > Endereço de mascara da rede <b/>obrigatorio.</b>
	* name: - > Nome do Endereço de DNS local do dispositivo <b/>obrigatorio.</b>
	</br>
* Exemplo de requisição: 
	
		niobox.local/form_input?ip=192.168.1.100&mask=255.255.255.0&gateway=192.168.1.1&name=sala	
	* <b/>ip</b>: endereço de ip que o usuario deseja configurar no dispositivo.
	* <b/>mask</b>: endereço da mascara de rede do local onde o dispositivo sera instalado.<br>
	* <b/>gateway</b>: endereço de ip do gateway da rede onde o dispositivo sera instalado.<br>
	* <b/>name</b>: nome do DNS <b/>local</b> do dispositivo.<br>
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>
	
* Retorno Esperado: </br>

		 {
		"result": "success"
		}
	* <i/>"result"</i>: campo que retorna o status da requisição.
</div>

<div id ='config_routes' >
<h2>Salvar Tabela de Automação 4x4</h2> 
  * Rota: "niobox.local/save_table" ou "<b/>ip_niobox</b>/save_table"</br>
* Método: POST. </br>
* Função: Rota utilizada para salvar todas as informações inseridas na tabela referente a automação. </br>
* <b/>PARAMETROS:</b>
	* dados: - > Campo que contem todas as informações referentes as linhas da tabela<b/>obrigatorio.</b>
	* entrada: - > Campo referente a linha da tabela <b/>obrigatorio.</b>
	* estado: - > Campo referente ao estado que a entrada deverá assumir para ativar o condicional <b/>obrigatorio.</b>
	* saidas: - > Vetor referente as saidas que devem sem acionadas <b/>obrigatorio.</b>
	* tempo: - > Campo referente a duração de tempo em que a saida devera ficar acionada<b/>obrigatorio.</b>
	* habilitarTempo: - > Campo referente a ativação do tempo de pulso do condicional <b/>obrigatorio.</b>
	* habilitarRegra: - > Campo referente a ativação do condicional <b/>obrigatorio.</b>
	</b>
	</br>
* Exemplo de requisição: 
	* Rota utilizada:
	
		niobox.local/save_table	
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>

* Como é utilizado um metodo POST para realizar a configuração do modo automação devemos enviar um json contendo as seguintes informações 

		{"dados":[{"entrada":1,"estado":"1","saidas":[1,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":2,"estado":"0","saidas":[0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":3,"estado":"0","saidas":[0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":4,"estado":"0","saidas":[0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0}]}
	
* Retorno Esperado: </br>

		 {
		"result": "success"
		}
	* <i/>"result"</i>: campo que retorna o status da requisição.
</div>  
<div id ='config_routes' >
<h2>Salvar Tabela de Automação 8x8</h2> 
  * Rota: "niobox.local/save_table" ou "<b/>ip_niobox</b>/save_table"</br>
* Método: POST. </br>
* Função: Rota utilizada para salvar todas as informações inseridas na tabela referente a automação. </br>
* <b/>PARAMETROS:</b>
	* dados: - > Campo que contem todas as informações referentes as linhas da tabela<b/>obrigatorio.</b>
	* entrada: - > Campo referente a linha da tabela <b/>obrigatorio.</b>
	* estado: - > Campo referente ao estado que a entrada deverá assumir para ativar o condicional <b/>obrigatorio.</b>
	* saidas: - > Vetor referente as saidas que devem sem acionadas <b/>obrigatorio.</b>
	* tempo: - > Campo referente a duração de tempo em que a saida devera ficar acionada<b/>obrigatorio.</b>
	* habilitarTempo: - > Campo referente a ativação do tempo de pulso do condicional <b/>obrigatorio.</b>
	* habilitarRegra: - > Campo referente a ativação do condicional <b/>obrigatorio.</b>
	</b>
	</br>
* Exemplo de requisição: 
	* Rota utilizada:
	
		niobox.local/save_table	
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>

* Como é utilizado um metodo POST para realizar a configuração do modo automação devemos enviar um json contendo as seguintes informações 

		{"dados":[{"entrada":1,"estado":"1","saidas":[1,0,0,0,0,0,0,1],"tempo":"0","habilitarTempo":0,"habilitarRegra":1},{"entrada":2,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":3,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":4,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":5,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":6,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":7,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":8,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0}]}
	
* Retorno Esperado: </br>

		 {
		"result": "success"
		}
	* <i/>"result"</i>: campo que retorna o status da requisição.
</div>  

<div id ='save_table' >
<h2>Salvar Tabela de Automação</h2> 
   * Rota: "niobox.local/save_table" ou "<b/>ip_niobox</b>/save_table"</br>
* Método: POST. </br>
* Função: Rota utilizada para salvar todas as informações inseridas na tabela referente a automação. </br>
* <b/>PARAMETROS:</b>
	* dados: - > Campo que contem todas as informações referentes as linhas da tabela<b/>obrigatorio.</b>
	* entrada: - > Campo referente a linha da tabela <b/>obrigatorio.</b>
	* estado: - > Campo referente ao estado que a entrada deverá assumir para ativar o condicional <b/>obrigatorio.</b>
	* saidas: - > Vetor referente as saidas que devem sem acionadas <b/>obrigatorio.</b>
	* tempo: - > Campo referente a duração de tempo em que a saida devera ficar acionada<b/>obrigatorio.</b>
	* habilitarTempo: - > Campo referente a ativação do tempo de pulso do condicional <b/>obrigatorio.</b>
	* habilitarRegra: - > Campo referente a ativação do condicional <b/>obrigatorio.</b>
	</b>
	</br>
* Exemplo de requisição: 
	* Rota utilizada:
	
		niobox.local/save_table	
	
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i></br>

* Como é utilizado um metodo POST para realizar a configuração do modo automação devemos enviar um json contendo as seguintes informações 

		{"dados":[{"entrada":1,"estado":"1","saidas":[1,0,0,0,0,0,0,1],"tempo":"0","habilitarTempo":0,"habilitarRegra":1},{"entrada":2,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":3,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":4,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":5,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":6,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":7,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0},{"entrada":8,"estado":"0","saidas":[0,0,0,0,0,0,0,0],"tempo":"0","habilitarTempo":0,"habilitarRegra":0}]}
	
* Retorno Esperado: </br>

		 {
		"result": "success"
		}
	* <i/>"result"</i>: campo que retorna o status da requisição.
</div>  

<div id ='return_automation_epprom' >
<h2>Retornar Dados de Automação Salvos no Dispositivo</h2> 
  * Rota: "niobox.local/return_EPPROM" ou "<b/>ip_niobox</b>/return_EPPROM".</br>
* Método: GET. </br>
* Função: Rota utilizada para obter as informações/configurações do modo automação salvo no dispositivo. </br>
* Parametros: <b/> *Não requer*.</b></br>
* Exemplo de Requisição: 

		niobox.local/return_EPPROM
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

			 {
		"l1": [
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0
		],
		"l2": [
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0
		],
		"l3": [
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0
		],
		"l4": [
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0,
			0
		],
		"conditional": 0
		}
	
	* <i/>"l"</i>: Campo referente a linha da tabela o mesmo contem um vetor contendo as informações salvas em cada campo.
		* <i/>"conditional"</i>: Campo que informa o estado das informações sendo 0 para informações de fabrica e 1 para informações inseridas por usuario.
	
</div>  

<div id ='or_out' >
<h2>Inverter Estado de Saidas</h2> 
   * Rota: "niobox.local/or_out" ou "<b/>ip_niobox</b>/or_out".</br>
* Método: GET. </br>
* Função: Rota utilizada para inverter o estado de uma saida do dispositivo. </br>
* <b/>PARAMETROS:</b>
	* address: - > Rele a ser atuado (1 - n° maximo de reles da niobox consultar manual<!--([consultar manual)](https://zionstech.com/))-->  <b/>obrigatório.</b>
* Exemplo de Requisição:

			niobox.local/or_out?address=1	
	* <b/>address</b>: numero do rele a ser atuado (1 - maximo de saidas da niobox).
		
		<i/>obs: o endereço de dns local pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição</i>.
		
* FORMATO DE RESPOSTA ESPERADO :

		{
		"result": "false"
		}

* <i/>"result"</i>: campo que informa o estado atual da saida sendo "success" para ativado e "false" para desativado.
 
</div>  
<div id ='get_io' >
<h2>Obter o Estado Atual das Entradas e Saidas</h2> 
   * Rota: "niobox.local/io_status" ou "<b/>ip_niobox</b>/io_status".</br>
* Método: GET. </br>
* Função: Rota utilizada para obter os estados atuais das entradas e saidas do dispositivo. </br>
* Parametros: <b/> *Não requer*.</b></br>
* Exemplo de Requisição: 
		niobox.local/io_status
	<i/>obs: o endereço de dns local ("niobox.local") pode falhar dependendo das configurações de sua rede, portanto recomendamos que o mesmo seja substituido pelo endereço de ip do dispositivo na hora de realizar a requisição.</i>

* Resposta Esperada:<br>

			 {
		"result": "success",
		"data": {
			"output": {
				"state": [
					true,
					false,
					false,
					false
				]
			},
			"input": {
				"state": [
					false,
					false,
					false,
					false
				]
			}
		}
	}
	
* <i/>"result"</i>: campo que informa o status da requisição. 
* <i/>"data"</i>: campo que contem as informações da requisição. 
* <i/>"output"</i>: campo referente ao estado atual de todas as saidas do dispositivo. 
* <i/>"input"</i>: campo referente ao estado atual de todas as entradas do dispositivo. 
* <i/>"state"</i>: campo que informa o estado atual das entradas e saidas do dispositivo. 

</div>  
 
   