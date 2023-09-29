# Resumo do curso de AWS Skill Builder - Data Analytics Fundamentals

Componentes de solução de avaliação de dados e a respectiva definição:
- Coletar;
    - Montar dados de várias fontes.
- Armazenar;
    - Manter dados em repositórios.
- Processar;
    - Manipular dados nas formas necessárias.
- Analisar;
    - Extrair dos dados informações importantes.

Os 5 V:
- **Volume** 
    - É a quantidade de dados que serão ingeridos pela solução ou, o tamanho total dos dados que ingressam.
- **Velocidade**
    - Refere-se a rapidez com que os dados entram em uma solução. A alta velocidade dos dados resulta em um tempo de análise mais curto do que o processamento de dados tradicional pode atender.
- **Variedade**
    - Refere-se ao número e tipos de fontes diferentes que a solução usará.
- **Veracidade**
    - É o grau de precisão, exatidão e confiabilidade dos dados. Ela depende da integridade e da confiabilidade dos dados.
- **Valor**
    - É a capacidade de uma solução de extrair informações significativas dos dados armazenados e analisados.

## Volume

**Dados Estruturados**: são organizados e armazenados na forma de valores que são agrupados em linhas e colunas de uma tabela.

**Dados Semiestruturados**: muitas vezes são armazenados em conjuntos de pares de chave-valor que são agrupados em elementos em um arquivo.

**Dados Não Estruturados**: não são estruturados de forma consistente. Alguns dados podem ter uma estrutura semelhante a dados semiestruturados, mas outros podem conter apenas metadados.

A AWS tem um serviço de armazenamento chamado de **Amazon Simple Storage Service** ou **Amazon S3**, é um serviço de armazenamento de objetos, o que significa que você pode armazenar praticamente qualquer tipo de objeto com dados dentro dele. Ele é escalável e pode chegar ao tamanho que você precisar, ele também implementa a escalabilidade, segurança e performance líderes do setor. As pessoas usam o Amazon S3 para sites, aplicativos para dispositivos móveis e Data Analytics.

**Buckets** são como pastas de arquivos, só que maiores, melhor organizados e com mais mecanismos de segurança. Para mover os dados para os buckets, a AWS oferece várias maneiras de fazer isso, não importando o tamanho do volume, podendo mover até exabytes de uma só vez.

Cada URL de objeto do Amazon S3 contém o bucket e a chave de objeto do item. Uma chave de objeto é o identificador exclusivo de um objeto no bucket.

Benefícios do Amazon S3:
- Armazenamento de qualquer coisa;
- Armazenamento seguro de objetos;
- Acesso HTTP nativamente on-line;
- Escalabilidade ilimitada;
- Durabilidade de 99,999999999%;

Após os dados serem armazenados no Amazon S3, você precisa de uma maneira de organizá-los pra que possa encontrá-los quando necessário, para isso usamos os *data lakes*.

O **Data Lake** é um conceito de arquitetura que ajuda você a gerenciar vários tipos de dados de fontes diferentes, tanto estruturados como não estruturados por meio de um único conjunto de ferramentas. Ele pode utilizar buckets do Amazon S3 e podemos organizar os dados em categorias dentro dele.

Um data lake é um repositório centralizado que permite armazenar dados estruturados, semiestruturados e não estruturados em qualquer escala.

Benefícios do data lake na AWS:
- São uma solução de armazenamento de dados econômica.

- Implemente a segurança e a conformidade líderes do setor.

- Permite que você aproveite muitas ferramentas diferentes de coleta e ingestão de dados para ingerir dados em seu data lake.

- Ajudam você a categorizar e gerenciar seus dados de forma simples e eficiente.

- Ajuda você a transformar dados em informações significativas.

Um **Data Warehouse** é um repositório central de dados estruturados de muitas origens de dados. Esses dados são transformados, agregados e preparados para relatórios e avaliações de negócios.

Na AWS, os frameworks **Hadoop** são implementados usando o Amazon EMR e o AWS Glue. Esses serviços implementam o framework Hadoop para consumir, transformar, analisar e mover resultados para datastores analíticos.

O **Hadoop** usa uma arquitetura de processamento distribuído, no qual uma tarefa é mapeada para um cluster de servidores convencionais para processamento. Cada bloco de trabalho distribuído aos servidores do cluster pode ser executado ou re-executado em qualquer um dos servidores. Os servidores do cluster usam frequentemente o Hadoop Distributed File System (HDFS) para armazenar dados localmente para processamento. Os resultados da computação realizada pelos servidores são reduzidos a um único conjunto de saída.

Benefícios do Apache Hadoop:

- Facilita a navegação de dados, descoberta e avaliação única de dados.

- Pode processar dados estruturados, semiestruturados ou não estruturados.

