---
title: Tarefa de limpeza de histórico | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.historycleanuptask.f1
helpviewer_keywords:
- history tables [SQL Server]
- History Cleanup task [Integration Services]
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4327be90b142556f0d41efd3228eead7b671d838
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161806"
---
# <a name="history-cleanup-task"></a>Tarefa Limpeza do Histórico
  A tarefa Limpeza do Histórico exclui entradas das seguintes tabelas de histórico do banco de dados msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 Por meio da tarefa Limpeza do Histórico, um pacote pode excluir dados históricos relacionados a atividades de backup e restauração, a trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e a planos de manutenção do banco de dados.  
  
 Essa tarefa encapsula o procedimento armazenado do sistema sp_delete_backuphistory e transfere a data especificada ao procedimento como um argumento. Para obter mais informações, consulte [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql).  
  
## <a name="configuration-of-the-history-cleanup-task"></a>Configuração da tarefa Limpeza do Histórico  
 A tarefa inclui uma propriedade para especificação da data mais antiga dos dados retidos nas tabelas de histórico. Você pode indicar a data por número de dias, semanas, meses ou anos do dia atual, e a tarefa automaticamente converte o intervalo para uma data.  
  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa limpeza de histórico &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de Controle](control-flow.md)  
  
  
