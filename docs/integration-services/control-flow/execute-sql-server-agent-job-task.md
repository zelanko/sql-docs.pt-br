---
title: Tarefa Executar Trabalho do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3e8532ea1b3d74d9a377627abcc9798af6825279
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40175055"
---
# <a name="execute-sql-server-agent-job-task"></a>Tarefa Executar Trabalho do SQL Server Agent
  A tarefa executar trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent é um serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que executa trabalhos que foram definidos em uma instância do SQL Server. Você pode criar trabalhos que executam instruções Transact-SQL e scripts ActiveX, pode executar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e tarefas de manutenção de Replicação ou pode executar pacotes. Você também pode configurar um trabalho para monitorar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e acionar alertas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Em geral, os trabalhos do Agent são usados para automatizar tarefas que você executa repetidamente. Para obter mais informações, consulte [Implementar trabalhos](../../ssms/agent/implement-jobs.md).  
  
 Quando você utiliza a tarefa executar trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, um pacote pode realizar tarefas administrativas relacionadas aos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode executar um procedimento armazenado do sistema como **sp_enum_dtspackages** para obter uma lista de pacotes em uma pasta.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar em execução antes que os trabalhos administrativos locais ou multisservidor possam ser executados automaticamente.  
  
 Essa tarefa encapsula o procedimento do sistema **sp_start_job** e passa o nome do trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o procedimento como um argumento. Para obter mais informações, consulte [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>Configurando a tarefa executar trabalho do SQL Server Agent  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Executar Trabalho do SQL Server Agent &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