- Tem código aberto, vários projetos de ecossistema estão disponíveis para ajudar a analisar os vários tipos de dados que o Hadoop pode processar e analisar.

-  Os clusters podem processar enormes quantidades de dados de maneira econômica.

## Velocidade

O **processamento de dados** significa a coleta e a manipulação de dados para produzir informações significativas. A coleta de dados é dividida em duas partes:

- Coleta de Dados
    - Coleta de dados de várias fontes para armazenamento e avaliação de origem única.
- Processamento de Dados
    - Formatação, organização e controle de dados.


**Processamento em Batch**:
- O processamento **programado em batch** representa dados que são processados em um volume muito grande de forma programada regularmente. Por exemplo, uma vez por semana ou uma vez por dia.

- O processamento **periódico em batch** é um batch de dados processados em momentos irregulares. Essas cargas de trabalho geralmente são executadas quando uma determinada quantidade de dados é coletada.

**Processamento em Stream**:
- O processamento **quase em tempo real** representa dados de streaming que são processados em pequenos batches individuais. Os batches são constantemente coletados e processados em minutos após a geração dos dados.

- O processamento **em tempo real** representa dados de streaming que são processados em batches individuais muito pequenos. Os batches são constantemente coletados e processados em milissegundos após a geração dos dados.

O **AWS Lambda** é um serviço computacional sem servidor que pode ser usado para acionar operações de processamento em um sistema de processamento em batch.

O **Amazon EMR** é um serviço gerenciado para executar cargas de trabalho em batches altamente complexas e massivas. Esse serviço também permite operações analíticas altamente complexas.

O **Amazon Redshift** é um serviço de data warehouse gerenciado que armazena grandes quantidades de dados de transações para fins de análise.

Em um sistema de *processamento em batch*, o processamento é sempre assíncrono e o sistema de coleta e de processamento costumam ser agrupados.

Com *soluções de streaming*, o sistema de coleta e o sistema de processamento são sempre separados. Os dados de streaming usam o que chamamos de produtores de dados, cada um desses produtores pode gravar seus dados no mesmo endpoint, permitindo que vários streams de dados sejam combinados em um único stream para processamento. Outra grande vantagem é a capacidade de preservar a ordem dos dados do cliente e a capacidade de executar o consumo paralelo de dados, permitindo que múltiplos usuários trabalhem simultaneamente nos mesmos dados.

A *análise de streaming* é muito limitada. Devido ao tamanho de cada pacote de dados e à velocidade de movimentação dos dados, você está limitado à análise simples, como agregar e filtrar os dados.

O **Amazon Kinesis Data Firehose** é o serviço mais fácil para capturar, transformar e carregar streams de dados em datastores da AWS.

O **Amazon Athena** é um serviço de consultas interativas que facilita a análise de dados no Amazon S3 usando SQL padrão.

O **Amazon Kinesis Data Analytics** é responsável por agregar, filtrar e processar dados em uma solução de processamento em stream.

## Variedade

**Dados estruturados** são armazenados em um formato tabular, muitas vezes em um sistema de gerenciamento de banco de dados (DBMS). Esses dados são organizados com base em um modelo de dados relacional que define e padroniza elementos de dados e a relação deles entre si. A desvantagem dos dados estruturados é a falta de flexibilidade.

**Dados semiestruturados** são armazenados na forma de elementos em um arquivo. Esses dados são organizados com base nos elementos e atributos que os definem. Os dados semiestruturados são bastante flexíveis e capazes de escalar para atender as demandas dinâmicas de uma empresa com mais rapidez do que os dados estruturados.

**Dados não estruturados** são armazenados na forma de arquivos. Esses dados não estão em conformidade com um modelo de dados predefinido nem organizados de maneira predefinida. Dados não estruturados podem ser arquivos de texto, fotografias, gravações de áudio ou até mesmo vídeos. Dados não estruturados estão cheios de informações irrelevantes, o que significa que os arquivos precisam ser pré-processados para fazer avaliações significativas.

A *normalização* é um conjunto de regras que funcionam juntas para reduzir a redundância, aumentar a confiabilidade e melhorar a consistência do armazenamento de dados.

Um **banco de dados relacional** é criado para armazenar dados estruturados para que possam ser coletados, atualizados e consultados facilmente. Bancos de dados relacionais dependem de uma série de estruturas, chamadas de tabelas, para armazenar os dados coletados. Essas tabelas são navegadas usando a linguagem de consulta estruturada ou SQL.

Em um **sistema OLTP**, as consultas mais comuns são chamadas de consultas de pesquisa, essas consultas precisam retornar várias colunas de dados para cada registro correspondente. Nesse tipo de sistema, você pode consultar para obter detalhes de uma ordem específica.

