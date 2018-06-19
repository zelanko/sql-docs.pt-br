---
title: Tarefa XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.xmltask.f1
- sql13.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d9726b86fd0d441b8e99a155b10abbd3804a7143
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331230"
---
# <a name="xml-task"></a>XML Task
  A tarefa XML é usada para se trabalhar com dados XML. Usando essa tarefa, um pacote pode recuperar documentos XML, aplicar operações aos documentos usando folhas de estilos XSLT e expressões XPath, mesclar vários documentos ou validar, comparar e salvar os documentos atualizados em arquivos e variáveis.  
  
 Essa tarefa permite que um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] modifique dinamicamente os documentos XML no tempo de execução. Você pode usar a tarefa XML para os seguintes propósitos:  
  
-   Reformatar um documento XML. Por exemplo, a tarefa pode acessar um relatório que esteja em um arquivo XML e dinamicamente aplicar uma folha de estilo XSLT para personalizar a apresentação do documento.  
  
-   Selecionar seções de um documento XML. Por exemplo, a tarefa pode acessar um relatório que esteja em um arquivo XML e dinamicamente aplicar uma expressão XPath para selecionar uma seção do documento. A operação também pode obter e processar valores do documento.  
  
-   Mesclar documentos de várias fontes. Por exemplo, a tarefa pode fazer o download de relatórios de várias fontes e dinamicamente mesclá-los em um documento XML abrangente.  
  
