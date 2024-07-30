# Relação com Modelo OSI

- Essa camada equivale as camadas de [[Sessão]], [[Apresentação]] e [[UTFPR/3º Semestre/Redes de Computadores/Modelos de Rede/Modelo ISO-OSI/Camadas/Aplicação|Aplicação]] no Modelo OSI
# Protocolos

- HTTP (HyperText Transfer Protocol)
- SMTP (Simple Mail Transfer Protocol)
- FTP (File Transfer Protocol)
- DNS (Domain Name Protocol)
- Telnet
# Funções

- Faz a comunicação entre os aplicativos e o protocolo de transporte
- Quando o aplicativo quiser realizar alguma tarefa que usa a rede, ele irá efetuar o pedido na camada de aplicação
- No processo de "descida" da pilha de protocolos, ela se comunica com a camada de transporte através de uma porta
- O protocolo HTTP utiliza por padrão a porta 80
- O uso das portas permite ao protocolo de transporte saber qual tipo de conteúdo do pacote de dados
- Ainda com uso das portas o receptor consegue saber para qual protocolo de aplicação ele deve entregar o pacote de dados

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo TCP-IP]]