---
title: CREATE EXTERNAL TABLE AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CREATE EXTERNAL TABLE AS SELECT
- CREATE_EXTERNAL_TABLE_AS_SELECT
- CREATE EXTERNAL TABLE AS SELECT_TSQL
helpviewer_keywords:
- External, table
- PolyBase, external table
- External, table create as select
- PolyBase, create table as select
ms.assetid: 32dfe254-6df7-4437-bfd6-ca7d37557b0a
caps.latest.revision: 16
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 716c0fdaa701865e8d35154cd19068051e0ab017
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-table-as-select-transact-sql"></a>CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Cria uma tabela externa e, em seguida, exporta, em paralelo, os resultados de uma [!INCLUDE[tsql](../../includes/tsql-md.md)] uma instrução SELECT para o Hadoop ou Blob de armazenamento do Azure.  
  
 Use a instrução CREATE EXTERNAL tabela como selecionar (CETAS):  
  
-   Exporte uma tabela de banco de dados para o armazenamento de BLOBs do Azure ou Hadoop.  
  
-   Importar dados do armazenamento de BLOBs do Azure ou Hadoop e armazená-lo no banco de dados.  
  
-   Consultar dados do armazenamento de BLOBs do Azure ou Hadoop, associá-lo com tabelas de banco de dados relacional e gravar os resultados de volta para o armazenamento de blob do Azure ou Hadoop.  
  
