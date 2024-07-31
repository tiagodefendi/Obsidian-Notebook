# Relação com Modelo OSI

- Tem é a representação direta da camada de [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Enlace|Enlace]] do Modelo OSI
# Protocolos

- LLC - Logical Link Control - IEEE 802.2
- MAC - Media Access Control - IEEE 802.3
# Funções

- Envia um datagrama pela Inter-rede em formato de frame
- Endereçar fisicamente os frames
- Gerenciar o meio físico de transmissão e torna-lo livre de erros
## Importância

- Trata de algoritmos para permitir uma comunicação eficiente
- Parece que a camada de enlace não é importante e cuida de problemas triviais
	- **Circuitos de comunicação produzem erros ocasionais**
	- Taxa de dados finita
	- Retardo de propagação diferente de zero entre o momento em que o bit é enviado e o momento em que ele é recebido
- **Protocolos usados para comunicações devem levar todos esses fatores**
- Fornece uma interface de serviço bem definida à camada de rede
	- Lidar com erros de transmissão
	- Fornecer controle de acesso ao meio
	- Regular o fluxo de dados, de tal forma que receptores lentos não sejam atropelados por transmissores rápidos
- Recebe os pacotes da camada de rede e os encapsula em quadros para transmissão
	- Cada quadro contém um cabeçalho (header) de quadro, um campo de carga útil, que conterá o pacote, e um final (trailer) de quadro
## Serviços

- Pode ser projetada de modo a oferecer diversos serviços
	- Serviço sem conexão e sem confirmação
		- Maior parte das LANs utiliza serviços sem conexão e sem confirmação na camada de enlace, ficando a cargo de camadas superiores
	- Serviço sem conexão e com confirmação
		- Útil em canais não confiáveis, como os sistemas sem fio
	- Serviço orientado a conexões com confirmação
		- Tem uso em algumas WANs
- Para oferecer serviços à camada de rede, a camada de enlace deve usar o serviço fornecidos a ela pela camada física
	- A camada física aceita um fluxo de bits brutos e entrega ao destino, sem garantia de estar livre de erros
	- Camada de enlace detecta e corrige os erros
- Geralmente processos da camada **física e de enlace estão rodando em um processador dentro de um chip especial de E/S de rede**
- Já o código da camada de **rede está na CPU principal**, porém outras implementações são possíveis
# Protocolos

## High-Level Data Link Control

- Todos são orientados a bits
	- Conjunto de Flags que indica o inicio e final do quadro
	- **Endereço** para identificar um dos vários terminais
		- Peer-to-peer: Utilizado para fazer distinção entre comandos e respostas
	- **Controle** é usado para números de sequência, confirmações e outras finalidades
	- **Dados** pode conter qualquer informação
	- **Soma de verificação** é uma variação do código de redundância cíclica	
	
| 01111110 | Endereço | Controle | Dados | Verificação | 01111110 |
| -------- | -------- | -------- | ----- | ----------- | -------- |


- Todos utilizam a técnica de inserção de bits para transferência de dados
- Diferem apenas em pequenos e irritantes detalhes
- **HDLC - High-Level Data Link Control**
	- ISO
	- Protocolo clássico orientado a bits
	- Variantes usadas décadas
	- Antigo
	- Longe de ser perfeito
- SDLC - Synchronous Data Link Control
	- IBM
	- Baseou HDLC e derivados
- ADCCP - Advanced Data Communication Control Procedure
	- Modificação do SDLC do ANSI
	- E depois virou o HDLC
- LAP - Link Access Procedure
	- Outra variação
	- Parte do padrão de interface de rede X.25
## Peer-to-peer

- Grande parte da infraestrutura geograficamente distribuída é construída a partir de linhas privadas P2P
- Duas situações:
	- Milhares de organizações têm uma LAN ou mais, cada uma com um determinado número de hosts e um roteador
		- Roteadores são interconectados por uma LAN de backbone
		- Todas as conexões com o mundo exterior passam por um ou dois roteadores que têm linhas privadas (dedicadas) **P2P com roteadores distantes**
		- Nesses roteadores e suas linhas privadas que compõem as sub-redes que a Internet se baseia
	- **Milhões de indivíduos que estabelecem conexões domésticas com a Internet utilizando modems** e linhas telefônicas com acesso por discagem
-  Necessário um protocolo de enlace de dados ponto-a-ponto na linha para cuidar do  enquadramento, do controle de erros e de outras funções da camada de enlace
## Point-to-Point Protocol - PPP

- Precisa de um protocolo ponto-a-ponto para diversos fins, inclusive para cuidar do tráfego de roteador para roteador e de usuário doméstico para ISP (provedor de serviços da Internet)
- Trata da detecção de erros
- Aceita vários protocolos
- Permite que endereços IP sejam negociados em tempo de conexão
- Permite a autenticação
- Dispões de 3 recuroso
	- Método de enquadramento que delineia de forma não ambígua o fim de um quadro e o início do quadro seguinte
		-  Formato do quadro também lida com a detecção de erros
	- Protocolo de controle de enlace usado para ativar linhas, testá-las, negociar opções e desativá-las novamente quando não forem mais necessárias
		- LCP - Link Control Protocol
		- Admite circuitos síncronos e assíncronos e codificações orientados a bytes e a bits
	- Maneira de negociar as opções da camada de rede de modo independente do protocolo da camada de rede a ser utilizada
		- NCP (Network Control Protocol) diferente para cada camada de rede aceita
- Quadro PPP foi definido de modo a ter uma aparência semelhante ao formato de quadro HDLC
- PPP é orientado a caracteres, e não a bits
- Não oferece uma transmissão confiável
- Uso de números de sequência e confirmações como padrão
	- Em redes sem fio podemos utilizar o PPP modificado para este tipo de recurso

| Flags <br> 01111110 | Endereço | Controle | Protocolo | Carga Útil | Verificação | Flags <br> 01111110 |
| :-----------------: | -------- | -------- | --------- | ---------- | ----------- | ------------------- |
- **Endereço** que sempre é definido como o valor binário 111111111
	- Indicando que todas as estações devem aceitar o quadro
	- evita o problema da necessidade de atribuição de endereços de enlace de dados
- **Controle** tem o valor 00000011
	- Indica um quadro não numerado, ou seja, o PPP não oferece transmissão confiável e confirmações como padrão
	- Ambientes ruidosos como em redes sem fio, pode ser utilizada a transmissão confiável que emprega o modo numerado
