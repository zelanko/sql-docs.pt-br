---
title: Editor da tarefa XML (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa0f92cc3275810b73d1dbe661a1f8473c7234df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054274"
---
# <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  Use o **nó Geral** da caixa de diálogo **Editor da Tarefa XML** para especificar o tipo de operação e configurar a operação.  
  
 Para obter informações sobre essa tarefa, consulte [XML Task](control-flow/xml-task.md). Para obter informações sobre como trabalhar com documentos e dados XML, consulte "[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)" na Biblioteca MSDN.  
  
## <a name="static-options"></a>Opções estáticas  
 **OperationType**  
 Selecione o tipo de operação na lista. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Validar**|Valida o documento XML com base em um esquema de definição de tipo de documento (DTD) ou definição de esquema XML (XSD). Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Validar**.|  
|**XSLT**|Executa transformações de XSL em documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **XSLT**.|  
|**XPATH**|Executa consultas e avaliações de XPath. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **XPATH**.|  
|**Mesclagem**|Mescla dois documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Mesclar**.|  
|**Diff**|Compara dois documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Diff**.|  
|**Patch**|Aplica a saída da operação Diff para criar um documento novo. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Patch**.|  
  
 **SourceType**  
 Selecione o tipo de origem do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **Origem**  
 Se a **Origem** for definida como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(...)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **Origem** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **Origem** for definida como **Variável**, selecione uma variável existente ou clique em **\<Nova variável...>** para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
## <a name="operationtype-dynamic-options"></a>Opções dinâmicas de OperationType  
  
### <a name="operationtype--validate"></a>OperationType = Validar  
 Especifique as opções para a operação Validar.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Validar.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Selecione um gerenciador de conexões de arquivos existente ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **ValidationType**  
 Selecione o tipo de validação. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**DTD**|Use uma DTD.|  
|**XSD**|Use um esquema XSD. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **ValidationType**.|  
  
 **FailOnValidationFail**  
 Especifique se a operação deve falhar caso o documento não seja validado.  
  
 **ValidationDetails**  
 Fornece a saída de erros completa quando o valor dessa propriedade é true. Para obter mais informações, consulte [Validate XML with the XML Task](control-flow/validate-xml-with-the-xml-task.md).  
  
### <a name="validationtype-dynamic-options"></a>Opções dinâmicas de ValidationType  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 Especifique as opções para a operação XSLT.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação XSLT.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 Especifique as opções para a operação XPath.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação XPath.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
 **PutResultInOneNode**  
 Especifique se o resultado é gravado em um único nó.  
  
 **XPathOperation**  
 Selecione o tipo de resultado XPath. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Evaluation**|Retorna os resultados de uma função XPath.|  
|**Lista de nós**|Retorna os nós selecionados como um fragmento XML.|  
|**Valores**|Retorna o valor do texto interno de todos os nós selecionados, concatenados em uma cadeia de caracteres.|  
  
### <a name="operationtype--merge"></a>OperationType = Mesclar  
 Especifique as opções para a operação Mesclar.  
  
 **XPathStringSourceType**  
 Selecione o tipo de origem do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **XPathStringSource**  
 Se **XPathStringSourceType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **XPathStringSourceType** for definido com **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
 Quando você usa uma instrução XPath para identificar o local de mesclagem no documento original, espera-se que esta instrução retorne um único nó. Se a instrução retornar vários nós, apenas o primeiro será usado. O conteúdo do segundo documento é mesclado no primeiro nó retornado pela consulta XPath.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Mesclar.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **SecondOperandType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--diff"></a>OperationType = Diff  
 Especifique as opções para a operação Diff.  
  
 **DiffAlgorithm**  
 Selecione o algoritmo Diff para ser usado ao comparar documentos. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Auto**|Deixe a tarefa XML determinar se o algoritmo rápido ou preciso deve ser usado.|  
|**Rápido**|Use um algoritmo Diff rápido, porém menos preciso.|  
|**Preciso**|Use um algoritmo Diff preciso.|  
  
 **Opções de comparação**  
 Defina as opções de Diff a serem aplicadas à operação Diff. As opções estão listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|Especifique se a declaração XML deve ser comparada.|  
|**IgnoreDTD**|Especifique se a DTD deve ser ignorada.|  
|**Espaços IgnoreWhite**|Especifique se devem ser ignoradas as diferenças na quantidade de espaços em branco ao comparar documentos.|  
|**IgnoreNamespaces**|Especifique se devem ser comparados o URI (Uniform Resource Identifier) no namespace de um elemento e seus nomes de atributo.<br /><br /> Observação: se essa opção for definida como `True`, dois elementos que têm o mesmo nome local, mas namespaces diferentes, serão considerados idênticos.|  
|**IgnoreProcessingInstructions**|Especifique se as instruções de processamento devem ser comparadas.|  
|**IgnoreOrderOf ChildElements**|Especifique se a ordem de elementos filho deve ser comparada.<br /><br /> Observação: se essa opção for definida como `True`, os elementos filhos que diferirem apenas em sua posição em uma lista de irmãos serão considerados idênticos.|  
|**IgnoreComments**|Especifique se os nós de comentário devem ser comparados.|  
|**IgnorePrefixes**|Especifique se os prefixos de elemento e nomes de atributo devem ser comparados.<br /><br /> Observação: se você definir esta opção como `True`, dois elementos que têm o mesmo nome local, porém URIs e prefixos de namespace diferentes, serão considerados idênticos.|  
  
 **FailOnDifference**  
 Especifique se a tarefa falha caso a operação Diff falhar.  
  
 **SaveDiffGram**  
 Especifique se o resultado da comparação deve ser salvo, um documento DiffGram.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Diff.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **SecondOperandType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--patch"></a>OperationType = Patch  
 Especifique as opções para a operação Patch.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Patch.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [adicione a variável](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Entrada direta**|Defina a origem de um documento XML.|  
|**Conexão de arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se a **SecondOperandType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  
