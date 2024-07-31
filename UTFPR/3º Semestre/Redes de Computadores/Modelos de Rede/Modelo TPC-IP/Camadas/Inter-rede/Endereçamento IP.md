# O que é?

- Um sistema de comunicação permite que qualquer host se comunique com qualquer host
- E para tornar o sistema de comunicação universal, ele precisa de um método aceito globalmente a fim de identificar cada computador que se conecta a ele
- Em redes TCP/IP isto é possível usando-se o endereçamento IP
- O protocolo TCP/IP é roteável
	- Ele foi criado pensando-se na interligação de diversas redes
	- Onde podemos ter diversos caminhos interligando um transmissor e o receptor
	- Isso possibilitou a criação da rede mundial de computadores (Internet)
- Endereçamento lógico / Endereçamento IP
- Cada rede e dispositivo conectado deve usar pelo menos um endereço IP
- O endereço IP permite identificar o dispositivo e a rede que ele pertence
- Para interligar diversas redes é preciso de um roteador
- Usa informações nos pacotes para entregar os pacotes aos respectivos destinos
- Uma rota é um caminho a ser seguido para entrega de um dado ao seu destino
- A entrega de dados é facilmente feita pois possuem endereço de destino e origem no pacote
# Formato de endereçamento IPv4

- Cada host em uma rede TCP/IP um endereço de 32 bits que é usado em toda a comunicação
- Serão chamados de IP somente
- É representado em decimal em forma de 4 número de 8 bits separados por um ponto no formato a.b.c.d
	- Menor valor é 0.0.0.0
	- Maior valor é 255.255.255.255
- O endereçamento IP possui basicamente duas partes uma que indica a rede e outra que indica o dispositivo dentro desta rede
- Uma rede TCP/IP usando o IPv4 pode ter até 4.294.967.296 endereços IP ou 2^32
	- Teoricamente porque existem alguns números de IP, que são reservados e não podem ser usados, nós veremos isto depois
- Um endereço IP tem quatro números separados por pontos. Esse tipo de sistema de notação é chamado de notação decimal separada por pontos
- O conjunto de quatro números é chamado de octeto, uma vez que eles na verdade representam um número binário de 8 bits ou 1 byte
- Consequentemente, o valor decimal máximo para cada um dos quatro números em um endereço IP é 255, e não 999
- O valor binário de bit (binary bit value – BBV) permite facilmente converter os bits em um valor decimal comum
	- Só somar os números da coluna BBV quando o bit um estiver ativo, caso nenhum bit estiver ativo (todos em zero) o número em decimal é zero
# Esquema de original de endereçamento IP Classfull

- Conceitualmente, cada endereço é um par (netID e hostID), em que netID identifica uma rede e hostID identifica um host nessa rede
- Para facilitar a distribuição dos endereços IP em redes e hosts, foram especificadas cinco classes de endereços IP
- Cada endereço é considerado como auto-identificável
- O limite entre prefixo e sufixo pode ser calculado a partir do endereço isolado, sem referência a informações externas
- Em particular, a classe de um endereço pode ser determinada a partir dos três bits de alta ordem
	- Classe A
		- Primeiro bit 0
		- netID - 7 bits
		- hostID - 24 bits
		- 0.0.0.0 -> 127.255.255.255
	- Classe B
		- Primeiros bits 10
		- netID - 14 bits
		- hostID - 26 bits
		- 128.0.0.0 -> 191.255.255.255
	- Classe C
		- Primeiros bits 110
		- netID - 21 bits
		- hostID - 8 bits
		- 192.0.0.0 -> 223.255.255.255
	- Classe D
		- Primeiros bits  1110
		- Endereço multicast
		- 224.0.0.0 -> 239.255.255.255
	- Classe E
		- Primeiros bits 1111
		- Reservado para uso futuro
		- 240.0.0.0 -> 255.255.255.255
