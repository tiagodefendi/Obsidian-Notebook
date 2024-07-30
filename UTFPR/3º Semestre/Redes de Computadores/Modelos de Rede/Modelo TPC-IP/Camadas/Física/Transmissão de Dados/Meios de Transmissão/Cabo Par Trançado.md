# O que é?

- Mais usado em redes atualmente
- Possui dois tipos
	- Sem blindagem - **UTP - Unshielded Twisted Pair**
	- Com Blindagem - **STP - Shielded Twisted Pair**
- O Par trançado sem blindagem é o mais utilizado hoje em dia, que usa o conector RJ-45
- Possui uma ótima proteção contra ruídos, a técnica usada é chamada de **cancelamento** e não usa blindagem
# Cancelamento

- As informações circulam repetidas em dois fios
- No segundo fio a informação possui a polaridade invertida
- Todo fio produz um campo eletromagnético, ao seu redor quando um dado é transmitido, se esse campo for forte o suficiente ele corromperá os dados do fio ao lado - **cross-talk**
- A direção desse campo depende do sentido da corrente que está circulando, se é positiva ou negativa
- Com o par trançado transmitindo a mesma informação com a polaridade invertida, os campos eletro magnéticos são anulados
- Além de que com a informação duplicada o receptor consegue verificar mais fácil se ela está corrompida
- Tudo que existe em um fio tem no outro, dessa forma o que for diferente nos dois sinais é ruído e tem como ser eliminado facilmente
- Esses fios são enrolados um no outro, por isso que o cabo é chamado de par trançado, já que são agrupados de dois em dois enrolados
# Características

- Dois pares de fios, um para transmissão de dados (TD) e outro para recepção (RD)
- É possível utilizar transmissão full-duplex
- Tradicionalmente usa 4 pares de fios (dois deles não são usados)
- Tem um custo relativamente baixo e flexível
- Usa um conceito de cabeamento estruturado
- Possui uma distância máxima de 100 metros
- Controle de interferência relativamente bom (exceto em ambientes industriais)
- Taxa de velocidade podendo assumir
	- 10BaseT - 10 Mbps uni-canal
	- 100BaseT - 100 Mbps
	- 1000BaseT / Gigabit Ethernet - 1000 Mbps
	- T vem de Twisted Pair
- Usa topologia estrela - Hub - só melhora a flexibilidade da rede
- Topologia linear
- Possuí limite de dois dispositivos por cabo
# Padrões

- O cabo par trançado foi padronizado pela EIA/TIA (Electronic Industries Alliance/Telecommunications Industry Association), e utiliza a norma 568.
- 5 categorias
	- Categoria 1 e 2: sistemas telefônicos
	-  Categoria 3: Comunicação até 16 Mbps - Rede 10BaseT
	-  Categoria 4: Comunicação até 20 Mbps
	-  Categoria 3: Comunicação até 100 Mbps - Impedância de 100 ohms, pode ser usado por redes 1000BaseT com técnicas especiais
		- Para que a rede alcance uma taxa de 1000 Mbps, é necessário utilizar os quatro pares de fios simultaneamente
		- Trabalhando assim de forma full-duplex.
		- O esquema de modulação utilizado é o 4D-PAM5, que permite que vários dados possam ser enviados por vez.
# Pinagem

- Possui 4 pares de fios -  2 usados (um receptor e outro transmissor)
- O cabo sem blindagem usa o conector RJ-45, que possui 8 canais, já que o cabo possui 8 fios
- Para melhor identificação são usadas cores nos fios
	- Verde
	- Laranja
	- Marrom
	- Azul
- Cada par terá um fio totalmente colorido e outro com uma listra branca
- Usa um esquema de ligação pino-a-pino
	- Pino 1 no pino 1, pino 2 no pino 2...
- Pode usar outras configurações
- Padrão usado na 10BaseT

| Pino |        Cor         | Função    |
| :--- | :----------------: | --------- |
| 1    |  Banco com Verde   | +TD       |
| 2    |       Verde        | -TD       |
| 3    | Branco com Laranja | +RD       |
| 4    |        Azul        | Não Usado |
| 5    |  Branco com Azul   | Não Usado |
| 6    |      Laranja       | -RD       |
| 7    | Branco com Marrom  | Não Usado |
| 8    |       Marrom       | Não Usado |
- Existem outros padrões como T568B e USOC (Universal Service Order Code), mas devem ser evitados em redes de dados
# Cross-over

- Para que haja conexão entre dois dispositivos é preciso que os sinais de saída de TD se conecte com as entradas das demais máquinas RD e vice-versa
- Isso recebe nome de **cross-over**
- Sem o cross-over isso não seria possível, porque os micros enviariam os dados para as saídas dos demais micros
- Essa tarefa é feita dentro do hub
- Ligar dois dispositivos que não façam cross-over internamente precisa fazer um cabo cross-over
	- Faz o cruzamento externo
- Para ligar dois hubs por portas convencionais é preciso usar o cabo cross-over, pois o cabo padrão iria cancelar o cruzamento
- A pinagem desse do cabo cross-over para redes 10BaseT e 100BaseT é mostrada na tabela a seguir:

| Pino        |        Cor         | Pino        |
| :---------- | :----------------: | ----------- |
| 1 +TD       |  Banco com Verde   | 1 +TD       |
| 2 -TD       |       Verde        | 2 -TD       |
| 3 +RD       | Branco com Laranja | 3 +RD       |
| 4 Não Usado |        Azul        | 4 Não Usado |
| 5 Não Usado |  Branco com Azul   | 5 Não Usado |
| 6 -RD       |      Laranja       | 6 -RD       |
| 7 Não Usado | Branco com Marrom  | 7 Não Usado |
| 8 Não usado |       Marrom       | 8 Não Usado |
# Par Trançado com Blindagem (STP)

- Par trançado com blindagem - STP - Shielded Twisted Pair
- A blindagem tem de ser aterrada nos dois pontos de conexão do cabo, ao contrario a blindagem ira funcionar como uma antena
- 2 Tipos
	- O mais simples possui apenas uma malha, que protege os pares trançados
		- Impedância de 100 ohms
		- É apenas um cabo UTP com uma malha adicionada
	- O outro apresenta uma malha individual para cada par trançado, além de uma malha externa protegendo todo o conjunto
		- Impedância de 150 ohms
		- Tipicamente usado pelo sistema de cabos das rede Token Ring
		- Esse cabo não é usado e redes Ethernet

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]], [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo TPC-IP/Camadas/Física/Física|Física]], [[Transmissão de Dados]]