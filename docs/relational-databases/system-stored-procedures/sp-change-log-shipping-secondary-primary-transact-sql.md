---
title: sp_change_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 757d842dfe0521bd8195bf85e02a3ed0eee2b5b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68045797"
---
# <a name="sp_change_log_shipping_secondary_primary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as configurações do banco de dados secundário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @primary_server = ] 'primary_server'`O nome da instância primária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs. *primary_server* é **sysname** e não pode ser nulo.  
  
`[ @primary_database = ] 'primary_database'`É o nome do banco de dados no servidor primário. *primary_database* é **sysname**, sem padrão.  
  
`[ @backup_source_directory = ] 'backup_source_directory'`O diretório em que os arquivos de backup de log de transações do servidor primário são armazenados. *backup_source_directory* é **nvarchar (500)** e não pode ser NULL.  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'`O diretório no servidor secundário para onde os arquivos de backup são copiados. *backup_destination_directory* é **nvarchar (500)** e não pode ser NULL.  
  
`[ @file_retention_period = ] 'file_retention_period'`É o período em minutos em que o histórico será retido. *history_retention_period* é **int**, com um padrão de NULL. Se nenhum valor for especificado, será usado o valor 14.420.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'`O modo de segurança usado para se conectar ao servidor monitor.  
  
 1 = Autenticação do Windows;  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. *monitor_server_security_mode* é **bit** e não pode ser nulo.  
  
`[ @monitor_server_login = ] 'monitor_server_login'`É o nome de usuário da conta usada para acessar o servidor monitor.  
  
`[ @monitor_server_password = ] 'monitor_server_password'`É a senha da conta usada para acessar o servidor monitor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_change_log_shipping_secondary_primary** deve ser executado do banco de dados **mestre** no servidor secundário. Esse procedimento armazenado faz o seguinte:  
  
1.  Altera as configurações na **log_shipping_secondary** registros conforme necessário.  
  
2.  Se o servidor monitor for diferente do servidor secundário, o registro do monitor de alterações no **log_shipping_monitor_secondary** no servidor monitor usando argumentos fornecidos, se necessário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