- Em suma apenas as classes A, B e C são usadas na prática
- Os números de redes na Internet são atribuídos por uma corporação sem fins lucrativos chamada ICANN (Internet Corporation for Assigned Names and Numbers) para evitar conflitos
- Por sua vez, a ICANN tem partes delegadas do espaço de endereços para diversas autoridades regionais, e estas fazem a doação de endereços IP a ISPs e outras empresas
- Cada host e roteador tem seu endereço IP que codifica seu número de rede e de host
- Combinações exclusivas, onde em uma rede duas maquinas não tem o mesmo valor
- Todos endereços tem 32 bits
	- São usados nos campos Source address e Destination address dos pacotes IP
- O endereço se não se refere diretamente a um hots, mas sim uma inteface da rede
- Caso um host esteja em mais de uma rede ele precisa ter um endereço para cada rede
- Maioria dos hosts estão em uma só rede
- Existe situações em que um computador convencional tem duas ou mais conexões físicas de rede, esses computadores são conhecidos como hosts multihomed
	- Cada uma das conexões de rede da máquina precisa receber um endereço
- Como os endereços IP codificam uma rede quanto um host nessa rede, um endereço não especifica um computador individual, mas uma conexão com uma rede
- Possibilita um encaminhamento eficiente entre origem e destino
- Endereços IPs podem se referir a redes e também a hosts
- Por convenção, o hostID com todos os bits marcados com 0 nunca endereça um host individual, pois entes representa uma rede
	- Assim, os endereços um endereço IP pode simbolizar a rede
- Outra vantagem do endereço IP é a representação de um endereço de broadcast
	- Usado quando se deseja enviar uma mensagem para todas as máquinas de uma dada rede
- Qualquer endereço com o hostID consistindo em todos os bits marcados em 1 é reservado para o broadcast (Broadcast direcionado)
- Sem o endereço de broadcast caso alguma máquina precise enviar uma mesma mensagem para todos na rede, esta deveria enviar uma a uma
	- No caso de uma rede classe A, serão aproximadamente 16 milhões de mensagens iguais
- O endereço IP 0.0.0.0 é usado pelos hosts quando eles estão sendo inicializados
- Os endereços IP que têm 0 como número de rede se referem à rede atual
- Esses endereços permitem que as máquinas façam referência às suas próprias redes sem saber seu número 
	- Mas elas precisam conhecer sua classe para saber quantos zeros devem ser incluídos
- O endereço que consiste apenas em dígitos 1 permite a difusão na rede local (Broadcast limitado)
- *Os endereços com um número de rede apropriado e que tiverem apenas valores 1 no campo de host permitem que as máquinas enviem pacotes de difusão para LANs distantes (Broadcast direcionado), em qualquer parte da Internet (embora muitos administradores de redes desativem esse recurso)*
## Endereço Loopback

- **Todos os endereços com o formato 127.xx.yy.zz são reservados para teste de loopback e para comunicação entre processos no computador local**
- Os pacotes enviados para esse endereço não são transmitidos
- Eles são processados localmente e tratados como pacotes de entrada
- Permite que os pacotes sejam enviados para a rede local, sem que o transmissor saiba seu número
- Um host ou um roteador nunca deverá rotear pacotes com endereços 127.xx.yy.zz, assim esses não são roteáveis em lugar algum e ficam restrito ao próprio host
## Resumo para os endereços especiais

- Todos os bits em 0: Endereço de origem inicial
- Todos os bits em 1: Broadcast limitado (rede local)
- netID e os bits de hostID em 1: Broadcast direcionado para a rede
- netID e os bits de hostID em 0: Endereço de rede
- 127.xx.yy.zz: endereço de loopback
## Sub-rede

- No esquema de endereçamento IP original Classful
	- Cada rede física recebe um endereço de rede exclusivo
	- Cada host em uma rede tem o endereço de rede como um prefixo do endereço individual do host
- A principal vantagem de dividir o endereço IP em duas partes surge do tamanho das tabelas de roteamento exigidas nos roteadores
- Em vez de manter uma entrada de roteamento por host de destino, um roteador pode manter uma entrada de roteamento por rede
- Examinar apenas a parte de rede de um endereço de destino quando tomar decisões de encaminhamento de pacotes
- Parece tratar de todas as possibilidades, mas possui um pequeno problema
	- Foi inventado no mundo dos mainframes caros, os projetistas não anteciparam o crescimento da Internet, que hoje cresce assombrosamente
	- Por fim os endereços IPv4 parecem estar findados a se esgotarem rapidamente, por isto já existe o IPv6 que pode atribuir mais de 1500 IPs por metro quadrado da terra
