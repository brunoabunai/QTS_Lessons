# Lesson by: Carlos Calixto, Bruno Ribeiro.

## O sistema vai ter:
* Sistema de controle de estoque
1. Cadastro de Produto
2. Cadastro de Fornecedor
3. Cadastro de Cliente
* Sistema de Vendas-Entrada e Saida

<br />

-----------------------------------

### Artefatos:
* Estoque- Quantidade de produtos que a empresa tem armazenada, que diminui a cada venda, ou que aumenta a cada compra.
* Lucro- Diferença entre o valor de custo e o valor de venda.
* Venda- pega um produto registrado e reduz sua quantidade de estoque
* Compra- registra um produto no estoque
  
<br />

-------------------------------------

### Regras de entrada:
- Para cadastrar um Produto, deve-se informar a quantidade de produto, seu nome, marca e o fabricante.
- Para cadastrar um fornecedor, deve-se informar: nome do fornecedor, endereço para se localizar caso não obtenha contato, telefone para contato, cnpj para indentificação, email para contato.
- Para cadastrar um Cliente, deve-se informar: nome do cliente, endereço, telefone para contato, cpf para indentificação, email para contato.
- Para realizar uma venda, deve-se informar: nome do produto vendido para verificação de estoque, marca do produto vendido para analise de mercado, quantidade para contagem de preço, preço, cliente para saber quem comprou determinada compra e seu endereço, data para saber quando foi comprado e não confundir os prazos.
- Para realizar uma compra, deve-se: a quantidade de produto, seu nome, marca e o fabricante.

<br />

--------------------------

* Nome do campo.
* Chave.
  * A chave Primária (P) é uma coluna ou conjunto de colunas que identifica exclusivamente o restante dos dados em qualquer linha específica da tabela.
  * A chave Externa (E/F) é uma coluna na tabela que é uma chave primária em outra tabela, indicando que quaisquer dados em uma coluna de chave externa deve ter dados correspondentes na outra tabela em que essa coluna é a chave primária. Para bancos de dados, essa correspondência é conhecida como integridade referencial.
  * O valor NOT NULL (NN) significa que a coluna deve ter um valor em cada linha. Se NULL foi utilizado, essa coluna pode ser deixada em branco em uma linha específica.
* Tipo de dado.
* Descrição do objetivo de cada campo.
* Tamanho do campo.
  
**Nota:**
  As características efetivas de "Tipo de Dados" e "Tamanho do Campo" dependem das implementações específicas do fornecedor de banco de dados.

<br />

------------------------

### **Tabela 0. Dicionário de Dados para Estoque**
| Nome do campo | Chave | Tipo de dado | Descrição do Campo | Tamanho do Campo (bytes) |
| :------------ | :---- | :----------- | :----------------- | :----------------------: |
| est_idPk | P | int | Um número seqüencial (incrementado em 1) ou aleatório exclusivo, atribuído pelo Enterprise Transaction Performance sempre que um novo registro é adicionado à tabela. | 4 |
| pro_idFk | F | int | O ID exclusico da tabela Produto | 4 |
| est_amount | NN | int | Quantidade total do produto (x) que está no estoque | 4 |

<br />
<br />

### **Tabela 1. Dicionário de Dados para Produto**
| Nome do campo | Chave | Tipo de dado | Descrição do Campo | Tamanho do Campo (bytes) |
| :------------ | :---- | :----------- | :----------------- | :----------------------: |
| pro_idPk | P | int | Um número seqüencial (incrementado em 1) ou aleatório exclusivo, atribuído pelo Enterprise Transaction Performance sempre que um novo registro é adicionado à tabela. | 4 |
| pro_amount | NN | int | Quantidade de produtos que estão sendo comprados | 4 |
| pro_name | NN | char | Nome oficial do produto que está sendo registrado | 255 |
| pro_manufacturer |  | char | Qual a fabricante original do produto | 255 |
| pro_price | NN | float | Preço que **cada** produto está sendo comprado  | 6 |