- Protocolo informa o tipo de pacote que se encontra no campo Carga útil
	- Ele indica, por exemplo, se a carga útil leva dados do protocolo IP, IPX, etc
- Carga útil tem comprimento variável, podendo se estender até o tamanho máximo negociado
	- Comprimento padrão de 1.500 bytes
- Total de verificação, que normalmente tem 2 bytes, embora seja possível negociar um total de verificação de 4 bytes
# Redes com Canais de Difusão

- Uma rede pode ser dividida em duas categorias
	- Ponto-a-ponto
	- Canais de difusão
- Maioria das redes de computadores, principalmente locais, utilizam canais de difusão
	- Determinar quem tem o direito de usar o canal quando há disputa
	- Canais de multi-acesso / Canais de acesso aleatório
- Protocolos usados para determinar quem será o próximo a usar a rede em um canal de multi-acesso pertencem a uma subcamada da de enlace
- Sub-camada **MAC - Medium Access Control**
- Problema é definir como alocar um único canal de difusão entre usuários concorrentes
- Padrões mais importantes do IEEE na camada de enlace:
	- 802.3 mais conhecido como Ethernet
	- 802.11 (LAN sem fio)
	- Estão engatinhando dois outros padrões 
		- 802.15 (Bluetooth) 
		- 802.16 (MAN sem fio)
- **802.3 e o 802.11 têm camadas físicas diferentes e subcamadas MAC diferentes**
- **Convergem para a mesma subcamada de controle de enlace lógico (Logical Link Control) IEEE 802.2**
# ALOHANET

- Havaí, no início da década de 1970 #1970s 
- Impossível estender cabos no mar para interligar as linhas para a comunicação em rede
- Ondas de rádio curtas como solução encontrada
- Cada terminal do usuário estava equipado com um pequeno rádio que tinha duas frequências
	- Ascendente (até o computador central)
	- Descendente (a partir do computador central)
- Transmitia um pacote contendo os dados no canal ascendente
- Se houvesse disputa pelo canal ascendente, o terminal perceberia a falta de confirmação e tentaria de novo
- Só havia um transmissor no canal descendente, nunca ocorria colisões nesse canal
- Funcionava bastante bem sob condições de baixo tráfego, mas fica fortemente congestionado quando o tráfego ascendente era pesado
# Ethernet

- Bob Metcalfe e David Boggs, projetaram e implementarão a primeira rede local, baseada na rede havaiana
- Foi chamado Ethernet, *uma menção ao éter luminoso, através do qual os antigos diziam que a radiação eletromagnética se propagava, mas a radiação se propaga no vácuo*
- Meio de transmissão era um cabo coaxial grosso com até 2,5 Km de comprimento, com repetidores a cada 500 metros.
- Até 256 máquinas podiam ser conectadas ao sistema por meio de transceptores presos ao cabo.
- O sistema funcionava a 2,94 Mbps
- Ethernet tinha um aperfeiçoamento importante em relação à ALOHANET
	- Antes de transmitir, **primeiro um computador inspecionava o cabo para ver se alguém mais já estava transmitindo**
	-  Computador ficava impedido até a transmissão atual terminar ( CSMA/CD - Carrier Sense Multiple Acess with Collision Detection)
- Eficiência muito maior
- O que acontece se dois ou mais computadores esperarem até a transmissão atual se completar e depois todos começarem a transmitir ao mesmo tempo?
	- Cada computador se mantem na escuta durante sua própria transmissão
	- **Se detectar interferência, bloquear o éter para alertar todos os transmissores**
	- **Recuar e esperar um tempo aleatório antes de tentar novamente**
	- Se ocorrer uma segunda colisão, o tempo aleatório de espera será duplicado e assim por diante, até separar as transmissões concorrentes
- Desde o seu surgimento a Ethernet não parou mais de se desenvolver e ainda está em desenvolvimento
	- 100 Mbps
	- 1000 Mbps
	- 10000 Mbps
- Porém a Ethernet (IEEE 802.3) não é o único padrão de LAN
	- O comitê IEEE também padronizou um Barramento de símbolos (802.4, token bus)
	- Anel de símbolo (802.6, token ring)
	- O símbolo seria a passagem de um pequeno pacote chamado símbolo ou tokem (ficha) de um computador para outro
	- Um computador só podia transmitir se tivesse a posse do símbolo, e isso evita colisões. Porém, esses padrões basicamente desapareceram
- Codificação manchester para identificar início e fim de cada bit
	- Cada período de bits tem dois intervervalos iguais
	- Um bit 1 binário é enviado quando a voltagem é definida como alta durante o primeiro intervalo, e como baixa no segundo intervalo
	- Um bit 0 binário é exatamente o oposto: primeiro baixo, e depois alto
	- Garante que cada período de bit terá uma transição na parte intermediária tornando fácil para o **receptor sincronizar-se com o transmissor**
	- Desvantagem da codificação Manchester é que ela exige duas vezes mais largura de banda que a codificação binário direta, pois os pulsos são a metade da largura
- A estrutura original de quadros Ethernet DIX (DEC, Intel, Xerox) começa com um **Preâmbulo** de 8 bytes
	- Cada um contendo o padrão de bits 10101010
	- Produz uma onda quadrada, a fim de permitir a sincronização entre o clock do receptor e o clock do transmissor
- Contém dois endereços, um para o destino e um para a origem
	- Endereços de 2 e de 6 bytes
		- Padrão de banda básica de 10 Mbps usam somente os endereços de 6 bytes
	- O bit de alta ordem do endereço de destino é 0 para endereços comuns e 1 para endereços de grupos
	- Os endereços de grupos permitem que diversas estações escutem um único endereço
	- Quando um quadro é enviado para um endereço de grupo, todas as estações do grupo o recebem
	- A transmissão para um grupo de estações é chamada de multidifusão (multicast)
	- O endereço que consiste em todos os bits 1 é reservado para difusão (broadcast)
- Tipo informa ao receptor o que fazer com o quadro
	- Vários protocolos da camada de rede podem estar em uso ao mesmo tempo na mesma máquina
	- Núcleo de processamento Ethernet tem de saber a qual protocolo da camada de rede deve entregar a carga útil do quadro
	- Especifica que processo deve receber o quadro
	- Dados, com até 1500 bytes 
	- Ethernet exige que os quadros válidos tenham pelo menos 64 bytes de extensão, do endereço de destino até o campo de total de verificação, incluindo ambos
	- Se dados de um quadro for menor que 46 bytes, o campo Preenchimento será usado para preencher o quadro até o tamanho mínimo
	- Total de verificação é efetivamente um código de hash de 32 bits dos dados
		- Se alguns bits de dados forem recebidos com erros (devido ao ruído no cabo), o total de verificação quase certamente estará errado, e o erro será detectado
		- O algoritmo do total de verificação é um CRC (Cyclic Redundancy Check)
			- O algoritmo do total de verificação é um CRC (Cyclic Redundancy Check)