- Uma técnica que permite que um único endereço de rede se espalhe por várias redes físicas é chamada endereçamento de sub-rede, encaminhamento de sub-rede ou subdivisão de redes
- Técnica mais genérica e padrão para a subdivisão de redes, na verdade a subdivisão de redes é parte obrigatória do endereçamento IP
- Importante observar que os sites individuais têm liberdade de modificar endereços e rotas desde que as modificações permaneçam invisíveis a outros sites
	- Todos os hosts e roteadores no site concordem em honrar o esquema de endereçamento do site
	- Outros sites na Internet possam tratar dos endereços como um prefixo de rede e um sufixo de host
- Ao usar o endereço de sub-rede, pensamos em um endereço IP de 32 bits como tendo uma parte de Rede e uma parte de Rede Local
	-  Parte de Rede identifica um site, possivelmente com várias redes físicas, e a parte local identifica uma rede física e host nesse site
	- Endereçamento hierárquico que leva ao roteamento hierárquico correspondente
### Implementação de sub-redes com máscaras

- A tecnologia de sub-rede facilita a configuração de tamanho fixo ou variável
- O padrão especifica que uma máscara de 32 bits
- Tal como o endereço IP, seja usada para especificar a divisão de sub-rede
- Um site usando o endereçamento de sub-rede precisa escolher uma máscara de sub-rede de 32 bits para cada rede
- Os bits na máscara de sub-rede são definidos como 1 se as máquinas na rede tratarem o bit correspondente no endereço IP como parte do prefixo de sub-rede
- 0 se tratarem o bit como parte do identificador de host
- É necessário casar bit-a-bit o endereço IP e a máscara de sub-rede
- O endereçamento de sub-rede não restringe a máscara de bits contíguos do endereço, embora seja altamente recomendado não fazer uso deste artifício
	- Complica a atribuição de endereços e complica a tabela de roteamento
#### Como os pacotes IP são processados em um roteador?

- Cada roteador tem uma tabela que lista algum número de endereços IP (rede, 0) e uma série de endereços IP (para essa rede ou host)
	- O primeiro tipo informa como chegar a redes distantes
	- O segundo, como chegar a hosts locais
- Associadas a essa tabela estão a interface de rede usada para alcançar o destino e algumas outras informações.
- Quando um pacote IP é recebido, seu endereço de destino é procurado na tabela de roteamento
- Se o destino for uma rede distante, o pacote será encaminhado para o próximo roteador da interface fornecida na tabela
- Caso o destino seja um host local (por exemplo, na LAN do roteador), o pacote será enviado diretamente para lá
- Se a rede não estiver presente, o pacote será enviado para um roteador predefinido que tenha tabelas maiores (roteador padrão/default)
- Esse algoritmo significa que cada roteador só precisa controlar as outras redes e hosts locais, deixando de lado os pares (rede, host), o que reduz muito o tamanho da tabela de roteamento
#### Divisão em sub-redes

- Quando a divisão em sub-redes é introduzida, as tabelas de roteamento são alteradas acrescentando-se entradas da forma (esta rede, sub-rede, 0) e (esta rede, esta sub-rede, host)
- Um roteador da sub-rede k sabe como alcançar todas as outras sub-redes, e também como chegar a todos os hosts da sub-rede k
- Ele não precisa saber detalhes sobre os hosts de outras sub-redes
- Na realidade, a única modificação é fazer com que cada roteador seja submetido a um AND booleano com a máscara de sub-rede
	- Eliminar o número do host e pesquisa o endereço resultante em suas tabelas (depois de determinar qual é a classe da rede)
# Endereçamento classless e super-redes

