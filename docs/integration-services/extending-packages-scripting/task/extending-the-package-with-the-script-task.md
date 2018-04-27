---
title: Estender o pacote com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a34e42c64bb86d0291c22189dcd9a4ac5b039ed1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="extending-the-package-with-the-script-task"></a>Estendendo o pacote com a tarefa Script
  A tarefa Script estende as capacidades de tempo de execução de pacotes do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] com o código personalizado escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# que é compilado e executado no tempo de execução do pacote. A tarefa Script simplifica o desenvolvimento de uma tarefa de tempo de execução personalizada quando as tarefas incluídas com o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] não atendem plenamente as suas necessidades. A tarefa Script grava todo o código de infraestrutura requerido, permitindo que você se concentre exclusivamente no código que é exigido para seu processamento personalizado.  
  
 Uma tarefa Script interage com o pacote de conteúdo através do objeto global **Dts**, uma instância da classe <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> que é exposta no ambiente de script. Você pode gravar o código em uma tarefa Script que modifica os valores armazenados nas variáveis de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]; posteriormente, o pacote poderá usar esses valores atualizados para determinar o caminho de seu fluxo de trabalho. A tarefa Script também pode usar o namespace [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e a biblioteca de classe [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], como também assemblies personalizados, para implementar a funcionalidade personalizada.  
  
 A tarefa Script e o código de infraestrutura que ela gera para você simplificam, significativamente, o processo de desenvolvimento de uma tarefa personalizada. Entretanto, para compreender como a tarefa Script funciona, você pode achar útil ler a seção [Desenvolver uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) para compreender as etapas envolvidas no desenvolvimento de uma tarefa personalizada.  
  
 Se você estiver criando uma tarefa que você planeja reutilizar em vários pacotes, deverá considerar o desenvolvimento de uma tarefa personalizada em vez de utilizar a tarefa Script. Para obter mais informações, consulte [Comparar soluções de script e objetos personalizados](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir fornecem mais informações sobre a tarefa Script.  
  
 [Configurar a tarefa Script no Editor da Tarefa Script](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 Explica como as propriedades que você configura no **Editor da Tarefa Script** afetam os recursos e o desempenho do código na tarefa Script.  
  
 [Codificar e depurar a tarefa Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 Explica como utilizar o VSTA ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) para desenvolver os scripts contidos na tarefa Script.  
  
 [Usar variáveis na tarefa Script](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Explica como usar variáveis com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>.  
  
 [Conectar-se a fontes de dados na tarefa Script](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Explica como usar conexões com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>.  
  
 [Gerar eventos na tarefa Script](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Explica como aumentar eventos com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>.  
  
 [Registrar a tarefa Script em log](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 Explica como anotar informações com o método <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>.  
  
 [Retornar resultados da tarefa Script](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 Explica como retornar resultados com a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> e a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>.  
  
 [Exemplos de tarefa Script](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 Fornece exemplos simples que demonstram vários usos possíveis para uma tarefa Script.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa Script](../../../integration-services/control-flow/script-task.md)   
 [Comparar a tarefa Script e o componente de Script](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
