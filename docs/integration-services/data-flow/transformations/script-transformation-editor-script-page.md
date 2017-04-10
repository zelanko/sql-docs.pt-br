---
title: "Editor de Transforma&#231;&#227;o Scripts (p&#225;gina Script) | Microsoft Docs"
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
  - "sql13.dts.designer.scriptcomponent.script.f1"
helpviewer_keywords: 
  - "Editor de Transformação Scripts"
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Editor de Transforma&#231;&#227;o Scripts (p&#225;gina Script)
  Use a guia **Script** da caixa de diálogo **Editor de Transformação Scripts** para especificar um script e propriedades relacionadas.  
  
 Para obter mais informações sobre o componente Script, consulte [Script Component](../../../integration-services/data-flow/transformations/script-component.md) e [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
## Opções  
 **Propriedades**  
 Visualize e modifique as propriedades da transformação Scripts. Muitas das propriedades exibidas são somente leitura. Você pode modificar as seguintes propriedades:  
  
|Value|Description|  
|-----------|-----------------|  
|**Description**|Descreva a finalidade da transformação scripts.|  
|**LocaleID**|Especifique a localidade para fornecer informações de solicitação e de conversão de data e hora específicas da região.|  
|**Nome**|Digite um nome descritivo para o componente.|  
|**ValidateExternalMetadata**|Indique se a transformação Scripts deve validar coluna de metadados contra fontes de dados externas em tempo de design. Um valor de **false** retarda a validação até o momento da execução.|  
|**ReadOnlyVariables**|Digite uma lista de variáveis separada por vírgulas a ser acessada em modo somente leitura pela transformação Scripts.<br /><br /> Observação: nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.|  
|**ReadWriteVariables**|Digite uma lista de variáveis separada por vírgulas a ser acessada em modo leitura/gravação pela transformação Scripts.<br /><br /> Observação: nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.|  
|**ScriptLanguage**|Selecione a linguagem de script a ser usada pelo componente de Script.<br /><br /> Para definir a linguagem de script padrão para componentes e tarefas de Script, use a opção **Linguagem de script** na página **Geral** da caixa de diálogo **Opções** .|  
|**UserComponentTypeName**|Especifica a classe <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> e o assembly **Microsoft.SqlServer.TxScript** que dá suporte à infraestrutura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
 **Editar Script**  
 Use o VSTA [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] (Tools for Applications) para criar ou modificar um script.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Selecionar Tipo de Componente do Script](../../../integration-services/data-flow/transformations/select-script-component-type.md)   
 [Editor de Transformação Scripts &#40;página Colunas de Entrada&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)   
 [Editor de Transformação Scripts &#40;Página Entradas e Saídas&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)   
 [Editor de Transformação Scripts &#40;Página Gerenciadores de Conexões&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)   
 [Exemplos de componentes Script adicionais](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  