- Por volta de 1993, ficou aparente que técnicas isoladas não impediriam que o crescimento da Internet rapidamente esgotasse o espaço de endereços válidos na Internet #1990s 
- É claro que isto exige um novo esquema de endereço o que deve ser fornecido pelo IPv6
- Mas enquanto isto não acontece, é usado uma solução temporária
- Conhecida como endereçamento classless, o esquema de endereçamento estende a idéia usada no endereçamento de sub-rede para permitir que um prefixo de rede tenha um tamanho qualquer
- Além de um novo modelo de endereçamento, os projetistas inventaram técnicas de encaminhamento e propagação de rota
- Como resultado, a tecnologia inteira ficou conhecida como Classless Inter-Domain Routing (CIDR)
	- Alocar os endereços IP restantes em blocos de tamanho variável, sem levar em consideração as classes
	- Se um site precisar, digamos, de 2000 endereços, ele receberá um bloco de 2048 endereços
- CIDR usa máscara de endereços de 32 bits para especificar o limite entre o que representa rede e o que representa hosts
- Como a identificação de um bloco CIDR exige um endereço e uma máscara, criou-se uma notação abreviada para expressar os dois itens
- Notação CIDR
	- Mas conhecida informalmente como notação slash, a abreviação representa o tamanho da máscara em decimal e sua uma barra para separá-la do endereço
- O endereçamento classless, que agora é usado por toda a Internet, trata os endereços IP como inteiros quaisquer
- Permite que um administrador de rede particione endereços em blocos contíguos, nos quais o número de endereços em um bloco é uma potência de dois
- Algoritmo padrão de roteamento não funciona mais
- Em vez disso, cada entrada de tabela de roteamento é estendida com uma máscara de 32 bits
- Desse modo, agora existe uma única tabela de roteamento para todas as redes, consistindo em um array de triplas (endereço IP, máscara de sub-rede, linha de saída)
- Quando um pacote chega, seu endereço IP de destino é extraído
- Depois (conceitualmente), a tabela de roteamento é varrida entrada por entrada, mascarando-se o endereço de destino e comparando-se esse endereço com a entrada de tabela, em busca de uma correspondência
- É possível que várias entradas (com diferentes comprimentos de máscaras de sub-redes) correspondam
	- Será usada a máscara mais longa. Portanto, se houver uma correspondência para a máscara /20 e uma máscara /24, será usada a entrada /24
- Foram criados algoritmos complexos para acelerar o processo de comparação de endereços
- Os roteadores comerciais utilizam chips VLSI personalizados com esses algoritmos incorporados em hardware
## Blocos de CIDR reservados para redes privadas

- Alguns prefixos de rede foram reservados pelo IETF de forma a serem somente utilizados em redes privadas, estes prefixos reservados nunca serão atribuídos a redes na Internet
- Coletivamente, os prefixos reservados são conhecidos com endereços privados ou endereços não-roteáveis
- Este último surge porque os roteadores na Internet entendem que os endereços são reservados
- Se um datagrama destinado a um dos endereços privados for acidentalmente encaminhado para a Internet, um roteador na Internet será capaz de detectar o problema e descartar o datagrama

| Prefixo        | Endereço mais baixo | Endereço mais alto |
| -------------- | ------------------- | ------------------ |
| 10.0.0.0/8     | 10.0.0.0            | 10.255.255.255     |
| 172.16.0.0/12  | 172.16.0.0          | 172.31.255.255     |
| 192.168.0.0/16 | 192.168.0.0         | 192.168.255.255    |
| 169.254.0.0/16 | 169.254.0.0         | 169.254.255.255    |

# Nat - Network Address Traslation

