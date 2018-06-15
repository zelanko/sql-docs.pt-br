---
title: managed_backup.sp_ backup_master_switch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_ backup_master_switch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 64d6681203962b54f1f3daae2de26e695cec240c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33237366"
---
# <a name="managedbackupsp-backupmasterswitch-transact-sql"></a>managed_backup.sp_ backup_master_switch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Pausa ou retoma o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 Use este procedimento armazenado para pausar temporariamente e, depois, retomar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Isso garante que todos os parâmetros de configuração permanecerão e serão mantidos quando as operações forem retomadas. Quando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] for pausado, o período de retenção não será imposto. Isso significa que não há nenhuma verificação para determinar se os arquivos devem ser excluídos do armazenamento, ou se há um arquivo de backup danificado ou uma interrupção na cadeia de logs.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@state = ] { 0 | 1}  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @state  
 Defina o estado do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. O @state parâmetro é **BIT**. Quando definido como um valor 0, as operações serão pausadas; quando definido como um valor 1, a operação será retomada.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
 Descreve assuntos de segurança relacionados às permissões statement.Include como uma subseção (título H3). Considere incluir outras subseções para o Encadeamento de Propriedade e Auditoria se apropriado.  
  
### <a name="permissions"></a>Permissões  
 Exige associação à função de banco de dados **db_backupoperator** , com permissões **ALTER ANY CREDENTIAL** e as permissões **EXECUTE** no procedimento armazenado **sp_delete_backuphistory**.  
  
## <a name="examples"></a>Exemplos  
 O seguinte exemplo pode ser usado para pausar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] na instância em que ele é executado:  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=0;  
Go  
  
```  
  
 O exemplo a seguir pode ser usado para retomar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=1;  
Go  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
