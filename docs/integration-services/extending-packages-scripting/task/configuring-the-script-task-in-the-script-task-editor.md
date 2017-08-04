---
title: Configurando a tarefa de Script no Editor da tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 182a7b8f04c2339a8f3d3b986c978a7998c8a9c3
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Configurando a tarefa Script no Editor da Tarefa Script
  Antes de escrever código personalizado na tarefa Script, configure suas propriedades principais nas três páginas do **Editor da tarefa Script**. É possível configurar propriedades de tarefa adicionais que não são exclusivas da tarefa Script através da janela Propriedades.  
  
> [!NOTE]  
>  Ao contrário das versões anteriores onde você podia indicar se os scripts seriam pré-compilados, todos os scripts são pré-compilados a partir do [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)].  
  
## <a name="general-page-of-the-script-task-editor"></a>Página Geral do Editor da Tarefa Script  
 No **geral** página do **Editor da tarefa Script**, atribua um nome exclusivo e uma descrição para a tarefa de Script.  
  
## <a name="script-page-of-the-script-task-editor"></a>Página Script do Editor da Tarefa Script  
 O **Script** página do **Editor da tarefa Script** exibe as propriedades personalizadas da tarefa de Script.  
  
### <a name="scriptlanguage-property"></a>Propriedade ScriptLanguage  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) oferece suporte a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] linguagens de programação Visual c#. Depois de criar um script na tarefa Script, você não pode alterar o valor de **ScriptLanguage** propriedade.  
  
 Para definir a linguagem de script padrão para tarefas de Script e componentes de Script, use o **ScriptLanguage** propriedade o **geral** página do **opções** caixa de diálogo. Para obter mais informações, consulte [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
### <a name="entrypoint-property"></a>Propriedade EntryPoint  
 O **EntryPoint** propriedade especifica o método de **ScriptMain** projeto de classe no VSTA que o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] chamadas de tempo de execução como ponto de entrada no código da tarefa de Script. O **ScriptMain** classe é a classe padrão gerada pelos modelos de script.  
  
 Caso altere o nome do método no projeto do VSTA, será preciso alterar o valor da propriedade **EntryPoint** .  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propriedades ReadOnlyVariables e ReadWriteVariables  
 Você pode inserir listas de variáveis existentes, delimitadas por vírgulas, como os valores dessas propriedades a fim de disponibilizar as variáveis para acesso somente leitura ou leitura/gravação dentro do código de tarefa Script. Variáveis de ambos os tipos são acessadas em código por meio de <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> propriedade o **Dts** objeto. Para obter mais informações, consulte [Usando variáveis na tarefa Script](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
 Para selecionar as variáveis, clique no botão de reticências (**...** ) botão ao lado do campo de propriedade. Para obter mais informações, consulte [selecionar variáveis de página](../../../integration-services/control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Botão Editar Script  
 O **Editar Script** botão inicia o ambiente de desenvolvimento do VSTA no qual você escreve seu script personalizado. Para obter mais informações, consulte [codificando e depurando a tarefa Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Página Expressões do Editor da Tarefa Script  
 Sobre o **expressões** página do **Editor da tarefa Script**, você pode usar expressões para fornecer valores para as propriedades da tarefa Script listados acima e para muitas outras propriedades da tarefa. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Codificando e depurando a tarefa de Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
