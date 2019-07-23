---
title: CREATE EXTERNAL TABLE AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.subservice: design
ms.topic: conceptual
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
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 24668748b97c44e825baee2dee95d9442aa1e11f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073140"
---
# <a name="create-external-table-as-select-transact-sql"></a>CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Cria uma tabela externa e, em seguida, exporta, em paralelo, os resultados de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT para o Hadoop ou o Azure Storage Blob.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ [ *database_name*. [ *schema_name* ]. ] | *schema_name* . ] *table_name*  
 O nome de uma a três partes da tabela a ser criado no banco de dados. Para uma tabela externa, apenas os metadados da tabela são armazenados no banco de dados relacional.  
  
 LOCATION = '*hdfs_folder*'  
 Especifica o local em que gravar os resultados da instrução SELECT na fonte de dados externa. O local é um nome de pasta e, opcionalmente, pode incluir um caminho relativo à pasta raiz do Cluster do Hadoop ou do Azure Storage Blob.  O PolyBase criará o caminho e a pasta, caso ela ainda não exista.  
  
 Os arquivos externos são gravados em *hdfs_folder* e nomeados *QueryID_date_time_ID.format*, em que *ID* é um identificador incremental e *format* é o formato de dados exportados. Por exemplo, QID776_20160130_182739_0.orc.  
  
 DATA_SOURCE = *external_data_source_name*  
 Especifica o nome do objeto de fonte de dados externa que contém o local em que os dados externos são ou serão armazenados. O local é um Cluster do Hadoop ou um Azure Storage Blob. Para criar uma fonte de dados externa, use [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Especifica o nome do objeto de formato de arquivo externo que contém o formato do arquivo de dados externo. Para criar um formato de arquivo externo, use [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Opções de rejeição  
 As opções de rejeição não se aplicam ao momento da execução desta instrução CREATE EXTERNAL TABLE AS SELECT. Em vez disso, elas são especificadas aqui, de modo que o banco de dados possa usá-las mais tarde ao importar dados da tabela externa. Posteriormente, quando a instrução CREATE TABLE AS SELECT selecionar dados da tabela externa, o banco de dados usará as opções de rejeição para determinar o número ou percentual de linhas que podem falhar ao serem importadas antes que a importação seja interrompida.  
  
 REJECT_VALUE = *reject_value*  
 Especifica o valor ou percentual de linhas que podem falhar ao serem importadas antes que o banco de dados interrompa a importação.  
  
 REJECT_TYPE = **value** | percentage  
 Esclarece se a opção REJECT_VALUE é especificada como um valor literal ou um percentual.  
  
 value  
 REJECT_VALUE é um valor literal, não um percentual.  O banco de dados interromperá a importação de linhas do arquivo de dados externo quando o número de linhas com falha exceder *reject_value*.  
  
 Por exemplo, se REJECT_VALUE = 5 e REJECT_TYPE = value, o banco de dados interromperá a importação de linhas após a falha na importação de 5 linhas.  
  
 percentage  
 REJECT_VALUE é um percentual, não um valor literal. O banco de dados interromperá a importação de linhas do arquivo de dados externo quando o *percentual* de linhas com falha exceder *reject_value*. O percentual de linhas com falha é calculado em intervalos.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Obrigatório quando REJECT_TYPE = percentage. Isso especifica o número de linhas na tentativa de importação antes que o banco de dados calcule novamente o percentual de linhas com falha.  
  
 Por exemplo, se REJECT_SAMPLE_VALUE = 1000, o banco de dados calculará o percentual de linhas com falha depois de tentar importar 1.000 linhas do arquivo de dados externo. Se o percentual de linhas com falha for menor que *reject_value*, o banco de dados tentará carregar outras 1.000 linhas. O banco de dados continuará calculando novamente o percentual de linhas com falha depois de tentar importar cada 1.000 linhas adicionais.  
  
> [!NOTE]  
>  Como o banco de dados calcula o percentual de linhas com falha em intervalos, o percentual real de linhas com falha pode exceder *reject_value*.  
  
 Exemplo:  
  
 Este exemplo mostra como as três opções REJECT interagem. Por exemplo, se REJECT_TYPE = percentage, REJECT_VALUE = 30 e REJECT_SAMPLE_VALUE = 100, o seguinte cenário poderá ocorrer:  
  
-   O banco de dados tenta carregar as primeiras 100 linhas; 25 falharão e 75 serão bem-sucedidas.  
  
-   O percentual de linhas com falha é calculado como 25%, que é menor que o valor de rejeição de 30%. Portanto, não é necessário interromper a carga.  
  
-   O banco de dados tenta carregar as próximas 100 linhas; agora, 25 são bem-sucedidas e 75 falham.  
  
-   O percentual de linhas com falha é recalculado como 50%. O percentual de linhas com falha excedeu o valor de rejeição de 30%.  
  
-   A carga falha com 50% de linhas com falha após a tentativa de carregar 200 linhas, que é maior que o limite de 30% especificado.  
  
 WITH *common_table_expression*  
 Especifica um conjunto de resultados nomeado temporário, conhecido como uma CTE (expressão de tabela comum). Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 SELECT \<select_criteria> Popula a nova tabela com os resultados de uma instrução SELECT. *select_criteria* é o corpo da instrução SELECT que determina quais dados serão copiados para a nova tabela. Para obter informações sobre as instruções SELECT, confira [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Para executar esse comando, o **usuário de banco de dados** precisa de todas estas permissões ou associações:  
  
-   Permissão **ALTER SCHEMA** no esquema local que conterá a nova tabela ou associação à função de banco de dados fixa **db_ddladmin**.  
  
-   Permissão **CREATE TABLE** ou associação à função de banco de dados fixa **db_ddladmin**.  
  
-   Permissão **SELECT** em todos os objetos referenciados no *select_criteria*.  
  
 O logon precisa de todas estas permissões:  
  
-   Permissão **ADMINISTER BULK OPERATIONS**  
  
-   Permissão **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   Permissão **ALTER ANY EXTERNAL FILE FORMAT**  
  
-   O logon deve ter permissão de gravação para leitura e gravação na pasta externa no Cluster Hadoop ou no Azure Storage Blob.  
 
 > [!IMPORTANT]  
 >  A permissão ALTER ANY EXTERNAL DATA SOURCE concede a qualquer entidade de segurança a capacidade de criar e modificar qualquer objeto de fonte de dados externa e, portanto, isso também concede a capacidade de acessar todas as credenciais no escopo do banco de dados no banco de dados. Essa permissão precisa ser considerada como altamente privilegiada e, portanto, ser concedida somente para entidades de segurança confiáveis no sistema.
  
## <a name="error-handling"></a>Tratamento de erros  
 Quando CREATE EXTERNAL TABLE AS SELECT exporta dados para um arquivo delimitado por texto, não há nenhum arquivo de rejeição para linhas com falha na exportação.  
  
 Ao criar a tabela externa, o banco de dados tenta se conectar ao cluster Hadoop externo ou ao Azure Storage Blob. Se a conexão falhar, o comando falhará e a tabela externa não será criada. Pode levar um minuto ou mais para que o comando falhe, pois o banco de dados tenta a conexão novamente pelo menos três vezes.  
  
 Se a instrução CREATE EXTERNAL TABLE AS SELECT for cancelada ou falhar, o banco de dados fará uma tentativa única para remover os novos arquivos e as pastas já criados na fonte de dados externa.  
  
 O banco de dados relatará os erros de Java ocorridos na fonte de dados externa durante a exportação de dados.  
  
##  <a name="GeneralRemarks"></a> Comentários gerais  
 Após a conclusão da instrução CETAS, execute consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] na tabela externa. Essas operações importarão dados para o banco de dados durante a consulta, a menos que você faça a importação usando a instrução CREATE TABLE AS SELECT.  
  
 O nome da tabela externa e a definição são armazenados nos metadados do banco de dados. Os dados são armazenados na fonte de dados externa.  
  
 Os arquivos externos são nomeados *QueryID_date_time_ID.format*, em que *ID* é um identificador incremental e *formato* é o formato de dados exportados. Por exemplo, QID776_20160130_182739_0.orc.  
  
 A instrução CETAS sempre cria uma tabela não particionada, mesmo se a tabela de origem está particionada.  
  
 Para planos de consulta, criados com EXPLAIN, o banco de dados usa essas operações do plano de consulta para tabelas externas:  
  
-   Movimentação de ordem aleatória externa  
  
-   Movimentação de difusão externa  
  
-   Movimentação de partição externa  
  
 **APLICA-SE A:**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Como pré-requisito para a criação de uma tabela externa, o administrador do dispositivo precisa configurar a conectividade do Hadoop. Para obter mais informações, consulte Configurar a conectividade com os dados externos (Analytics Platform System) na documentação do APS que pode ser baixada [aqui](https://www.microsoft.com/download/details.aspx?id=48241).  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Como os dados da tabela externa residem fora do banco de dados, as operações de backup e restauração apenas funcionarão em dados armazenados no banco de dados. Isso significa que apenas os metadados serão copiados em backup e restaurados.  
  
 O banco de dados não verifica a conexão com a fonte de dados externa ao restaurar um backup de banco de dados que contém uma tabela externa. Se a fonte original não estiver acessível, a restauração de metadados da tabela externa ainda terá êxito, mas as operações SELECT na tabela externa falharão.  
  
 O banco de dados não assegura a consistência dos dados entre o banco de dados e os dados externos. Você, o cliente, é o único responsável por manter a consistência entre os dados externos e o banco de dados.  
  
 Não há compatibilidade com as operações DML (linguagem de manipulação de dados) em tabelas externas. Por exemplo, não é possível usar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] atualizar, inserir ou excluir[!INCLUDE[tsql](../../includes/tsql-md.md)] para modificar os dados externos.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW e DROP VIEW são as únicas operações DDL (linguagem de definição de dados) permitidas em tabelas externas.  
  
 O PolyBase pode consumir um máximo de 33 mil arquivos por pasta durante a execução de 32 consultas simultâneas do PolyBase. O número máximo inclui arquivos e subpastas em cada pasta do HDFS. Se o grau de simultaneidade é menor que 32, um usuário pode executar consultas do PolyBase em pastas do HDFS que contêm mais de 33 mil arquivos. A [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que os usuários do Hadoop e do PolyBase mantenham os caminhos de arquivo curtos e não usem mais do que 30 mil arquivos por pasta do HDFS. Quando há muitos arquivos referenciados, ocorre uma exceção de memória insuficiente da JVM.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md) não tem nenhum efeito sobre esta instrução CREATE EXTERNAL TABLE AS SELECT. Para obter um comportamento semelhante, use [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 Quando CREATE EXTERNAL TABLE AS SELECT seleciona um RCFile, os valores da coluna no RCFile não devem conter o caractere de barra vertical '|'.  
  
## <a name="locking"></a>Bloqueio  
 Usa um bloqueio compartilhado no objeto SCHEMARESOLUTION.  
  
##  <a name="Examples"></a> Exemplos  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. Criar uma tabela do Hadoop usando CETAS (CREATE EXTERNAL TABLE AS SELECT)  
 O exemplo a seguir cria uma nova tabela externa chamada `hdfsCustomer`, usando as definições de coluna e os dados da tabela de origem `dimCustomer`.  
  
 A definição de tabela é armazenada no banco de dados e os resultados da instrução SELECT são exportados para o arquivo '/pdwdata/customer.tbl' na fonte de dados externa do Hadoop *customer_ds*. O arquivo é formatado de acordo com o formato de arquivo externo *customer_ff*.  
  
 O nome do arquivo é gerado pelo banco de dados e contém a ID de consulta para facilitar o alinhamento do arquivo com a consulta que o gerou.  
  
 O caminho `hdfs://xxx.xxx.xxx.xxx:5000/files/` que precede o diretório Customer já deve existir. No entanto, se o diretório Customer não existir, o banco de dados criará o diretório.  
  
> [!NOTE]  
>  Este exemplo especifica 5000. Se a porta não for especificada, o banco de dados usará 8020 como a porta padrão.  
  
 O local e o nome de arquivo do Hadoop resultantes serão `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. Usar uma Dica de Consulta com CREATE EXTERNAL TABLE AS SELECT (CETAS)  
 Essa consulta mostra a sintaxe básica para uso de uma dica de consulta de junção com a instrução CETAS. Depois que a consulta é enviada, o banco de dados usa a estratégia de junção hash para gerar o plano de consulta. Para obter mais informações sobre dicas de junção e como usar a cláusula OPTION, consulte [Cláusula OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  Este exemplo especifica 5000. Se a porta não for especificada, o banco de dados usará 8020 como a porta padrão.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE TABLE &#40;SQL Data Warehouse do Azure, Parallel Data Warehouse&#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [CREATE TABLE AS SELECT &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


