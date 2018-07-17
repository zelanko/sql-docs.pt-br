---
title: SHUTDOWN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ee366089ceb6451aeea16669f45f06b0bc5a97fe
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36244058"
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Para imediatamente o SQL Server.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NOWAIT  
 Opcional. Desliga o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem executar pontos de verificação em todo o banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sai depois de tentar finalizar todos os processos de usuário. Quando o servidor é reiniciado, ocorre uma operação de reversão para transações incompletas.  
  
## <a name="remarks"></a>Remarks  
 A menos que a opção WITHNOWAIT seja usada, SHUTDOWN desligará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Desabilitando logons (exceto para membros das funções de servidor fixas **sysadmin** e **serveradmin**).  
  
    > [!NOTE]  
    >  Para exibir uma lista de todos os usuários atuais, execute **sp_who**.  
  
2.  Esperando a conclusão de procedimentos armazenados ou instruções Transact-SQL em execução. Para exibir uma lista de todos os processos e bloqueios ativos, execute **sp_who** e **sp_lock**, respectivamente.  
  
3.  Inserindo um ponto de verificação em cada banco de dados.  
  
 O uso da instrução SHUTDOWN minimiza a quantidade de trabalho de recuperação automática necessária quando membros da função de servidor fixa **sysadmin** reiniciam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Outras ferramentas e métodos também podem ser usados para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada um deles cria um ponto de verificação em todos os bancos de dados. É possível liberar dados confirmados do cache de dados e interromper o servidor:  
  
-   Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Executando **net stop mssqlserver** em um prompt de comando para uma instância padrão ou executando **net stop mssql$***instancename* em um prompt de comando para uma instância nomeada.  
  
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
  
  
