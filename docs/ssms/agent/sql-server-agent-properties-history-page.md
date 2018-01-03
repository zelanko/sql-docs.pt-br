---
title: "Propriedades do SQL Server Agent (página Histórico) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 355754c4e7f3d766b67017629b3c0ac32944c047
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-agent-properties-history-page"></a>Propriedades do SQL Server Agent (página Histórico)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use essa página para exibir e modificar as configurações de gerenciamento do log de histórico do serviço [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Limitar tamanho do log do histórico de trabalho**  
Define limites para a quantidade de informações do histórico de trabalho que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent mantém no log.  
  
**Tamanho máximo (em linhas) do log do histórico de trabalho**  
Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent mantém. Quando o log aumenta para conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas forem inseridas.  
  
**Máximo de linhas do histórico de trabalho por trabalho**  
Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent mantém por trabalho. Quando o log de um determinado trabalho cresce até conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas são inseridas.  
  
**Remover histórico de agente**  
Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent removerá as entradas presentes no log por mais tempo do que o período especificado. Essa é uma execução de uma vez para remover o histórico. Se um trabalho recorrente for necessário, crie e agende um plano de manutenção com um trabalho de limpeza.  
  
**Com mais de**  
Define o período durante o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent manterá entradas.  
  
## <a name="see-also"></a>Consulte Também  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
