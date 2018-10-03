---
title: Tarefa Executar Instrução T-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a2ad857b2174528db8f6c2d7c8453b956129686d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058486"
---
# <a name="execute-t-sql-statement-task"></a>Tarefa Executar Instrução T-SQL
  A tarefa Executar Instrução T-SQL executa instruções Transact-SQL. Para obter mais informações, consulte [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference) e [Integration Services &#40;SSIS&#41; Consultas](../integration-services-ssis-queries.md).  
  
 Essa tarefa é semelhante à tarefa Executar SQL. Porém, a tarefa Executar Instrução T-SQL só dá suporte à versão Transact-SQL da linguagem SQL e, por isso, você não pode usá-la para executar instruções em servidores que usam outros dialetos de linguagem SQL. Se for necessário executar consultas parametrizadas, salvar resultados de consulta em variáveis ou usar expressões de propriedade, você deverá usar a tarefa Executar SQL em vez de a tarefa Executar Instrução T-SQL. Para obter mais informações, consulte [Execute SQL Task](execute-sql-task.md).  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>Configuração da Tarefa Executar T-SQL  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Executar Instrução T-SQL &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de controle](control-flow.md)   
 [MERGE em pacotes do Integration Services](merge-in-integration-services-packages.md)  
  
  
