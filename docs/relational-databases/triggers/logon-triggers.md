---
title: Gatilhos de logon | Microsoft Docs
ms.custom: ''
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ebc4f10802f7a90dc828bab4b6f2aa1d01d6ccd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68058618"
---
# <a name="logon-triggers"></a>Gatilhos de logon
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  Os gatilhos de logon acionam procedimentos armazenados em resposta a um evento LOGON. Esse evento ocorre quando é estabelecida uma sessão de usuário com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os gatilhos de logon são acionados após o término da fase de autenticação, mas antes da sessão de usuário ser realmente estabelecida. Logo, todas as mensagens originadas no gatilho que chegariam, normalmente, ao usuário, como mensagens de erro e mensagens da instrução PRINT, são desviadas para o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os gatilhos de logon não são acionados quando a autenticação falha.  
  
 Você pode usar gatilhos de logon para auditar e controlar sessões do servidor, por exemplo, rastreando a atividade de logon, restringindo os logons ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou limitando o número de sessões para um logon específico. Por exemplo, no código abaixo, o gatilho de logon negará as tentativas de logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciadas por *login_test* se já houver três sessões de usuário criadas pelo logon em questão.  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
```  
  
 Observe que o evento LOGON corresponde ao evento AUDIT_LOGIN do Rastreamento do SQL, que pode ser usado em [Notificações de Eventos](../../relational-databases/service-broker/event-notifications.md). A principal diferença entre gatilhos e notificações de evento é que os primeiros ocorrem de maneira síncrona com os eventos, ao passo que os últimos são assíncronos. Isso significa, por exemplo, que se quiser interromper o estabelecimento de uma sessão, você deve usar um gatilho de logon. Uma notificação de evento em um evento AUDIT_LOGIN não pode ser usada para esse fim.  
  
## <a name="specifying-first-and-last-trigger"></a>Especificando o primeiro e o último gatilhos  
 Vários gatilhos podem ser definidos no evento LOGON. Qualquer um deles pode ser designado como o primeiro ou último gatilho a ser disparado mediante em um evento por meio do procedimento armazenado do sistema [sp_settriggerorder](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md) . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante a ordem de execução dos gatilhos restantes.  
  
## <a name="managing-transactions"></a>Gerenciando transações  
 Antes de o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disparar um gatilho de logon, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma transação implícita independente de qualquer transação de usuário. Assim, quando o primeiro gatilho de logon é acionado, a contagem de transações é 1. Terminada a execução de todos os gatilhos de logon, a transação é confirmada. Como em outros tipos de gatilhos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro se o gatilho de logon terminar a execução com uma contagem de transações de 0. A instrução ROLLBACK TRANSACTION zera a contagem de transações, mesmo quando é emitida dentro de uma transação aninhada. COMMIT TRANSACTION pode decrementar a contagem de transações para 0. Logo, nós não aconselhamos emitir instruções COMMIT TRANSACTION dentro de gatilhos de logon.  
  
 Considere o seguinte ao usar uma instrução ROLLBACK TRANSACTION dentro de gatilhos de logon:  
  
-   Toda modificação de dados efetuada até o ponto de ROLLBACK TRANSACTION é revertida. Isso inclui modificações feitas pelo gatilho atual e por gatilhos anteriores executados no mesmo evento. Quaisquer gatilhos restantes para o evento específico não são executados.  
  
-   O gatilho atual continua a executar todas as instruções restantes que apareçam depois da instrução ROLLBACK. Se alguma dessas instruções modificar dados, as modificações não serão revertidas.  
  
 Não será estabelecida uma sessão de usuário se ocorrer uma das seguintes condições durante a execução de um gatilho em um evento LOGON:  
  
-   A transação implícita original é revertida ou falha.  
  
-   Um erro com severidade maior que 20 é emitido dentro do corpo do gatilho.  
  
## <a name="disabling-a-logon-trigger"></a>Desabilitando um gatilho de logon  
 Um gatilho de logon pode, efetivamente, impedir conexões com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para todos os usuários, incluindo membros da função de servidor fixa **sysadmin** . Quando um gatilho de logon está impedindo conexões, os membros da função de servidor fixa **sysadmin** podem se conectar usando a conexão de administrador dedicada ou iniciando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] no modo de configuração mínima (-f). Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar gatilhos de logon. Os gatilhos de logon podem ser criados a partir de qualquer banco de dados, mas são registrados no nível do servidor e residem no banco de dados **mestre** .|[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)|  
|Descreve como modificar gatilhos de logon.|[ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)|  
|Descreve como excluir gatilhos de logon.|[DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)|  
|Descreve como retornar informações sobre gatilhos de logon.|[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)<br /><br /> [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)|  
|Descreve como capturar dados de evento do gatilho de logon.||  
  
## <a name="see-also"></a>Consulte Também  
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)  
  
  