| Preâmbulo | Endereço Destino | Endereço Origem | Tipo | Dados | Total de Verificações |
| --------- | ---------------- | --------------- | ---- | ----- | --------------------- |
## Evolução da Ethernet

- IEEE reuniu o comitê do 802.3 em 1992, para produzir uma LAN mais rápida #1990s 
- Manter o 802.3 exatamente como estava, e apenas torná-lo mais rápido
- Três principais razões pelas quais o comitê do 802.3 decidiu continuar com uma rede Ethernet aperfeiçoada
	1. A necessidade de manter a compatibilidade retroativa com as LANs Ethernet existentes
	2. O medo de que um novo protocolo criasse problemas imprevistos
	3. O desejo de terminar o trabalho antes que a tecnologia mudasse
- O 802.3u, foi oficialmente aprovado pelo IEEE em junho de 1995 #1990s 
	- Adendo ao padrão 802.3 existente (para enfatizar sua compatibilidade retroativa)
	- Fast Ethernet - 802.3u
	- Manter os antigos formatos de quadros, interfaces e regras de procedimentos
- Apenas reduzir o tempo de bit de 100ns para 10ns
- Tecnicamente, teria sido possível fazer isto apenas reduzindo o tamanho dos cabos 10Base2 e 10Base5, mas isto não seria muito interessante
- Tipos de fios que seriam aceitos, e os cabos coaxiais não eram a escolha
- Um dos concorrentes era o par trançado da categoria 3
	- Desvantagem é sua incapacidade para transportar sinais de 200 megabauds (100 Mbps com codificação Manchester) por 100 metros
	- Distância máxima entre o computador e o hub especificada para 10Base-T.
- Por outro lado, a fiação de par trançado da categoria 5 é capaz de tratar 100 metros com facilidade, e a fibra pode ir muito mais longe que isso. 
- Decidiu-se permitir as três possibilidades

| Nome      | Cabo              | Tam. Máx de Seguimento | Vantagens         |
| --------- | ----------------- | ---------------------- | ----------------- |
| 100BaseT4 | Cabo par trançado | 100 m                  | Utiliza UTP cat-3 |
| 100BaseTX | Cabo par trançado | 100 m                  | Full-duplex cat-5 |
| 100BaseFx | Fibra ótica       | 2000 m                 | Full-duplex       |

- Para a fiação da categoria 5, o projeto 100Base-TX é mais simples, porque os fios são capazes de manipular velocidades do clock de até 125 MHz
- Dois pares trançados por estação, um que vai para o hub e outro que sai do hub
- 100Base-TX é um sistema full-duplex; as estações podem transmitir a 100 Mbps e receber a 100 Mbps, ao mesmo tempo
- 100Base-TX e o 100Base-T4 são referidos em conjunto como 100Base-T
- O comitê 802 começou a trabalhar em uma Ethernet ainda mais rápida (1995) #1990s 
- Ethernet de gigabit e foi ratificado pelo IEEE em 1998, com o nome 802.3z #1990s 
	- Tornar a Ethernet 10 vezes mais rápida, mantendo a compatibilidade retroativa com todos os padrões Ethernet existentes
- 10 Gb Ethernet, definido pela recomendação IEEE 802.3an, neste padrão só é suportado o modo full-duplex
## Padrões
- Ethernet ou IEEE 802.3 com velocidades de 10Mbps
- Fast Ethernet ou IEEE 802.3u com velocidades de 100Mbps
- Gigabit Ethernet ou IEEE 802.3z com velocidades de 1.000Mbps
- 10 Gigabit Ethernet ou IEEE 802.3an com velocidades de 10.000Mbps
# Camada de Enlace sem fio

- A demanda cada vez maior, por portabilidade, mobilidade, conveniência
- Atrativos oferecidos atualmente pelos sistemas de comunicação sem fio
- Conectar seu Notebook à Internet sem nenhum fio faz com que cada dia mais e mais pessoas invistam em dispositivos sem fio
- Wireless Local Area Networking ou simplesmente WLAN é uma tecnologia desenvolvida ao longo da década de 90 pelo IEEE #1990s 
	- Está em fase de amadurecimento, principalmente em questões relacionadas com qualidade de serviço e segurança
- A comercialização de WLANs por várias empresas não demorou, e o IEEE teve de padronizar este tipo de rede para que estas fossem compatíveis
- Ao padrão de LANs sem fio deu-se o nome de 802.11, e um apelido comum para este é WiFi (Wireless Fidelity)
	- Tal padrão proposto tinha de funcionar em dois modos
	- Na presença de uma estação base, neste toda a comunicação deveria passar por um ponto de acesso comum aos hosts da rede
	- Na ausência de uma estação base, este modo é chamado de interligação de redes **ad hoc** e não requer um ponto de acesso como o primeiro caso, no modo ad hoc os hosts podem comunicar entre si diretamente
- IEEE teve de abordar alguns pontos críticos
	- Descobrir uma banda de frequência adequada que estivesse disponível, de preferência em todo o mundo
	- Sinais de rádio têm um alcance finito
	- Assegurar que a privacidade dos usuários seja mantida
	- Compreender as implicações de mobilidade dos computadores
	- Largura de banda suficiente para ser economicamente viável
- Padronização das redes sem fio a Ethernet já havia dominado o mercado de redes locais
- Tornar o 802.11 compatível com a Ethernet tornando possível enviar um pacote IP pela WLAN
- Dificuldades
	- A chance de colisão em uma rede sem fio é muito maior do que em uma rede com fio, isto se dá devido ao meio de transmissão, o ar
	- Objetos sólidos refletirem o sinal de rádio, de forma que o sinal pudesse ser recebido várias vezes (atenuação multiponto)
	- Softwares dos usuários em sua grande maioria não estão ciente da mobilidade do host
- Em 1997 a WLAN 802.11 começou a funcionar a 1Mbps ou 2 Mbps #1990s 
- Pessoas reclamaram que isto era muito lento, já que o padrão da época para redes com fio era no mínimo 10 Mbps
## Dois novos padrôes
-  802.11a
	- Utiliza uma faixa de frequências mais larga e funcionava em velocidades de 54 Mbps na banda de 5 Ghz
	- Utilizando a técnica OFDM (Orthogonal Frequency Division Multiplexing)
	- Chamado de 802.11a
