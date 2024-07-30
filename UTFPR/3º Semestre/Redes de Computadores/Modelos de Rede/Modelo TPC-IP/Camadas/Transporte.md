# Relação com Modelo OSI

- Faz relação direta com a camada de [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Transporte|Transporte]] do Modelo OSI
# Protocolos

- **TCP - Transmission Control Protocol**
	- Protocolo mais usado na transmissão de dados
	- Pega os pacotes da camada Internet e trata de colocá-los em ordem e verificar se todos chegaram em ordem
	- Tratar de erros
		- Dados fora de ordem
		- Dados corrompidos
		- Dados não chegam
- **UDP - User Datagram Protocol**
	- Não verifica se o dado chegou ou não ao destino
	- Usado na transmissão de informação de controle
# Funções

- Pega os dados enviados pela camada de aplicação e transforma eles em pacotes a serem repassados para a camada Inter-rede
## Intercalamento de Pacotes

- Ela possuí um esquema de multiplexação, onde é possível transmitir "simultaneamente" dados das mais diferentes aplicações
- Na verdade eles não são enviados juntos, mas sim de forma **intercalada** 
- Permite que vários programas se comuniquem na rede ao mesmo tempo, mas os pacotes serão enviados de forma intercalada
- Isso se deve ao conceito do uso de portas

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]]