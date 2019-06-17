---
title: Fazer backup e restaurar índices e catálogos de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 28ab36c2f9f500df89b1d936ec60871c0904bc1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012817"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>Fazer backup e restaurar índices e catálogos de texto completo
  Este tópico explica como fazer backup e restauração de índices de texto completo criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o catálogo de texto completo é um conceito lógico e não reside em um grupo de arquivos. Por isso, para fazer backup de um catálogo de texto completo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessário identificar cada grupo de arquivos que contém um índice de texto completo do catálogo e fazer backup de cada um deles. Depois, faça backup desses grupos de arquivos, um por um.  
  
> [!IMPORTANT]  
>  É possível importar catálogos de texto completo durante a atualização de um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Cada catálogo de texto completo importado é um arquivo de banco de dados em seu próprio grupo de arquivos. Para fazer backup de um catálogo importado, basta fazer backup do grupo de arquivos correspondente. Para obter mais informações, veja [Fazendo backup e restaurando catálogos de texto completo](https://go.microsoft.com/fwlink/?LinkID=121052), nos Manuais Online do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
##  <a name="backingup"></a> Fazendo backup dos índices de texto completo de um catálogo de texto completo  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> Localizando os índices de texto completo de um catálogo de texto completo  
 É possível recuperar as propriedades dos índices de texto completo usando a seguinte instrução [SELECT](/sql/t-sql/queries/select-transact-sql) , que seleciona colunas das exibições do catálogo [sys.fulltext_indexes](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql) e [sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql) .  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  

  
###  <a name="Find_FG_of_FTI"></a> Localizando o grupo de arquivos ou o arquivo que contém um índice de texto completo  
 Quando criado, um índice de texto completo é colocado em um destes locais:  
  
-   Um grupo de arquivos especificado pelo usuário.  
  
-   O mesmo grupo de arquivos como tabela base ou exibição, para uma tabela não particionada.  
  
-   O grupo de arquivos principal, para uma tabela particionada.  
  
> [!NOTE]  
>  Para obter informações sobre como criar um índice de texto completo, veja [Criar e gerenciar índices de texto completo](create-and-manage-full-text-indexes.md) e [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql).  
  
 Para localizar o grupo de arquivos do índice de texto completo em uma tabela ou exibição, use a seguinte consulta, em que *object_name* corresponde ao nome da tabela ou exibição:  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  

  
###  <a name="Back_up_FTIs_of_FTC"></a> Fazendo backup dos grupos de arquivos que contêm índices de texto completo  
 Depois de localizar os grupos de arquivos que contêm os índices de um catálogo de texto completo, você precisa fazer backup de cada um dos grupos de arquivos. Durante o processo de backup, catálogos de texto completo não podem ser descartados ou adicionados.  
  
 O primeiro backup de um grupo de arquivos deve ser um backup de arquivo completo. Depois de ter criado um backup de arquivo completo de um grupo de arquivos, você pode fazer backup somente das alterações feitas em um grupo de arquivos; para isso, crie uma série de um ou mais backups de arquivo diferenciais baseados no backup de arquivo completo.  
  
 **Para efetuar backup de arquivos e grupos de arquivos**  
  
-   [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  

  
##  <a name="Restore_FTI"></a> Restaurando um índice de texto completo  
 A restauração de um grupo de arquivos submetido a backup restaura os arquivos de índice de texto completo, bem como os demais arquivos do grupo de arquivos. Por padrão, o grupo de arquivos é restaurado no local do disco em que foi feito backup do grupo de arquivos.  
  
 Se uma tabela indexada com texto completo estava online e uma operação de população estava sendo executada quando o backup foi criado, a população será retomada após a restauração.  
  
 **Para restaurar um grupo de arquivos**  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos sobre arquivos existentes &#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar arquivos em um novo local &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  

  
## <a name="see-also"></a>Consulte também  
 [Gerenciar e monitorar a pesquisa de texto completo em uma instância do servidor](manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [Atualizar pesquisa de texto completo](upgrade-full-text-search.md)  
  
  
