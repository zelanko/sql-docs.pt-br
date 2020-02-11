---
title: Propriedades do SQL Server Agent (página Histórico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10796dde3513e5c4b7970d1e4f6c4eedcad3c6c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245601"
---
# <a name="sql-server-agent-properties-history-page"></a>Propriedades do SQL Server Agent (página Histórico)
  Use esta página para exibir e modificar as configurações de gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do log de histórico de serviço do Agent.  
  
## <a name="options"></a>Opções  
 **Limitar o tamanho do log do histórico de trabalhos**  
 Define limites para a quantidade de informações do histórico de trabalho que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém no log.  
  
 **Tamanho máximo do log do histórico de trabalhos (em linhas)**  
 Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém. Quando o log aumenta para conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas forem inseridas.  
  
 **Máximo de linhas do histórico de trabalhos por trabalho**  
 Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém por trabalho. Quando o log de um determinado trabalho cresce até conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas são inseridas.  
  
 **Remover histórico do agente**  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent removerá as entradas presentes no log por mais tempo do que o período especificado. Essa é uma execução de uma vez para remover o histórico. Se um trabalho recorrente for necessário, crie e agende um plano de manutenção com um trabalho de limpeza.  
  
 **Com mais de**  
 Define o período durante o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent manterá entradas.  
  
## <a name="see-also"></a>Consulte Também  
 [Log de erros do SQL Server Agent](sql-server-agent-error-log.md)  
  
  
