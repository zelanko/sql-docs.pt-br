---
title: ALTER PARTITION FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION FUNCTION
- ALTER_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- splitting partitions [SQL Server]
- partitioned tables [SQL Server], splitting
- ALTER PARTITION FUNCTION statement
- merging partitions [SQL Server]
- partitioned indexes [SQL Server], merging
- partitioned indexes [SQL Server], splitting
- modifying partition functions
- partition functions [SQL Server], modifying
- partitioned tables [SQL Server], merging
ms.assetid: 70866dac-0a8f-4235-8108-51547949ada4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 577e3013c3538d641da81d416cd016041df80143
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51637863"
---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Altera uma função de partição dividindo ou mesclando seus valores de limite. Ao executar ALTER PARTITION FUNCTION, uma partição de qualquer tabela ou índice que usa a função de partição pode ser dividida em duas partições, ou duas partições podem ser mescladas em uma única partição.  
  
> [!CAUTION]  
>  Mais de uma tabela ou índice podem usar a mesma função de partição. ALTER PARTITION FUNCTION afeta todos em uma única transação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER PARTITION FUNCTION partition_function_name()  
{   
    SPLIT RANGE ( boundary_value )  
  | MERGE RANGE ( boundary_value )   
} [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_function_name*  
 É o nome da função de partição a ser modificada.  
  
 SPLIT RANGE ( *boundary_value* )  
 Adiciona uma partição à função de partição. *boundary_value* determina o intervalo da nova partição e deve ser diferente dos intervalos de limite existentes da função de partição. Com base em *boundary_value*, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] divide um dos intervalos existentes em dois. Desses dois, aquele em que o novo *boundary_value* reside é considerado a nova partição.  
  
 Um grupo de arquivos deve existir online e ser marcado pelo esquema de partição que usa a função de partição como NEXT USED para reter a nova partição. Os grupos de arquivos são alocados em partições em uma instrução CREATE PARTITION SCHEME. Se uma instrução CREATE PARTITION SCHEME alocar mais grupos de arquivos que o necessário (são criadas menos partições na instrução CREATE PARTITION FUNCTION do que grupos de arquivos para retê-las), haverá grupos de arquivos não atribuídos e um deles será marcado como NEXT USED pelo esquema de partição. Esse grupo de arquivos irá reter a nova partição. Se não houver nenhum grupo de arquivos marcado como NEXT USED pelo esquema de partição, será necessário usar ALTER PARTITION SCHEME para adicionar um grupo de arquivos, ou designar um existente, para reter a nova partição. Um grupo de arquivos que já retém partições pode ser designado para reter partições adicionais. Como uma função de partição pode participar de mais de um esquema de partição, todos os esquemas de partição que usarem a função de partição à qual você está adicionando as partições deverão ter um grupo de arquivos NEXT USED. Caso contrário, ALTER PARTITION FUNCTION falhará com um erro que exibe o esquema ou os esquemas de partição que não possuem um grupo de arquivos NEXT USED.  
  
 Se você criar todas as partições no mesmo grupo de arquivos, esse grupo de arquivos será inicialmente designado a ser o grupo de arquivos NEXT USED automaticamente. Entretanto, após a execução de uma operação de divisão, não existe mais um grupo de arquivos NEXT USED designado. É necessário atribuir explicitamente o NEXT USED como grupo de arquivos usando ALTER PARITION SCHEME; caso contrário, uma operação de divisão subsequente falhará.  
  
> [!NOTE]  
>  Limitações com índice columnstore: somente partições vazias podem ser divididas quando existe um índice columnstore na tabela. Você precisará remover ou desabilitar o índice columnstore antes de executar esta operação  
  
 MERGE [ RANGE ( *boundary_value*) ]  
 Descarta uma partição e mescla os valores que existirem na partição em uma das partições restantes. RANGE (*boundary_value*) deve ser um valor de limite existente no qual são mesclados os valores da partição descartada. O grupo de arquivos que originalmente continha o *boundary_value* é removido do esquema de partição, a menos que seja usado por uma partição restante ou marcado com a propriedade NEXT USED. A partição mesclada reside no grupo de arquivos que originalmente não continha *boundary_value*. *boundary_value* é uma expressão constante que pode fazer referência a variáveis (incluindo variáveis de tipo definido pelo usuário) ou funções (incluindo funções definidas pelo usuário). Ela não pode referenciar uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)]. *boundary_value* deve corresponder ou poder ser implicitamente convertido no tipo de dados de suas colunas de particionamento correspondentes e não pode ser truncado durante conversão implícita de modo que o tamanho e a escala do valor não sejam equivalentes a seu *input_parameter_type* correspondente.  
  