-   Validar um documento XML e, opcionalmente, obter saída de erros detalhada. Para obter mais informações, consulte [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
 Você pode incluir dados XML em um fluxo de dados por meio de uma origem XML para extrair valores de um documento XML. Para obter mais informações, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="xml-operations"></a>Operações XML  
 A primeira ação que a tarefa XML executa é recuperar um documento XML específico. Essa ação está incorporada à tarefa XML e ocorre automaticamente. O documento XML recuperado é usado como a fonte de dados para a operação que a tarefa XML executa.  
  
 As operações XML Diff, Merge e Patch requerem dois operandos. O primeiro operando especifica o documento XML de origem. O segundo operando também especifica um documento XML, e seu conteúdo depende dos requisitos da operação. Por exemplo, a operação Diff compara dois documentos; por isso, o segundo operando especifica outro documento XML similar com o qual o documento XML de origem é comparado.  
  
 A tarefa XML pode usar uma variável ou um gerenciador de conexões de arquivo como sua fonte ou incluir os dados XML em uma propriedade de tarefa.  
  
 Se a fonte for uma variável, a variável especificada conterá o caminho do documento XML.  
  
 Se a origem for um gerenciador de conexões de arquivo, o gerenciador de conexões de arquivo fornecerá as informações de origem. O gerenciador de conexões de arquivo é configurado separadamente da tarefa XML e, em seguida, é mencionado na tarefa XML. A cadeia de caracteres de conexão do gerenciador de conexões de arquivo especifica o caminho do arquivo XML. Para obter mais informações, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 A tarefa XML pode ser configurada para salvar o resultado da operação em uma variável ou em um arquivo. Caso salve um arquivo, a tarefa XML usará um gerenciador de conexões de arquivo para acessar o arquivo. Você também pode salvar os resultados de Diffgram gerados pela operação Diff nos arquivos e variáveis.  
  
## <a name="predefined-xml-operations"></a>Operações XML predefinidas  
 A tarefa XML inclui um conjunto predefinido de operações para trabalhar com documentos XML. A tabela a seguir descreve essas operações.  
  
|Operação|Descrição|  
|---------------|-----------------|  
|Diff|Compara dois documentos XML. Usando o documento XML de origem como documento base, a operação Diff o compara a um segundo documento XML, detecta as suas diferenças e as grava em um documento Diffgram XML. Essa operação inclui propriedades para personalizar a comparação.|  
|Mesclagem|Mescla dois documentos XML. Usando o documento XML de origem como o documento base, a operação Merge adiciona o conteúdo de um segundo documento ao documento base. A operação pode especificar um local de mesclagem dentro do documento base.|  
|Patch|Aplica a saída da operação Diff, conhecida como documento Diffgram, a um documento XML para criar um novo documento pai que inclua o conteúdo do documento Diffgram.|  
|Validar|Valida o documento XML com base em um esquema de definição de tipo de documento (DTD) ou definição de esquema XML (XSD).|  
|XPath|Executa consultas e avaliações de XPath.|  
|XSLT|Executa transformações de XSL em documentos XML.|  
  
### <a name="diff-operation"></a>Operação Diff  
 A operação Diff pode ser configurada para usar um algoritmo de comparação diferente, dependendo de a comparação precisar ser rápida ou precisa. A operação também pode ser configurada para selecionar automaticamente a comparação rápida ou precisa com base no tamanho dos documentos que são comparados.  
  
 A operação Diff inclui um conjunto de opções que personalizam a comparação XML. A tabela a seguir descreve as opções.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**IgnoreComments**|Um valor que especifica se os nós de comentários devem ser comparados.|  
|**IgnoreNamespaces**|Um valor que especifica se o URI (uniform resource identifier) no namespace de um elemento e seus nomes de atributo devem ser comparados. Se essa opção for definida como **true**, dois elementos que têm o mesmo nome local, mas um namespace diferente, serão considerados idênticos.|  
|**IgnorePrefixes**|Um valor que especifica se devem ser comparados os prefixos de elemento e nomes de atributo. Se essa opção for definida como **true,** , dois elementos que têm o mesmo nome local, mas um URI de namespace e um prefixo diferentes, serão considerados idênticos.|  
|**IgnoreXMLDeclaration**|Um valor que especifica se as declarações XML devem ser comparadas.|  
|**IgnoreOrderOfChildElements**|Um valor que especifica se a ordem de elementos filho deve ser comparada. Se essa opção for definida como **true**, os elementos filho diferentes apenas em sua posição em uma lista de irmãos serão considerados idênticos.|  
|**IgnoreWhiteSpaces**|Um valor que especifica se os espaços em branco devem ser comparados.|  
|**IgnoreProcessingInstructions**|Um valor que especifica se as instruções de processamento devem ser comparadas.|  
|**IgnoreDTD**|Um valor que especifica se o DTD deve ser ignorado.|  
  
### <a name="merge-operation"></a>Operação de mesclagem  
 Quando você usa uma instrução XPath para identificar o local de mesclagem no documento original, espera-se que esta instrução retorne um único nó. Se a instrução retornar vários nós, apenas o primeiro será usado. O conteúdo do segundo documento é mesclado no primeiro nó retornado pela consulta XPath.  
  
### <a name="xpath-operation"></a>Operação XPath  
 A operação XPath pode ser configurada para usar tipos diferentes de funcionalidade XPath.  
  
-   Selecione a opção **Avaliação** para implementar as funções XPath, como sum().  
  
-   Selecione a opção **Lista de nós** para retornar os nós selecionados como um fragmento XML.  
  
-   Selecione a opção **Valores** para retornar o valor de texto interno de todos os nós selecionados, concatenados em uma cadeia de caracteres.  
  
### <a name="validation-operation"></a>Operação Validation  
 A operação Validation pode ser configurada para usar um esquema de definição DTD (Document Type Definition) ou XSD (XML Schema).  
  
 Habilite **ValidationDetails** para obter saída de erros detalhada. Para obter mais informações, consulte [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
## <a name="xml-document-encoding"></a>Codificação de documentos XML  
 A tarefa XML oferece suporte a mesclagem apenas de documentos Unicode. Isso significa que a tarefa só pode ser aplicada à operação Merge em documentos que tenham a codificação Unicode. O uso de outras codificações fará a tarefa XML falhar.  
  
> [!NOTE]  
>  As operações Diff e Patch incluem uma opção para ignorar a declaração XML nos dados XML do segundo operando, possibilitando o uso de documentos que tenham outras codificações nessas operações.  
  
 Para verificar se o documento XML pode ser usado, analise a declaração XML. A declaração deve especificar explicitamente UTF-8, que indica a codificação Unicode de 8 bits.  
  
 A marca a seguir mostra a codificação Unicode de 8 bits.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>Mensagens de log personalizadas disponíveis na tarefa XML  
 A tabela a seguir descreve a entrada de log personalizada da tarefa XML. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**XMLOperation**|Fornece informações sobre a operação executada pela tarefa|  
  
## <a name="configuration-of-the-xml-task"></a>Configuração da tarefa XML  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Validar XML com a Tarefa XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>Configuração programática da tarefa XML  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  Use o **nó Geral** da caixa de diálogo **Editor da Tarefa XML** para especificar o tipo de operação e configurar a operação.  
  
 Para saber mais sobre essa tarefa, consulte [Validar XML com a Tarefa XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md). Para obter informações sobre como trabalhar com documentos e dados XML, consulte "[Employing XML in the .NET Framework](http://go.microsoft.com/fwlink/?LinkId=56214)" na Biblioteca MSDN.  
  
### <a name="static-options"></a>Opções estáticas  
 **OperationType**  
 Selecione o tipo de operação na lista. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Validar**|Valida o documento XML com base em um esquema de definição de tipo de documento (DTD) ou definição de esquema XML (XSD). Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Validar**.|  
|**XSLT**|Executa transformações de XSL em documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **XSLT**.|  
|**XPATH**|Executa consultas e avaliações de XPath. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **XPATH**.|  
|**Mesclagem**|Mescla dois documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Mesclar**.|  
|**Diff**|Compara dois documentos XML. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Diff**.|  
|**Patch**|Aplica a saída da operação Diff para criar um documento novo. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas na seção **Patch**.|  
  
 **SourceType**  
 Selecione o tipo de origem do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **Origem**  
 Se a **Origem** for definida como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(...)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **Origem** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **Origem** for definida como **Variável**, selecione uma variável existente ou clique em **\<Nova variável...>** para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="operationtype-dynamic-options"></a>Opções dinâmicas de OperationType  
  
#### <a name="operationtype--validate"></a>OperationType = Validar  
 Especifique as opções para a operação Validar.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Validar.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Selecione um gerenciador de conexões de arquivos existente ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **ValidationType**  
 Selecione o tipo de validação. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
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
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
#### <a name="operationtype--xslt"></a>OperationType = XSLT  
 Especifique as opções para a operação XSLT.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação XSLT.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
#### <a name="operationtype--xpath"></a>OperationType = XPATH  
 Especifique as opções para a operação XPath.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação XPath.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de origem do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML utilizando a caixa de diálogo **Editor de Origem**.  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **PutResultInOneNode**  
 Especifique se o resultado é gravado em um único nó.  
  
 **XPathOperation**  
 Selecione o tipo de resultado XPath. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Evaluation**|Retorna os resultados de uma função XPath.|  
|**Lista de nós**|Retorna os nós selecionados como um fragmento XML.|  
|**Valores**|Retorna o valor do texto interno de todos os nós selecionados, concatenados em uma cadeia de caracteres.|  
  
#### <a name="operationtype--merge"></a>OperationType = Mesclar  
 Especifique as opções para a operação Mesclar.  
  
 **XPathStringSourceType**  
 Selecione o tipo de origem do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **XPathStringSource**  
 Se **XPathStringSourceType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento**.  
  
 Se **XPathStringSourceType** for definido com **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **XPathStringSourceType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 Quando você usa uma instrução XPath para identificar o local de mesclagem no documento original, espera-se que esta instrução retorne um único nó. Se a instrução retornar vários nós, apenas o primeiro será usado. O conteúdo do segundo documento é mesclado no primeiro nó retornado pela consulta XPath.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Mesclar.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do segundo documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **SecondOperandType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--diff"></a>OperationType = Diff  
 Especifique as opções para a operação Diff.  
  
 **DiffAlgorithm**  
 Selecione o algoritmo Diff para ser usado ao comparar documentos. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Auto**|Deixe a tarefa XML determinar se o algoritmo rápido ou preciso deve ser usado.|  
|**Rápido**|Use um algoritmo Diff rápido, porém menos preciso.|  
|**Preciso**|Use um algoritmo Diff preciso.|  
  
 **Opções de Diff**  
 Defina as opções de Diff a serem aplicadas à operação Diff. As opções estão listadas na tabela a seguir.  
  
|Valor|Descrição|  
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
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **SecondOperandType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--patch"></a>OperationType = Patch  
 Especifique as opções para a operação Patch.  
  
 **SaveOperationResult**  
 Especifique se a tarefa XML salva a saída da operação Patch.  
  
 **OverwriteDestination**  
 Especifique se o arquivo ou a variável de destino deve ser substituída.  
  
 **Destino**  
 Se **DestinationType** está definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **DestinationType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperandType**  
 Selecione o tipo de destino do documento XML. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de um documento XML.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém o documento XML.|  
|**Variável**|Defina a origem como uma variável que contém o documento XML.|  
  
 **SecondOperand**  
 Se **SecondOperandType** for definido como **Entrada direta**, forneça o código XML ou clique no botão de reticências **(…)** e forneça o XML usando a caixa de diálogo **Editor de Origem de Documento** .  
  
 Se **SecondOperandType** for definido como **Conexão do arquivo**, selecione um gerenciador de conexões de arquivos ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Se a **SecondOperandType** for definida como **Variável**, selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados**: [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [XML Destination Script Component](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/), em agilebi.com  
  
-   Exemplo do CodePlex, [Process XML Data Package Sample](http://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples), em www.codeplex.com  
  
  
