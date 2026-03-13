---
# Copyright (c) 2017-2026 Manticore Software Ltd. All rights reserved.

# Documentation licensed under the GNU General Public License Version 3 or
# later.
# The original work was translated from English into Brazilian Portuguese.
# https://github.com/manticoresoftware/manticoresearch/blob/-/LICENSE

source_url: https://github.com/manticoresoftware/manticoresearch/blob/master/manual/english/Read_this_first.md
revision: adbbf4d8ab8beda20c125200bd2c6450729e6ec3
status: ready
---

# Leia isto primeiro

## Sobre este manual

Este manual foi organizado para refletir a maneira provável de usar o Manticore:

- Começando com informações básicas sobre o programa e como instalá-lo e
  conectá-lo.
- Recursos essenciais, como adicionar documentos e executar pesquisas.
- Dicas de otimização de desempenho, truques e extensão do Manticore com a ajuda
  de plugins e funções personalizadas.

##### Não pule1️⃣ 2️⃣ 3️⃣

As seções principais do manual estão marcadas com 1️⃣, 2️⃣, 3️⃣ etc. no menu para
sua conveniência, já que suas respectivas funcionalidades são as mais
utilizadas.
Se você é iniciante no Manticore, **recomendamos fortemente que não pule essas
seções**.

##### Guia de início rápido

Se você está procurando uma compreensão rápida de como o Manticore funciona em
geral, o [Guia de início rápido](Quick_start_guide.md) é um bom lugar para
começar.

##### Usando exemplos

Cada exemplo de consulta tem um pequeno ícone 📋 no canto superior direito:

![Copy example](copy_example.png)

Você pode usá-lo para copiar exemplos para a área de transferência.
**Se a consulta for uma requisição HTTP, ela será copiada como um comando
CURL**.
Você pode configurar o host/porta pressionando ⚙️.

##### Pesquisa neste manual

Amamos a pesquisa e nos esforçamos ao máximo para torná-la o mais prática
possível neste manual.
Claro que ela é suportada pelo Manticore Search.
Além de usar a barra de pesquisa, que exige que o manual seja aberto primeiro,
existe uma maneira muito fácil de encontrar algo, basta abrir
**mnt.cr/sua-palavra-chave-de-pesquisa**:

![mnt.cr quick manual search](mnt.cr.gif)

## Boas práticas

Há alguns aspectos importantes que você precisa entender sobre o Manticore
Search para seguir as melhores práticas de uso.

#### Tabela em tempo real vs. tabela simples

- **[Tabela em tempo real](Creating_a_table/Local_tables/Real-time_table.md)**
  permite adicionar, atualizar e excluir documentos com disponibilidade imediata
  das alterações.
- **[Tabela simples](Creating_a_table/Local_tables/Plain_table.md)** é uma
  estrutura de dados praticamente imutável e um elemento básico usado por
  tabelas em tempo real.
  Uma tabela simples armazena um conjunto de documentos, seu dicionário comum e
  configurações de indexação.
  Uma tabela em tempo real pode consistir em várias tabelas simples (pedaços),
  mas **além disso, o Manticore fornece acesso direto à criação de tabelas
  simples** usando a ferramenta
  [indexer](Data_creation_and_modification/Adding_data_from_external_storages/Plain_tables_creation.md#Indexer-tool).
  Isso faz sentido quando seus dados são praticamente imutáveis, portanto, você
  não precisa de uma tabela em tempo real.

#### Modo em tempo real vs. modo simples

O Manticore Search funciona em dois modos:

- **Modo em tempo real** (modo RT).
  Este é o modo padrão e permite gerenciar seu esquema de dados
  **imperativamente**:
  - Permite gerenciar seu esquema de dados online usando os comandos SQL
    `CREATE`/`ALTER`/`DROP TABLE` e seus equivalentes em clientes não-SQL.
  - No arquivo de configuração, você precisa definir apenas as configurações
    relacionadas ao servidor, incluindo
    [data_dir](Server_settings/Searchd.md#data_dir).
- O **modo simples** permite definir seus esquemas de dados em um arquivo de
  configuração, ou seja, fornece um gerenciamento de esquema **declarativo**.
  Faz sentido em três casos:
  - Quando você lida apenas com tabelas simples.
  - Ou quando seu esquema de dados é muito estável e você não precisa de
    replicação (já que ela está disponível apenas no modo RT).
  - Quando você precisa tornar seu esquema de dados portátil (por exemplo, para
    facilitar a implantação em um novo servidor).

Não é possível combinar os dois modos e é necessário decidir qual deles seguir,
especificando o [data_dir](Server_settings/Searchd.md#data_dir) no seu arquivo
de configuração (que é o comportamento padrão).
Se você não tiver certeza, **nossa recomendação é seguir o modo RT**, pois,
mesmo que precise de uma tabela simples, você pode
[criá-la](Data_creation_and_modification/Adding_data_from_external_storages/Plain_tables_creation.md)
com uma configuração de tabela simples separada e
[importá-la](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Importing_table.md)
para a sua instância principal do Manticore.

Tabelas em tempo real podem ser usadas tanto no modo RT quanto no modo simples.
No modo RT, uma tabela em tempo real é definida com um comando `CREATE TABLE`,
enquanto no modo simples ela é definida no arquivo de configuração.
Tabelas simples (offline) são suportadas apenas no modo simples.
Tabelas simples não podem ser criadas no modo RT, mas tabelas simples existentes
criadas no modo simples podem ser
[convertidas](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Attaching_one_table_to_another.md)
para tabelas em tempo real e
[importadas](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Importing_table.md)
no modo RT.

#### SQL vs JSON

O Manticore oferece várias maneiras e interfaces para gerenciar seus esquemas e
dados, mas as duas principais são:

- **SQL**.
  Esta é uma linguagem nativa do Manticore que habilita todas as funcionalidades
  do Manticore.
  **A melhor prática é usar SQL para:**
  - Gerenciar seus esquemas e realizar outras rotinas de DBA, pois é a maneira
    mais fácil de fazer isso.
  - Projetar suas consultas, pois o SQL é muito mais próximo da linguagem
    natural do que a DSL JSON, o que é importante ao projetar algo novo.
    Você pode usar o SQL do Manticore por meio de qualquer cliente MySQL ou
    [/sql](Connecting_to_the_server/MySQL_protocol.md).
- **JSON**. A maioria das funcionalidades também está disponível por meio da
  linguagem específica de domínio JSON.
  Isso é especialmente útil ao integrar o Manticore à sua aplicação, pois com
  JSON você pode fazer isso de forma mais programática do que com SQL.
  A melhor prática é **primeiro explorar como fazer algo via SQL e, em seguida,
  usar JSON para integrá-lo à sua aplicação.**

<!-- proofread -->
