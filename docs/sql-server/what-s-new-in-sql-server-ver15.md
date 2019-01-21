---
title: Novidades no SQL Server 2019 | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e0a5dab4eeccc5c4e31a151ec9611d7ed8367a78
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54300173"
---
# <a name="whats-new-in-sql-server-2019"></a>Novidades no SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  > [!div class="nextstepaction"]
  > [Compartilhe seus comentários sobre o Sumário do SQL Docs!](https://aka.ms/sqldocsurvey)

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se baseia em versões anteriores para ampliar o SQL Server como uma plataforma que fornece opções de linguagens de desenvolvimento, tipos de dados, operações locais ou na nuvem e sistemas operacionais. Este artigo resume o que há de novo para o SQL Server 2019. Para obter mais informações e ver os problemas conhecidos, consulte as [Notas sobre a versão do SQL Server 2019](sql-server-ver15-release-notes.md).

**Experimente o SQL Server 2019!**
- [![Baixar no Centro de Avaliação](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [Baixar o SQL Server 2019 para instalar no Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- Instalar no Linux para [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) e [Ubuntu](../linux/quickstart-install-connect-ubuntu.md).
- [Executar no SQL Server 2019 no Docker](../linux/quickstart-install-connect-docker.md).

## <a name="ctp-22"></a>CTP 2.2

A versão prévia do CTP (Community Technology Preview) 2.2 é a última versão pública do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Esta versão inclui aprimoramentos de versões CTP anteriores para corrigir bugs, melhorar a segurança e otimizar o desempenho. Além disso, os recursos a seguir foram adicionados ou aprimorados no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.2.

- [Clusters de Big Data](#bigdatacluster)
  - Usar o SparkR do Azure Data Studio em um cluster de Big Data

- [Mecanismo de banco de dados](#databaseengine)
  - Use a codificação de caracteres UTF-8 com replicação do SQL Server.

## <a name="previous-ctps"></a>CTPs anteriores

Versões anteriores de CTP adicionaram ou aprimoraram os recursos a seguir para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

- [Clusters de Big Data](#bigdatacluster) 
  - Implantar um cluster de Big Data com contêineres SQL e Spark Linux no Kubernetes (CTP 2.0)
  - Acessar Big Data do HDFS (CTP 2.0)
  - Executar análises avançadas e aprendizado de máquina com o Spark (CTP 2.0)
  - Usar o Spark para fazer streaming de dados para pools de dados SQL (CTP 2.0)
  - Usar o Azure Data Studio para executar livros de consulta que fornecem uma experiência de notebook (CTP 2.0)
  - Implantar aplicativos Python e R (CTP 2.1)

- [Mecanismo de banco de dados](#databaseengine)
  - Suporte a UTF-8 (CTP 2.0)
  - A criação de índice online retomável permite que a criação de índice seja retomada após uma interrupção (CTP 2.0)
  - Build e recompilação de índice online de columnstore em cluster (CTP 2.0)
  - Always Encrypted com enclaves seguros (CTP 2.0)
  - Processamento de consulta inteligente (CTP 2.0)
  - Extensão de programação de linguagem Java (CTP 2.0)
  - Recursos do SQL Graph (CTP 2.0)
  - Definição de configuração com escopo de banco de dados para operações de DDL online e retomáveis (CTP 2.0)
  - Grupos de Disponibilidade Always On – redirecionamento de conexão da réplica secundária (CTP 2.0)
  - Descoberta de dados e classificação – incorporado ao SQL Server de maneira nativa (CTP 2.0)
  - Suporte estendido para dispositivos de memória persistentes (CTP 2.0)
  - Suporte para estatísticas de columnstore em `DBCC CLONEDATABASE` (CTP 2.0)
  - Novas opções adicionadas a `sp_estimate_data_compression_savings` (CTP 2.0)
  - Cluster de failover dos Serviços do Machine Learning do SQL Server (CTP 2.0)
  - Infraestrutura de perfil de consulta leve habilitada por padrão (CTP 2.0)
  - Novos conectores de PolyBase (CTP 2.0)
  - Nova função de sistema `sys.dm_db_page_info` retorna informações da página (CTP 2.0)
  - O processamento de consulta inteligente adiciona inlining do UDF escalar (CTP 2.1)
  - Mensagem de erro de truncamento aprimorada para incluir nomes de tabela e coluna e o valor truncado (CTP 2.1)
  - Suporte a agrupamentos UTF-8 na instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (CTP 2.1)
  - Usar aliases de exibição ou tabela derivada em consultas de correspondência de gráfico (CTP 2.1)
  - Dados de diagnóstico aprimorados para estatísticas de bloqueio (CTP 2.1)
  - Pool de buffers híbrido (CTP 2.1)
  - Mascaramento de dados estáticos (CTP 2.1)

- [SQL Server no Linux](#sqllinux)
  - Suporte para replicação (CTP 2.0)
  - Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) (CTP 2.0)
  - Grupos de Disponibilidade Always On em contêineres do Docker com Kubernetes (CTP 2.0)
  - Suporte para OpenLDAP para provedores de AD de terceiros (CTP 2.0)
  - Machine Learning no Linux (CTP 2.0)
  - Novo registro de contêiner (CTP 2.0)
  - Novas imagens de contêiner baseadas em RHEL (CTP 2.0)
  - Notificação de pressão de memória (CTP 2.0)

- [Master Data Services](#mds)
  - Substituição dos controles do Silverlight (CTP 2.0)

- [Segurança](#security)
  - Gerenciamento de certificados no SQL Server Configuration Manager (CTP 2.0)

- [Ferramentas](#tools)
  - SQL Server Management Studio (SSMS) 18.0 (versão prévia) (CTP 2.0)
  - Azure Data Studio (CTP 2.0)
  - Azure Data Studio (CTP 2.1)

Continue lendo para conhecer mais detalhes desses recursos.

## <a id="bigdatacluster"></a>Clusters de Big Data

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [Clusters de Big Data](../big-data-cluster/big-data-cluster-overview.md) permitem novos cenários, incluindo o seguinte:

- Usar o SparkR do Azure Data Studio em um cluster de Big Data. (CTP 2.2)
- [Implantar aplicativos Python e R](../big-data-cluster/big-data-cluster-create-apps.md). (CTP 2.1)
- Implantar um cluster de Big Data com contêineres Spark Linux e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Kubernetes (CTP 2.0)
- Acessar Big Data do HDFS (CTP 2.0)
- Executar análises avançadas e aprendizado de máquina com o Spark (CTP 2.0)
- Usar o Spark para fazer streaming de dados para pools de dados SQL (CTP 2.0)
- Executar livros de consulta que fornecem uma experiência de notebook no [**Azure Data Studio**](../sql-operations-studio/what-is.md). (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> Mecanismo de Banco de Dados

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz ou aprimora os seguintes recursos novos para o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]

### <a name="scalar-udf-inlining-ctp-21"></a>Inlining do UDF escalar (CTP 2.1)

O inlining do UDF escalar transforma automaticamente funções definidas pelo usuário (UDF) escalares em expressões relacionais e as insere na consulta SQL de chamada, melhorando o desempenho de cargas de trabalho que aproveitam UDFs escalares. O inlining do UDF escalar possibilita a otimização baseada em custo de operações em UDFs e resulta em planos eficientes que são orientados ao conjunto e paralelos, em vez de planos de execução seriais ineficientes e iterativos. Esse recurso é habilitado por padrão no nível de compatibilidade do banco de dados 150.

Para saber mais, confira [Scalar UDF Inlining](../relational-databases/user-defined-functions/scalar-udf-inlining.md) (Embutimento de UDF escalar).

### <a name="truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a>Mensagem de erro de truncamento aprimorada para incluir nomes de tabela e coluna e o valor truncado (CTP 2.1)

A mensagem de erro com ID 8152 `String or binary data would be truncated` é familiar para muitos desenvolvedores e administradores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que desenvolvem ou mantêm cargas de trabalho de movimentação de dados. O erro é gerado durante transferências de dados entre uma origem e um destino com esquemas diferentes quando os dados de origem são muito grandes para caber no tipo de dados de destino. Essa mensagem de erro pode ter resolução demorada. O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta uma mensagem de erro nova e mais específica (2628) para esse cenário:  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

A nova mensagem de erro 2628 fornece mais contexto para o problema de truncamento de dados, simplificando o processo de solução de problemas. Para o CTP 2.1 e CTP 2.2, essa é uma mensagem de erro para aceitação e requer que o [sinalizador de rastreamento](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 esteja habilitado.

### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>Dados de diagnóstico aprimorados para estatísticas de bloqueio (CTP 2.1)

A [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] fornece dados de diagnóstico aprimorados para consultas de longa execução que esperam operações de atualização de estatísticas síncronas. O modo de exibição de gerenciamento dinâmico `sys.dm_exec_requests` de coluna `command` mostra `SELECT (STATMAN)` se um `SELECT` está aguardando até que uma operação de atualização de estatísticas síncronas seja concluída antes de continuar a execução da consulta.  Além disso, o novo tipo de espera `WAIT_ON_SYNC_STATISTICS_REFRESH` será exposto no modo de exibição de gerenciamento dinâmico `sys.dm_os_wait_stats`. Ele mostra o tempo de nível de instância acumulado gasto em operações de atualização de estatísticas síncronas.

### <a name="static-data-masking-ctp-21"></a>Mascaramento de dados estáticos (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz o mascaramento de dados estáticos. Você pode usar o de mascaramento dados estáticos para limpar dados confidenciais em cópias de bancos de dados do SQL Server. O mascaramento de dados estáticos ajuda a criar uma cópia limpa de bancos de dados em que todas as informações confidenciais são alteradas de forma a tornar a cópia compartilhável com usuários de não produção. O mascaramento de dados estáticos pode ser usado para desenvolvimento, teste, análise e relatórios de negócios, conformidade, solução de problemas e qualquer outro cenário em que dados específicos não possam ser copiados para ambientes diferentes.

O mascaramento de dados estáticos opera no nível de coluna. Selecione quais colunas mascarar e, para cada coluna selecionada, especifique uma função de mascaramento. O mascaramento de dados estáticos copia o banco de dados e, em seguida, aplica as funções de mascaramento especificadas às colunas.

#### <a name="static-data-masking-vs-dynamic-data-masking"></a>Mascaramento de dados estáticos versus mascaramento de dados dinâmicos

O mascaramento de dados é o processo de aplicação de uma máscara a um banco de dados para ocultar informações confidenciais e substituí-la por dados novos ou dados limpos. A Microsoft oferece duas opções de mascaramento: o mascaramento de dados estáticos e o mascaramento de dados dinâmicos. A Máscara de Dados Dinâmicos foi introduzida no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A seguinte tabela compara essas duas soluções:

|Mascaramento de dados estáticos |Mascaramento de dados dinâmicos|
|:----|:----|
|Ocorre em uma cópia do banco de dados <br/><br/>Dados originais não recuperáveis<br/><br/>O mascaramento ocorre no nível de armazenamento<br/><br/>Todos os usuários têm acesso aos mesmos dados mascarados<br/><br/>Voltado para o acesso contínuo de toda a equipe|Ocorre no banco de dados original<br/><br/>Dados originais intactos<br/><br/>O mascaramento ocorre dinamicamente no momento da consulta<br/><br/>O mascaramento varia com base na permissão do usuário <br/><br/>Voltado para o acesso específico de usuário pontual|

### <a name="database-compatibility-level-ctp-20"></a>Nível de compatibilidade de banco de dados (CTP 2.0)

**COMPATIBILITY_LEVEL 150** do banco de dados adicionado. Para habilitar um banco de dados de usuário específico, execute:

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="utf-8-support-ctp-22"></a>Suporte a UTF-8 (CTP 2.2)

Suporte completo para a amplamente utilizada codificação de caracteres UTF-8 como codificação de importação ou exportação, ou como ordenação em nível de banco de dados ou nível de coluna para dados de texto. A UTF-8 é permitida nos tipos de dados `CHAR` e `VARCHAR` e é habilitada quando você cria ou altera a ordenação de um objeto para uma ordenação com o sufixo `UTF8`. 

Por exemplo, `LATIN1_GENERAL_100_CI_AS_SC` para `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. A UTF-8 só está disponível para agrupamentos do Windows com suporte para caracteres suplementares, conforme introduzido no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. `NCHAR` e `NVARCHAR` permitem somente a codificação UTF-16 e permanecem inalterados.

Esse recurso pode fornecer economia de armazenamento significativa dependendo do conjunto de caracteres utilizado. Por exemplo, a alteração de um tipo de dados de coluna existente com cadeias de caracteres Latinas de `NCHAR(10)` para `CHAR(10)` usando uma ordenação habilitada para UTF-8 resulta em 50% de redução nos requisitos de armazenamento. Essa redução ocorre porque `NCHAR(10)` exige 20 bytes para armazenamento, enquanto `CHAR(10)` requer 10 bytes para a mesma cadeia de caracteres Unicode.

Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../relational-databases/collations/collation-and-unicode-support.md).

O CTP 2.1 adiciona suporte para selecionar a ordenação de UTF-8 como padrão durante a instalação do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

O CTP 2.2 adiciona suporte para codificação de caracteres UTF-8 com replicação do SQL Server.

### <a name="resumable-online-index-create-ctp-20"></a>Criação de índice online retomável (CTP 2.0)

- A **criação de índice online retomável** permite que uma operação de criação de índice fique em pausa e seja retomada posteriormente do ponto em que a operação parou ou falhou, em vez de reiniciar desde o início.

  A criação de índice online retomável dá suporte aos cenários a seguir:
  - retomar uma operação de criação de índice após uma falha na criação do índice, por exemplo, após um failover do banco de dados ou após faltar espaço em disco.
  - pausar uma operação de criação de índice em andamento e retomá-la mais tarde permitindo a liberação temporária de recursos, conforme necessário.
  - criar índices grandes sem usar muito espaço de log e uma transação de execução longa que bloqueia outras atividades de manutenção e permite o truncamento de log.

  No caso de falha na criação de um índice, sem esse recurso, uma operação de criação de índice online deve ser executada novamente e a operação deve ser reiniciada desde o início.

Com esta versão, estendemos a funcionalidade retomável adicionando o recurso à [recompilação de índice online retomável](https://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/).

Além disso, esse recurso pode ser definido como padrão para um banco de dados específico usando a [configuração padrão de escopo do banco de dados para operações de DDL online e retomáveis](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Para obter mais informações, consulte [Criação de índice online retomável](../t-sql/statements/create-index-transact-sql.md#resumable-indexes).

### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>Compilar e recompilar índices de columnstore em cluster online (CTP 2.0)

Converta tabelas de repositório de linha no formato columnstore. A criação de CCIs (índices columnstore clusterizados) era um processo offline nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] – exigindo que todas as alterações parassem enquanto o CCI era criado. Com o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e o [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)], você pode criar ou recriar CCI online. A carga de trabalho não será bloqueada e todas as alterações feitas nos dados subjacentes serão adicionadas de maneira transparente à tabela de destino de columnstore. Exemplos de novas instruções [!INCLUDE[tsql](../includes/tsql-md.md)] que podem ser usadas são:

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>Always Encrypted com enclaves seguros (CTP 2.0)

Expande o Always Encrypted com criptografia no local e cálculos avançados. As expansões são decorrentes da habilitação de cálculos em dados de texto sem formatação, dentro de um enclave seguro no lado do servidor.

Operações de criptografia incluem a criptografia de colunas e a rotação de chaves de criptografia de coluna. Agora, essas operações podem ser emitidas usando [!INCLUDE[tsql](../includes/tsql-md.md)] e não exigem que os dados sejam movidos para fora do banco de dados. Enclaves seguros fornecem o Always Encrypted para um conjunto mais amplo de cenários que têm os dois requisitos a seguir:  

- a demanda que dados confidenciais sejam protegidos contra usuários de alto privilégio, porém não autorizados, incluindo administradores de banco de dados, administradores do sistema, operadores de nuvem ou malware.
- o requisito de que cálculos avançados em dados protegidos tenham suporte dentro do sistema de banco de dados.

Para conhecer detalhes, consulte [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).

> [!NOTE]
> O Always Encrypted com enclaves seguros está disponível apenas no SO Windows.

### <a name="intelligent-query-processing-ctp-20"></a>Processamento de consulta inteligente (CTP 2.0)

- **Feedback de concessão de memória no modo de linha** expande o recurso de feedback de concessão de memória introduzido no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], ajustando os tamanhos da concessão de memória para os operadores de modo de lote e de linha.  Para uma condição de concessão excessiva, se a memória concedida tiver mais de duas vezes o tamanho da memória real usada, o feedback de concessão de memória recalculará a concessão de memória. As execuções consecutivas, em seguida, solicitarão menos memória. Para uma concessão de memória de tamanho insuficiente que resulta em um despejo no disco, o feedback de concessão de memória acionará o recálculo da concessão de memória. As execuções consecutivas, em seguida, solicitarão mais memória. Esse recurso é habilitado por padrão no nível de compatibilidade do banco de dados 150.

- **COUNT DISTINCT aproximado** retorna o número aproximado de valores não nulos exclusivos em um grupo. Essa função foi criada para uso em cenários de Big Data. Essa função é otimizada para consultas em que todas as seguintes condições forem verdadeiras:
   - acesso a conjuntos de dados com pelo menos milhões de linhas.
   - agregação de uma coluna ou colunas com grande número de valores distintos.
   - a capacidade de resposta é mais crítica que a precisão absoluta.
      - `APPROX_COUNT_DISTINCT` retorna resultados que normalmente estão dentro de 2% da resposta precisa.
      - E retorna a resposta aproximada em uma pequena fração do tempo necessário para a resposta precisa.

- **O modo de lote em rowstore** não requer mais um índice columnstore para processar uma consulta no modo de lote. O modo de lote permite que operadores de consulta funcionem em um conjunto de linhas, em vez de apenas uma linha por vez. Esse recurso é habilitado por padrão no nível de compatibilidade do banco de dados 150. O modo de lote aumenta a velocidade de consultas que acessam tabelas de rowstore quando todos os itens a seguir são verdadeiras:
   - a consulta usa operadores analíticos como junções ou operadores de agregação.
   - a consulta envolve 100.000 linhas ou mais.
   - a consulta é limitada pela CPU, em vez de ser limitada por dados de entrada/saída.
   - a criação e uso de um índice columnstore teria uma das seguintes desvantagens:
      - adicionaria muita sobrecarga à consulta.
      - ou não é viável porque seu aplicativo depende de um recurso que ainda não tem suporte de índices columnstore.

- **A compilação adiada de variável da tabela** melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e compilação inicial, esse recurso propagará estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela.  Essas informações de contagem de linha precisas serão ser usadas para otimizar operações de plano de downstream. Esse recurso é habilitado por padrão no nível de compatibilidade do banco de dados 150.

Para usar recursos de processamento de consulta inteligente, defina o banco de dados `COMPATIBILITY_LEVEL = 150`.

### <a id="programmability"></a> Extensões de programação de linguagem Java (CTP 2.0)

- **Extensão da linguagem Java (versão prévia)**: Use a extensão da linguagem Java para executar o código Java em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], esta extensão é instalada quando você adiciona o recurso 'Serviços do Machine Learning (No Banco de Dados)' à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

### <a id="sqlgraph"></a> Recursos do SQL Graph

- **Usar aliases de tabela derivada ou exibição na consulta de correspondência de gráfico (CTP 2.1)** Consultas do Graph na versão prévia do SQL Server 2019 dão suporte ao uso de aliases de tabela derivada e exibição na sintaxe `MATCH`. Para usar esses aliases no `MATCH`, as exibições e as tabelas derivadas devem ser criadas em um conjunto de nós ou em um conjunto de tabelas de borda, usando o operador `UNION ALL`. As tabelas de nós ou de borda podem ou não ter filtros nelas. A capacidade de usar aliases de tabela derivada e exibição em consultas `MATCH` pode ser muito útil em cenários em que você deseja consultar entidades heterogêneas ou conexões heterogêneas entre duas ou mais entidades no gráfico.

- **O suporte a correspondência em `MERGE` DML (CTP 2.0)** permite que você especifique relações de gráfico em uma única instrução, em vez de instruções `INSERT`, `UPDATE` ou `DELETE` separadas. Mescle seus dados de gráfico atuais de tabelas de nó ou de borda com novos dados usando os predicados `MATCH` na instrução `MERGE`. Esse recurso permite cenários de `UPSERT` nas tabelas de borda. Agora, os usuários podem usar uma única instrução merge para inserir uma nova borda ou atualizar uma existente entre dois nós.

- **Restrições de borda (CTP 2.0)** são introduzidas para tabelas de borda no SQL Graph. Tabelas de borda podem conectar qualquer nó a qualquer outro nó no banco de dados. Com a introdução das restrições de borda, agora você pode aplicar algumas restrições a esse comportamento. A nova restrição `CONNECTION` pode ser usada para especificar o tipo de nós a que uma determinada tabela de borda terá permissão para se conectar no esquema.

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations--ctp-20"></a>Configuração padrão com escopo de banco de dados para operações de DDL online e retomáveis (CTP 2.0)

- **A configuração padrão com escopo de banco de dados para operações de DDL online e retomáveis** permite a configuração de um comportamento padrão para operações de índice `ONLINE` e `RESUMABLE` no nível do banco de dados, em vez de definir essas opções para cada instrução DDL de índice individual, como criar ou recompilar o índice.

- Defina esses padrões usando as opções de configuração de escopo do banco de dados `ELEVATE_ONLINE` e `ELEVATE_RESUMABLE`. Ambas as opções farão com que o mecanismo eleve automaticamente as operações com suporte para execução online ou retomável. Você pode habilitar os seguintes comportamentos usando essas opções:

  - a opção `FAIL_UNSUPPORTED` permite todas as operações de índice online ou operações de índice retomáveis e com falha que não têm suporte para a opção online ou retomável.
  - a opção `WHEN_SUPPPORTED` permite operações com suporte online ou operações sem suporte de retomáveis e de execução de índice offline ou não retomáveis.
  - a opção `OFF` permite o comportamento atual de executar todas as operações de índice offline e não retomáveis a menos que explicitamente especificado na instrução DDL.

Para substituir a configuração padrão, inclua a opção `ONLINE` ou `RESUMABLE` nos comandos de criação e recompilação do índice.  

Sem esse recurso, você precisa especificar as opções online e retomáveis diretamente na instrução DDL do índice, como criar e recompilar índice.

Para obter mais informações sobre operações retomáveis de índice, consulte [Criação de índice online retomável](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/).

### <a id="ha"></a>Grupos de Disponibilidade Always On – mais réplicas síncronas (CTP 2.0)

- **Até cinco réplicas síncronas**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta o número máximo de réplicas síncronas para 5, de até de 3 no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] . Você pode configurar esse grupo de 5 réplicas para ter failover automático dentro do grupo. Há 1 réplica primária, além de 4 réplicas secundárias síncronas.

- **Redirecionamento de conexão de réplica secundária para primária**: Permite que conexões do aplicativo cliente sejam direcionadas para a réplica primária, independentemente do servidor de destino especificado na cadeia de conexão. Esse recurso permite o redirecionamento de conexão sem um ouvinte. Use o redirecionamento de conexão de réplica secundária para primária nos seguintes casos:

  - a tecnologia de cluster não oferece um recurso de ouvinte.
  - uma configuração de várias sub-redes em que o redirecionamento se torna complexo.
  - cenários de expansão de leitura ou de recuperação de desastre em que o tipo de cluster é `NONE`.

Para conhecer os detalhes, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redirecionamento de conexão de leitura/gravação de réplica secundária para primária [Grupos de Disponibilidade Always On]).

### <a name="data-discovery-and-classification-ctp-20"></a>Descoberta e classificação de dados (CTP 2.0)

A descoberta e classificação de dados fornece recursos avançados que são internos e nativos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Classificar e rotular seus dados mais confidenciais fornece os seguintes benefícios:
- ajuda a atender a padrões de privacidade de dados e requisitos de conformidade regulamentar.
- dá suporte a cenários de segurança, como monitoramento (auditoria) e alertas sobre acesso anômalo a dados confidenciais.
- torna mais fácil identificar onde os dados confidenciais residem na empresa, para que os administradores possam adotar as etapas corretas para proteger o banco de dados.

Para obter mais informações, consulte [Descoberta e classificação de dados SQL](../relational-databases/security/sql-data-discovery-and-classification.md).

A [auditoria](../relational-databases/security/auditing/sql-server-audit-database-engine.md) também foi aprimorada para incluir um novo campo no log de auditoria chamado `data_sensitivity_information`, que registra a classificações (rótulos) de confidencialidade dos dados reais que foram retornados pela consulta. Para obter detalhes e exemplos, consulte [Adicionar classificação de confidencialidade](../t-sql/statements/add-sensitivity-classification-transact-sql.md).

>[!NOTE]
>Não há nenhuma alteração em termos de como a auditoria é habilitada. Foi adicionado um novo campo aos registros de auditoria, `data_sensitivity_information`, que registra a classificações (rótulos) de confidencialidade dos dados reais que foram retornados pela consulta. Consulte [Auditoria de acesso a dados confidenciais](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification#subheading-3).

### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>Suporte estendido para dispositivos de memória persistentes (CTP 2.0)

Agora, qualquer arquivo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] colocado em um dispositivo de memória persistente pode funcionar no modo *capacitado*. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acessa o dispositivo diretamente, ignorando a pilha de armazenamento do sistema operacional usando operações de memória eficientes. Esse modo melhora o desempenho porque permite entrada/saída de baixa latência em relação a esses dispositivos.
    - Exemplos de arquivos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluem:
        - Arquivos de banco de dados
        - Arquivos de log de transações
        - Arquivos de ponto de verificação de OLTP in-memory
    - A memória persistente também é conhecida como memória de classe de armazenamento.
    - Ocasionalmente, a memória persistente é chamada informalmente de *pmem* em alguns sites que não são da Microsoft.

> [!NOTE]
> Para esta versão prévia, a capacitação de arquivos em dispositivos de memória persistente só está disponível no Linux. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Windows dá suporte a dispositivos de memória persistente começando com o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)].

### <a name="hybrid-buffer-pool-ctp-21"></a>Pool de buffers híbrido (CTP 2.1)

O pool de buffers híbrido é um novo recurso do mecanismo de banco de dados do SQL Server em que páginas de banco de dados em arquivos de banco de dados são colocadas em um dispositivo de PMEM (memória persistente) que será acessado diretamente quando necessário. Como dispositivos PMEM fornecem uma latência muito baixa para o acesso a dados, o mecanismo pode não fazer uma cópia dos dados em uma área de "páginas limpas" do pool de buffers e simplesmente acessar a página diretamente no PMEM. O acesso é realizado usando E/S de memória mapeada, como ocorre com a capacitação. Isso oferece benefícios de desempenho, por evitar uma cópia da página para a DRAM e evitar a pilha de E/S do sistema operacional para acessar a página no armazenamento persistente. Esse recurso está disponível no SQL Server no Windows e no SQL Server no Linux.

Para obter mais informações, confira [Pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md)

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>Suporte para estatísticas de columnstore em DBCC CLONEDATABASE (CTP 2.0)

O `DBCC CLONEDATABASE` cria uma cópia somente de esquema de um banco de dados que inclui todos os elementos necessários para solucionar problemas de desempenho de consulta sem copiar os dados.  Em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o comando não copiava as estatísticas necessárias para solucionar problemas com precisão em consultas de índice de columnstore, e etapas manuais eram necessárias para capturar essas informações. Agora, no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], o `DBCC CLONEDATABASE` captura automaticamente os blobs de estatísticas para índices columnstore, de modo que nenhuma etapa manual é necessária.

### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>Novas opções adicionadas a sp_estimate_data_compression_savings (CTP 2.0)

`sp_estimate_data_compression_savings` retorna o tamanho atual do objeto solicitado e faz a estimativa do tamanho do objeto para o estado de compactação solicitado.  Atualmente, esse procedimento dá suporte a três opções: `NONE`, `ROW` e `PAGE`. O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz duas novas opções: `COLUMNSTORE` e `COLUMNSTORE_ARCHIVE`. Essas novas opções permitirão que você estime a economia de espaço se um índice columnstore for criado na tabela usando a compactação de columnstore padrão ou de arquivos.

### <a id="ml"></a> Modelagem baseada em partição e clusters de failover dos Serviços do Machine Learning do SQL Server (CTP 2.0)

- **Modelagem baseada em partição**: Processe scripts externos por partição de seus dados usando os novos parâmetros adicionados ao `sp_execute_external_script`. Essa funcionalidade dá suporte ao treinamento de muitos modelos pequenos (um modelo para cada partição de dados) em vez de um modelo grande.

- **Cluster de failover do Windows Server**: Configure alta disponibilidade para Serviços do Machine Learning em um Cluster de failover do Windows Server.

Para obter informações detalhadas, consulte [Novidades dos Serviços do Machine Learning do SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>Infraestrutura de perfil de consulta leve habilitada por padrão (CTP 2.0)

A infraestrutura de criação de perfil com consulta leve (LWP) fornece dados de desempenho de consulta de maneira mais eficiente do que os mecanismos de criação de perfil padrão. A criação de perfil leve agora está habilitada por padrão. Ela foi introduzida no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. A criação de perfil leve oferece um mecanismo de coleção de estatísticas de execução de consulta com uma sobrecarga esperada de 2% da CPU, em comparação com uma sobrecarga de até 75% da CPU para o mecanismo de criação de perfil com consulta padrão. Em versões anteriores, ela ficava DESATIVADA por padrão. Os administradores de banco de dados podiam habilitá-la com o [sinalizador de rastreamento 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

Para obter mais informações sobre essa criação de perfil leve, confira [Infraestrutura de criação de perfil de consulta](../relational-databases/performance/query-profiling-infrastructure.md).

### <a id="polybase"></a>Novos conectores de PolyBase

- **Novos conectores para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB**: o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz novos conectores para dados externos para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB.

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>A nova função de sistema sys.dm_db_page_info retorna informações da página (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` retorna informações sobre uma página em um banco de dados. A função retorna uma linha que contém as informações de cabeçalho da página, incluindo `object_id`, `index_id` e `partition_id`. Essa função substitui a necessidade de usar `DBCC PAGE` na maioria dos casos.  

Para facilitar a solução de problemas de esperas relacionadas à página, uma nova coluna chamada page_resource também foi adicionada a `sys.dm_exec_requests` e `sys.sysprocesses`. Essa nova coluna permite unir `sys.dm_db_page_info` a essas exibições por meio de uma nova função de sistema – `sys.fn_PageResCracker`. Consulte o seguinte script como exemplo:

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

## <a id="sqllinux"></a> SQL Server no Linux

- **Suporte de replicação (CTP 2.0)**: o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] dá suporte à Replicação do SQL Server no Linux. Uma máquina de virtual do Linux com SQL Agent pode ser um publicador, distribuidor ou assinante. 

  Crie os tipos seguintes de publicações:
  - Transacional.
  - Instantâneo
  - Mesclagem

  Configure a replicação [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou use [procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

- **Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) (CTP 2.0)**: O SQL Server 2019 no Linux dá suporte ao MSDTC (Coordenador de Transações Distribuídas da Microsoft). Para obter detalhes, consulte [Como configurar o MSDTC no Linux](../linux/sql-server-linux-configure-msdtc.md).

- **Grupos de Disponibilidade Always On em contêineres do Docker com Kubernetes (CTP 2.2)**: O Kubernetes pode orquestrar contêineres que executam instâncias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para fornecer um conjunto altamente disponível de bancos de dados com os Grupos de Disponibilidade Always On do SQL Server. Um operador de Kubernetes implanta um StatefulSet incluindo um contêiner com **contêiner mssql-server** e um monitor de integridade.

- **Suporte de OpenLDAP para provedores terceirizados do AD (CTP 2.0)**: o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] no Linux dá suporte a OpenLDAP, que permite que provedores terceirizados ingressem no Active Directory.

- **Machine Learning no Linux (CTP 2.0)**: Os Serviços do Machine Learning do SQL Server 2019 (no banco de dados) agora são compatíveis com o Linux. O suporte inclui o procedimento armazenado `sp_execute_external_script`. Para obter instruções de como instalar os Serviços do Machine Learning no Linux, consulte [Instalar o suporte dos Serviços do Machine Learning do SQL Server 2019 para R e Python no Linux](../linux/sql-server-linux-setup-machine-learning.md).

- **Novo registro de contêiner (CTP 2.1)**: Todas as imagens de contêiner para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], bem como [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], agora estão localizadas no Registro de Contêiner da Microsoft. O Registro de Contêiner da Microsoft é o registro de contêiner oficial para distribuição de contêineres de produtos da Microsoft. Além disso, imagens certificadas baseadas em RHEL agora foram publicadas.

  - Registro de Contêiner da Microsoft: `mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - Imagens de contêiner baseadas em RHEL certificadas: `mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

## <a id="mds"></a> Master Data Services (CTP 2.0) 

- **Controles do Silverlight substituídos por HTML**: O portal do MDS (Master Data Services) não depende mais do Silverlight. Todos os componentes do Silverlight anteriores foram substituídos por controles HTML.

## <a id="security"></a>Segurança (CTP 2.0)

- **Gerenciamento de certificados no SQL Server Configuration Manager**: Certificados SSL/TLS são amplamente usados para proteger o acesso a instâncias do SQL Server. O gerenciamento de certificados agora está integrado ao SQL Server Configuration Manager, simplificando tarefas comuns como:

  - exibir e validar certificados instalados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  - exibindo certificados prestes a expirar.
  - implantar certificados em computadores que participam de Grupos de Disponibilidade Always On (começando no nó que contém a réplica primária).
  - implantar certificados em computadores que participam de uma instância de cluster de failover (começando no nó ativo).

  > [!NOTE]
  > O usuário precisa ter permissões de administrador em todos os nós de cluster.

## <a id="tools"></a>Ferramentas

- [**Azure Data Studio**](../azure-data-studio/what-is.md): Lançado anteriormente com nome de versão prévia SQL Operations Studio, o Azure Data Studio é uma ferramenta de área de trabalho leve, moderna, de software livre e multiplataforma comuns usada para as tarefas mais comuns no desenvolvimento e administração de dados. Com o Azure Data Studio, você pode se conectar ao SQL Server local e na nuvem do Windows, macOS e Linux. O Azure Data Studio permite:

  - Atualizar para a [extensão do SQL Server 2019 (versão prévia)](../azure-data-studio/sql-server-2019-extension.md). (CTP 2.1)
  - editar e executar consultas em um ambiente de desenvolvimento moderno com Intellisense extremamente rápido, trechos de código e integração de controle do código-fonte. (CTP 2.0) 
  - visualizar rapidamente dados com gráficos internos de seus conjuntos de resultados. (CTP 2.0)
  - criar painéis personalizados para seus servidores e bancos de dados usando widgets personalizáveis. (CTP 2.0)  
  - gerenciar facilmente seu ambiente mais abrangente com o terminal interno. (CTP 2.0)
  - analisar dados em uma experiência de notebook integrada baseado em Jupyter. (CTP 2.0)
  - Aprimorar sua experiência com extensões e temas personalizados. (CTP 2.0)
  - e explorar seus recursos do Azure com um navegador de recursos e assinatura interno. (CTP 2.0)
  - Dá suporte a cenários que usam um cluster de Big Data do SQL Server. (CTP 2.0)

- [**SSMS (SQL Server Management Studio) 18.0 (versão prévia)**](../ssms/sql-server-management-studio-ssms.md)

  - Suporte para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. (CTP 2.0)
  - Suporte para Always Encrypted com enclaves seguros. (CTP 2.0)
  - Menor tamanho de download. (CTP 2.0)
  - Agora baseado no Shell Isolado do Visual Studio 2017. (CTP 2.0)
  - Para obter uma lista completa, consulte o [Log de mudanças do SSMS](../ssms/sql-server-management-studio-changelog-ssms.md). (CTP 2.0)

## <a name="other-services"></a>Outros serviços

No CTP 2.2, o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] não introduz novos recursos para os seguintes serviços:

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>Próximas etapas

- [Notas sobre a versão do SQL Server 2019](sql-server-ver15-release-notes.md)

- [Microsoft SQL Server 2019: White paper técnico](https://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Publicado em setembro de 2018. Aplica-se ao Microsoft SQL Server 2019 CTP 2.0 para contêineres do Windows, Linux e Docker.


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