- 802.11b
	- Mesma faixa de frequências que o 802.11
	- Técnica de modulação HR-DSSS (High Rate Direct Sequence Spread Spectrum) para alcançar 11 Mbps na banda 2,4 GHz
	- Emprega bandas de freqüência ISM (Instrumentation, Scientific & Medical)
	- Compreendem três segmentos do espectro reservado para uso sem a necessidade de licença
	- Frequências disponíveis:
		- 902 a 928 Mhz
		- 2400 a 2483,5 Mhz
		- 5.725 a 5.850 MHz
- 802.11g
	- Com o passar do tempo o comitê 802 apresentou ainda outra variante
	- Técnica de modulação do 802.11a (OFDM)
	- Emprega a faixa de frequência do 802.11b (2.4Ghz)
	- Atualmente este tem se tornado o padrão mais procurado
## Diferenças nas Subcamadas

- A camada física corresponde muito bem à camada física do modelo OSI em todos os padrões
- Já camada de enlace de dados em todos os protocolos 802 se divide em duas ou mais subcamadas
- No 802.11 a subcamada MAC (Medium Access Control)
	- Determina como o canal é alocado
	- Quem terá oportunidade de transmitir em seguida
- Subcamada LLC (Logical Link Control)
	- Ocultar as diferenças entre as diversas variações do 802 e torná-las indistinguíveis no que se refere à camada de rede
- Protocolo da subcamada MAC do 802.11 é bastante diferente do protocolo Ethernet
	- Devido à complexidade inerente do ambiente sem fio, em comparação com o de um sistema fisicamente conectado
	- Com a Ethernet, uma estação só precisa esperar até o éter ficar inativo e começar a transmitir
	- Se não receber de volta uma rajada de ruído dentro dos primeiros 64 bytes, é quase certo que o quadro tenha sido entregue corretamente
	- No caso das LANs sem fios, essa situação não ocorre, por que nem todas as estações estão dentro do alcance de rádio umas das outras
	- As transmissões realizadas em uma parte de uma célula podem não ser recebidas em outros lugares na mesma célula
	- 802.11 não utiliza o CSMA/CD, como faz o padrão Ethernet
- 802.11 admite dois modos de operação
	- DFC - Distributed Coordination Function
		- Não usa nenhuma espécie de controle central (seria um esquema parecido com o Ethernet)
		- DCF utiliza um protocolo chamado CSMA/CA - CSMA with Collision Avoidance
		- Utiliza tanto detecção do canal físico quanto a do canal virtual
		- CSMA/CA admite dois métodos de operação
			- Quando uma estação quer transmitir, ela escuta o canal, se estiver ocioso, a estação simplesmente começará a transmitir
				- Não escuta o canal enquanto está transmitindo, mas emite seu quadro inteiro
				- Pode muito bem ser destruído no receptor devido à interferência
				- Se o canal estiver ocupado, a transmissão será adiada até o canal ficar inativo
				- Se ocorrer uma colisão, as estações que colidirem terão de esperar um tempo aleatório, e então tentarão novamente mais tarde
				- Caso tudo corra bem durante a transmissão a estação receptora envia uma confirmação da entrega do pacote
			- Se baseada no MACAW e emprega a detecção de canal virtual
				- *"Um host A quer transmitir para um host B. E C é um host dentro do alcance de A. E o Host D é uma estação dentro do alcance de B, mas não dentro do alcance de A. O protocolo começa quando o host A decide transmitir dados para o host B. Ele inicia a transmissão enviando um quadro RTS para o host B, a fim de solicitar permissão para enviar um quadro. Quando recebe essa solicitação, o host B pode decidir conceder a permissão e, nesse caso, envia de volta um quadro CTS. Após a recepção do CTS, o host A envia seu quadro e inicia um timer ACK. Ao receber corretamente o quadro de dados, o host B responde com um quadro ACK, concluindo a troca de quadros. Se o timer ACK de host A expirar antes do quadro ACK voltar a ele, o protocolo inteiro será executado novamente. No pondo de vista dos hosts C e D. O host C está dentro do alcance de A, e então pode receber o quadro RTS. Se o fizer, host C perceberá que alguém vai transmitir dados em breve e assim, para o bem de todos, desiste de transmitir qualquer coisa até a troca ser concluída (isto é feito a partir de informações do RTS). Após este tempo ele reivindica uma espécie de canal virtual, indicado por NAV (Network Allocation Vector – vetor de alocação de rede). O host D não escuta o RTS, mas escuta o CTS, e assim também reivindica o sinal NAV para ele próprio. Observe que os sinais NAV não são transmitidos; eles são apenas lembretes internos de que a estação deve se manter inativa por um determinado período de tempo."*
				- Se um quadro for longo demais, ele terá bem pouca chance de chegar sem danos e é provável que tenha de ser retransmitido. 
				- O 802.11 permite que os quadros sejam fragmentados em partes menores, cada uma com seu próprio total de verificação.
				- Depois que um canal é adquirido com o uso de RTS e CTS, vários fragmentos podem ser enviados em sequência e é chamada rajada de fragmentos. 
					- A fragmentação aumenta o throughput, restringindo as retransmissões aos fragmentos defeituosos, em vez de retransmitir o quadro inteiro. 
					- O tamanho do fragmento não é fixado pelo padrão, mas é um parâmetro de cada célula e pode ser ajustado pela estação base.
	- PCF - Point Coordination Function
		- Utiliza a estação base para controlar toda a atividade em sua célula
		- Estação base efetua o polling das outras estações, perguntando se elas têm algum quadro a enviar
		- A ordem de transmissão é totalmente controlada pela estação base em modo PCF, não ocorre nenhuma colisão
		- O padrão prescreve o mecanismo de polling, mas não a frequência de polling, a ordem de polling, ou mesmo se todas as estações precisam receber um atendimento idêntico
- O mecanismo básico consiste na difusão periódica pela estação base de um quadro de baliza
	- O quadro de baliza contém parâmetros do sistema, como sequências de saltos (hops) e tempos de parada, sincronização de clock, etc
	- Convida novas estações a se inscreverem no serviço de polling
	- Depois que uma estação se inscreve para receber o serviço de polling a uma certa taxa, ela tem a garantia efetiva de uma certa fração da largura de banda, tornando possível assim oferecer garantias de qualidade de serviço
