---
description: Estendendo o pacote com a tarefa Script
title: Estender o pacote com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c70136ad09aaa3cb24c04c2828e8335f96aef467
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122834"
---
# <a name="extending-the-package-with-the-script-task"></a>Estendendo o pacote com a tarefa Script

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  A tarefa Script estende as capacidades de tempo de execução de pacotes do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] com o código personalizado escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# que é compilado e executado no tempo de execução do pacote. A tarefa Script simplifica o desenvolvimento de uma tarefa de tempo de execução personalizada quando as tarefas incluídas com o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] não atendem plenamente as suas necessidades. A tarefa Script grava todo o código de infraestrutura requerido, permitindo que você se concentre exclusivamente no código que é exigido para seu processamento personalizado.  
  
 Uma tarefa Script interage com o pacote de conteúdo através do objeto global **Dts**, uma instância da classe <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> que é exposta no ambiente de script. Você pode gravar o código em uma tarefa Script que modifica os valores armazenados nas variáveis de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]; posteriormente, o pacote poderá usar esses valores atualizados para determinar o caminho de seu fluxo de trabalho. A tarefa Script também pode usar o namespace [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e a biblioteca de classe [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], como também assemblies personalizados, para implementar a funcionalidade personalizada.  
  
 A tarefa Script e o código de infraestrutura que ela gera para você simplificam, significativamente, o processo de desenvolvimento de uma tarefa personalizada. Entretanto, para compreender como a tarefa Script funciona, você pode achar útil ler a seção [Desenvolver uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) para compreender as etapas envolvidas no desenvolvimento de uma tarefa personalizada.  
  
 Se você estiver criando uma tarefa que você planeja reutilizar em vários pacotes, deverá considerar o desenvolvimento de uma tarefa personalizada em vez de utilizar a tarefa Script. Para obter mais informações, consulte [Comparar soluções de script e objetos personalizados](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre a tarefa Script.  
  
 [Configurando a tarefa Script no Editor da Tarefa Script](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 Explica como as propriedades que você configura no **Editor da Tarefa Script** afetam os recursos e o desempenho do código na tarefa Script.  
  
 [Codificando e depurando a tarefa Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 Explica como usar o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] VSTA (Tools for Applications) para desenvolver os scripts contidos na tarefa Script.  
  
 [Usando variáveis na tarefa Script](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Explica como usar variáveis com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>.  
  
 [Conectando a fontes de dados na tarefa Script](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Explica como usar conexões com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>.  
  
 [Gerando eventos na tarefa Script](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Explica como aumentar eventos com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>.  
  
 [Registrando a tarefa Script](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 Explica como anotar informações com o método <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>.  
  
 [Retornando resultados da tarefa Script](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 Explica como retornar resultados com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> e a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>.  
  
 [Exemplos de tarefa Script](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 Fornece exemplos simples que demonstram vários usos possíveis para uma tarefa Script.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa Script](../../../integration-services/control-flow/script-task.md)   
 [Comparando a tarefa Script e o componente Script](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
