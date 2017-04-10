---
title: "XML Task | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.xmltask.f1"
helpviewer_keywords: 
  - "XML [Integration Services]"
  - "Tarefa XML [Integration Services]"
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
caps.latest.revision: 59
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 59
---
# XML Task
  A tarefa XML é usada para se trabalhar com dados XML. Usando essa tarefa, um pacote pode recuperar documentos XML, aplicar operações aos documentos usando folhas de estilos XSLT e expressões XPath, mesclar vários documentos ou validar, comparar e salvar os documentos atualizados em arquivos e variáveis.  
  
 Essa tarefa permite que um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] modifique dinamicamente os documentos XML no tempo de execução. Você pode usar a tarefa XML para os seguintes propósitos:  
  
-   Reformatar um documento XML. Por exemplo, a tarefa pode acessar um relatório que esteja em um arquivo XML e dinamicamente aplicar uma folha de estilo XSLT para personalizar a apresentação do documento.  
  
-   Selecionar seções de um documento XML. Por exemplo, a tarefa pode acessar um relatório que esteja em um arquivo XML e dinamicamente aplicar uma expressão XPath para selecionar uma seção do documento. A operação também pode obter e processar valores do documento.  
  
-   Mesclar documentos de várias fontes. Por exemplo, a tarefa pode fazer o download de relatórios de várias fontes e dinamicamente mesclá-los em um documento XML abrangente.  
  
