---
title: Erros comuns com o Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ee5e7fd6511a624b05b4d6c7d03c1f2dcd288054
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288020"
---
# <a name="common-errors-with-database-mail"></a>Erros comuns com o Database Mail 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Este artigo descreve alguns erros comuns encontrados no Database Mail e suas soluções.

## <a name="could-not-find-stored-procedure-sp_send_dbmail"></a>Não foi possível localizar o procedimento armazenado 'sp_send_dbmail'
O procedimento armazenado [sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) é instalado no banco de dados msdb. Você deve executar **sp_send_dbmail** do banco de dados msdb ou especificar um nome de três partes para o procedimento armazenado.

Exemplo:
```sql
EXEC msdb.dbo.sp_send_dbmail ...
```

Ou:

```sql
USE msdb;
GO
EXEC dbo.sp_send_dbmail ...
```

Use o [Assistente de Configuração do Database Mail](configure-database-mail.md) para habilitar e configurar o Database Mail.

## <a name="profile-not-valid"></a>O perfil não é válido
Há duas causas possíveis para essa mensagem. Ou o perfil especificado não existe ou o usuário que está executando [sp_send_dbmail (Transact-SQL)](../system-stored-procedures/sp-send-dbmail-transact-sql.md) não tem permissão para acessar o perfil.

Para verificar permissões para um perfil, execute o procedimento armazenado [sysmail_help_principalprofile_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md) com o nome do perfil. Use o procedimento armazenado [sysmail_add_principalprofile_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md) ou o [Assistente de Configuração do Database Mail](configure-database-mail.md) para permitir um usuário do msdb ou grupo acessar um perfil.

## <a name="permission-denied-on-sp_send_dbmail"></a>Permissão negada em sp_send_dbmail

Este tópico descreve como solucionar o problema de uma mensagem de erro que afirma que o usuário que está tentando enviar Database Mail não tem permissão para executar sp_send_dbmail.

O texto do erro é:

```
EXECUTE permission denied on object 'sp_send_dbmail', 
database 'msdb', schema 'dbo'.
```

Para enviar Database Mail, é necessário ser um usuário do banco de dados msdb e membro da função de banco de dados DatabaseMailUserRole no banco de dados msdb. Para adicionar usuários ou grupos do msdb a essa função, use o SQL Server Management Studio ou execute a instrução a seguir para o usuário ou função que precisa enviar Database Mail.

```sql
EXEC msdb.dbo.sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<user or role name>';
GO
```
Para obter mais informações, veja [sp_addrolemember](../system-stored-procedures/sp-addrolemember-transact-sql.md) e [sp_droprolemember](../system-stored-procedures/sp-droprolemember-transact-sql.md).

## <a name="database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log"></a>Database Mail colocado na fila, nenhuma entrada em sysmail_event_log ou no log de eventos de aplicativos do Windows 

O Database Mail depende do Service Broker para enfileiramento de mensagens de email. Se o Database Mail for interrompido ou se a entrega de mensagens do Service Broker não estiver ativada no banco de dados **msdb**, o Database Mail formará a fila do banco de dados de mensagens, mas não conseguirá entregar as mensagens. Nesse caso, as mensagens do Service Broker permanecem na fila de email do Service Broker. O Service Broker não ativará o programa externo e, logo, não haverá entradas de log em **sysmail_event_log**, nem atualizações do status do item em **sysmail_allitems** e nas exibições relacionadas.

Execute a seguinte instrução para verificar se o Service Broker está habilitado no banco de dados **msdb**:

```sql
SELECT is_broker_enabled FROM sys.databases WHERE name = 'msdb';
```

Um valor de 0 indica que a entrega de mensagens do Service Broker não está ativada no banco de dados msdb. Para corrigir o problema, ative o Service Broker no banco de dados com o seguinte comando Transact-SQL:

```sql
USE master ;
GO

ALTER DATABASE msdb SET ENABLE_BROKER ;
GO
``` 

O Database Mail depende de uma série de procedimentos armazenados internos. Para reduzir a área de superfície, esses procedimentos armazenados encontram-se desabilitados em novas instalações do SQL Server. Para habilitar esses procedimentos armazenados, use a [opção Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) do procedimento armazenado do sistema **sp_configure**, como no exemplo a seguir:

```sql
EXEC sp_configure 'show advanced options', 1;  
RECONFIGURE;
EXEC sp_configure 'Database Mail XPs', 1;  
RECONFIGURE  
GO  

Database Mail may be stopped in the **msdb** database. To check status of Database Mail, execute the following statement:

```sql
EXECUTE dbo.sysmail_help_status_sp;
```

Para iniciar o Database Mail em um banco de dados host de correio, execute o seguinte comando no banco de dados msdb:

```sql
EXECUTE dbo.sysmail_start_sp;
```

O Service Broker examina o tempo de vida da caixa de diálogo das mensagens quando se encontra ativado; portanto, toda mensagem que estiver na fila de transmissão do Service Broker por mais tempo que o tempo de vida configurado para a caixa de diálogo falhará imediatamente. O Database Mail atualiza o status de mensagens que falharam em [sysmail_allitems](../system-catalog-views/sysmail-allitems-transact-sql.md) e em exibições relacionadas. Você deve decidir se as mensagens devem ou não ser enviadas novamente. Para obter mais informações sobre como configurar o tempo de vida do diálogo utilizado pelo Database Mail, veja [sysmail_configure_sp (Transact-SQL)](../system-stored-procedures/sysmail-configure-sp-transact-sql.md).



##  <a name="see-also"></a><a name="RelatedContent"></a> Confira também
  
-  [Visão geral do Database Mail](database-mail.md)
-  [Criar um perfil do Database Mail](create-a-database-mail-profile.md)
  
  
