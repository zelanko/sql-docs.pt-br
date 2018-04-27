---
title: Configurar a tarefa Script no Editor da Tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46b636fc957c08c52876c321d2b7211f9d627a15
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Configurando a tarefa Script no Editor da Tarefa Script
  Antes de escrever um código personalizado na tarefa Script, configure suas propriedades de entidade de segurança nas três páginas do **Editor da Tarefa Script**. É possível configurar propriedades de tarefa adicionais que não são exclusivas da tarefa Script através da janela Propriedades.  
  
> [!NOTE]  
>  Ao contrário das versões anteriores onde você podia indicar se os scripts seriam pré-compilados, todos os scripts são pré-compilados a partir do [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)].  
  
## <a name="general-page-of-the-script-task-editor"></a>Página Geral do Editor da Tarefa Script  
 Na página **Geral** do **Editor da Tarefa Script**, você atribui um nome exclusivo e uma descrição para a tarefa Script.  
  
## <a name="script-page-of-the-script-task-editor"></a>Página Script do Editor da Tarefa Script  
 A página **Script** do **Editor da Tarefa Script** exibe as propriedades personalizadas da tarefa Script.  
  
### <a name="scriptlanguage-property"></a>Propriedade ScriptLanguage  
 O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) dá suporte às linguagens de programação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Depois de criar um script na tarefa Script, você não poderá alterar o valor da propriedade **ScriptLanguage**.  
  
 Para definir a linguagem de script padrão para componentes e tarefas de Script, use a propriedade **ScriptLanguage** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
### <a name="entrypoint-property"></a>Propriedade EntryPoint  
 A propriedade **EntryPoint** especifica o método da classe **ScriptMain** no projeto do VSTA que chamado pelo tempo de execução do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] como ponto de entrada no código da tarefa Script. A **ScriptMain** é a classe padrão gerada pelos modelos de script.  
  
 Caso altere o nome do método no projeto do VSTA, será preciso alterar o valor da propriedade **EntryPoint** .  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propriedades ReadOnlyVariables e ReadWriteVariables  
 Você pode inserir listas de variáveis existentes, delimitadas por vírgulas, como os valores dessas propriedades a fim de disponibilizar as variáveis para acesso somente leitura ou leitura/gravação dentro do código de tarefa Script. Variáveis de ambos os tipos são acessadas em código através da propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> do objeto **Dts**. Para obter mais informações, consulte [Usando variáveis na tarefa Script](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
 Para selecionar as variáveis, clique no botão de reticências (**...**) ao lado do campo de propriedade. Para obter mais informações, consulte [Página Selecionar Variáveis](../../../integration-services/control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Botão Editar Script  
 O botão **Editar Script** inicia o ambiente de desenvolvimento do VSTA no qual você escreve seu script personalizado. Para obter mais informações, consulte [Codificar e depurar a Tarefa Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Página Expressões do Editor da Tarefa Script  
 Na página **Expressões** do **Editor da Tarefa Script**, você pode usar expressões para fornecer valores para as propriedades da tarefa Script listadas anteriormente e para muitas outras propriedades da tarefa. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Codificar e depurar a tarefa Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