- Um grande problema hoje na Internet é que os endereços IPs válidos na Internet estão escassos
- Porém os clientes de negócios (empresas) esperam estar continuamente on-line durante o horário comercial
- Tanto pequenas empresas, como as agências de viagens com três funcionários, quanto as grandes corporações têm vários computadores conectados por uma LAN
- Alguns computadores são PCs de funcionários; outros podem ser servidores da Web
- Em geral, existe um roteador na LAN que está conectada ao ISP por uma linha dedicada com a finalidade de fornecer conectividade contínua
- Essa organização significa que cada computador deve ter seu próprio endereço IP durante o dia inteiro
- Na realidade, o número total de computadores pertencentes a total dos os clientes comerciais combinados não pode ultrapassar o número de endereços IP que o ISP tem
- Para piorar, mais e mais usuários estão assinando os serviços de ADSL ou Internet via cabo
- Duas características desses serviços são (1) o usuário recebe um endereço IP permanente e (2) não existe nenhuma tarifa por conexão (apenas uma tarifa mensal)
- Muitos usuários de ADSL e cabo simplesmente ficam conectados de modo permanente
- Esse desenvolvimento acelera a redução da quantidade de endereços IP
- Atribuir endereços IP no momento da utilização, como ocorre no caso dos usuários de discagem (DHCP), não tem utilidade, porque o número de endereços IP em uso em qualquer instante pode ser muitas vezes maior que o número de clientes do ISP
- Apenas para complicar um pouco mais, muitos usuários de ADSL e cabo têm dois ou mais computadores em casa
- Muitas vezes um computador para cada membro da família, e todos eles querem estar on-line o tempo todo, usando o único endereço IP que o ISP lhes forneceu
- A solução aqui é conectar todos os PCs por meio de uma LAN e inserir um roteador nessa LAN
- Do ponto de vista do ISP, agora a família equivale a uma pequena empresa com alguns computadores
- O problema de esgotar os endereços IP não é um problema teórico que pode ocorrer em algum momento no futuro distante
- Ele está acontecendo aqui mesmo e agora mesmo
- A solução a longo prazo é a Internet inteira migrar para o IPv6, que tem endereços de 128 bits
- Essa transição está ocorrendo com lentidão e a conclusão do processo irá demorar muitos anos
- Em conseqüência disso, algumas pessoas consideraram necessário fazer uma rápida correção a curto prazo
- Essa correção veio sob a forma da NAT (Network Address Translation), descrita na RFC 3022
- A idéia básica por trás da NAT é atribuir a cada empresa um único endereço IP (ou no máximo, um número pequeno deles) para tráfego da Internet
- Dentro da empresa, todo computador obtém um endereço IP exclusivo, usado para roteamento do tráfego interno
- Porém, quando um pacote sai da empresa e vai para o ISP, ocorre uma conversão de endereço
- Para tornar esse esquema possível, é preciso usar os IPs privados não roteáveis na Internet
- As empresas podem utilizá-los internamente como desejarem
- A única regra é que nenhum pacote contendo esses endereços pode aparecer na própria Internet
- O que vai acontecer com o uso do NAT é o seguinte
	- (1) Quando o pacote for sair da rede privada para a Internet, o ponto de acesso a Internet (normalmente um modem ADSL) irá “mascarar” o pacote, ou seja ele trocará o IP de origem contendo um IP privado (ex. 10.1.1.1) pelo por um IP válido (ex. 200.1.2.3 do ADLS)
	- (2) Quando o pacote voltar com a resposta, está troca deve ser desfeita pelo ponto de acesso a Internet (no nosso exemplo, pelo modem ADSL), isto é possível porque o ponto de acesso a Internet armazena algumas características do pacote (endereços IP's de origem e destino, portas de origem presentes na camada de transporte e destino, etc)
	- (3) Depois de desfazer o NAT o ponto de acesso a Internet (ADSL) envia o pacote original (destinado a rede com IP não roteável a Internet, para a rede, no nosso exemplo 10.1.1.1)
- Este processo é totalmente transparente para o usuário da rede privada e da Internet
- Porém não para o ponto de acesso a Internet (á máquina que fará o NAT), já que está máquina terá de armazenar informações sobre a conexão de rede para poder fazer a tarefa de NAT, usando muito de sua memória e processamento
- O que não seria necessário usando apenas roteadores e IP's válidos na Internet
- O NAT normalmente aplica a rede um certo nível de atraso aos pacotes
	- O ponto de acesso a Internet tem que analisar e alterar a grande maioria dos pacotes que passam por ele
- O NAT também cria uma rede pseudo orientada a conexão
## Benefícios

- Esconder o layout da rede privada
- Não permitir que as máquinas a trás do NAT sejam acessadas como servidor. Mas em alguns casos isto pode ser um ponto negativo
- Manter um certo nível de segurança na rede
- Mas a principal vantagem é permitir que várias máquinas naveguem na Internet usando apenas um único IP válido
	- Isso dá uma acerta folga para o problema da falta de endereços IP's na Internet.