---
title: Tarefa Notificar Operador | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9ee8ee285d395425e925f2d5ec1e8a169d4ac5fa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918396"
---
# <a name="notify-operator-task"></a>Tarefa de Notificação do Operador
  A tarefa de Notificação do Operador envia mensagens de notificação aos operadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Um operador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é um alias para uma pessoa ou para grupo que pode receber notificações eletrônicas. Para obter mais informações sobre operadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Operadores](../../ssms/agent//operators.md).  
  
 Ao usar a tarefa Notificar Operador, um pacote pode notificar um ou mais operadores usando email, pager ou **net send**. Cada operador pode ser notificado por métodos diferentes. Por exemplo, OperatorA é notificado por email e pager, e OperatorB é notificado por pager e **net send**. Os operadores que recebem notificações da tarefa devem ser membros da coleção **OperatorNotify** na tarefa de Notificação do Operador.  
  
 A tarefa de Notificar Operador é a única tarefa de manutenção de banco de dados que não encapsula uma instrução Transact-SQL ou um comando DBCC.  
  
## <a name="configuration-of-the-notify-operator-task"></a>Configuração da tarefa Notificar Operador  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Notificar Operador &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
  