-   Consultar dados do armazenamento de BLOBs do Azure ou Hadoop, transformando-os usando recursos de processamento rápido do banco de dados e gravá-lo no armazenamento de BLOBs do Azure ou Hadoop.  
  
 Para obter mais informações, consulte [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name   
    WITH (   
        LOCATION = 'hdfs_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
    AS <select_statement>  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
}  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumentos  
 [[ *database_name* . [ *schema_name* ]. ] | *schema_name* . ] *table_name*  
 Um a três - parte nome da tabela para criar o banco de dados. Para uma tabela externa, apenas os metadados de tabela são armazenados no banco de dados relacional.  
  
 LOCAL = '*hdfs_folder*'  
 Especifica onde gravar os resultados da instrução SELECT na fonte de dados externa. O local é um nome de pasta e, opcionalmente, pode incluir um caminho relativo à pasta raiz do Cluster do Hadoop ou do Blob de armazenamento do Azure.  PolyBase criará o caminho e a pasta se ela ainda não existir.  
  
 Os arquivos externos são gravados em *hdfs_folder* e nomeado *queryid_date_time_id. Format*, onde *ID* é um identificador incremental e *formato* é o formato de dados exportados. Por exemplo, QID776_20160130_182739_0.orc.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica o nome do objeto de origem de dados externos que contém o local onde os dados externos são armazenados ou serão armazenados. O local é um Hadoop Cluster ou um Blob de armazenamento do Azure. Para criar uma fonte de dados externa, use [CREATE EXTERNAL DATA SOURCE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica o nome do objeto de formato de arquivo externo que contém o formato de arquivo de dados externa. Para criar um formato de arquivo externo, use [CREATE EXTERNAL FILE FORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Rejeitar opções  
 As opções de rejeitar não se aplicam ao tempo em que essa instrução CREATE EXTERNAL TABLE AS SELECT é executada. Em vez disso, eles são especificados aqui para que o banco de dados pode usá-los mais tarde ao importar dados da tabela externa. Posteriormente, quando a instrução CREATE TABLE AS SELECT seleciona dados da tabela externa, o banco de dados usará as opções de rejeitar para determinar o número ou porcentagem de linhas que podem falhar ao importar antes de parar a importação.  
  
 REJECT_VALUE = *reject_value*  
 Especifica o valor ou a porcentagem de linhas que podem falhar ao importar antes do banco de dados é interrompida a importação.  
  
 REJECT_TYPE = **valor** | porcentagem  
 Esclarece se a opção REJECT_VALUE é especificada como um valor literal ou uma porcentagem.  
  
 value  
 REJECT_VALUE é um valor literal, não uma porcentagem.  O banco de dados irá parar importação linhas do arquivo de dados externa quando excede o número de linhas com falha *reject_value*.  
  
 Por exemplo, se REJECT_VALUE = 5 e REJECT_TYPE = valor, o banco de dados irá parar importação linhas depois de 5 linhas falharam importar.  
  
 Porcentagem  
 REJECT_VALUE é uma porcentagem, não é um valor literal. O banco de dados irá parar importação de linhas de externo do arquivo de dados quando o *porcentagem* de linhas com falha excede *reject_value*. A porcentagem de linhas com falha é calculada em intervalos.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Necessário quando REJECT_TYPE = porcentagem, especifica o número de linhas para tentar importar antes do banco de dados recalcula a porcentagem de linhas com falha.  
  
 Por exemplo, se REJECT_SAMPLE_VALUE = 1000, o banco de dados irá calcular a porcentagem de linhas com falha depois que ele tentou importar 1000 linhas do arquivo de dados externa. Se a porcentagem de linhas com falha for menor que *reject_value*, o banco de dados tentará carregar outro 1000 linhas. O banco de dados continua a recalcular a porcentagem de linhas com falha quando ele tenta importar cada 1000 linhas adicionais.  
  
> [!NOTE]  
>  Desde que o banco de dados calcula a porcentagem de linhas com falha em intervalos, a porcentagem real de linhas com falha pode exceder *reject_value*.  
  
 Exemplo:  
  
 Este exemplo mostra como as três opções de rejeitar interagem entre si. Por exemplo, se REJECT_TYPE = porcentagem, REJECT_VALUE = 30 e REJECT_SAMPLE_VALUE = 100, o cenário a seguir pode ocorrer:  
  
-   O banco de dados tenta carregar as primeiras 100 linhas; 25 falharão e 75 bem-sucedida.  
  
-   Porcentagem de linhas com falha é calculada como 25%, que é menor que o valor de rejeição de 30%. Portanto, não é necessário interromper a carga.  
  
-   O banco de dados tenta carregar as próximo de 100 linhas; Esse tempo 25 êxito e falha de 75.  
  
-   Porcentagem de linhas com falha é recalculada como 50%. A porcentagem de linhas com falha excedeu o valor de rejeição de 30%.  
  
-   A carga falhará com linhas de 50% falhado após a tentativa de carregar 200 linhas, que é maior que o limite de 30% de especificada.  
  
 COM *common_table_expression*  
 Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Para obter mais informações, consulte [com common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Selecione \<select_criteria > preenche a nova tabela com os resultados de uma instrução SELECT. *select_criteria* é o corpo da instrução SELECT que determina quais dados a serem copiados para a nova tabela. Para obter informações sobre instruções SELECT, consulte [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse comando o **usuário de banco de dados** precisa de todas essas permissões ou associações:  
  
-   **ALTER SCHEMA** permissão no esquema local que conterá a nova tabela ou a associação a **db_ddladmin** função fixa de banco de dados.  
  
-   **CREATE TABLE** permissão ou associação no **db_ddladmin** função fixa de banco de dados.  
  
-   **Selecione** permissão em todos os objetos referenciados no *select_criteria*.  
  
 O logon precisa de todas essas permissões:  
  
-   **ADMINISTER BULK OPERATIONS** permissão  
  
-   **ALTER ANY EXTERNAL DATA SOURCE** permissão  
  
-   **ALTER ANY EXTERNAL FILE FORMAT** permissão  
  
-   O logon deve ter permissão de gravação para leitura e gravação para a pasta externa no Cluster de Hadoop ou Blob de armazenamento do Azure.  
 
 > [!IMPORTANT]  
 >  A permissão ALTER ANY EXTERNAL DATA SOURCE concede qualquer entidade de segurança a capacidade de criar e modificar qualquer objeto de fonte de dados externa e, portanto, isso também concede a capacidade de acessar todas as credenciais de banco de dados com escopo no banco de dados. Essa permissão deve ser considerada como altamente privilegiada e, portanto, deve ser concedida somente para entidades confiáveis no sistema.
  
## <a name="error-handling"></a>Tratamento de erros  
 Quando CREATE EXTERNAL TABLE AS SELECT exporta dados para um arquivo delimitado por texto, não há nenhum arquivo de rejeição de linhas com falha para exportar.  
  
 Ao criar a tabela externa, o banco de dados tenta se conectar ao cluster Hadoop externo ou Blob de armazenamento do Azure. Se a conexão falhar, o comando falhará e a tabela externa não será criada. Pode levar um minuto ou mais para o comando falha desde que as tentativas de banco de dados de conexão pelo menos 3 vezes.  
  
 Se criar EXTERNAL TABLE AS SELECT for cancelada ou falhar, o banco de dados fará uma tentativa de uso única para remover todos os novos arquivos e pastas já criadas na fonte de dados externa.  
  
 O banco de dados irão relatar erros de Java que ocorrem na fonte de dados externa durante a exportação de dados.  
  
##  <a name="GeneralRemarks"></a>Comentários gerais  
 Após a conclusão da instrução CETAS, você pode executar [!INCLUDE[tsql](../../includes/tsql-md.md)] consultas na tabela externa. Essas operações serão importar dados para o banco de dados para a duração da consulta, a menos que você importar, usando a instrução CREATE TABLE AS SELECT.  
  
 O nome da tabela externa e a definição são armazenadas nos metadados do banco de dados. Os dados são armazenados na fonte de dados externa.  
  
 Os arquivos externos são nomeados *QueryID_date_time_ID.format*, em que *ID* é um identificador incremental e *formato* é o formato de dados exportados. Por exemplo, QID776_20160130_182739_0.orc.  
  
 A instrução CETAS sempre cria uma tabela não particionada, mesmo se a tabela de origem está particionada.  
  
 Para planos de consulta, criada com EXPLICAR, o databaseuses essas operações do plano de consulta para tabelas externas:  
  
-   Movimentação de ordem aleatória externo  
  
-   Mover de difusão externa  
  
-   Movimentação de partição externo  
  
 **Aplica-se a:**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]como um pré-requisito para a criação de uma tabela externa, o administrador de dispositivo precisa configurar a conectividade do hadoop.   Para obter mais informações, consulte Configurar conectividade a dados externos (Analytics Platform System) na documentação do APS que você pode baixar do [aqui](http://www.microsoft.com/download/details.aspx?id=48241).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Como os dados de tabela externa residem fora do banco de dados, backup e restauram operações só funciona em dados armazenados no banco de dados. Isso significa que apenas os metadados de backup e restaurados.  
  
 O banco de dados não verifica a conexão com a fonte de dados ao restaurar um backup de banco de dados que contém uma tabela externa. Se a fonte original não estiver acessível, a restauração de metadados da tabela externa ainda terá êxito, mas as operações SELECT na tabela externa falharão.  
  
 O banco de dados não garante a consistência dos dados entre os dados externos reconectados. Você, o cliente, é exclusivamente responsável para manter a consistência entre os dados externos e o banco de dados.  
  
 Não há suporte para operações de DML (linguagem) de manipulação de dados em tabelas externas. Por exemplo, você não pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] atualizar, inserir ou excluir [!INCLUDE[tsql](../../includes/tsql-md.md)]instruções para modificar os dados externos.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW e DROP VIEW são as operações de DDL (linguagem) de definição de apenas os dados permitidas em tabelas externas.  
  
 PolyBase pode consumir um máximo de 33 k de arquivos por pasta durante a execução de 32 consultas simultâneas do PolyBase. O número máximo inclui arquivos e subpastas em cada pasta HDFS. Se o grau de simultaneidade é menor que 32, um usuário pode executar consultas do PolyBase em relação a pastas no HDFS que contêm mais de 33 k de arquivos. [!INCLUDE[msCoName](../../includes/msconame-md.md)]recomenda aos usuários do Hadoop e PolyBase manter caminhos de arquivo curtos e usa não mais do que 30 k de arquivos por pasta HDFS. Quando há muitos arquivos são referenciados ocorre uma exceção de falta de memória da JVM.  
  
 [Número de linhas do conjunto de &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) não tem efeito sobre essa CREATE EXTERNAL TABLE AS SELECT. Para obter um comportamento semelhante, use [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 Quando CREATE EXTERNAL TABLE AS SELECT seleciona um RCFile, os valores da coluna de RCFile não devem conter o pipe ' |' caracteres.  
  
## <a name="locking"></a>Bloqueio  
 Leva um bloqueio compartilhado no objeto SCHEMARESOLUTION.  
  
##  <a name="Examples"></a> Exemplos  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. Criar uma tabela de Hadoop usando criar externo tabela como selecionar (CETAS)  
 O exemplo a seguir cria uma nova tabela externa denominada `hdfsCustomer`, usando as definições de coluna e os dados da tabela de origem `dimCustomer`.  
  
 A definição de tabela é armazenada no banco de dados e os resultados da instrução SELECT são exportados para o ' / pdwdata/customer.tbl' arquivo de fonte de dados externa Hadoop *customer_ds*. O arquivo é formatado de acordo com o formato de arquivo externo *customer_ff*.  
  
 O nome do arquivo é gerado pelo banco de dados e contém a ID de consulta para facilitar o alinhamento de arquivo com a consulta que o gerou.  
  
 O caminho `hdfs://xxx.xxx.xxx.xxx:5000/files/` precede o diretório de clientes já deve existir. No entanto, se o diretório do cliente não existir, o banco de dados criará o diretório.  
  
> [!NOTE]  
>  Este exemplo especifica para 5000. Se a porta não for especificada, o banco de dados usa 8020 como a porta padrão.  
  
 O Hadoop resultante será o local e nome de arquivo `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. Use uma dica de consulta com CREATE EXTERNAL TABLE AS selecione (CETAS)  
 Esta consulta mostra a sintaxe básica para usar uma dica de consulta de junção com a instrução CETAS. Depois que a consulta é enviada para que o banco de dados usa a estratégia de junção de hash para gerar o plano de consulta. Para obter mais informações sobre dicas de junção e como usar a cláusula OPTION, consulte [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  Este exemplo especifica para 5000. Se a porta não for especificada, o banco de dados usa 8020 como a porta padrão.  
  
```  
  
      -- Example is based on AdventureWorks  
CREATE EXTERNAL TABLE dbo.FactInternetSalesNew  
WITH   
    (   
        LOCATION = '/files/Customer',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
    )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [Criar tabela &#40; Depósito de dados SQL do Azure, Parallel Data Warehouse &#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [Criar tabela como SELECT &#40; Depósito de dados SQL do Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [Remover tabela &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  



