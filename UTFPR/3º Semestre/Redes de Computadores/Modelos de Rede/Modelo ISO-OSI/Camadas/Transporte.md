# O que é?

- Responsável pelo controle lógico dos dados que pode ser orientado a conexão e não orientado a conexão
- **Orientado a conexão** se preocupa com a **entrega correta de dados**
- Já a **não orientado a conexão não se preocupa** com os dados
## Tanenbaum

- Determina o tipo de serviço deve ser fornecido ao usuário/aplicação
- O tipo de conexão mais popular é um **canal ponto a ponto livre de erros** 
	- mensagens ou bytes na ordem em que eles foram enviados
- É possível outro, que entrega mensagens isoladas sem nenhuma garantia relativa a ordem de entrega
- O tipo de serviço é determinado quando a conexão é estabelecida

## Wendell Odom

- Variedade de serviços entre dois hosts
- **Estabelecimento e a finalização da conexão**
- **Recuperação de Erros**
- **Segmentação de grandes blocos de dados em partes menores**

Refs: [[Redes de Computadores]], [[Modelos de Rede]], [[Modelo ISO-OSI]]