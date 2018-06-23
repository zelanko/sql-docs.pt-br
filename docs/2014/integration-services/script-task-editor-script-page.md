---
title: Editor da tarefa script (página Script) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.scripttask.script.f1
helpviewer_keywords:
- Script Task Editor
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b5641a837761e113368eea47777c3c3bf82ee20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130786"
---
# <a name="script-task-editor-script-page"></a>Editor da Tarefa Script (página Script)
  Use a página **Script** da caixa de diálogo **Editor da Tarefa Script** para definir propriedades de script e especificar variáveis que podem ser acessados pelo script.  
  
> [!NOTE]  
>  No [!INCLUDE[ssISversion10](../includes/ssisversion10-md.md)] e versões posteriores, todos os scripts são pré-compilados. Em versões anteriores, devia ser definida uma propriedade **PrecompileScriptIntoBinaryCode** para especificar que o script estava pré-compilado.  
  
 Para obter mais informações sobre a tarefa Script, consulte [Script Task](control-flow/script-task.md) e [Configurando a tarefa Script no Editor da Tarefa Script](extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md). Para obter informações sobre a programação da tarefa Script, consulte [Extending the Package with the Script Task](extending-packages-scripting/task/extending-the-package-with-the-script-task.md).  
  
## <a name="options"></a>Opções  
 **ScriptLanguage**  
 Selecione a linguagem de criação de scripts para a tarefa, o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic ou o [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.  
  
 Depois de criar um script para a tarefa, você não poderá alterar o valor da propriedade **ScriptLanguage** .  
  
 Para definir a linguagem de criação de scripts padrão para a tarefa Script, use a opção **Idiomas de script** na página **Geral** da caixa de diálogo **Opções** . Para obter mais informações, consulte [General Page](general-page-of-integration-services-designers-options.md).  
  
 **EntryPoint**  
 Especifique o método a ser chamado pelo tempo de execução do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como ponto de entrada no código da tarefa Script. O método especificado deve estar na classe ScriptMain do projeto do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA). ScriptMain é a classe padrão gerada pelos modelos de script.  
  
 Caso altere o nome do método no projeto do VSTA, será preciso alterar o valor da propriedade **EntryPoint** .  
  
 **ReadOnlyVariables**  
 Digite uma lista, separada por vírgulas, de variáveis somente leitura disponíveis para o script ou clique no botão de reticências (**...**) e selecione as variáveis na caixa de diálogo **Selecionar variáveis** .  
  
> [!NOTE]  
>  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
 **ReadWriteVariables**  
 Digite uma lista, separada por vírgulas, de variáveis de leitura/gravação disponíveis para o script ou clique no botão de reticências (**…**) e selecione as variáveis na caixa de diálogo **Selecionar variáveis** .  
  
> [!NOTE]  
>  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
 **Editar Script**  
 Abre o VSTA IDE, onde você pode criar ou modificar o script.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página geral](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa script &#40;página geral&#41;](../../2014/integration-services/script-task-editor-general-page.md)   
 [Página expressões](expressions/expressions-page.md)   
 [Exemplos de tarefa de script](extending-packages-scripting-task-examples/script-task-examples.md)   
 [Serviços de integração &#40;SSIS&#41; variáveis](integration-services-ssis-variables.md)   
 [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  