---
title: managed_backup. sp_set_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_parameter_TSQL
- sp_set_parameter
- smart_admin.sp_set_parameter
- smart_admin.sp_set_parameter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_parameter
- smart_admin.sp_set_parameter
ms.assetid: bd8ae5fd-1337-4b7f-b0a4-153cbca9fa5f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 838a8b0d998476a37b0dd4d30cab5041ad4276a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942031"
---
# <a name="managed_backupsp_set_parameter-transact-sql"></a>managed_backup. sp_set_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Define o valor do parâmetro do sistema Smart Admin especificado.  
  
 Os parâmetros disponíveis são relacionados a [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Esses parâmetros são usados para definir as notificações de email, habilitar eventos estendidos específicos e habilitar políticas de gerenciamento com base em políticas definidas pelo usuário. Você deve especificar o nome do parâmetro e os pares de valor do parâmetro.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @parameter_name  
 O nome do parâmetro para o qual você quer definir o valor. @parameter_nameé NVARCHAR (128). Os nomes de parâmetro disponíveis são **SSMBackup2WANotificationEmailIds**, **SSMBackup2WADebugXevent**, **SSMBackup2WAEnableUserDefinedPolicy**, **FileRetentionDebugXevent**e **StorageOperationDebugXevent**.  
  
 @parameter_value  
 O valor para o parâmetro que você quer definir. @parametero valor é NVARCHAR (128).  Veja a seguir o nome do parâmetro e os pares de valor permitidos:  
  
-   @parameter_name= ' SSMBackup2WANotificationEmailIds ': @parameter_value = ' email '  
  
-   @parameter_name= ' SSMBackup2WAEnableUserDefinedPolicy ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' SSMBackup2WADebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' FileRetentionDebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' StorageOperationDebugXevent ' = {' true ' | ' false '}  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="best-practices"></a>Práticas Recomendadas  
 A seção opcional que descreve as práticas recomendadas que o usuário deve saber ao executar a instrução ou a rotina.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer permissões **Execute** em **managed_backup. sp_set_parameter** procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir permitem eventos operacionais e estendidos de depuração.  
  
```  
-- to enable operational events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionOperationalXevent', 'True'  
--  to enable debug events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
```  
  
 O exemplo a seguir habilita notificações de email de erros e avisos, e define o emailID a ser usado para enviar notificações para:  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
```  
  
  