> [!NOTE]  
>  Limitações com índice columnstore: duas partições não vazias contendo um índice columnstore não podem ser mescladas. Você precisará remover ou desabilitar o índice columnstore antes de executar esta operação  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Sempre mantenha partições vazias em ambas as extremidades do intervalo de partição para garantir que a divisão de partição (antes de carregar novos dados) e a mesclagem de partição (depois de descarregar dados antigos) não incorram em nenhum movimento de dados. Evite dividir ou mesclar partições populadas. Isso pode ser extremamente ineficiente, pois pode causar até quatro vezes mais geração de log e também pode causar bloqueio severo.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 ALTER PARTITION FUNCTION reparticiona quaisquer tabelas e índices que usam a função em uma única operação atômica. Entretanto, essa operação acontece offline e, dependendo da extensão de reparticionamento, pode utilizar muitos recursos.  
  
 ALTER PARTITION FUNCTION só pode ser usada para dividir uma partição em duas ou mesclar duas partições em uma. Para alterar a forma como uma tabela é particionada (por exemplo, de 10 partições em 5), execute qualquer uma das opções a seguir. Dependendo da configuração do sistema, essas opções podem variar em consumo de recursos:  
  
-   Crie uma nova tabela particionada com a função de partição desejada e insira os dados da tabela antiga na nova tabela, usando uma instrução INSERT INTO...SELECT FROM.  
  
-   Crie um índice clusterizado particionado em um heap.  
  
    > [!NOTE]  
    >  Descartando resultados de um índice clusterizado particionado em um heap particionado.  
  
-   Descarte e recrie um índice particionado existente usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX com a cláusula DROP EXISTING = ON.  
  
-   Execute uma sequência de instruções ALTER PARTITION FUNCTION.  
  
 Todos os grupos de arquivos afetados por ALTER PARTITION FUNCTION devem estar online.  
  
 ALTER PARTITION FUNCTION falha quando há um índice clusterizado desabilitado em qualquer tabela que usa a função de partição.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornece suporte de replicação para modificar uma função de partição. As alterações em uma função de partição no banco de dados de publicação devem ser aplicadas manualmente no banco de dados de assinatura.  
  
## <a name="permissions"></a>Permissões  
 Qualquer uma das permissões a seguir pode ser usada para executar ALTER PARTITION FUNCTION:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   A permissão CONTROL ou ALTER no banco de dados no qual a função de partição foi criada.  
  
-   A permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual a função de partição foi criada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-splitting-a-partition-of-a-partitioned-table-or-index-into-two-partitions"></a>A. Dividindo uma partição de uma tabela ou índice particionado em duas partições  
 O exemplo a seguir cria uma função de partição para dividir uma tabela ou índice em quatro partições. `ALTER PARTITION FUNCTION` divide uma das partições em dois para criar um total de cinco partições.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Split the partition between boundary_values 100 and 1000  
--to create two partitions between boundary_values 100 and 500  
--and between boundary_values 500 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
SPLIT RANGE (500);  
```  
  
### <a name="b-merging-two-partitions-of-a-partitioned-table-into-one-partition"></a>B. Mesclando duas partições de uma tabela particionada em uma partição  
 O exemplo a seguir cria a mesma função de partição anterior e mescla duas partições em uma, para um total de três partições.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Merge the partitions between boundary_values 1 and 100  
--and between boundary_values 100 and 1000 to create one partition  
--between boundary_values 1 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
MERGE RANGE (100);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices particionados](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