- Todas as implementações devem aceitar DCF, mas PCF é opcional
- Redes sem fio também tem mecanismos para conservar recursos de baterias em dispositivos móveis sem fio, já que tem limitações quanto a bateria
- 3 diferentes classe de quadros em trânsito
	- Dados
		- Duração, endereço de origem de destino, endereço de origem e destino dos AP das células, sequências
	- Controle
		- Versão do protocolo, tipo, subtipo, MF
	- Gerenciamento
		- Origem destino apenas dos hosts sem fio, RTS, CTS, ACK
- Cada um deles tem um cabeçalho com uma variedade de campos usados na subcamada MAC
- Cada LAN sem fio compatível deve fornecer 9 serviços
	- Estão divididos em 2 categorias
		- 5 serviços de distribuição
			- Relacionam-se ao gerenciamento da associação a célula e à interação com estações situadas fora da célula
			- Fornecidos pelas estações base
			- Lidam com a mobilidade das estações à medida que elas entram e saem das células, conectando-se e desconectando-se das estações base
			- Tipos:
				- Associação
					- Usado pelas estações móveis para conectá-las às estações base
					- Usado imediatamente após uma estação se deslocar dentro do alcance de rádio da estação base
					- Ao chegar, ela anuncia sua identidade e seus recursos.
					- Os recursos incluem as taxas de dados admitidas, a necessidade de serviço PCF (polling) e requisitos de gerenciamento da energia
				- Desassociação
					- Usado antes da estação desligar ou sair, a estação base também pode usá-lo
				- Reassociação
					- Uma estação pode mudar sua estação base usando este serviço
					- Útil para estações móveis que se deslocam de uma célula para outra
				- Distribuição
					- Esse serviço determina como rotear quadros enviados à estação base
					- Se o destino for local para a estação base, os quadros poderão ser enviados diretamente pelo ar
					- Caso contrário, eles terão de ser encaminhados pela rede fisicamente conectada
				- Integração
					- Cuidará de conversão do formato 802.11 para o formato exigido pela rede de destino.
		- 4 serviços da estação
			- Relacionam-se à atividade dentro de uma única célula
			- Serviços intra-células, ou seja, dentro de uma única célula
			- Usados depois que ocorre a associação
			- Tipos
				- Autenticação
					- Comunicação sem fio pode ser enviada ou recebida facilmente por estações não autorizadas
					- Deve se autenticar antes de ter permissão para transmitir dados
					- Após associada pela estação base (aceita em sua célula), ela envia um quadro de desafio especial para ver se a estação móvel conhece a chave secreta (senha) que foi atribuída
					- Se o resultado for correto, a estação móvel será completamente aceita na célula
				- Desautenticação
					- Quando uma estação autenticada anteriormente quer deixar a rede, ela é desautenticada
				- Privacidade
					- Administra a criptografia e a descriptografia
				- Entrega de dados
					- Oferece naturalmente um meio para transmitir e receber dados
					- Não tem garantia de serviço e as camadas mais altas devem ligar com a detecção e a correção de erros
## Redes WPANs

- Transmitem a taxas de dados mais baixas e cobrem distâncias menores
- Bluetooth, por exemplo, permite taxas de transmissão de até 1Mbps e atinge uma distância nominal de até 10 metros
- Substituir os cabos de conexão entre equipamentos pessoais portáteis (telefones, pagers, laptops) e também permitir acesso à Internet
- Ficando mais populares e um número crescente de edifícios de escritórios, aeroportos e outros lugares públicos estão sendo equipados com redes sem fio
### Bluetooth

- Bluetooth fornece conexão sem fio a curta distâncias
- desenvolvida inicialmente pela Ericsson (1994) #1990s 
- Substituir os cabos que conectavam estes dispositivos ganhou o suporte da Intel, IBM dentre outras empresas de renome
- Opera na faixa de frequência de 2,4 a 2,482 GHz
- Adotou o espalhamento espectral por salto de frequência de modo a garantir comunicação robusta em uma faixa de frequência compartilhada com outras aplicações como o WiFi
- Vantagens em relação a conexão via infravermelho
	- Suporta vários dispositivos e não exige visada direta entre transmissor e receptor
- Apesar de ser padronizada pelo IEEE 802.15 esta assemelha-se mais a um barramento como um USB, mas é wireless
- Um piconet, que consiste em um nó mestre e até sete nós escravos ativos, situados dentro de uma distância de 10 metros
- Se existir muitas piconets na mesma sala elas podem até mesmo ser conectadas por um nó de ponto, sendo então denominadas de scatternet
- Seu sucesso depende agora de sua adoção em larga escala
- Gerando volumes que tornem insignificantes o custo de sua acréscimo a dispositivos portáteis
- Caso isto não ocorra ele poderá ser eclipsado por soluções que oferecem taxas de dados mais altas e mais opções de conectividade como o WiFi
### WIMAX

- Padrão o 802.16
- Permite velocidades de aproximadamente 54 Mbps, podendo chegar a 75 Mbps
- Distância de 6 Km a 9 Km
- Fornecem desempenho equivalentes aos dos tradicionais meios com fio como DSL, cable modem ou E1/T1 porém com tecnologia sem fio
- Promete revolucionar a indústria de acesso de banda larga
# Switching

- A comutação (switching) é baseada no endereço de hardware
- O endereço MAC da placa de rede do dispositivo é utilizado para filtragem de rede
- Switches utilizam chips especiais, chamados “ASICS” (Application Specific Integrated Circuits), para formar e manter as tabelas de filtragem (filter tables)
- Switches são rápidos porque não analisam informações pertinentes à camada de Rede
- Analisando os endereços de hardware dos quadros (frames) antes de decidir pelo encaminhamento ou abandono desse quadro
- O que torna a comutação na camada de Enlace tão eficiente é a nãomodificação de dados, apenas no frame que o encapsula
	- Nenhuma modificação no pacote é realizada
	- processo de comutação é muito mais rápido e menos suscetível a erros do que o processo de roteamento existente na camada de Redes
- Pode ser utilizada para conectividade entre grupos de trabalho e para a segmentação da rede, ou quebra dos domínios de colisão
- Aumenta a largura de banda disponível para cada usuário
- Cada conexão (interface) disponibilizada pelo switch representa seu próprio domínio de colisão
- Devido a esse fator pode-se conectar múltiplos dispositivos em cada interface
- Possui algumas limitações
	- Modo correto de se criar redes comutadas eficientes é certificando-se que os usuários permanecerão ao menos 80% de seu tempo no segmento local
	- Quebram domínios de colisão, entretanto, a rede ainda é um grande domínio de broadcast, o que pode limitar o tamanho da rede, assim como causar problemas de performance
	- Assim, pacotes em broadcast e multicast pode vir a ser problemas sérios à medida que a rede cresce
