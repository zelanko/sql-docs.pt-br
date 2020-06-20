---
title: Editor de transformação scripts (página script) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script Transformation Editor
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f172aa778cbaa959671da870521641147186f571
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964016"
---
# <a name="script-transformation-editor-script-page"></a>Editor de Transformação Scripts (página Script)
  Use a guia **Script** da caixa de diálogo **Editor de Transformação Scripts** para especificar um script e propriedades relacionadas.  
  
 Para obter mais informações sobre o componente Script, consulte [Script Component](data-flow/transformations/script-component.md) e [Configuring the Script Component in the Script Component Editor](extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obter informações sobre a programação do componente Script, consulte [Estender o fluxo de dados com o componente de Script](extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
## <a name="options"></a>Opções  
 **Propriedades**  
 Visualize e modifique as propriedades da transformação Scripts. Muitas das propriedades exibidas são somente leitura. Você pode modificar as seguintes propriedades:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Descrição**|Descreva a finalidade da transformação scripts.|  
|**LocaleID**|Especifique a localidade para fornecer informações de solicitação e de conversão de data e hora específicas da região.|  
|**Nome**|Digite um nome descritivo para o componente.|  
|**ValidateExternalMetadata**|Indique se a transformação Scripts deve validar coluna de metadados contra fontes de dados externas em tempo de design. Um valor de `false` retarda a validação até o momento da execução.|  
|**ReadOnlyVariables**|Digite uma lista de variáveis separada por vírgulas a ser acessada em modo somente leitura pela transformação Scripts.<br /><br /> Observação: nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.|  
|**ReadWriteVariables**|Digite uma lista de variáveis separada por vírgulas a ser acessada em modo leitura/gravação pela transformação Scripts.<br /><br /> Observação: nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.|  
|**ScriptLanguage**|Selecione a linguagem de script a ser usada pelo componente de Script.<br /><br /> Para definir a linguagem de script padrão para componentes e tarefas de Script, use a opção **Linguagem de script** na página **Geral** da caixa de diálogo **Opções** . Para obter mais informações, consulte [General Page](general-page-of-integration-services-designers-options.md).|  
|**UserComponentTypeName**|Especifica a classe <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> e o `Microsoft.SqlServer.TxScript` assembly que aceitam a infraestrutura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
 **Editar Script**  
 Use [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o VSTA (Tools for Applications) para criar ou modificar um script.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Selecionar tipo de componente de script](../../2014/integration-services/select-script-component-type.md)   
 [Editor de transformação scripts &#40;página colunas de entrada&#41;](../../2014/integration-services/script-transformation-editor-input-columns-page.md)   
 [Editor de transformação scripts &#40;página entradas e saídas&#41;](../../2014/integration-services/script-transformation-editor-inputs-and-outputs-page.md)   
 [Editor de transformação scripts &#40;página gerenciadores de conexões&#41;](../../2014/integration-services/script-transformation-editor-connection-managers-page.md)   
 [Exemplos de componentes Script adicionais](extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  
