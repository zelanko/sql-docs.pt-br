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
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Modifica as opções de tamanho máximo do banco de dados para tabelas replicadas, tabelas distribuídas e para o log de transações no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use esta instrução para gerenciar as alocações de espaço em disco para um banco de dados à medida que ele aumenta ou diminui de tamanho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 O nome do banco de dados a ser modificado. Para exibir uma lista de bancos de dados no dispositivo, use [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 AUTOGROW = { ON | OFF }  
 Atualiza a opção AUTOGROW. Quando AUTOGROW for ON, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] aumentará automaticamente o espaço alocado para tabelas replicadas, tabelas distribuídas e log de transações, conforme o necessário, para acomodar o crescimento dos requisitos de armazenamento. Quando o crescimento automático for OFF, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] retornará um erro se as tabelas, replicadas, as tabelas distribuída ou o log de transações exceder o tamanho máximo.  
  
 REPLICATED_SIZE = *size* [GB]  
 Especifica o novo máximo de gigabytes por nó de computação para armazenar todas as tabelas replicadas no banco de dados que está sendo alterado. Se você estiver planejando o espaço de armazenamento do dispositivo, multiplique REPLICATED_SIZE pelo número de nós de computação no dispositivo.  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 Especifica o novo máximo de gigabytes por banco de dados para armazenar todas as tabelas distribuídas no banco de dados que está sendo alterado. O tamanho é distribuído entre todos os nós de computação no dispositivo.  
  
 LOG_SIZE = *size* [GB]  
 Especifica o novo máximo de gigabytes por banco de dados para armazenar todos os logs de transações no banco de dados que está sendo alterado. O tamanho é distribuído entre todos os nós de computação no dispositivo.  
  
 ENCRYPTION { ON | OFF }  
 Define o banco de dados a ser criptografado (ON) ou não criptografado (OFF). A criptografia poderá ser configurada para o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] somente quando [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) tiver sido definido como **1**. Uma chave de criptografia do banco de dados precisa ser criada para que a Transparent Data Encryption possa ser configurada. Para obter mais informações sobre a criptografia do banco de dados, confira [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no banco de dados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Os valores de REPLICATED_SIZE, DISTRIBUTED_SIZE e LOG_SIZE podem ser maiores, iguais ou menores que os valores atuais do banco de dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 As operações de crescimento e redução são aproximadas. Os tamanhos reais resultantes podem variar em relação aos parâmetros de tamanho.  
  
 O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não executa a instrução ALTER DATABASE como uma operação atômica. Se a instrução for anulada durante a execução, as alterações já feitas permanecerão.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Usa um bloqueio compartilhado no objeto DATABASE. Não é possível alterar um banco de dados que esteja sendo usado por outro usuário para leitura ou gravação. Isso inclui as sessões que emitiram uma instrução [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) no banco de dados.  
  
## <a name="performance"></a>Desempenho  
 A redução de um banco de dados pode demorar bastante e usar uma grande quantidade de recursos do sistema, dependendo do tamanho dos dados reais no banco de dados e da quantidade de fragmentação no disco. Por exemplo, a redução de um banco de dados pode levar várias horas ou mais.  
  
## <a name="determining-encryption-progress"></a>Determinando o andamento da criptografia  
 Use a consulta a seguir para determinar o andamento da Transparent Data Encryption do banco de dados como um percentual:  
  
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
  
 Para obter um exemplo abrangente que demonstra todas as etapas da implementação de TDE, confira [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Alterando a configuração AUTOGROW  
 Defina AUTOGROW como ON para o banco de dados `CustomerSales`.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. Alterando o armazenamento máximo para tabelas replicadas  
 O exemplo a seguir define o limite de armazenamento de tabela replicada em 1 GB para o banco de dados `CustomerSales`. Este é o limite de armazenamento por nó de computação.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Alterando o armazenamento máximo para tabelas distribuídas  
 O exemplo a seguir define o limite de armazenamento de tabela distribuída para 1000 GB (um terabyte) para o banco de dados `CustomerSales`. Este é o limite de armazenamento combinado no dispositivo para todos os nós de computação, não o limite de armazenamento por nó de computação.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Alterando o armazenamento máximo para o log de transações  
 O exemplo a seguir atualiza o banco de dados `CustomerSales` para que o tamanho máximo do log de transações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja de 10 GB para o dispositivo.  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