- Switches da camada de Enlace não podem substituir completamente os roteadores da camada de Redes em uma internetwork
# Processo de aprendizagem de endereços físicos pelos switches

- Todo switch forma uma tabela, chamada de tabela MAC
	- Mapeia os endereços de hardware (MAC Address) dos dispositivos às portas (interfaces) às quais eles se encontram conectados
- Assim, que um switch é ligado, essa tabela encontra-se vazia
- Quando um dispositivo inicia uma transmissão em uma porta do switch recebe um quadro
- o switch armazena o endereço de hardware do dispositivo transmissor em sua tabela MAC, registrando a interface à qual esse dispositivos está conectado
- Em um primeiro momento, o switch não tem outra opção a não ser “inundar” a rede com esse quadro
- Uma vez que ele ainda não possui em usa tabela MAC o registro da localização do dispositivo destinatário
- Esse tipo de transmissão é conhecida como broadcast
- Se um determinado dispositivo responder a essa mensagem de broadcast enviando um frame de volta, o switch irá, então, capturar o endereço de hardware (MAC) desse dispositivo e registrá-lo em sua tabela MAC
- Associando o endereço MAC desse dispositivo à interface (porta) que recebeu o quadro
- O switch tem agora dois endereços em sua tabela MAC, podendo assim estabelecer uma conexão ponto-a-ponto entre os dois dispositivos
	- Os quadros pertencentes a essa transmissão serão encaminhados apenas aos dois dispositivos participantes
- Nenhuma outra porta do switch irá receber os quadros, a não ser as duas portas mapeadas
- É essa a grande diferença entre switches e hubs
- Em uma rede composta por hubs, quadros são encaminhados a todas as portas, o tempo todo, criando um grande domínio de colisão
- Se os dois dispositivos não se comunicarem com o switch novamente por um determinado período de tempo, o switch irá deletar os endereços de usa tabela MAC, mantendo-a assim a mais atualizada possível
## Tipos de Comutação

- A latência envolvida na comutação de um quadro em um switch depende do modo de comutação (switching mode) configurado do switch
- 3 tipos de comutação
	- Store and forward
		- “Armazene e encaminhe"
		- O quadro é, em um primeiro momento, completamente recebido e armazenado no buffer do switch
		- Em seguida, uma checagem de erros (CRC – Cyclic Redundant Check) é efetuada
		- Finalmente, o endereço de destino é localizado na tabela MAC
		- Método mais lento
	- Cut-through - tempo real
		- Esse é o modo predominante quando se fala em comutação em LAN
		- Copia apenas o endereço de destino (os primeiros 7 bytes seguindo o campo Preamble) para seu buffer
		- O endereço do hardware de destino é localizado na tabela MAC, a interface de saída é determinada e o quadro é encaminhado ao seu destino
		- Provê baixa latência, pois o encaminhamento do quadro começa assim que o endereço de destino é identificado e a interface de saída determinada
	- FragmentFree - cut-through modificado
		- Mdificação do cut-through
		- Aguarda a passagem da janela de colisão (collision window de 64 bytes) antes de encaminhar o pacote
		- Se considera a alta probabilidade de que, se um quadro possui algum erro, este será identidicado nos 64 bytes iniciais
		- O modo FragmentFree promove uma checagem de erros mais confiável, acrescentando muito pouco à latência do processo
## Esquemas de inibição de loops em comutadores

- Estabelecer conexões (links) redundantes é sempre uma boa ideia entre switches
- Redundância, nesse caso, é usada para evitar a completa queda da rede no caso de falha de um link (cabo par trançado, por exemplo)
- Embora a redundância em links possa ser extremamente útil, tal redundância pode trazer mais problemas do que resolvê-los
- Quadros podem ser propagados através de todos os links redundantes simultaneamente, um fenômeno chamado loop pode ocorrer
- Caso nenhum esquema de inibição de loops de rede seja implantado, os switches poderão propagar quadros continuamente na rede. 
	- Esse fenômeno é chamado de broadcast storm (tempestade de broadcast)
- Aumento das chances de um dispositivo receber múltiplas cópias de mesmo quadro, uma vez que esse quadro pode chegar de diferentes segmentos simultaneamente
- A tabela MAC ficará “confusa” sobre a localização (interface) de um determinado dispositivo, uma vez que o switch pode receber determinado quadro de mais de um link. 
	- Pode ocorrer de o switch não encaminhar o quadro, uma vez que estará constantemente atualizando sua tabela MAC com a localização do hardware transmissor. 
	- Esse fenômeno é conhecido como trashing da tabela MAC
- Um dos maiores problemas é a geração de múltiplos loops, ou seja, um loop dentro de outro. 
	- Se uma tempestade de broadcast então ocorrer, o switch ficará sem condições de desempenhar a comutação de pacotes, literalmente “travando” a rede
## Protocolo STP

- Uma solução para o problema de loop é com o Protocolo Spanning Tree (STP)
- Criado pela DEC (Digital Equipment Corporation)
- Homologado posteriormente pela IEEE como 802.1d, não é compatível com a versão original do protocolo criado com o DEC
- Evitar que loops ocorram
- Monitora constantemente a rede identificando todos os links em atividade e certificando-se que loops de rede não ocorram, através da desativação de links redundantes
- “Elegendo” um switch-raiz (root bridge) responsável pela definição de toda a topologia da rede
- Apenas um switch-raiz pode existir
- Todas as interfaces ou portas do switch-raiz são denominadas “portas designadas”
	- Encontram-se sempre no modo de operação denominado “modo de encaminhamento” (forwarding-state)
	- Interfaces operando em modo de encaminhamento podem tanto enviar quanto receber dados
- Outros switches presentes na rede são denominados não-raiz (non-root bridges)
- A porta com “menor custo” (determinada pela largura de banda do link em questão) ao switch-raiz é chamada de “portaraiz” (root-port) 
	- Se encontrará em modo de encaminhamento, podendo enviar e receber dados
