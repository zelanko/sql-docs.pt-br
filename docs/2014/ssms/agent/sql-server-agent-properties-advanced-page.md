---
title: Propriedades do SQL Server Agent (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3825ba87f9012a7dcc33fb8585a2d2c4f83e9d6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328836"
---
# <a name="sql-server-agent-properties-advanced-page"></a>Propriedades do SQL Server Agent (página Avançado)
  Use esta página para exibir e modificar as propriedades avançadas do serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
 **Encaminhamento de evento do SQL Server**  
 As opções nesta categoria ativam e configuram o encaminhamento de evento.  
  
 **Encaminhar eventos para um servidor diferente**  
 Encaminha eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para um servidor diferente.  
  
 **Servidor**  
 Selecionar o nome do servidor ao qual os eventos serão encaminhados.  
  
 **Eventos sem-tratamento**  
 Encaminha apenas os eventos sem-tratamento para o servidor especificado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent só encaminha os eventos aos quais não haja respostas de nenhum alerta.  
  
 **Todos os eventos**  
 Encaminha todos os eventos. Quando um alerta na instância local responde ao evento, o agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encaminhará o evento e processará o alerta.  
  
 **Se a gravidade do evento for esta ou acima**  
 Encaminha apenas os eventos com nível de severidade igual ou maior que o nível especificado.  
  
 **Condição de CPU ociosa**  
 As opções nesta categoria definem as condições sobre as quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa trabalhos agendados para serem executados na agenda da CPU ociosa.  
  
 **Definir condição de CPU ociosa**  
 Define as condições sob as quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent considera que a CPU está ociosa.  
  
 **Uso médio de CPU cai abaixo de**  
 Porcentagem de uso de CPU abaixo do qual a CPU é considerada ociosa.  
  
 **E permanece abaixo desse nível por**  
 Quantidade de tempo em que o uso médio da CPU deve estar abaixo do nível especificado antes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent execute trabalhos na agenda de CPU ociosa.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e anexar agendas a trabalhos](create-and-attach-schedules-to-jobs.md)   
 [Gerenciar eventos](manage-events.md)  
  
  
