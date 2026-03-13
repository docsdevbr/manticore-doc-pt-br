---
# Copyright (c) 2017-2026 Manticore Software Ltd. All rights reserved.

# Documentation licensed under the GNU General Public License Version 3 or
# later.
# The original work was translated from English into Brazilian Portuguese.
# https://github.com/manticoresoftware/manticoresearch/blob/-/LICENSE

source_url: https://github.com/manticoresoftware/manticoresearch/blob/master/manual/english/Introduction.md
revision: 00868fa6cff637e121d8d81034de78ac7a64aea1
status: ready
---

# Introdução

O Manticore Search é um banco de dados de alto desempenho e com múltiplos
armazenamentos, desenvolvido especificamente para busca e análise.
Ele oferece busca de texto completo extremamente rápida, indexação em tempo real
e recursos avançados, como busca vetorial e armazenamento colunar, para uma
análise de dados eficiente.
Projetado para lidar com conjuntos de dados de pequeno e grande porte, ele
oferece escalabilidade perfeita e compreensões poderosas para aplicações
modernas.

Como um banco de dados de código aberto (disponível no
[GitHub](https://github.com/manticoresoftware/manticoresearch/)), o Manticore
Search foi criado em 2017 como uma continuação do mecanismo de busca
[Sphinx Search](https://sphinxsearch.com/).
Nosso time de desenvolvimento aproveitou todos os melhores recursos do Sphinx e
aprimorou significativamente sua funcionalidade, corrigindo centenas de falhas
ao longo do processo (conforme detalhado em nosso
[Changelog](https://manual.manticoresearch.com/Changelog)).
O Manticore Search é um banco de dados moderno, rápido e leve, com recursos
excepcionais de busca em texto completo, construído a partir de uma reescrita
quase completa de seu antecessor.

## Os principais recursos do Manticore são:

### Busca de texto completo poderosa e rápida, que funciona bem para conjuntos de dados pequenos e grandes

- [Complemento automático de consultas](Searching/Autocomplete.md)
- [Busca fuzzy](Searching/Spell_correction.md#Fuzzy-Search)
- Mais de 20 [operadores de texto completo](https://play.manticoresearch.com/fulltextintro/)
  e mais de 20 fatores de classificação
- [Classificação personalizada](Searching/Sorting_and_ranking.md#Ranking-overview)
- [Stemming](Creating_a_table/NLP_and_tokenization/Morphology.md)
- [Lemmatização](Creating_a_table/NLP_and_tokenization/Morphology.md)
- [Palavras irrelevantes](Creating_a_table/NLP_and_tokenization/Ignoring_stop-words.md)
- [Sinônimos](Creating_a_table/NLP_and_tokenization/Exceptions.md)
- [Formas de palavras](Creating_a_table/NLP_and_tokenization/Wordforms.md)
- [Tokenização avançada em nível de caractere e palavra](Creating_a_table/NLP_and_tokenization/Low-level_tokenization.md)
- [Segmentação adequada de chinês](Creating_a_table/NLP_and_tokenization/Languages_with_continuous_scripts.md)
- [Realce de texto](Searching/Highlighting.md)

### Recursos de busca vetorial

O Manticore Search oferece suporte à capacidade de adicionar embeddings gerados
por seus modelos de Machine Learning a cada documento e, em seguida, realizar
uma [busca por vizinho mais próximo](Searching/KNN.md) neles.
Isso permite criar recursos como busca por similaridade, recomendações, busca
semântica e classificação por relevância com base em algoritmos de PNL, entre
outros, incluindo buscas por imagem, vídeo e áudio.

### JOIN

O Manticore Search oferece suporte a consultas [JOIN](Searching/Joining.md) via
SQL e JSON, permitindo combinar dados de várias tabelas.

### Multithreading

O Manticore Search utiliza uma paralelização inteligente de consultas para
reduzir o tempo de resposta e utilizar totalmente todos os núcleos da CPU quando
necessário.

### Otimizador de consultas baseado em custo

O otimizador de consultas baseado em custo utiliza dados estatísticos sobre os
dados indexados para avaliar os custos relativos de diferentes planos de
execução para uma determinada consulta.
Isso permite que o otimizador determine o plano mais eficiente para recuperar os
resultados desejados, levando em consideração fatores como o tamanho dos dados
indexados, a complexidade da consulta e os recursos disponíveis.

### Opções de armazenamento

O Manticore oferece
[opções de armazenamento orientadas a linhas e colunas](Creating_a_table/Data_types.md#Row-wise-and-columnar-attribute-storages)
para acomodar conjuntos de dados de vários tamanhos.
A opção de armazenamento tradicional e padrão orientada a linhas está disponível
para conjuntos de dados de todos os tamanhos - pequenos, médios e grandes,
enquanto a opção de armazenamento em colunas é fornecida pela Biblioteca Colunar
do Manticore para conjuntos de dados ainda maiores.
A principal diferença entre essas opções de armazenamento é que o armazenamento
em linhas exige que todos os atributos (exceto os campos de texto completo)
sejam mantidos na RAM para um desempenho ideal, enquanto o armazenamento em
colunas não exige isso, oferecendo assim menor consumo de RAM, mas com potencial
para desempenho ligeiramente mais lento (como demonstrado pelas estatísticas em
https://db-benchmarks.com/).

### Índices secundários automáticos

A
[Biblioteca Colunar do Manticore](https://github.com/manticoresoftware/columnar/)
utiliza o
[Índice de Modelo Geométrico por Partes](https://github.com/gvinciguerra/PGM-index),
que explora um mapeamento aprendido entre as chaves indexadas e sua localização
na memória.
A concisão desse mapeamento, aliada a um algoritmo de construção recursivo
peculiar, torna o índice PGM uma estrutura de dados que supera os índices
tradicionais em termos de espaço, oferecendo ainda o melhor desempenho em tempo
de consulta e atualização.
Os índices secundários estão ATIVADOS por padrão para todos os campos numéricos
e de texto e podem ser habilitados para atributos JSON.

### SQL em primeiro lugar

A sintaxe nativa do Manticore é SQL e ele suporta SQL sobre HTTP e protocolo
MySQL, permitindo a conexão por meio de clientes MySQL populares em qualquer
linguagem de programação.

### JSON sobre HTTP

Para uma abordagem mais programática ao gerenciamento de dados e esquemas, o
Manticore fornece o protocolo
[HTTP JSON](Searching/Full_text_matching/Basic_usage.md#HTTP-JSON), semelhante
ao do Elasticsearch.

### Escritas compatíveis com Elasticsearch

Você pode executar consultas JSON de
[inserção](Data_creation_and_modification/Adding_documents_to_a_table/Adding_documents_to_a_real-time_table.md#Adding-documents-to-a-real-time-table)
e
[substituição](Data_creation_and_modification/Updating_documents/REPLACE.md#REPLACE)
compatíveis com Elasticsearch, o que permite usar o Manticore com ferramentas
como Logstash (versão < 7.13), Filebeat e outras ferramentas da família Beats.

### Gerenciamento declarativo e imperativo de esquemas

Crie, atualize e exclua tabelas facilmente online ou por meio de um arquivo de
configuração.

### Os benefícios do C++ e a conveniência do PHP

O daemon de pesquisa do Manticore é desenvolvido em C++, oferecendo tempos de
inicialização rápidos e utilização eficiente de memória.
Otimizações de baixo nível aprimoram ainda mais o desempenho.
Outro componente crucial, chamado
[Manticore Buddy](https://github.com/manticoresoftware/manticoresearch-buddy), é
escrito em PHP e utilizado para funcionalidades de alto nível que não exigem
tempos de resposta extremamente rápidos ou poder de processamento muito elevado.
Embora contribuir para o código C++ possa representar um desafio, adicionar um
novo comando SQL/JSON usando o Manticore Buddy deve ser um processo simples.

### Inserções em tempo real

Documentos recém-adicionados ou atualizados podem ser lidos imediatamente.

### Cursos interativos para facilitar o aprendizado

Oferecemos [cursos interativos gratuitos](https://play.manticoresearch.com/)
para tornar o aprendizado fácil.

### Transações

Embora o Manticore não seja totalmente compatível com ACID, ele oferece suporte
a transações isoladas para alterações atômicas e logging binário para gravações
seguras.

### Replicação e balanceamento de carga integrados

Os dados podem ser distribuídos entre servidores e data centers, com qualquer nó
do Manticore Search atuando como balanceador de carga e nó de dados.
O Manticore implementa
[replicação](https://play.manticoresearch.com/replication/) multi-mestre
virtualmente síncrona usando a [biblioteca Galera](https://galeracluster.com/),
garantindo a consistência dos dados em todos os nós, evitando perda de dados e
proporcionando desempenho de replicação excepcional.

### Recursos de backup integrados

O Manticore está equipado com uma ferramenta externa
[manticore-backup](Securing_and_compacting_a_table/Backup_and_restore.md) e o
comando SQL
[BACKUP](Securing_and_compacting_a_table/Backup_and_restore.md#BACKUP-SQL-command-reference)
para simplificar o processo de backup e restauração de seus dados.
Como alternativa, você pode usar o
[mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) para
[fazer backups lógicos](Securing_and_compacting_a_table/Backup_and_restore.md#Backup-and-restore-with-mysqldump).

### Sincronização de dados pronta para uso

A ferramenta `indexer` e a sintaxe de configuração abrangente do Manticore
facilitam a sincronização de dados de fontes como MySQL, PostgreSQL, bancos de
dados compatíveis com ODBC, XML e CSV.

### Opções de integração

Você pode integrar o Manticore Search com um servidor MySQL/MariaDB usando a
[engine FEDERATED](Extensions/FEDERATED.md) ou via
[ProxySQL](https://manticoresearch.com/blog/using-proxysql-to-route-inserts-in-a-distributed-realtime-index/).

Você pode usar o
[Apache Superset](https://manticoresearch.com/blog/manticoresearch-apache-superset-integration/)
e o
[Grafana](https://manticoresearch.com/blog/manticoresearch-grafana-integration/)
para visualizar os dados armazenados no Manticore.
Diversas ferramentas MySQL podem ser usadas para desenvolver consultas
interativas ao Manticore, como o [HeidiSQL](https://www.heidisql.com/) e o
[DBForge](https://www.devart.com/dbforge/).

Você também pode usar o Manticore Search com o [Kibana](Integration/Kibana.md).

### Filtragem de fluxos facilitada

O Manticore oferece um tipo de tabela especial, a tabela
"[percolate](Creating_a_table/Local_tables/Percolate_table.md)", que permite
pesquisar consultas em vez de dados, tornando-a uma ferramenta eficiente para
filtrar fluxos de dados de texto completo.
Basta armazenar suas consultas na tabela, processar seu fluxo de dados enviando
cada lote de documentos para o Manticore Search e receber apenas os resultados
que correspondem às suas consultas armazenadas.

### Possíveis aplicações

O Manticore Search é versátil e pode ser aplicado em diversos cenários,
incluindo:

- **Busca de texto completo**:
  - Ideal para plataformas de e-commerce, permitindo buscas rápidas e precisas
    de produtos com recursos como autocompletar e busca aproximada.
  - Perfeito para sites com grande volume de conteúdo, permitindo que as pessoas
    usuárias encontrem rapidamente artigos ou documentos relevantes.

- **Análise de dados**:
  - Ingestão de dados no Manticore Search usando
    [Beats/Logstash](https://manticoresearch.com/blog/integration-of-manticore-with-logstash-filebeat/),
    [Vector.dev](https://manticoresearch.com/blog/integration-of-manticore-with-vectordev/)
    e
    [Fluentbit](https://manticoresearch.com/blog/integration-of-manticore-with-fluentbit/).
  - Análise eficiente de grandes conjuntos de dados utilizando o armazenamento
    colunar e os recursos OLAP do Manticore.
  - Execute consultas complexas em terabytes de dados com latência mínima.
  - Visualize dados usando Kibana,
    [Grafana](https://manticoresearch.com/blog/manticoresearch-grafana-integration/)
    ou
    [Apache Superset](https://manticoresearch.com/blog/manticoresearch-apache-superset-integration/).

- **Busca refinada**:
  - Permita que as pessoas usuárias filtrem os resultados da busca por
    categorias, como preço, marca ou data, para uma experiência de busca mais
    precisa.

- **Busca geoespacial**:
  - Implemente buscas baseadas em localização, como encontrar restaurantes ou
    lojas próximas, com os recursos geoespaciais do Manticore.

- **Correção ortográfica**:
  - Corrija automaticamente erros de digitação nas consultas de busca para
    melhorar a precisão e a experiência da pessoa usuária.

- **Preenchimento automático**:
  - Forneça sugestões em tempo real enquanto as pessoas usuárias digitam,
    aprimorando a usabilidade e a velocidade da busca.

- **Filtragem de fluxo de dados**:
  - Utilize tabelas de percolação para filtrar e processar fluxos de dados em
    tempo real, como feeds de mídias sociais ou dados de log, de forma
    eficiente.

## Requisitos

- Arquitetura: arm64 ou x86_64
- SO: baseado em Debian (por exemplo, Debian, Ubuntu, Mint), baseado em RHEL
  (por exemplo, RHEL, CentOS, Alma, Oracle Linux, Amazon Linux), Windows ou
  MacOS.
- A
  [Biblioteca Colunar Manticore](https://github.com/manticoresoftware/columnar),
  que fornece
  [armazenamento colunar](Creating_a_table/Data_types.md#Row-wise-and-columnar-attribute-storages)
  e
  [índices secundários](Introduction.md#Automatic-secondary-indexes), requer uma
  CPU com SSE >= 4.2.
- Não há requisitos específicos de espaço em disco ou RAM.
  Uma instância vazia do Manticore Search utiliza apenas cerca de 40 MB de RAM
  RSS.

<!-- proofread -->
