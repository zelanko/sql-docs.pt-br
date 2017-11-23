---
title: sys.DM db_persisted_sku_features (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs: TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6108de273aedd3808a1941da5c152c6c774e5804
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Alguns recursos do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] alterar a maneira que [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena informações nos arquivos de banco de dados. Esses recursos são restritos a edições específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um banco de dados que contém esses recursos não pode ser movido para uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dê suporte a eles. Use o modo de exibição de gerenciamento dinâmico sys.DM db_persisted_sku_features para listar os recursos específicos de edição habilitados no banco de dados atual.
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Nome externo do recurso habilitado no banco de dados, mas que não possui suporte em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse recurso deve ser removido antes que o banco de dados possa ser migrado a todas as edições disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|feature_id|**int**|ID de recurso associada ao recurso. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Se nenhum recurso que pode ser restrita por uma edição específica é usado pelo banco de dados, a exibição não retorna nenhuma linha.  
  
 sys.DM db_persisted_sku_features pode listar os seguintes recursos de alteração de banco de dados como restritos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edições:  
  
-   **ChangeCapture**: indica que um banco de dados tem o change data capture está habilitado. Para remover o change data capture, use o [sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) procedimento armazenado. Para obter mais informações, veja [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **ColumnStoreIndex**: indica que pelo menos uma tabela tem um índice columnstore. Para habilitar um banco de dados a ser movida para uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dá suporte a esse recurso, use o [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) ou [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instrução para remover o índice columnstore. Para obter mais informações, consulte [índices Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **Compactação**: indica que pelo menos uma tabela ou índice usa compactação de dados ou o formato de armazenamento vardecimal. Para habilitar um banco de dados a ser movida para uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dá suporte a esse recurso, use o [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instrução para remover a compactação de dados. Para remover o formato de armazenamento vardecimal, use a instrução sp_tableoption. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **MultipleFSContainers**: indica que o banco de dados usa vários contêineres FILESTREAM. O banco de dados tem um grupo de arquivos FILESTREAM com vários contêineres (arquivos). Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **InMemoryOLTP**: indica que o banco de dados usa OLTP na memória. O banco de dados tem um grupo de arquivos MEMORY_OPTIMIZED_DATA. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **O particionamento.** Indica que o banco de dados contém tabelas particionadas, índices particionados, esquemas de partição ou funções de partição. Para que seja possível mover um banco de dados para outra edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não seja Enterprise ou Developer, não basta modificar a tabela para que se torne uma única partição. É necessário remover a tabela particionada. Se a tabela contiver dados, use SWITCH PARTITION para converter cada partição em uma tabela não particionada. Depois exclua a tabela particionada, o esquema de partição e a função de partição.  
  
-   **TransparentDataEncryption.** Indica que um banco de dados deve ser criptografado usando criptografia transparente de dados. Para remover a criptografia transparente de dados, use a instrução ALTER DATABASE. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1, esses recursos estão disponíveis em vários [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edições e não se limitando a Enterprise ou Developer Editions somente.

 Para determinar se um banco de dados usa qualquer recurso que seja restrito a edições específicas, execute a seguinte instrução no banco de dados:  
  
```t-sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
