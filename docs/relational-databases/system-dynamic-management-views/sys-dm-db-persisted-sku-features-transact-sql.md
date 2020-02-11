---
title: sys. dm_db_persisted_sku_features (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server]
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: stevestein
ms.author: sstein
ms.openlocfilehash: f689541d455f4f7e6da4cc68742519a74f671506
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73981834"
---
# <a name="sysdm_db_persisted_sku_features-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Alguns recursos da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] alteração da maneira que [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena informações nos arquivos de banco de dados. Esses recursos são restritos a edições específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um banco de dados que contém esses recursos não pode ser movido para uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dê suporte a eles. Use a exibição de gerenciamento dinâmico sys. dm_db_persisted_sku_features para listar recursos específicos da edição que estão habilitados no banco de dados atual.
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior).
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Nome externo do recurso habilitado no banco de dados, mas que não possui suporte em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse recurso deve ser removido antes que o banco de dados possa ser migrado a todas as edições disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|feature_id|**int**|ID de recurso associada ao recurso. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="remarks"></a>Comentários  
 Se nenhum recurso que possa ser restringido por uma edição específica for usado pelo banco de dados, a exibição não retornará nenhuma linha.  
  
 sys. dm_db_persisted_sku_features pode listar os seguintes recursos de alteração de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como restrito a edições específicas:  
  
-   **ChangeCapture**: indica que um banco de dados está com o Change Data Capture habilitado. Para remover a captura de dados de alterações, use o procedimento armazenado [Sys. sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) . Para obter mais informações, veja [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **ColumnStoreIndex**: indica que pelo menos uma tabela tem um índice columnstore. Para permitir que um banco de dados seja movido para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição do que não ofereça suporte a esse recurso, use a instrução [drop index](../../t-sql/statements/drop-index-transact-sql.md) ou [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) para remover o índice columnstore. Para obter mais informações, consulte [índices Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior).  
  
-   **Compactação**: indica que pelo menos uma tabela ou índice usa a compactação de dados ou o formato de armazenamento vardecimal. Para habilitar um banco de dados a ser movido para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição do que não ofereça suporte a esse recurso, use a instrução [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) para remover a compactação de dados. Para remover o formato de armazenamento vardecimal, use a instrução sp_tableoption. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **MultipleFSContainers**: indica que o banco de dados usa vários contêineres FileStream. O banco de dados tem um grupo de arquivos FILESTREAM com vários contêineres (arquivos). Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **InMemoryOLTP**: indica que o banco de dados usa OLTP na memória. O banco de dados tem um grupo de arquivos MEMORY_OPTIMIZED_DATA. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior). 
  
-   **Particionamento.** Indica que o banco de dados contém tabelas particionadas, índices particionados, esquemas de partição ou funções de partição. Para que seja possível mover um banco de dados para outra edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não seja Enterprise ou Developer, não basta modificar a tabela para que se torne uma única partição. É necessário remover a tabela particionada. Se a tabela contiver dados, use SWITCH PARTITION para converter cada partição em uma tabela não particionada. Depois exclua a tabela particionada, o esquema de partição e a função de partição.  
  
-   **TransparentDataEncryption.** Indica que um banco de dados deve ser criptografado usando criptografia transparente de dados. Para remover a criptografia transparente de dados, use a instrução ALTER DATABASE. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> A [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] partir do Service Pack 1, esses recursos, exceto **TransparentDataEncryption.** estão disponíveis em várias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edições e não se limitam apenas às edições Enterprise ou Developer.

 Para determinar se um banco de dados usa qualquer recurso que seja restrito a edições específicas, execute a seguinte instrução no banco de dados:  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
