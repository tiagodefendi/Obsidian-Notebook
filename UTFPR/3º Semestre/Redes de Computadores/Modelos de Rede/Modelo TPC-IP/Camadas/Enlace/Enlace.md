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
- 
- 

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]]