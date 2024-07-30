# O que é?

- Um cabo coaxial consiste em um fio de cobre esticado na parte central envolvido por um material isolante
- O isolante é protegido por um condutor cilíndrico, geralmente uma malha entrelaçada
- O condutor externo / malha é protegido por uma camada de isolante externo, geralmente uma camada plástica protetora
- Possui uma impedância, que é medida em ohms
- Redes Ethernet usam cabo coaxial de 50 ohms, já o cabo coaxial usado nas TVs são de 70 ohms
# Vantagens

- Sua blindagem permite que o cabo seja longo
- Permite o uso de redes multi-canal (Broadband)
- Mais barato que o par trançado blindado
- Melhor imunidade contra ruídos e contra atenuação do sinal (perda de força de sinal) que o par trançado sem blindagem
- Possui limite de distância de 185 metros
# Desvantagens
- Pouco flexíveis, quebra e apresenta mau contato com facilidade
- Pelo mesmo motivo é difícil de ser passado em conduítes, dificultando a instalação da rede no ambiente de trabalho
- Usado normalmente em topologia linear, onde caso o cabo quebre ou apresente mau contato, o segmento inteiro da rede deixa de funcionar
- Mais caro que o par trançado sem blindagem
- Taxa média de transferência de 10 Mbps

# Tipos de Transmissão

- Pode ter dois tipos de transmissão
## Baseband

- Uni-canal
- Transmite apenas em um canal de dados
- Forma digital
- Mais usado em redes locais
- Unidirecional, com transmissão half-duplex
## Broadband

- Multi-canal
- Transmite em vários canais de dados
- forma analógica
- Unidirecional (pode ser feito com dois canais, ou dividindo o canal em dois um para recepção e outro para transmissão)
# Tipos de Cabos Coaxiais

- Existem dois tipos de cabos coaxiais, sendo eles fino e grosso
- Os dois tipos necessitam de terminação resistiva, o cabo fino usa terminador de 50 Ω, em cada uma das pontas do cabo
## Cabo Coaxial Fino (10Base2)

- Também chamado de RG-58
- Taxa de transferência de 10 Mbps
- Transmite no tipo baseband
- Comprimento máximo de 185 metros (é possível aumentar a distância com repetidores)
- Distância mínima de 0,5 metros (50 centímetros)
- Impedância de 50 Ω
- Máximo de 30 maquinas por seguimento de rede (é possível uso de repetidores)
- Topologia Linear
- Conexões são feitas através de  conectores BNC em "T"
## Cabo Coaxial Grosso (10Base5)

- Comprimento máximo de 500 metros
- Possui blindagem dupla (por isso é grosso)
- Menos flexível
- Menos usado que o 10Base2
- Antigamente, antes da fibra ótica, era a espinha dorsal da rede (Backbone)
- Transferência de 10 Mbps
- Usa um conector chamado *Vampiro*, que por sua vez é ligado a um transceptor (tranceiver), que é ligado a placa de rede através de um cabo no máximo 15 metros ligado a um conector de 15 pinos (porta AUI - Attachment Unit Interface, ou DIX - Digital Intel Xerox)
- Não é necessário desligar a rede para instalar o conector
- Distância mínima de 2,5 metros (identificado por faixa preta no cabo)
- A cor do cabo é laranja ou amarelo
- Conector coaxial chamado N, é parecido com o BNC porém o encaixe é em N

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]], [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo TPC-IP/Camadas/Física/Física|Física]], [[Transmissão de Dados]]