Em um **sistema OLAP**, as consultas mais comuns são consultas agregadas, essas consultas utilizam um grande número de linhas e as reduzem a uma única linha agregando os valores em uma ou mais colunas. Nesse tipo de sistema, você pode consultar para descobrir o número total de itens vendidos em uma data específica.

Os *dados OLTP* são estruturados para fins de entrada de dados. Enquanto os *dados OLAP* são estruturados para fins de recuperação de dados.

**Bancos de dados não relacionais** são criados para armazenar dados semiestruturados e não estruturados de uma forma que ofereça rápida coleta e recuperação.

## Veracidade

A *integridade dos dados* tem a ver com garantir que seus dados sejam confiáveis. Entender o ciclo de vida completo dos seus dados e saber como protegê-los com eficácia reforçará significativamente a integridade deles.

O estágio de *compartilhamento* é aquele em que os consumidores obtêm acesso aos dados na forma de relatórios. A maioria dos consumidores terá uma boa ideia de quais números devem ser. Se os consumidores não encontrarem o que esperam, questionarão a validade dos dados.

**Integridade relacional**, garante que ambos os membros de uma relação permaneçam consistentes.

**Integridade da entidade**, garante que os valores em um campo permaneçam consistentes.

**Esquema de informações**, um banco de dados de metadados contendo informações sobre todos os objetos do banco de dados.

**Esquema lógico**, lista as restrições, relações e propriedades de tabelas e exibições em um banco de dados.

Para manter a veracidade nos dados armazenados, *consistência* é essencial. Quando dados são armazenados como arquivos, a consistência é controlada pelo aplicativo que está desenvolvendo os arquivos. Quando os dados são armazenados em um banco de dados, a consistência é responsabilidade do banco de dados que os armazena.

**ACID** é um acrônimo para *Atomicidade*, *Consistência*, *Isolamento* e *Durabilidade*. É um método para manter a consistência e a integridade em um banco de dados estruturado. O objetivo de um banco de dados compatível com ACID é retornar a versão mais recente de todos os dados e garantir que os dados inseridos no sistema atendam a todas as regras e restrições atribuídas em todos os momentos.

**BASE** é um acrônimo para *BAsicamente disponível*, *eStado flexível*, *Eventualmente consistente*. É um método para manter a consistência e a integridade em um banco de dados estruturado ou semiestruturado. O BASE promove a integridade de dados em bancos de dados não relacionais, às vezes são chamados de bancos de dados NoSQL.

Os serviços de ETL da AWS permitem transformar um tipo de origem de dados em um formato de armazenamento diferente, incluindo formatos de destino relacionais, não relacionais e baseados em arquivos.

## Valor

**Análise de informações** é o processo de análise de informações para encontrar o valor contido nelas. É uma ampla classificação de análise de dados que pode abranger tópicos que vão desde contabilidade financeira de uma empresa até a análise do número de entradas e saídas em um edifício protegido.

**Análise operacional** é uma forma de análise usada especificamente para recuperar, analisar e relatar dados para operações de TI. Esses dados incluem logs de sistema, logs de segurança, eventos e processos complexos de infraestrutura de TI, transações de usuários e até mesmo ameaças à segurança.

**Análise cognitiva** é a forma mais recente de análise de dados. Ele oferece uma oportunidade incrível de fornecer recomendações altamente especializadas para empresas sem qualquer envolvimento humano, além da configuração inicial e do treinamento dos modelos de ML.

**Análise em batch** geralmente envolve consulta a grandes quantidades de dados “frios”. A análise em batch é implementada em grandes conjuntos de dados para produzir um grande número de resultados analíticos de forma regular.

**Análise interativa** normalmente envolve a execução de consultas intrincadas em conjuntos de dados complexos em altas velocidades. Esse tipo de análise é interativo, pois permite que o usuário consulte e veja os resultados imediatamente.

**Análise em stream** exige a ingestão de uma sequência de dados e a atualização incremental de métricas, relatórios e estatísticas de resumo em resposta a cada registro de dados recebido. Esse método é mais adequado para funções de monitoramento e resposta em tempo real.

Há um processo pelo qual os dados devem passar para serem realmente valiosos, como:

- Exploração de dados - essa primeira fase geralmente faz parte do planejamento envolvido na criação de uma operação de ETL.

- Limpeza de dados - esse é o processo de normalização dos dados dentro da operação de ETL para garantir que os campos contenham os valores corretos e lidar com o problema de valores ausentes.

- Transformação de dados - essa fase envolve a aplicação de funções para manipular dados em novos formatos para fins analíticos.

- Visualização de dados - esse é o processo de criação de relatórios e painéis para apresentar o valor contido nos dados.