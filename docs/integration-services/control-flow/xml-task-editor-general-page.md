---
title: "Editor da tarefa XML (página geral) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9dc1f49a7e2fcee8b87546585075d016f1f6ace
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  Use o **nó Geral** da caixa de diálogo **Editor da Tarefa XML** para especificar o tipo de operação e configurar a operação.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa XML](../../integration-services/control-flow/xml-task.md) e [Validar XML com a Tarefa XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md). Para obter informações sobre como trabalhar com documentos e dados XML, consulte "[Employing XML in the .NET Framework](http://go.microsoft.com/fwlink/?LinkId=56214)" na Biblioteca MSDN.  
  
## <a name="static-options"></a>Opções estáticas  
 **OperationType**  
 Selecione o tipo de operação na lista. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Validar**|Valida o documento XML com base em um esquema de definição de tipo de documento (DTD) ou definição de esquema XML (XSD). Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Validar**.|  
|**XSLT**|Executa transformações de XSL em documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **XSLT**.|  
|**XPATH**|Executa consultas e avaliações de XPath. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **XPATH**.|  
|**Mesclagem**|Mescla dois documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Mesclar**.|  
|**Diff**|Compara dois documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Diff**.|  
|**Patch**|Aplica a saída da operação Diff para criar um documento novo. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Patch**.|  
  
 **SourceType**  
 Selecione o tipo de origem do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **Origem**  
 Se a **Origem** for definida como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(...)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **fonte** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **fonte** é definido como **variável**, selecione uma variável existente ou clique em  **\<nova variável... >** para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
## <a name="operationtype-dynamic-options"></a>Opções dinâmicas de OperationType  
  
### <a name="operationtype--validate"></a>OperationType = Validar  
 Especifique as opções para a operação Validar.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Validar.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Selecione um Gerenciador de conexão de arquivo existente ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **ValidationType**  
 Selecione o tipo de validação. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**DTD**|Use uma DTD.|  
|**XSD**|Use um esquema XSD. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **ValidationType**.|  
  
 **FailOnValidationFail**  
 Especifique se a operação deve falhar caso o documento não seja validado.  
  
 **ValidationDetails**  
 Fornece a saída de erros completa quando o valor dessa propriedade é true. Para obter mais informações, consulte [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
### <a name="validationtype-dynamic-options"></a>Opções dinâmicas de ValidationType  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem** .  
  
 Se **SecondOperandType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 Especifique as opções para a operação XSLT.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação XSLT.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **DestinationType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem** .  
  
 Se **SecondOperandType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 Especifique as opções para a operação XPath.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação XPath.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **DestinationType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem** .  
  
 Se **SecondOperandType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **PutResultInOneNode**  
 Especifique se o resultado é gravado em um único nó.  
  
 **XPathOperation**  
 Selecione o tipo de resultado XPath. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Evaluation**|Retorna os resultados de uma função XPath.|  
|**Lista de nós**|Retorna os nós selecionados como um fragmento XML.|  
|**Valores**|Retorna o valor do texto interno de todos os nós selecionados, concatenados em uma cadeia de caracteres.|  
  
### <a name="operationtype--merge"></a>OperationType = Mesclar  
 Especifique as opções para a operação Mesclar.  
  
 **XPathStringSourceType**  
 Selecione o tipo de origem do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **XPathStringSource**  
 Se **XPathStringSourceType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **XPathStringSourceType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 Quando você usa uma instrução XPath para identificar o local de mesclagem no documento original, espera-se que esta instrução retorne um único nó. Se a instrução retornar vários nós, apenas o primeiro será usado. O conteúdo do segundo documento é mesclado no primeiro nó retornado pela consulta XPath.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Mesclar.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **DestinationType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **SecondOperandType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **SecondOperandType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="operationtype--diff"></a>OperationType = Diff  
 Especifique as opções para a operação Diff.  
  
 **DiffAlgorithm**  
 Selecione o algoritmo Diff para ser usado ao comparar documentos. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Auto**|Deixe a tarefa XML determinar se o algoritmo rápido ou preciso deve ser usado.|  
|**Rápido**|Use um algoritmo Diff rápido, porém menos preciso.|  
|**Preciso**|Use um algoritmo Diff preciso.|  
  
 **Opções de Diff**  
 Defina as opções de Diff a serem aplicadas à operação Diff. As opções estão listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|Especifique se a declaração XML deve ser comparada.|  
|**IgnoreDTD**|Especifique se a DTD deve ser ignorada.|  
|**IgnoreWhite Spaces**|Especifique se devem ser ignoradas as diferenças na quantidade de espaços em branco ao comparar documentos.|  
|**IgnoreNamespaces**|Especifique se devem ser comparados o URI (Uniform Resource Identifier) no namespace de um elemento e seus nomes de atributo.<br /><br /> Observação: se essa opção for definida como **True**, dois elementos que têm o mesmo nome local, mas namespaces diferentes, serão considerados idênticos.|  
|**IgnoreProcessingInstructions**|Especifique se as instruções de processamento devem ser comparadas.|  
|**IgnoreOrderOf ChildElements**|Especifique se a ordem de elementos filho deve ser comparada.<br /><br /> Observação: se essa opção for definida como **True**, os elementos filhos que diferirem apenas em sua posição em uma lista de irmãos serão considerados idênticos.|  
|**IgnoreComments**|Especifique se os nós de comentário devem ser comparados.|  
|**IgnorePrefixes**|Especifique se os prefixos de elemento e nomes de atributo devem ser comparados.<br /><br /> Observação: se você definir esta opção como **True**, dois elementos que têm o mesmo nome local, porém URIs e prefixos de namespace diferentes, serão considerados idênticos.|  
  
 **FailOnDifference**  
 Especifique se a tarefa falha caso a operação Diff falhar.  
  
 **SaveDiffGram**  
 Especifique se o resultado da comparação deve ser salvo, um documento DiffGram.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Diff.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **DestinationType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **SecondOperandType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **SecondOperandType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="operationtype--patch"></a>OperationType = Patch  
 Especifique as opções para a operação Patch.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Patch.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **DestinationType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **SecondOperandType** é definido como **conexão de arquivo**, selecione um Gerenciador de conexão de arquivo ou clique em \< **nova conexão...** > para criar uma nova conexão Gerenciador.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se **SecondOperandType** é definido como **variável**, selecione uma variável existente ou clique em \< **nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  
