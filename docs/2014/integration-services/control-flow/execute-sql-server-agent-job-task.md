---
title: Tarefa Executar Trabalho do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5f91fcb7033dfe2944e863d67a6c6bf53434e6db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62831918"
---
# <a name="execute-sql-server-agent-job-task"></a>Tarefa Executar Trabalho do SQL Server Agent
  A tarefa executar trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent é um serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que executa trabalhos que foram definidos em uma instância do SQL Server. Você pode criar trabalhos que executam instruções Transact-SQL e scripts ActiveX, pode executar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e tarefas de manutenção de Replicação ou pode executar pacotes. Você também pode configurar um trabalho para monitorar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e acionar alertas. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Em geral, os trabalhos do Agent são usados para automatizar tarefas que você executa repetidamente. Para obter mais informações, consulte [Implementar trabalhos](../../ssms/agent/implement-jobs.md).  
  
 Quando você utiliza a tarefa executar trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, um pacote pode realizar tarefas administrativas relacionadas aos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode executar um procedimento armazenado do sistema como **sp_enum_dtspackages** para obter uma lista de pacotes em uma pasta.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar em execução antes que os trabalhos administrativos locais ou multisservidor possam ser executados automaticamente.  
  
 Essa tarefa encapsula o procedimento do sistema **sp_start_job** e passa o nome do trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o procedimento como um argumento. Para obter mais informações, consulte [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql).  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>Configurando a tarefa executar trabalho do SQL Server Agent  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Executar SQL Server Agent trabalho &#40;plano de manutenção&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
  
