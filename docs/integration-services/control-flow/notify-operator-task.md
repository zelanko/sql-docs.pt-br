---
title: "Tarefa de Notifica&#231;&#227;o do Operador | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.notifyoperatortask.f1"
helpviewer_keywords: 
  - "Tarefa de Notificação do Operador"
  - "notificações [Integration Services]"
  - "SQL Server Agent [Integration Services]"
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Tarefa de Notifica&#231;&#227;o do Operador
  A tarefa de Notificação do Operador envia mensagens de notificação aos operadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Um operador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é um alias para uma pessoa ou para grupo que pode receber notificações eletrônicas. Para obter mais informações sobre operadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Operadores](../../ssms/agent/operators.md).  
  
 Ao usar a tarefa Notificar Operador, um pacote pode notificar um ou mais operadores usando email, pager ou **net send**. Cada operador pode ser notificado por métodos diferentes. Por exemplo, OperatorA é notificado por email e pager, e OperatorB é notificado por pager e **net send**. Os operadores que recebem notificações da tarefa devem ser membros da coleção **OperatorNotify** na tarefa de Notificação do Operador.  
  
 A tarefa de Notificar Operador é a única tarefa de manutenção de banco de dados que não encapsula uma instrução Transact-SQL ou um comando DBCC.  
  
## Configuração da tarefa Notificar Operador  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Notificar Operador &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
  