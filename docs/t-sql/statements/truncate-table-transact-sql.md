---
title: TRUNCATE TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TRUNCATE
- TRUNCATE TABLE
- TRUNCATE_TSQL
- TRUNCATE_TABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server], TRUNCATE TABLE statement
- table truncating [SQL Server]
- removing rows
- TRUNCATE TABLE statement
- deleting rows
- dropping rows
ms.assetid: 3d544eed-3993-4055-983d-ea334f8c5c58
caps.latest.revision: 41
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e72eb9b870a0525739f657432a3cddbf17ac438f
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451290"
---
# <a name="truncate-table-transact-sql"></a>TRUNCATE TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove todas as linhas de uma tabela ou partições especificadas de uma tabela sem registrar as exclusões de linha individual. TRUNCATE TABLE é semelhante à instrução DELETE sem nenhuma cláusula WHERE; entretanto, TRUNCATE TABLE é mais rápida e utiliza menos recursos de sistema e log de transações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
TRUNCATE TABLE   
    [ { database_name .[ schema_name ] . | schema_name . } ]  
    table_name  
    [ WITH ( PARTITIONS ( { <partition_number_expression> | <range> }   
    [ , ...n ] ) ) ]  
[ ; ]  
  
<range> ::=  
<partition_number_expression> TO <partition_number_expression>  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
TRUNCATE TABLE [ { database_name . [ schema_name ] . | schema_name . ] table_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela pertence.  
  
 *table_name*  
 É o nome da tabela a ser truncada ou da qual todas as linhas são removidas. *table_name* deve ser um literal. *table_name* não pode ser a função **OBJECT_ID()** nem uma variável.  
  
 WITH ( PARTITIONS ( { \<*partition_number_expression*> | \<*range*> } [ , ...n ] ) )  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Especifica as partições para truncar ou das quais todas as linhas são removidas. Se a tabela não for particionada, o argumento **WITH PARTITIONS** gerará um erro. Se a cláusula **WITH PARTITIONS** não for fornecida, a tabela inteira será truncada.  
  
 *\<partition_number_expression>* pode ser especificado das seguintes maneiras: 
  
-   Forneça o número de uma partição, por exemplo: `WITH (PARTITIONS (2))`  
  
-   Forneça os números de várias partições individuais separados por vírgulas, por exemplo: `WITH (PARTITIONS (1, 5))`  
  
-   Forneça os intervalos e as partições individuais, por exemplo: `WITH (PARTITIONS (2, 4, 6 TO 8))`  
  
-   *\<range>* pode ser especificado como números de partição separados pela palavra **TO**, por exemplo: `WITH (PARTITIONS (6 TO 8))`  
  
 Para truncar uma tabela particionada, a tabela e os índices deverão estar alinhados (particionados na mesma função de partição).  
  
## <a name="remarks"></a>Remarks  
 Em comparação com a instrução DELETE, TRUNCATE TABLE possui as seguintes vantagens:  
  
-   O espaço utilizado para log de transações é menor.  
  
     A instrução DELETE remove as linhas uma de cada vez e registra uma entrada no log de transações para cada linha excluída. TRUNCATE TABLE remove os dados desalocando as páginas de dados usadas para armazenar os dados da tabela e registra somente as desalocações de página no log de transações.  
  
-   Normalmente são utilizados menos bloqueios.  
  
     Quando a instrução DELETE é executada com o uso de um bloqueio de linha, cada linha na tabela é bloqueada para exclusão. TRUNCATE TABLE sempre bloqueia a tabela (incluindo um bloqueio de esquema (SCH-M)) e a página, mas não cada linha.  
  
-   Sem exceção, nenhuma página é deixada na tabela.  
  
     Após a execução de uma instrução DELETE, a tabela ainda pode conter páginas vazias. Por exemplo, páginas vazias em um heap não podem ser desalocadas sem pelo menos um bloqueio de tabela exclusivo (LCK_M_X). Se a operação de exclusão não usar um bloqueio de tabela, a tabela (heap) conterá muitas páginas vazias. Para índices, a operação de exclusão pode deixar páginas vazias, embora essas páginas sejam desalocadas rapidamente por um processo de limpeza em segundo plano.  
  
 TRUNCATE TABLE remove todas as linhas de uma tabela, mas permanecem a estrutura da tabela e suas colunas, restrições, índices, etc. Para remover a definição de tabela junto com seus dados, use a instrução DROP TABLE.  
  
 Se a tabela contiver uma coluna de identidade, o contador daquela coluna será redefinido no valor da semente definido para a coluna. Se não for definida nenhuma semente, o valor padrão utilizado será 1. Para manter o contador de identidade, use DELETE.  
  
## <a name="restrictions"></a>Restrictions  
 Você não pode usar TRUNCATE TABLE em tabelas que:  
  
-   São referenciadas por uma restrição FOREIGN KEY. (É possível truncar uma tabela que tenha uma chave estrangeira que referencie a ela mesma.)  
  
-   Participam de uma exibição indexada.  
  
-   São publicadas com replicação transacional ou replicação de mesclagem.  
  
 Para tabelas com uma ou mais dessas características, use a instrução DELETE.  
  
 TRUNCATE TABLE não pode ativar um gatilho porque a operação não registra exclusões de linhas individuais. Para obter mais informações, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md). 
 
 Em [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[sspdw](../../includes/sspdw-md.md)]:

- TRUNCATE TABLE não é permitida dentro da instrução EXPLAIN.

- TRUNCATE TABLE não pode ser executada dentro de uma transação.
  
## <a name="truncating-large-tables"></a>Truncando tabelas grandes  
 O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem a capacidade de remover ou truncar tabelas com mais de 128 extensões sem manter bloqueios simultâneos em todas as extensões necessárias para a remoção.  
  
## <a name="permissions"></a>Permissões  
 A permissão mínima necessária é ALTER em *table_name*. As permissões TRUNCATE TABLE assumem como padrão o proprietário da tabela, membros da função de servidor fixa sysadmin, e das funções de banco de dados fixas db_owner e db_ddladmin, e não são transferíveis. Entretanto, você pode incorporar a instrução TRUNCATE TABLE dentro de um módulo, como um procedimento armazenado, e conceder permissões adequadas ao módulo por meio da cláusula EXECUTE AS.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-truncate-a-table"></a>A. Truncar uma tabela  
 O exemplo a seguir remove todos os dados da tabela `JobCandidate`. São incluídas instruções `SELECT` antes e depois da instrução `TRUNCATE TABLE` para comparar resultados.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT COUNT(*) AS BeforeTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
TRUNCATE TABLE HumanResources.JobCandidate;  
GO  
SELECT COUNT(*) AS AfterTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
```  
  
### <a name="b-truncate-table-partitions"></a>B. Truncar a tabela de partições  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 O exemplo a seguir trunca as partições especificadas de uma tabela particionada. A sintaxe `WITH (PARTITIONS (2, 4, 6 TO 8))` faz com que os número de partição 2, 4, 6, 7 e 8 sejam truncados.  
  
```sql  
TRUNCATE TABLE PartitionTable1   
WITH (PARTITIONS (2, 4, 6 TO 8));  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  

