---
title: "Criar função de partição (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION FUNCTION
- PARTITION
- PARTITION FUNCTION
- PARTITION_FUNCTION_TSQL
- PARTITION_TSQL
- CREATE_PARTITION_FUNCTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- RANGE RIGHT partition functions
- RANGE LEFT partition functions
- partitioned indexes [SQL Server], functions
- functions [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], functions
- CREATE PARTITION FUNCTION statement
ms.assetid: 9dfe8b76-721e-42fd-81ae-14e22258c4f2
caps.latest.revision: "57"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a095e1de4fdffc97d615a39fd7cf185c99493d02
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="create-partition-function-transact-sql"></a>CREATE PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria uma função no banco de dados atual que mapeia as linhas de uma tabela ou índice em partições com base nos valores de uma coluna especificada. Usar CREATE PARTITION FUNCTION é a primeira etapa na criação de uma tabela particionada ou índice. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], uma tabela ou índice pode ter no máximo 15.000 partições.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE PARTITION FUNCTION partition_function_name ( input_parameter_type )  
AS RANGE [ LEFT | RIGHT ]   
FOR VALUES ( [ boundary_value [ ,...n ] ] )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_function_name*  
 É o nome da função de partição. Nomes de função de partição devem ser exclusivo no banco de dados e estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *input_parameter_type*  
 É o tipo de dados da coluna usada para particionamento. Todos os tipos de dados são válidos para uso como colunas de particionamento, exceto **text**, **ntext**, **image**, **xml**, **timestamp**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, tipos de dados de alias ou tipos de dados CLR definidos pelo usuário.  
  
 A coluna real, conhecida como uma coluna de particionamento, é especificada na instrução CREATE TABLE ou CREATE INDEX.  
  
 *boundary_value*  
 Especifica os valores de limite para cada partição de uma tabela particionada ou índice que usa *partition_function_name*. Se *boundary_value* está vazio, a função de partição mapeia toda a tabela ou índice usando *partition_function_name* em uma única partição. É possível usar somente uma coluna de divisão, especificada em uma instrução CREATE TABLE ou CREATE INDEX.  
  
 *boundary_value* é uma expressão constante que pode fazer referência a variáveis. Isso inclui variáveis ou funções de tipo definido pelo usuário e funções definidas pelo usuário. Não pode fazer referência a expressões [!INCLUDE[tsql](../../includes/tsql-md.md)]. *boundary_value* deve corresponder ou ser implicitamente conversível para o tipo de dados fornecido no *input_parameter_type*e não pode ser truncado durante a conversão implícita de forma que o tamanho e a escala do valor não corresponde do correspondente *input_parameter_type*.  
  
> [!NOTE]  
>  Se *boundary_value* consiste em **datetime** ou **smalldatetime** literais, esses literais serão avaliados supondo que us_english é o idioma da sessão. Este comportamento é preterido. Para certificar-se de que a definição da função de partição se comporta conforme esperado para todos os idiomas de sessão, recomendamos usar constantes que sejam interpretadas da mesma maneira para todas as configurações de idioma, tal como o formato aaaammdd; ou converter explicitamente literais em um estilo específico. Para determinar a sessão de idioma de seu servidor, execute `SELECT @@LANGUAGE`.  
  
 *... n*  
 Especifica o número de valores fornecidos por *boundary_value*, não deve exceder 14.999. O número de partições criadas é igual a  *n*  + 1. Os valores não precisam ser listados em ordem. Se os valores não estiverem em ordem, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] os classifica, cria a função e retorna um aviso de que os valores não foram fornecidos em ordem. O mecanismo de banco de dados retornará um erro se  *n*  inclui valores duplicados.  
  
 **ESQUERDA** | CERTO  
 Especifica para qual lado de cada intervalo de valor de limite, esquerda ou direita, o *boundary_value* [ **,***... n* ] pertence, quando valores de intervalo são classificados pela [!INCLUDE[ssDE](../../includes/ssde-md.md)]em ordem crescente da esquerda para a direita. Se não for especificado, LEFT será o padrão.  
  
## <a name="remarks"></a>Remarks  
 O escopo de uma função de partição é limitado ao banco de dados em que é criado. No banco de dados, as funções das partições residem em um namespace separado das outras funções.  
  
 Quaisquer linhas cuja coluna de particionamento tenha valores nulos serão colocadas na partição mais à esquerda, a menos que NULL seja especificado como um valor de limite e RIGHT seja indicado. Nesse caso, a partição mais à esquerda será uma partição vazia e os valores NULL serão colocados na partição seguinte.  
  
## <a name="permissions"></a>Permissões  
 Qualquer uma das permissões a seguir pode ser usada para executar CREATE PARTITION FUNCTION:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   Permissão CONTROL ou ALTER no banco de dados no qual a função de partição está sendo criada.  
  
