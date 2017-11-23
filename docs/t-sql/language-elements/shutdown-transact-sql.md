---
title: DESLIGAMENTO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs: TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 10a6b2c5bf093eaee3eacf183f98ecb644d2fc68
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Interrompe imediatamente o SQL Server.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NOWAIT  
 Opcional. Desliga o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem executar pontos de verificação em todo o banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sai depois de tentar finalizar todos os processos de usuário. Quando o servidor é reiniciado, ocorre uma operação de reversão para transações incompletas.  
  
## <a name="remarks"></a>Comentários  
 A menos que a opção WITHNOWAIT é usada, SHUTDOWN desligará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por:  
  
1.  Desabilitando logons (exceto para membros do **sysadmin** e **serveradmin** funções de servidor fixas).  
  
    > [!NOTE]  
    >  Para exibir uma lista de todos os usuários atuais, execute **sp_who**.  
  
2.  Esperando a conclusão de procedimentos armazenados ou instruções Transact-SQL em execução. Para exibir uma lista de todos os processos ativos e bloqueios, execute **sp_who** e **sp_lock**, respectivamente.  
  
3.  Inserindo um ponto de verificação em cada banco de dados.  
  
 Usando a instrução SHUTDOWN minimiza a quantidade de recuperação automática de trabalho necessário quando membros o **sysadmin** fixa reinicialização da função de servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Outras ferramentas e métodos também podem ser usados para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada um deles cria um ponto de verificação em todos os bancos de dados. É possível liberar dados confirmados do cache de dados e interromper o servidor:  
  
-   Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Executando **mssqlserver net stop** em um prompt de comando para uma instância padrão ou executando **net stop mssql$***instancename* em um prompt de comando para uma instância nomeada.  
  
-   Usando Serviços do Painel de Controle.  
  
 Se **sqlservr.exe** foi iniciado no prompt de comando, pressionar CTRL + C desligará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Entretanto, pressionar CTRL+C não inserirá um ponto de verificação.  
  
> [!NOTE]  
>  O uso de um desses métodos para interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia a mensagem `SERVICE_CONTROL_STOP` ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Permissões SHUTDOWN são atribuídas aos membros do **sysadmin** e **serveradmin** funções de servidor fixas e eles não são transferíveis.  
  
## <a name="see-also"></a>Consulte também  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [SP_WHO &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Aplicativo sqlservr](../../tools/sqlservr-application.md)   
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
