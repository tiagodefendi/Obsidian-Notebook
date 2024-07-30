# Origem

- Modelo de referência **OSI - Open Systems Interconnection**
- Desenvolvido pela ISO - International Standards Organization
- Objetivo de **padronizar** a maneira de desenvolver soluções para a troca de dados
- Permite que as empresas diferentes que produzem produtos diferente possam trocar informações
- Ideia de Sistema aberto a comunicação com outros sistemas
# Camadas

- *"Dividir para conquistar*
- Dividido em 7 Camadas
- Cada camada resolve um problema em específico
- Vários benefícios ao se dividir funções ou tarefas em camadas e definir interfaces
	- **Menor complexidade**
		- Resolvemos problemas menores para depois os maiores
	- **Interfaces padronizadas**
		- Permite que fabricantes concorrentes criem seus produtos e todos interajam
		- Permite a interoperabilidade entre fabricantes
	- **Engenharia Modular**
		- Uso de conceito de funções ou classes para solução de problemas
		- Uma alteração só afeta a respectiva camada
		- Mais fácil desenvolver/corrigir soluções de rede
## Quais são as camadas?

- [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Física|Física]] - Layer 1
- [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Enlace|Enlace]] - Layer 2
- [[Rede]] - Layer 3
- [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Transporte|Transporte]] - Layer 4
- [[Sessão]] - Layer 5
- [[Apresentação]] - Layer 6
- [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Aplicação|Aplicação]] - Layer 7
# Tráfego entre camadas

- Quando são enviados dados pelas camadas cada uma adiciona seu cabeçalho neles
- Nesses cabeçalhos existem informações específicas sobre cada camada
- Os dados mais o cabeçalho recebe o nome de **pacote**
- Todas as camadas se comunicam com as camadas que lhe são adjacente
## Pacote de dados

- O tráfego na rede é enviado em **pacotes de dados / pacote de rede**
- Um pacote é uma informação de usuário transformado em um formato entendido pela rede
- Cada camada adiciona sua informação, porem o pacote de dados não é alterado
- As informações adicionadas são chamadas de **cabeçalho**
	- Um cabeçalho é simplesmente a informação que detalha o formato do pacote
# Modelo Teórico

 - É um modelo de referência teórico
 - Não é implementado na prática (algumas partes não todas)
 - O modelo prático é o [[Modelo TCP-IP|Modelo TCP/IP]]
 - Por que entender um modelo de rede que não existe no mundo real?
	 - Ele que nos guia nos conceitos e entendimentos sobre as partes que compõem as redes e como elas funcionam
 - O modelo OSI é um resumo ou mapa das redes de computadores
 - Cobre de forma simples e resumida praticamente todos os aspectos envolvendo redes de computadores
# Protocolos de Rede

- Um protocolo basicamente é um acordo entre as partes que se comunicam , estabelecendo como se dará a comunicação
- Tipo de software/hardware que cuida de alguma tarefa específica da transmissão de dados na rede
	- Implementação lógica (Programação)
	- Estruturação de dados (Pacote de rede com dados e cabeçalho)
- Para duas ou mais máquinas trocarem informações elas devem executar o mesmo protocolo
# Protocolos x Camadas X Modelos

- É comum a confusão entre esses conceitos
- Protocolo está contido dentro de uma Camada e ela em um Modelo
- Protocolos são implementações práticas de uma camada ou parte dela, ou podem interagir com as funções de mais de uma camada
- A camada resolve alguma problema específico da rede (através do protocolo) e o modelo resolve "todos" os problemas referentes a transmissão de dados na rede
- Em resumo o Modelo é a ideia de como resolver os problemas da rede, as camadas são as soluções de parte dos problemas, e os protocolos são a implementação prática da camada

Refs: [[Redes de Computadores]], [[Modelos de Rede]]