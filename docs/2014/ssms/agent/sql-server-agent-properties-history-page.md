---
title: Propriedades do SQL Server Agent (página Histórico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e882745886a3a9a2c2575461d96d24355e2139bb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010580"
---
# <a name="sql-server-agent-properties-history-page"></a>Propriedades do SQL Server Agent (página Histórico)
  Use essa página para exibir e modificar as configurações de gerenciamento do log de histórico do serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
 **Limitar tamanho do log do histórico de trabalho**  
 Define limites para a quantidade de informações do histórico de trabalho que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém no log.  
  
 **Tamanho máximo (em linhas) do log do histórico de trabalho**  
 Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém. Quando o log aumenta para conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas forem inseridas.  
  
 **Máximo de linhas do histórico de trabalho por trabalho**  
 Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém por trabalho. Quando o log de um determinado trabalho cresce até conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas são inseridas.  
  
 **Remover histórico de agente**  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent removerá as entradas presentes no log por mais tempo do que o período especificado. Essa é uma execução de uma vez para remover o histórico. Se um trabalho recorrente for necessário, crie e agende um plano de manutenção com um trabalho de limpeza.  
  
 **Com mais de**  
 Define o período durante o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent manterá entradas.  
  
## <a name="see-also"></a>Consulte também  
 [Log de erros do SQL Server Agent](sql-server-agent-error-log.md)  
  
  