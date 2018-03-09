---
title: ALTER DATABASE (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7db44d9c9f02618e4d95a9d3eb9dfc581438dea5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTERAR o banco de dados (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Modifica as opções de tamanho máximo do banco de dados para tabelas replicadas, tabelas distribuídas e o log de transações em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use esta instrução para gerenciar as alocações de espaço em disco para um banco de dados, pois ele aumenta ou diminui de tamanho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]  
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados a ser modificado. Para exibir uma lista de bancos de dados no dispositivo, use [sys. Databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 AUMENTO AUTOMÁTICO = {ON | OFF}  
 A opção de aumento automático de atualizações. Quando o crescimento automático for ON, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] automaticamente aumenta o espaço alocado para tabelas replicadas, tabelas distribuídas e o log de transações conforme necessário para acomodar o crescimento dos requisitos de armazenamento. Quando o crescimento automático for OFF, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] retorna um erro se tabelas, replicadas distribuídas tabelas, ou o log de transações excede o tamanho máximo.  
  
 REPLICATED_SIZE = *size* [GB]  
 Especifica os novo gigabytes máxima por nó de computação para armazenar todas as tabelas replicadas no banco de dados que está sendo alterado. Se você estiver planejando para espaço de armazenamento do dispositivo, você precisará multiplicar REPLICATED_SIZE pelo número de nós de computação no dispositivo.  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 Especifica os novo gigabytes máximo por banco de dados para armazenar todas as tabelas distribuídas no banco de dados que está sendo alterado. O tamanho é distribuído por todos os nós de computação no dispositivo.  
  
 LOG_SIZE = *size* [GB]  
 Especifica os novo gigabytes máximo por banco de dados para armazenar todos os logs de transação no banco de dados que está sendo alterado. O tamanho é distribuído por todos os nós de computação no dispositivo.  
  
 CRIPTOGRAFIA {ON | OFF}  
 Define o banco de dados a ser criptografado (ON) ou não criptografado (OFF). Criptografia só pode ser configurada para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] quando [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) foi definida como **1**. Uma chave de criptografia do banco de dados deve ser criada antes de criptografia transparente de dados pode ser configurada. Para obter mais informações sobre criptografia de banco de dados, consulte [Transparent Data Encryption &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no banco de dados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Os valores para REPLICATED_SIZE, DISTRIBUTED_SIZE e LOG_SIZE podem ser maior que, igual ou menor do que os valores atuais para o banco de dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Crescimento e operações de redução são aproximadas. Os tamanhos reais resultantes podem variar com os parâmetros de tamanho.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]não execute a instrução ALTER DATABASE como uma operação atômica. Se a instrução é interrompida durante a execução, as alterações que já tenham ocorrido permanecerá.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Leva um bloqueio compartilhado no objeto de banco de dados. Não é possível alterar um banco de dados está em uso por outro usuário para leitura ou gravação. Isso inclui sessões que emitiram um [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) instrução no banco de dados.  
  
## <a name="performance"></a>Desempenho  
 Reduzindo um banco de dados pode levar a uma grande quantidade de tempo e recursos do sistema, dependendo do tamanho dos dados reais no banco de dados e a quantidade de fragmentação no disco. Por exemplo, a redução de um banco de dados pode levar várias horas ou mais.  
  
## <a name="determining-encryption-progress"></a>Determinando o andamento de criptografia  
 Use a consulta a seguir para determinar o progresso da criptografia transparente de dados de banco de dados como uma porcentagem:  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 Para um exemplo completo que demonstra todas as etapas na TDE de implementação, consulte [Transparent Data Encryption &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Alterando a configuração de aumento automático  
 Defina o crescimento automático como ON para o banco de dados `CustomerSales`.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Alterando o máximo de armazenamento para tabelas replicadas  
 O exemplo a seguir define o limite de armazenamento de tabela replicada a 1 GB para o banco de dados `CustomerSales`. Este é o limite de armazenamento por nó de computação.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Alterando o máximo de armazenamento para tabelas distribuídas  
 O exemplo a seguir define o limite de armazenamento de tabela distribuída para 1000 GB (um terabyte) para o banco de dados `CustomerSales`. Este é o limite de armazenamento combinado de dispositivo para todos os nós de computação, não o limite de armazenamento por nó de computação.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Alterando o armazenamento máximo para o log de transações  
 O exemplo a seguir atualiza o banco de dados `CustomerSales` para ter no máximo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tamanho do log de transações de 10 GB para o dispositivo.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar banco de dados &#40; Parallel Data Warehouse &#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
