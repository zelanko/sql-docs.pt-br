---
title: managed_backup. fn_get_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_get_parameter_TSQL
- smart_admin.fn_get_parameter
- fn_get_parameter_TSQL
- fn_get_parameter
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_parameter
- smart_admin.fn_get_parameter
ms.assetid: ed94e54d-4516-4806-a8ce-f013d3a04122
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 18a42273218bb73de55694b9b54877a4f2e0f669
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68140648"
---
# <a name="managed_backupfn_get_parameter-transact-sql"></a>managed_backup. fn_get_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna uma tabela com 0, 1 ou mais linhas de pares de parâmetro e valor.  
  
 Use este procedimento armazenado para revisar todos os parâmetros de configuração ou um específico para o Smart Admin.  
  
 Se o parâmetro nunca tiver sido configurado, a função não retornará linhas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
managed_backup.fn_get_parameter ('parameter_name' | '' | NULL )  
```  
  
##  <a name="Arguments"></a> Argumentos  
 parameter_name  
 Nome do parâmetro. parameter_name é **nvarchar (128)**. Se NULL ou uma cadeia de caracteres vazia for fornecido como um argumento para a função, os pares de nome-valor para todos os parâmetros configurados do Smart Admin serão retornados.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|parameter_name|NVARCHAR(128)|Nome do parâmetro. Veja a seguir uma lista atual de parâmetros retornados:<br/><br/>**FileRetentionDebugXevent**<br/><br/>**SSMBackup2WADebugXevent**<br/><br/>**SSMBackup2WANotificationEmailIds**<br/><br/>**SSMBackup2WAEnableUserDefinedPolicy**<br/><br/>**SSMBackup2WAEverConfigured**<br/><br/>**StorageOperationDebugXevent**|  
|parameter_value|NVARCHAR(128)|Valor do conjunto atual do parâmetro.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer permissões SELECT na função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todos os parâmetros configurados pelo menos uma vez e os valores atuais.  
  
```  
USE MSDB  
GO  
SELECT *   
FROM managed_backup.fn_get_parameter (NULL)  
  
```  
  
 O exemplo a seguir retorna a ID de email especificada para receber as notificações de erro. Se nenhuma linha for retornada, isso significará que essa opção de notificação de email não foi habilitada.  
  
```  
USE MSDB  
GO  
SELECT *  
FROM managed_backup.fn_get_parameter ('SSMBackup2WANotficationEmailIds')  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Backup Gerenciado do SQL Server para o Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
