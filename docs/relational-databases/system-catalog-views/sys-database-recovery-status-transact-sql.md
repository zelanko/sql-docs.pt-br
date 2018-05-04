---
title: sys. database_recovery_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 665b0d28cd6b77387058c95cd84b4677ab0fc98a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaserecoverystatus-transact-sql"></a>sys.database_recovery_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha por banco de dados. Se o banco de dados não estiver aberto, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] tentará iniciá-lo.  
  
 Para ver a linha para um banco de dados diferente de **mestre** ou **tempdb**, aplique um dos seguintes:  
  
-   Ser o proprietário do banco de dados.  
  
-   Ter permissões ALTER ANY DATABASE ou VIEW ANY DATABASE no nível de servidor.  
  
-   Ter a permissão CREATE DATABASE o **mestre** banco de dados.    
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**Int**|ID do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**database_guid**|**uniqueidentifier**|Usado para relacionar em conjunto todos os arquivos de um banco de dados. Todos os arquivos devem ter este GUID na página de cabeçalho para que o banco de dados seja iniciado como esperado. Apenas um banco de dados deve ter esse GUID, mas duplicatas podem ser criadas copiando-se e anexando-se bancos de dados. RESTORE sempre gera um novo GUID quando você restaura um banco de dados que ainda não existe.<br /><br /> NULL= O banco de dados está offline ou não será iniciado.|  
|**family_guid**|**uniqueidentifier**|Identificador da "família de backup" do banco de dados para detectar estados de restauração correspondentes.<br /><br /> NULL = banco de dados está offline ou o banco de dados não será iniciado.|  
|**last_log_backup_lsn**|**numeric(25,0)**|O número de sequência de log inicial do próximo backup de log.<br /><br /> Se for NULL, um log de transações de volta até não pode ser executado porque o banco de dados está em recuperação simples ou não há nenhum backup de banco de dados atual.|  
|**recovery_fork_guid**|**uniqueidentifier**|Identifica a bifurcação de recuperação atual em que o banco de dados está atualmente ativo.<br /><br /> NULL= O banco de dados está offline ou não será iniciado.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|Identificador da bifurcação de recuperação inicial.<br /><br /> NULL= O banco de dados está offline ou não será iniciado.|  
|**fork_point_lsn**|**numeric(25,0)**|Se **first_recovery_fork_guid** não é igual (! =) para **recovery_fork_guid**, **fork_point_lsn** é o número de sequência de log do ponto de bifurcação atual. Caso contrário, o valor será NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibição de catálogo do bancos de dados e de arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
