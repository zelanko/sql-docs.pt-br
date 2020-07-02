---
title: sys. database_recovery_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_recovery_status_TSQL
- database_recovery_status
- sys.database_recovery_status
- sys.database_recovery_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_recovery_status catalog view
ms.assetid: 46fab234-1542-49be-8edf-aa101e728acf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e91b41815f39e27bc368a4d61ce84fc23635f160
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734826"
---
# <a name="sysdatabase_recovery_status-transact-sql"></a>sys.database_recovery_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha por banco de dados. Se o banco de dados não estiver aberto, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] tentará iniciá-lo.  
  
 Para ver a linha de um banco de dados que não seja o **mestre** ou o **tempdb**, uma das seguintes opções deve ser aplicada:  
  
-   Ser o proprietário do banco de dados.  
  
-   Ter permissões ALTER ANY DATABASE ou VIEW ANY DATABASE no nível de servidor.  
  
-   Ter a permissão CREATE DATABASE no banco de dados **mestre** .    
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**database_guid**|**uniqueidentifier**|Usado para relacionar em conjunto todos os arquivos de um banco de dados. Todos os arquivos devem ter este GUID na página de cabeçalho para que o banco de dados seja iniciado como esperado. Apenas um banco de dados deve ter esse GUID, mas duplicatas podem ser criadas copiando-se e anexando-se bancos de dados. RESTORE sempre gera um novo GUID quando você restaura um banco de dados que ainda não existe.<br /><br /> NULL= O banco de dados está offline ou não será iniciado.|  
|**family_guid**|**uniqueidentifier**|Identificador da "família de backup" do banco de dados para detectar estados de restauração correspondentes.<br /><br /> NULL = o banco de dados está offline ou o banco de dados não será iniciado.|  
|**last_log_backup_lsn**|**numeric(25,0)**|O número de sequência de log inicial do próximo backup de log.<br /><br /> Se for NULL, um backup de log de transações não poderá ser executado porque o banco de dados está em uma recuperação simples ou não há backup de banco de dados atual.|  
|**recovery_fork_guid**|**uniqueidentifier**|Identifica a bifurcação de recuperação atual em que o banco de dados está atualmente ativo.<br /><br /> NULL= O banco de dados está offline ou não será iniciado.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|Identificador da bifurcação de recuperação inicial.<br /><br /> NULL= O banco de dados está offline ou não será iniciado.|  
|**fork_point_lsn**|**numeric(25,0)**|Se **first_recovery_fork_guid** não for igual (! =) a **recovery_fork_guid**, **fork_point_lsn** será o número de sequência de log do ponto de bifurcação atual. Caso contrário, o valor será NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de bancos de dados e arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
