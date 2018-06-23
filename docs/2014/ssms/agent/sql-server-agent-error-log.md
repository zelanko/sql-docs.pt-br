---
title: Log de erros do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d5622321e1b947b6f5fb6c31463d9ea7e71d395b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122766"
---
# <a name="sql-server-agent-error-log"></a>Log de erros do SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent cria um log de erros que registra avisos e erros por padrão. Os seguintes avisos e erros são exibidos no log:  
  
-   Mensagens de aviso que fornecem informações sobre problemas potenciais, como "O trabalho \<*job_name*> foi excluído durante sua execução".  
  
-   Mensagens de erro que normalmente requerem intervenção de um administrador de sistema, como "Não é possível iniciar a sessão de email". As mensagens de erro podem ser enviadas a um usuário ou computador específico por meio de **net send**.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém até nove logs de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Cada log arquivado tem uma extensão que indica sua idade relativa. Por exemplo, uma extensão .1 indica o log de erros arquivado mais recentemente e a extensão .9, o mais antigo.  
  
 Por padrão, mensagens de rastreamento de execução não são gravadas no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, pois elas podem lotá-lo. Quando o log de erros fica cheio, sua capacidade de selecionar e analisar erros mais difíceis é reduzida. Como o log é somado à carga de processamento do servidor, é importante considerar com atenção o valor obtido ao capturar mensagens de rastreamento de execução para o log de erros. Geralmente, é melhor capturar todas as mensagens apenas quando você estiver depurando um problema específico.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é interrompido, você pode modificar o local do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Quando o log de erros está vazio, não é possível abri-lo. É possível reciclar o log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a qualquer hora, sem ter que interromper o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Para exibir o log de erros do SQL Server Agent**  
  
-   [Exibir o log de erros do SQL Server Agent &#40;SQL Server Management Studio&#41;](view-sql-server-agent-error-log-sql-server-management-studio.md) 
  
 **Para renomear o log de erros do SQL Server Agent**  
  
-   [Renomear um log de erros do SQL Server Agent &#40;SQL Server Management Studio&#41;](rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
 **Para enviar mensagens de erro do SQL Server Agent**  
  
-   [Send SQL Server Agent Error Messages](send-sql-server-agent-error-messages.md)  
  
 **Para gravar mensagens de rastreamento de execução no log de erros do SQL Server Agent**  
  
-   [Gravar mensagens de rastreamento de execução no log de erros do SQL Server Agent &#40;SQL Server Management Studio&#41;](write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
  