- As portas restantes com menor custo ao switch-raiz serão denominadas “portas designadas”.
- Se em uma rede com diversos switches o custo de duas ou mais portas for o mesmo, o ID (número de identificação) do switch deverá ser usado e será considerada designada a porta referente ao switch com o menor ID
- O valor de ID padrão para todos os dispositivos rodando o STP do IEEE é 32.768
- As portas restantes serão consideradas portas não-designadas
	- Encontrarão-se em modo bloqueio (blocking mode), não podendo enviar ou receber dados
- Switches e bridges rodando STP trocam informações através do protocolo Bridge Protocol Data Units (BPDU)
- O BPDUs enviam mensagens de configuração via quadros em broadcast
- O ID de cada switch é enviado aos outros dispositivos através das BPDUs
## Modos de operação das portas de um switch

- Os modos de operação de switches e bridges rodando em STP podem variar entre quatro modos
	- Bloking
		- Não encaminhará quadros. 
		- Pode receber e analisar BPDUs.
		- Todas as portas de um switch encontram-se em modo bloking quando ele é ligado
	- Listening
		- Recebe e analisa BPDUs para certificar-se de que não ocorrerão loops na rede antes de começar o encaminhamento de quadros
	- Learning
		- Registra os endereços dos hardwares conectados às interfaces e forma a tabela MAC. 
		- Não encaminha quadros, ainda
	- Forwarding
		- Envia e recebe quadros
- Switches se encontram ou no modo blocking ou forwarding
- Uma porta no modo forwarding é tida como tendo o menor custo ao switch raiz
- Se a topologia de rede se alterar (devido a uma falha) todas as portas conectadas em redundância de um switch retornarão aos modos listening e learning
- Blocking é usado para impedir o acontecimento de loops de rede
	- O switch determina o melhor caminho ao switch-raiz, todas os portas entrarão em modo blocking
	- Portas em modo blocking podem receber BPDUs
- Se um switch por alum motivo determinar que uma porta em modo blocking deve tornar-se uma posta designada, ela entrará em modo listening
	- Analisando todas as BPDUs recebidas para certificar-se de que não criará um loop uma vez que entre em modo forwarding
## VLAN

- Em uma rede comutada, ela é plana (flat)
	- Todos os pacotes broadcast transmitidos são "enxergados" por todos os dispositivos conectados as redes
	- Mesmo se um dispositivo não seja o destinatário de tais pacotes
- Comutação segrega domínios de colisão, criando segmentos individuais para cada dispositivo conectado ao switch
	- Restrições à distância impostas pelo padrão Ethernet são reduzidas
	- Redes geograficamente podem ser construídas
- Quanto maior o número de usuários e dispositivos, maior o volume de broadcast e pacotes que cada dispositivos tem de processar transitando na rede
- Problema inerente é a segurança
	- Todos usuários "enxergam" todos dispositivos
- Tamanho de broadcast ser reduzido, mas seu número aumenta
- Antes do uso de VLANs tínhamos apenas um grande domínio de broadcast
- Conforme VLANs vão sendo criadas, o número de domínios de broadcast aumenta, porém o tamanho de cada novo domínio é menor de que domínio original
- Possível resolver uma boa parte dos problemas associados à comutação na camada de enlace
- Razões para criar LANs Virtuais
	- Redução do tamanho e aumento do número de domínios de broadcast
	- Agrupamento lógicos de usuários e de recursos conectados em portas administrativamente definidas no switch
	- VLANs podem ser organizadas por localidade, função, departamento, etc
		- Independente da localização física dos recursos
	- Melhor gerenciabilidade e aumento de segurança da rede local (LAN)
	- Flexibilidade e escabilidade
## Redução do tamanho dos domínios de Broadcast

- Roteadores, matêm as mensagens de broadcast dentro da rede que os originou
- Switches, propagam mensagens de broadcas para todos os seus segmentos
	- Chamamos uma rede comutada de "plana", porque trata de um grande domínio de broadcast
- Um bom administrador de redes deve certificar-se de que a rede esteja devidamente segmentada
	- Evitar que problemas em um determinado segmento se propaguem para toda rede
	- Combinação entre comutação  roteamento
- Uma vez que o preço dos switches vem caindo é tendência real que as empresas substituam hubs por switches
- Em uma VLAN, todos dispositivos são membros do mesmo domínio de broadcast
	- Mensagens de broadcast são barradas de todas as portas em um switch que não seja membros da mesma VLAN
- Roteadores devem ser usados em conjunto com switches para que se estabeleça a comutação entre VLANs
	- Impede que mensagens de broadcast sejam propagadas por toda rede
## Gerenciabilidade e aumento de segurança em LANs através de switches

- Problemas com redes planas é a segurança que é implementada através dos roteadores
- Segurança é gerenciada e mantida pelo roteador, porém qualquer um que se conecte localmente à rede tem acesso aos recursos disponíveis naquela VLAN específica
- Outro problema é que qualquer um pode conectar um analisador em um hub
	- Assim, tendo acesso a todo tráfego daquele segmento de rede
- Mais um problema é que usuários podem se associar a um determinado grupo de trabalho simplesmente conectando suas estações ou laptops a um hub existente, ocasionando um "caos"
- Através da criação de VLANs, os administradores adquirem  controle sobre cada porta e cada usuário
	- Controla cada porta e quais recursos serão alocados a ela
	- Se a comunicação inter-VLANs é necessária, restrições em um roteador podem ser implementadas
	- Restrições também podem ser impostas a endereços MAC, protocolos e a aplicação
- Possibilitam uma flexibilidade e escabilidade mais que os roteadores
- Com Switches é possível agrupar usuários por grupos de interesse
	- VLANs organizacionais
- Switchers não podem substituir os roteadores
- Para comunicação inter-VLAN é necessário obrigatoriamente o uso de roteadores
## Tipos de VLAN

- São tipicamente criadas por um administrador de redes, que designa determinadas portas de um switch para uma determinada VLAN
- Associação estática
	- O modo mais comum e seguro de se criar uma VLAN é estaticamente
	- A porta do switch designada para manter a associação em uma determinada VLAN fará isso até que um administrador mude a sua designação
	- Fácil de implementar e monitorar
	- Funciona bem em ambientes com movimento  de usuário é controlado na rede
- Associação dinâmica
	- Determinam a designação de uma VLAN para um dispositivo automaticamente
	- Com uso de softwares específicos de gerenciamento é possível mapear endereços de hardware (MAC), protocolos e aplicações ou logins de usuário para uma VLAN específica
	- Simplifica o a vida do administrador uma vez que o banco de ados MAC x VLAN está formado
	- Esforço considerável é exigido inicialmente, na criação do mesmo
