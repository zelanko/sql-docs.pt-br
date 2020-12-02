---
description: SHUTDOWN (Transact-SQL)
title: SHUTDOWN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b2d327df39cb0c3a891fc5f4bc624619e7964e8
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92195448"
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Para imediatamente o SQL Server.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SHUTDOWN [ WITH NOWAIT ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 WITH NOWAIT  
 Opcional. Desliga o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem executar pontos de verificação em todo o banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sai depois de tentar finalizar todos os processos de usuário. Quando o servidor é reiniciado, ocorre uma operação de reversão para transações incompletas.  
  
## <a name="remarks"></a>Comentários  
 A menos que a opção WITHNOWAIT seja usada, SHUTDOWN desligará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Desabilitando logons (exceto para membros das funções de servidor fixas **sysadmin** e **serveradmin**).  
  
    > [!NOTE]  
    >  Para exibir uma lista de todos os usuários atuais, execute **sp_who**.  
  
2.  Esperando a conclusão de procedimentos armazenados ou instruções Transact-SQL em execução. Para exibir uma lista de todos os processos e bloqueios ativos, execute **sp_who** e **sp_lock**, respectivamente.  
  
3.  Inserindo um ponto de verificação em cada banco de dados.  
  
 O uso da instrução SHUTDOWN minimiza a quantidade de trabalho de recuperação automática necessária quando membros da função de servidor fixa **sysadmin** reiniciam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Outras ferramentas e métodos também podem ser usados para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada um deles cria um ponto de verificação em todos os bancos de dados. É possível liberar dados confirmados do cache de dados e interromper o servidor:  
  
-   Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Executando **net stop mssqlserver** em um prompt de comando para uma instância padrão ou executando **net stop mssql$** _instancename_ em um prompt de comando para uma instância nomeada.  
  
-   Usando Serviços do Painel de Controle.  
  
 Se **sqlservr.exe** foi iniciado no prompt de comando, pressionar CTRL+C desliga o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Entretanto, pressionar CTRL+C não inserirá um ponto de verificação.  
  
> [!NOTE]  
>  O uso de um desses métodos para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia a mensagem `SERVICE_CONTROL_STOP` ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissões  
 As permissões SHUTDOWN são atribuídas a membros das funções de servidor fixas **sysadmin** e **serveradmin** e não podem ser transferidas.  
  
## <a name="see-also"></a>Consulte Também  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Aplicativo sqlservr](../../tools/sqlservr-application.md)   
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