-   Permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual a função de partição está sendo criada.  
  
##  <a name="BKMK_examples"></a> Exemplos  
  
### <a name="a-creating-a-range-left-partition-function-on-an-int-column"></a>A. Criando uma função de partição RANGE LEFT em uma coluna int  
 A função de partição a seguir particionará uma tabela ou um índice em quatro partições.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
```  
  
 A tabela a seguir mostra como uma tabela que usa essa função de partição na coluna de particionamento **col1** seria particionada.  
  
|Partition|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**Valores**|**Col1** <= `1`|**Col1**  >  `1` AND **col1** <= `100`|**Col1**  >  `100` AND **col1** <=`1000`|**Col1** > `1000`|  
  
### <a name="b-creating-a-range-right-partition-function-on-an-int-column"></a>B. Criando uma função de partição RANGE RIGHT em uma coluna int  
 A função de partição a seguir usa os mesmos valores para *boundary_value* [ **,***... n* ] como no exemplo anterior, exceto que ela especifica RANGE RIGHT.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE RIGHT FOR VALUES (1, 100, 1000);  
```  
  
 A tabela a seguir mostra como uma tabela que usa essa função de partição na coluna de particionamento **col1** seria particionada.  
  
|Partition|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**Valores**|**Col1** \<`1`|**Col1**  >=  `1` AND **col1** \<`100`|**Col1**  >=  `100` AND **col1** \<`1000`|**Col1** >= `1000`| 
  
### <a name="c-creating-a-range-right-partition-function-on-a-datetime-column"></a>C. Criando uma função de partição RANGE RIGHT em uma coluna datetime  
 A função de partição a seguir particiona uma tabela ou índice em 12 partições, uma para cada mês de registros um ano de valores em uma **datetime** coluna.  
  
```sql  
CREATE PARTITION FUNCTION [myDateRangePF1] (datetime)  
AS RANGE RIGHT FOR VALUES ('20030201', '20030301', '20030401',  
               '20030501', '20030601', '20030701', '20030801',   
               '20030901', '20031001', '20031101', '20031201');  
```  
  
 A tabela a seguir mostra como uma tabela ou índice que usa essa função de partição na coluna de particionamento **datecol** seria particionada.  
  
|Partition|1|2|...|11|12|  
|---------------|-------|-------|---------|--------|--------|  
|**Valores**|**datecol** \<`February 1, 2003`|**datecol**  >=  `February 1, 2003` AND **datecol** \<`March 1, 2003`||**datecol**  >=  `November 1, 2003` AND **col1** \<`December 1, 2003`|**datecol** >= `December 1, 2003`| 
  
### <a name="d-creating-a-partition-function-on-a-char-column"></a>D. Criando uma função de partição em uma coluna char  
 A função de partição a seguir particiona uma tabela ou um índice em quatro partições.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF3 (char(20))  
AS RANGE RIGHT FOR VALUES ('EX', 'RXE', 'XR');  
```  
  
 A tabela a seguir mostra como uma tabela que usa essa função de partição na coluna de particionamento **col1** seria particionada.  
  
|Partition|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**Valores**|**Col1** \< `EX`...|**Col1**  >=  `EX` AND **col1** \< `RXE`...|**Col1**  >=  `RXE` AND **col1** \< `XR`...|**Col1** >= `XR`| 
  
### <a name="e-creating-15000-partitions"></a>E. Criando 15.000 partições  
 A função de partição a seguir particiona uma tabela ou um índice em 15.000 partições.  
  
```sql  
--Create integer partition function for 15,000 partitions.  
DECLARE @IntegerPartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION IntegerPartitionFunction (int) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i int = 1;  
WHILE @i < 14999  
BEGIN  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N', ';  
SET @i += 1;  
END  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N');';  
EXEC sp_executesql @IntegerPartitionFunction;  
GO  
```  
  
### <a name="f-creating-partitions-for-multiple-years"></a>F. Criando partições para vários anos  
 A função de partição a seguir particiona uma tabela ou índice em 50 partições em um **datetime2** coluna. Há uma partição para cada mês entre janeiro de 2007 e janeiro de 2011.  
  
```sql  
--Create date partition function with increment by month.  
DECLARE @DatePartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION DatePartitionFunction (datetime2) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i datetime2 = '20070101';  
WHILE @i < '20110101'  
BEGIN  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10)) + '''' + N', ';  
SET @i = DATEADD(MM, 1, @i);  
END  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10))+ '''' + N');';  
EXEC sp_executesql @DatePartitionFunction;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [$PARTITION &#40; Transact-SQL &#41;](../../t-sql/functions/partition-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [partition_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys. Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