## Identificação de VLANs

- Podem ser espalhar por uma “malha” de switches interconectados
- Os switches desse emaranhado devem ser capazes de identificar os quadros e as respectivas VLANs às quais estes pertencem
- Frame tagging (etiquetamento de quadro)
	- Podem direcionar os quadros para as portas apropriadas
- Existem dois tipos de links (portas) em um ambiente comutado (portas em switch)
- Links de acesso – access links
	- Parte de uma VLAN e são tidos como a VLAN nativa
	- Qualquer dispositivo conectado a uma porta ou link de acesso não sabe a qual VLAN pertence
	- O dispositivo apenas assumirá que é parte de um domínio de broadcast, sem entender a real topologia da rede
	- Os switches removem qualquer informação referentes às VLANs dos quadros antes de enviálos a um link de acesso
	- Dispositivos conectados a links de acesso não podem se comunicar com dispositivos fora de sua própria VLAN
		- A não ser que um roteador faça o roteamento dos pacotes
- Links de transportes – trunk links
	- Também denominados uplinks
	- Podem carregar informações sobre múltiplas VLANs
	- Usados para conectar switches a outros switches, routeadores ou mesmo a servidores
	- São suportados em Fast ou Gigabit Ethernet, mas não pode ser suportado em redes 10BaseT Ethernet
	- Transportar VLANs entre dispositivos e podem ser configurados para transportar todas as VLANs ou somente algumas
	- Links de Transporte ainda possuem uma VLAN nativa (default – VLAN1), que é utilizada para gerenciamento em caso de falhas
- O processo de “entroncamento” de links permite colocar uma única porta como parte de múltiplas VLANs
	- Bastante comum na conexão quando se que conectar um servidor que prove serviço a várias VLANs sem usar um roteador
- Uso de entroncamentos na conexão entre switches (uplink)
	- Links de transporte podem transportar informações sobre algumas ou todas as VLANs existentes através de um único link (porta) física
- Ao se criar uma porta de transporte, informações sobre todas as VLANs são transportadas através dela, por padrão
- VLANs indesejadas devem ser manualmente excluídas do link para que suas informações não sejam propagadas através dele
### Frame tagging

- Um switch conectado a uma rede de grande porte necessita fazer um acompanhamento dos usuários e quadros que atravessam o aglomerado de switches e VLANs
- O processo de identificação de quadros associa, de forma única, uma identificação a cada quadro
- Essa identificação é conhecida como VLAN ID ou VLAN color
#### Métodos de Identificação de VLANs

- Existem alguns métodos de identificação de VLANs, dois métodos muito usados são: o ISL e o 802.1q
- ISL (Inter-Switch Link)
	- Switches Cisco, o encapsulamento ISL pode ser utilizado às interfaces de switches, de roteadores e de servidores, para seu entroncamento
	- O servidor truncado é membro de todas as VLANs simultaneamente
		- Os usuários não precisam atravessar um dispositivo de camada 3 para ter acesso a ele, reduzindo a complexidade e aumentando a performance da rede
	- O método ISL literalmente escapsula quadros Ethernet com informações sobre VLANs
	- Essa informação, adicionada ao encapsulamento do quadro, permite a multiplexação de VLANs por meio de apenas um link de transporte
	- Método externo de identificação, ou seja, o quadro original não é alterado, sendo apenas encapsulado por um cabeçalho ISL
	- Uma vez que o quadro é encapsulado, apenas dispositivos (ou interfaces) compatíveis com ISL estarão habilitados e decodificá-dos
	- Dispositivos não ISL que recebam um quadro ISL iram achar que o quadro está corrompido
	- **É importante entender que o encapsulamento ISL apenas ocorre se o quadro for encaminhado a uma porta de transporte (trunk link) e o encapsulamento é removido caso o quadro seja encaminhado a uma porta de acesso**
	- Para para gerenciar e manter a consistência de todas as VLANs configuradas em uma rede pode ser usado o protocolo VTP (Virtual Trunk Protocol)
		- Necessário também a criação de um servidor VTP
		- Todos os servidores que necessitem compartilhar informações sobre VLANs devem utilizar a mesma identificação de domínio
- 802.1q
	- Criado pela IEEE para ser um método padrão para identificação de quadros
	- Método padrão para identificação de quadros, esse método insere um campo específico dentro do quadro, responsável pela identificação da VLAN
	- O quadro Ethernet não possui campos sobressalentes
	- Então o que fazer para identificar as VLANs?
	- Lembrando que alterar o quadro implica em vários problemas com os placas de redes compatíveis com o padrão Ethernet
	- A IEEE enfrentou esse problema em 1995 e depois de muita discussão, o IEEE fez o impensável e mudou o cabeçalho do padrão Ethernet #1990s 
	- O novo formato foi publicado no padrão 802.1q, emitido em 1998 #1990s 
	- O novo formato contém uma tag de VLAN, é claro que com esta solução não temos que jogar as placas de redes Ethernet padrão fora
	- **A chave para a solução é perceber que os campos VLAN só são realmente usados pelas pontes e switches, e não pelas máquinas dos usuários**
	- Apenas as pontes e switches devem reconhecer o 802.1q
	- Como a origem não gera os campos VLAN, quem o fará?
		- A resposta é que o primeiro switch capaz de reconhecer a VLAN que tocar um quadro incluirá esses campos, e o último dispositivo do percurso os removerá
	- Porém, como saber à qual VLAN pertence cada quadro? 
		- Bem, o primeiro switch poderia atribuir um número de VLAN a uma porta, examinar o MAC, etc
	- Esperá-se que em um futuramente as novas placas tal como Gigabit Ethernet suportem o 802.1q
	- Ao quadro 802.1q foi adicionado o campo tag que possui um campo identificador de VLAN, que indica a que campo o quadro pertence
	- Um campo de 3 bits de Prioridade, que não tem nenhuma relação com a VLAN
		- mas como a alteração do formato do quadro não acontece sempre foram adicionados campos extras
		- Tal campo pode ser usado para informar a prioridade do quadro
		- Usado por exemplo para dizer que um quadro é de voz, ou outra informação em tempo real que deve ter um certo nível de prioridade de entrega
	- O último bit é o CFI (Canonical Format Indicator – indicador de formato canônico)
		- Originalmente criado para indicar endereços MAC littleendian versus endereços MAC big-endian
		- Esse uso se perdeu em outras controvérsias e também não tem relação com VLANs

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]]