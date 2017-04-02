---
title: "Editor da Tarefa Script (p&#225;gina Script) | Microsoft Docs"
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
  - "sql13.dts.designer.scripttask.script.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Script"
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Editor da Tarefa Script (p&#225;gina Script)
  Use a página **Script** da caixa de diálogo **Editor da Tarefa Script** para definir propriedades de script e especificar variáveis que podem ser acessados pelo script.  
  
> [!NOTE]  
>  No [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] e versões posteriores, todos os scripts são pré-compilados. Em versões anteriores, devia ser definida uma propriedade **PrecompileScriptIntoBinaryCode** para especificar que o script estava pré-compilado.  
  
 Para obter mais informações sobre a tarefa Script, consulte [Script Task](../../integration-services/control-flow/script-task.md) e [Configuring the Script Task in the Script Task Editor](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md). Para obter informações sobre a programação da tarefa Script, consulte [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md).  
  
## Opções  
 **ScriptLanguage**  
 Selecione a linguagem de criação de scripts para a tarefa, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Depois de criar um script para a tarefa, você não poderá alterar o valor da propriedade **ScriptLanguage** .  
  
 Para definir a linguagem de criação de scripts padrão para a tarefa Script, use a opção **Idiomas de script** na página **Geral** da caixa de diálogo **Opções** . Para obter mais informações, consulte [General Page](../Topic/General%20Page.md).  
  
 **EntryPoint**  
 Especifique o método a ser chamado pelo tempo de execução do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como ponto de entrada no código da tarefa Script. O método especificado deve estar na classe ScriptMain do projeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). ScriptMain é a classe padrão gerada pelos modelos de script.  
  
 Caso altere o nome do método no projeto do VSTA, será preciso alterar o valor da propriedade **EntryPoint** .  
  
 **ReadOnlyVariables**  
 Digite uma lista, separada por vírgulas, de variáveis somente leitura disponíveis para o script ou clique no botão de reticências (**...**) e selecione as variáveis na caixa de diálogo **Selecionar variáveis**.  
  
> [!NOTE]  
>  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
 **ReadWriteVariables**  
 Digite uma lista, separada por vírgulas, de variáveis de leitura/gravação disponíveis para o script ou clique no botão de reticências (**…**) e selecione as variáveis na caixa de diálogo **Selecionar variáveis**.  
  
> [!NOTE]  
>  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
 **Editar Script**  
 Abre o VSTA IDE, onde você pode criar ou modificar o script.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Página Geral](../Topic/General%20Page.md)   
 [Editor da Tarefa Script &#40;Página Geral&#41;](../../integration-services/control-flow/script-task-editor-general-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)   
 [Exemplos de tarefa Script](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../Topic/Add,%20Delete,%20Change%20Scope%20of%20User-Defined%20Variable%20in%20a%20Package.md)  
  
  