-   Validar um documento XML e, opcionalmente, obter saída de erros detalhada. Para obter mais informações, consulte [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
 Você pode incluir dados XML em um fluxo de dados por meio de uma origem XML para extrair valores de um documento XML. Para obter mais informações, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## Operações XML  
 A primeira ação que a tarefa XML executa é recuperar um documento XML específico. Essa ação está incorporada à tarefa XML e ocorre automaticamente. O documento XML recuperado é usado como a fonte de dados para a operação que a tarefa XML executa.  
  
 As operações XML Diff, Merge e Patch requerem dois operandos. O primeiro operando especifica o documento XML de origem. O segundo operando também especifica um documento XML, e seu conteúdo depende dos requisitos da operação. Por exemplo, a operação Diff compara dois documentos; por isso, o segundo operando especifica outro documento XML similar com o qual o documento XML de origem é comparado.  
  
 A tarefa XML pode usar uma variável ou um gerenciador de conexões de arquivo como sua fonte ou incluir os dados XML em uma propriedade de tarefa.  
  
 Se a fonte for uma variável, a variável especificada conterá o caminho do documento XML.  
  
 Se a origem for um gerenciador de conexões de arquivo, o gerenciador de conexões de arquivo fornecerá as informações de origem. O gerenciador de conexões de arquivo é configurado separadamente da tarefa XML e, em seguida, é mencionado na tarefa XML. A cadeia de caracteres de conexão do gerenciador de conexões de arquivo especifica o caminho do arquivo XML. Para obter mais informações, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 A tarefa XML pode ser configurada para salvar o resultado da operação em uma variável ou em um arquivo. Caso salve um arquivo, a tarefa XML usará um gerenciador de conexões de arquivo para acessar o arquivo. Você também pode salvar os resultados de Diffgram gerados pela operação Diff nos arquivos e variáveis.  
  
## Operações XML predefinidas  
 A tarefa XML inclui um conjunto predefinido de operações para trabalhar com documentos XML. A tabela a seguir descreve essas operações.  
  
|Operação|Description|  
|---------------|-----------------|  
|Diff|Compara dois documentos XML. Usando o documento XML de origem como documento base, a operação Diff o compara a um segundo documento XML, detecta as suas diferenças e as grava em um documento Diffgram XML. Essa operação inclui propriedades para personalizar a comparação.|  
|Mesclagem|Mescla dois documentos XML. Usando o documento XML de origem como o documento base, a operação Merge adiciona o conteúdo de um segundo documento ao documento base. A operação pode especificar um local de mesclagem dentro do documento base.|  
|Patch|Aplica a saída da operação Diff, conhecida como documento Diffgram, a um documento XML para criar um novo documento pai que inclua o conteúdo do documento Diffgram.|  
|Validar|Valida o documento XML com base em um esquema de definição de tipo de documento (DTD) ou definição de esquema XML (XSD).|  
|XPath|Executa consultas e avaliações de XPath.|  
|XSLT|Executa transformações de XSL em documentos XML.|  
  
### Operação Diff  
 A operação Diff pode ser configurada para usar um algoritmo de comparação diferente, dependendo de a comparação precisar ser rápida ou precisa. A operação também pode ser configurada para selecionar automaticamente a comparação rápida ou precisa com base no tamanho dos documentos que são comparados.  
  
 A operação Diff inclui um conjunto de opções que personalizam a comparação XML. A tabela a seguir descreve as opções.  
  
|Opção|Description|  
|------------|-----------------|  
|**IgnoreComments**|Um valor que especifica se os nós de comentários devem ser comparados.|  
|**IgnoreNamespaces**|Um valor que especifica se o URI (uniform resource identifier) no namespace de um elemento e seus nomes de atributo devem ser comparados. Se essa opção for definida como **true**, dois elementos que têm o mesmo nome local, mas um namespace diferente, serão considerados idênticos.|  
|**IgnorePrefixes**|Um valor que especifica se devem ser comparados os prefixos de elemento e nomes de atributo. Se essa opção for definida como **true,** , dois elementos que têm o mesmo nome local, mas um URI de namespace e um prefixo diferentes, serão considerados idênticos.|  
|**IgnoreXMLDeclaration**|Um valor que especifica se as declarações XML devem ser comparadas.|  
|**IgnoreOrderOfChildElements**|Um valor que especifica se a ordem de elementos filho deve ser comparada. Se essa opção for definida como **true**, os elementos filho diferentes apenas em sua posição em uma lista de irmãos serão considerados idênticos.|  
|**IgnoreWhiteSpaces**|Um valor que especifica se os espaços em branco devem ser comparados.|  
|**IgnoreProcessingInstructions**|Um valor que especifica se as instruções de processamento devem ser comparadas.|  
|**IgnoreDTD**|Um valor que especifica se o DTD deve ser ignorado.|  
  
### Operação de mesclagem  
 Quando você usa uma instrução XPath para identificar o local de mesclagem no documento original, espera-se que esta instrução retorne um único nó. Se a instrução retornar vários nós, apenas o primeiro será usado. O conteúdo do segundo documento é mesclado no primeiro nó retornado pela consulta XPath.  
  
### Operação XPath  
 A operação XPath pode ser configurada para usar tipos diferentes de funcionalidade XPath.  
  
-   Selecione a opção **Avaliação** para implementar as funções XPath, como sum().  
  
-   Selecione a opção **Lista de nós** para retornar os nós selecionados como um fragmento XML.  
  
-   Selecione a opção **Valores** para retornar o valor de texto interno de todos os nós selecionados, concatenados em uma cadeia de caracteres.  
  
### Operação Validation  
 A operação Validation pode ser configurada para usar um esquema de definição DTD (Document Type Definition) ou XSD (XML Schema).  
  
 Habilite **ValidationDetails** para obter saída de erros detalhada. Para obter mais informações, consulte [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
## Codificação de documentos XML  
 A tarefa XML oferece suporte a mesclagem apenas de documentos Unicode. Isso significa que a tarefa só pode ser aplicada à operação Merge em documentos que tenham a codificação Unicode. O uso de outras codificações fará a tarefa XML falhar.  
  
> [!NOTE]  
>  As operações Diff e Patch incluem uma opção para ignorar a declaração XML nos dados XML do segundo operando, possibilitando o uso de documentos que tenham outras codificações nessas operações.  
  
 Para verificar se o documento XML pode ser usado, analise a declaração XML. A declaração deve especificar explicitamente UTF-8, que indica a codificação Unicode de 8 bits.  
  
 A marca a seguir mostra a codificação Unicode de 8 bits.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## Mensagens de log personalizadas disponíveis na tarefa XML  
 A tabela a seguir descreve a entrada de log personalizada da tarefa XML. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**XMLOperation**|Fornece informações sobre a operação executada pela tarefa|  
  
## Configuração da tarefa XML  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa XML &#40;página Geral&#41;](../../integration-services/control-flow/xml-task-editor-general-page.md)  
  
-   [Validar XML com a Tarefa XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Configuração programática da tarefa XML  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## Tarefas relacionadas  
 [Definir as propriedades de uma tarefa ou contêiner](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Conteúdo relacionado  
  
-   Entrada de blog, [XML Destination Script Component](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/), em agilebi.com  
  
-   Exemplo do CodePlex, [Process XML Data Package Sample](http://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples), em www.codeplex.com  
  
  