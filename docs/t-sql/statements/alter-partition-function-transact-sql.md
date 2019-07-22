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
ms.openlocfilehash: c2418bedb172464002fd640a50c8b57f3daca712
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071255"
---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Altera uma função de partição dividindo ou mesclando seus valores de limite. Com a instrução ALTER PARTITION FUNCTION, é possível dividir em duas partições uma partição de tabela ou um índice que usa a função de partição. A instrução também pode mesclar duas partições em uma só.  
  
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
Adiciona uma partição à função de partição. *boundary_value* determina o intervalo da nova partição e deve ser diferente dos intervalos de limite existentes da função de partição. Com base em *boundary_value*, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] divide um dos intervalos existentes em dois. Desses dois intervalos, aquele com o novo *boundary_value* é a nova partição.  
  
É preciso que haja um grupo de arquivos online. E, o esquema de partição que usa a função de partição como NEXT USED para armazenar a nova partição tem que marcar o grupo de arquivos. Uma instrução CREATE PARTITION SCHEME atribui grupos de arquivos a partições. A instrução CREATE PARTITION FUNCTION cria menos partições do que grupos de arquivos para armazená-las. Uma instrução CREATE PARTITION SCHEME pode separar mais grupos de arquivos do que o necessário. Se isso acontecer, você acabará com grupos de arquivos não atribuídos. Além disso, o esquema de partição marca um dos grupos de arquivos como NEXT USED. Esse grupo de arquivos armazena a nova partição. Se não houver grupos de arquivos, o esquema de partições será marcado como NEXT USED e você precisará usar uma instrução ALTER PARTITION SCHEME. 

Devido a isso, todos os esquemas de partição que usam a função de partição à qual você está adicionando partições precisam ter um grupo de arquivos NEXT USED. Você pode atribuir um grupo de arquivos que já possui partições para armazenar partições adicionais. Uma função de partição pode participar de mais de um esquema de partição. Por esse motivo, todos os esquemas de partição que usam a função de partição na qual você está adicionando partições têm que ter um grupo de arquivos NEXT USED. Caso contrário, a instrução ALTER PARTITION FUNCTION apresenta falha com um erro que exibe o esquema ou os esquemas de partição que não têm um grupo de arquivos NEXT USED.  
  
Se você criar todas as partições no mesmo grupo de arquivos, esse grupo de arquivos será inicialmente designado a ser o grupo de arquivos NEXT USED automaticamente. No entanto, depois que uma operação de divisão é executada, não há mais um grupo de arquivos NEXT USED selecionado. Atribua explicitamente o grupo de arquivos como o grupo de arquivos NEXT USED usando ALTER PARTITION SCHEME ou uma operação de divisão subsequente irá falhar.  
  
> [!NOTE]  
>  Limitações com índice columnstore: somente partições vazias podem ser divididas quando existe um índice columnstore na tabela. Você precisará remover ou desabilitar o índice columnstore antes de executar esta operação.  
  
MERGE [ RANGE ( *boundary_value*) ]  
Descarta uma partição e mescla os valores que existirem na partição em uma partição restante. RANGE (*boundary_value*) deve ser um valor de limite existente no qual são mesclados os valores da partição descartada. Esse argumento remove o grupo de arquivos que originalmente continha *boundary_value* do esquema de partição, a menos que uma partição restante o utilize ou marque com a propriedade NEXT USED. A partição mesclada existe no grupo de arquivos que originalmente não continha *boundary_value*. *boundary_value* é uma expressão constante que pode fazer referência a variáveis (incluindo variáveis de tipo definido pelo usuário) ou funções (incluindo funções definidas pelo usuário). Ela não pode referenciar uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)]. *boundary_value* tem que corresponder ou ser implicitamente conversível para o tipo de dados de sua coluna de particionamento correspondente. Você também não pode truncar *boundary_value* durante a conversão implícita de forma que o tamanho e a escala do valor não correspondam aos valores correspondentes ao *input_parameter_type*.  
  
> [!NOTE]  
>  Limitações com índice columnstore: duas partições não vazias contendo um índice columnstore não podem ser mescladas. Você precisará remover ou desabilitar o índice columnstore antes de executar esta operação  
  
## <a name="best-practices"></a>Práticas recomendadas  
Sempre mantenha as partições vazias em ambas as extremidades do intervalo de partição. Mantenha as partições em ambas as extremidades para garantir que a divisão da partição e a mesclagem da partição não gerem nenhuma movimentação de dados. A divisão da partição ocorre no início e a mesclagem da partição ocorre no final. Evite dividir ou mesclar partições populadas. A divisão ou mesclagem de partições preenchidas pode ser ineficiente. Elas podem ser ineficientes porque a divisão ou mesclagem pode causar até quatro vezes mais geração de logs, e também pode causar bloqueio grave.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
ALTER PARTITION FUNCTION reparticiona quaisquer tabelas e índices que usam a função em uma única operação atômica. Entretanto, essa operação acontece offline e, dependendo da extensão de reparticionamento, pode utilizar muitos recursos.  
  
Use ALTER PARTITION FUNCTION somente para dividir uma partição em duas ou mesclar duas partições em uma. Para alterar a forma como uma tabela é particionada (por exemplo, de 10 partições em cinco), execute qualquer uma das opções a seguir. Dependendo da configuração do sistema, essas opções podem variar em consumo de recursos:  
  
-   Crie uma nova tabela particionada com a função de partição necessária. Em seguida, insira os dados da tabela antiga na nova tabela usando uma instrução INSERT INTO...SELECT FROM.  
  
-   Crie um índice clusterizado particionado em um heap.  
  
    > [!NOTE]  
    >  Descartando resultados de um índice clusterizado particionado em um heap particionado.  
  
-   Descarte e recrie um índice particionado existente usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE INDEX com a cláusula DROP EXISTING = ON.  
  
-   Execute uma sequência de instruções ALTER PARTITION FUNCTION.  
  
Todos os grupos de arquivos afetados por ALTER PARTITION FUNCTION devem estar online.  
  
ALTER PARTITION FUNCTION falha quando há um índice clusterizado desativado em qualquer tabela que usa a função de partição.  
  
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
[sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md) [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
[sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
[sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
