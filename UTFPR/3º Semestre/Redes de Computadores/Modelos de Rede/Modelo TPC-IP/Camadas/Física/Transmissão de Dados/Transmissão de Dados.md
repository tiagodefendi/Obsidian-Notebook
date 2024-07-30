# O que é?

- Pressupõe a passagem de sinais através dos meios físicos de comunicação que compõem as redes
- As propriedades físicas de meios de transmissão e as características dos sinais transmitidos influenciam na construção das redes de computadores
# Informação e Sinal

- Transmitir dados de um ponto ao outro envolve uma série de processos
	1. Geração de uma ideia, padrão ou imagem na origem
	2. Descrição dessa ideia, padrão ou imagem na origem
	3. Codificação desses símbolos em uma forma propícia à transmissão em um meio físico disponível
	4. Transmitir esses símbolos codificados ao destino
	5. Decodificação e reprodução dos símbolos
	6. A recriação da ideia pelo destinatário, com uma possível degradação de qualidade
# Tipos de Transmissão de dados

- As rede de computadores foram criadas basicamente para a transmissão de dados
- Tecnicamente falando existem 3 tipos
	- [[Simplex]]
	- [[Half-duplex]]
	- [[Full-duplex]]
# Informação Analógica vs. Digital

- Existem dois tipos de informações
	- [[Analógica|Informações Analógicas]]
	- [[Digital|Informações Digitais]]
- Computadores suam informações digitais por aceitarem apenas dois valores 0 ou 1
# Modulação

- Os números digitais são transmitidos em forma de pulsos elétricos, ópticos ou ondas de rádio, dependendo do meio usado na conexão
- Os sinais digitais precisam serem transformados em sinais analógicos para serem transmitidos pelo meio de transmissão
- Esse processo se chama **Modulação de dados**
- Ao contrário da transmissão analógica "pura", essa transmissão analógica está enviando, por meio de sinais analógico, dados originalmente digitais
- Possibilita que o receptor, após desmodular os dados, verificar se ele estão corrompidos, e pedir uma retransmissão se os dados estiverem errados
- O **modem** (MOdulador/DEModulador) é responsável pela transmissão de dados digitais através da linha telefônica, que é um canal analógico
- Nas redes locais a modulação e demodulação dos dados é feita pela placa de rede
# Transmissão em Série vs. Paralela
## Paralela

- Em um computador o tipo de **transmissão mais usada é a paralela**
	- Transmissor envia todos os bits de dados que ele é capas de enviar de uma vez só
- Desvantagens da transmissão paralela
	- Interferência eletromagnética
	- Altamente dependente do meio
	- Fisicamente é necessário um fio para transmitir cada bit de dado
	- Os fios precisam ser curtos para evitar a degradação no sinal e também para diminuir a incidência de erros
## Série

- Na transmissão serial é preciso somente um fio para transmitir os dados
- Bits enviados um a um
- Apesar de lenta tem como vantagem o limite de comprimento do cabo ser maior
- **Redes locais usam comunicação do tipo série**
- A unidade medida de transmissões seriais é dada em bps (bits por segundo)
# Meio de Transmissão

- O objetivo da camada física é transmitir um fluxo bruto de bits de uma máquina para outra
- vários **meios físicos** podem ser usados para isso, podendo ser agrupados em
	- **Meios guiados**
		- Fio de cobre
		- Fibras óticas
	- **Meios não guiados**
		- Onda de rádios
		- Raios laser transmitidos pelo ar
- **Meio Magnético** 
	- Uma das formas mais comuns de transportar dados de um computador para outro
	- Gravar dados em uma fita magnética ou em discos flexíveis
	- Transportar fisicamente a fita ou os discos para outros computador
	- DPC/DPL - Disquet Para Cá / Disquet Para Lá
## Quais são os meios mais usados?

- [[Cabo Coaxial]]
- [[Cabo Par Trançado]]
- [[Fibra Ótica]]
- [[Rádio]]
- [[Infravermelho]]
- [[Laser]]

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]], [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo TPC-IP/Camadas/Física/Física|Física]]