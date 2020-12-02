---
description: Tarefa Executar Instrução T-SQL
title: Tarefa Executar Instrução T-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 060fa6ad9faae0fa6159eba2591623af57a41c5b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123516"
---
# <a name="execute-t-sql-statement-task"></a>Tarefa Executar Instrução T-SQL

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A tarefa Executar Instrução T-SQL executa instruções Transact-SQL. Para obter mais informações, consulte [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/language-reference.md) e [Integration Services &#40;SSIS&#41; Consultas](../../integration-services/integration-services-ssis-queries.md).  
  
 Essa tarefa é semelhante à tarefa Executar SQL. Porém, a tarefa Executar Instrução T-SQL só dá suporte à versão Transact-SQL da linguagem SQL e, por isso, você não pode usá-la para executar instruções em servidores que usam outros dialetos de linguagem SQL. Se for necessário executar consultas parametrizadas, salvar resultados de consulta em variáveis ou usar expressões de propriedade, você deverá usar a tarefa Executar SQL em vez de a tarefa Executar Instrução T-SQL. Para obter mais informações, consulte [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md).  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>Configuração da Tarefa Executar T-SQL  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Executar Instrução T-SQL &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)   
 [MERGE em pacotes do Integration Services](../../integration-services/control-flow/merge-in-integration-services-packages.md)  
  