<br />
<br />


### **Tabela 2. Dicionário de Dados para Fornecedor**
| Nome do campo | Chave | Tipo de dado | Descrição do Campo | Tamanho do Campo (bytes) |
| :------------ | :---- | :----------- | :----------------- | :----------------------: |
| for_idPk | P | int | Um número seqüencial (incrementado em 1) ou aleatório exclusivo, atribuído pelo Enterprise Transaction Performance sempre que um novo registro é adicionado à tabela. | 4 |
| for_name | NN | char | Nome utilizado pelo fornecedor | 255 |
| for_address | NN | char | Endereço para se localizar caso não se obtenha contato com o fornecedor, ou caso queira buscar o produto pessoalmente | 255 |
| for_telephone |  | char | Telefone (recidêncial) do fornecedor, para manter contato com ele | 12 |
| for_phone | NN | char | Telefone (celular) do fornecedor, para manter contanto | 15 |
| for_email | NN | char | Email do fornecedor para manter contato | 255 |
| for_cnpj_cpf | NN | char | CNPJ para identificação (pode ser utilizado como chave primário, irá depender do que o cliente deseja) | 20 |

<br />
<br />


### **Tabela 3. Dicionário de Dados para Cliente**
| Nome do campo | Chave | Tipo de dado | Descrição do Campo | Tamanho do Campo (bytes) |
| :------------ | :---- | :----------- | :----------------- | :----------------------: |
| cli_idPk | P | int | Um número seqüencial (incrementado em 1) ou aleatório exclusivo, atribuído pelo Enterprise Transaction Performance sempre que um novo registro é adicionado à tabela. | 4 |
| cli_name | NN | char | Nome utilizado pelo cliente | 255 |
| cli_address | NN | char | Endereço para se localizar caso não se obtenha contato com o cliente | 255 |
| cli_telephone |  | char | Telefone (recidêncial) do cliente, para manter contato | 12 |
| cli_phone | NN | char | Telefone (celular) do cliente, para manter contanto | 15 |
| cli_email |  | char | Email do fornecedor para manter contato | 255 |
| cli_cpf | NN | char | CPF para identificação (pode ser utilizado como chave primário, irá depender do que o cliente deseja) | 15 |

<br />
<br />


### **Tabela 4. Dicionário de Dados para Venda**
| Nome do campo | Chave | Tipo de dado | Descrição do Campo | Tamanho do Campo (bytes) |
| :------------ | :---- | :----------- | :----------------- | :----------------------: |
| ven_idPk | P | int | Um número seqüencial (incrementado em 1) ou aleatório exclusivo, atribuído pelo Enterprise Transaction Performance sempre que um novo registro é adicionado à tabela. | 4 |
| pro_idFk | F | int | O ID exclusico da tabela Produto, definir o produto que está sendo vendido | 4 |
| cli_idFk | F | int | O ID exclusico da tabela Cliente, definir o cliente que está comprando (caso deseje marcar ou que faça a entrega da recidencia dele) | 4 |
| ven_amount | NN | int | Quantidade de produtos (X) que serão vendidos | 4 |
| ven_address |  | char | Caso o comprador tenha enterece em receber a entrega no endereço (X) | 255 |
| ven_date | NN | date | Saber quando foi efetuado a compra e não confundir os prazos | 25 |

<br />
<br />

----------------------------------

### **Controle de estoque**
ao efetuar um registro de um produto, ele irá fazer uma pesquisa dentro da tabela (estoque) para saber se aquele produto já existe, caso o produto já tenha um registro salvo, ele irá incrementar (pegar o valor que já tem e somar) ao (est_amount) a quantidade que está sendo referenciada em (est_idFk (pro_amount))

### **Controle de venda**
Ele irá verificar o estoque para ver se o tal produto que esta sendo deseja está disponivel para venda, caso tenha ele irá reduzir a quantidade desejada do (estoque).

<br />
