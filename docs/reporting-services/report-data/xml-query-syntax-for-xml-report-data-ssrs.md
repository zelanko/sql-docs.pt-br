---
title: "Sintaxe de consulta XML para dados de relatório XML (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1dd867551f7413e07ac70b290e73e817f34878b9
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>Sintaxe de consulta XML para dados de relatório XML (SSRS)
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é possível criar conjuntos de dados para fontes de dados XML. Após definir uma fonte de dados, crie uma consulta para o conjunto de dados. Dependendo do tipo de dados XML apontado pela fonte de dados, a consulta do conjunto de dados é criada incluindo uma **Query** XML ou um caminho de elemento. Um XML **consulta** começa com um  **\<consulta >** marca e inclui namespaces e elementos XML que variam de acordo com a fonte de dados. Um caminho de elemento não depende do namespace e especifica quais nós e atributos de nós devem ser usados nos dados XML subjacentes com uma sintaxe do tipo XPath. Para obter mais informações sobre os caminhos de elemento, consulte [Sintaxe do caminho do elemento para dados de relatório XML &#40;SSRS&#41;](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md).  
  
 É possível criar uma fonte de dados XML para os seguintes tipos de dados XML:  
  
-   Documentos Xml apontados por uma URL que usa protocolo http  
  
-   Pontos de extremidade do serviço Web que retornam dados XML  
  
-   Dados XML inseridos  
  
 Como especificar uma **Query** XML ou um caminho de elemento no tipo de dados XML.  
  
 Para um documento XML, a **Query** XML é opcional. Se ela for incluída, poderá conter um **ElementPath**XML opcional. O valor do **ElementPath** XML usa a sintaxe de caminho de elemento. A **Query** XML e o **ElementPath** XML são incluídos para processar namespaces corretamente quando exigidos pelos dados XML da fonte de dados.  
  
 Para um ponto de extremidade de serviço Web apontado por uma URL de cadeia de conexão, a **Query** XML define o método de serviço Web, a ação SOAP ou ambos. O provedor de dados XML cria uma solicitação de serviço Web que recupera dados XML a serem usados no relatório.  
  
> [!NOTE]  
>  Quando um namespace de serviço Web inclui um caractere de barra (**/)** , inclua o método de serviço Web e a ação SOAP de modo que a extensão de processamento de dados XML possa derivar o namespace corretamente.  
  
 Para um documento XML inserido, a **Query** XML define os dados XML inseridos a serem usados, inclui espaços para nome opcionais e contém um **ElementPath**XML opcional.  
  
## <a name="specifying-query-parameters-for-xml-data"></a>Especificando parâmetros de consulta para dados XML  
 É possível especificar parâmetros de consulta para documentos XML.  
  
-   Para solicitações de URL, os parâmetros de consulta são incluídos como parâmetros de URL padrão.  
  
-   Para solicitações de serviço Web, os parâmetros de consulta são passados para o método de serviço Web. Para definir um parâmetro de consulta, use a página **Parâmetros** da caixa de diálogo **Propriedades do Conjunto de Dados** . Para obter mais informações, consulte [Caixa de Diálogo Propriedades de Conjunto de Dados, Parâmetros](../../reporting-services/report-data/dataset-properties-dialog-box-parameters.md).  
  
### <a name="example"></a>Exemplo  
 Os exemplos na seguinte tabela ilustram como recuperar dados do serviço Web Servidor de Relatórios, de um documento XML e de dados XML inseridos.  
  
|Fonte de dados XML|Exemplo de consulta|  
|---------------------|-------------------|  
|Dados XML de serviço da Web <xref:ReportService2010.ReportingService2010.ListChildren%2A> método.|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="http://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|Dados XML de serviço Web do SoapAction.|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>http://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|Documento XML ou dados XML inseridos que usam namespaces.<br /><br /> Elemento de consulta que especifica namespaces para um caminho de elemento.|`<Query xmlns:es="http://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML inserido.|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML que usa padrão.|*Nenhuma consulta*.<br /><br /> O caminho de elemento deriva do próprio documento XML e independe do namespace.|  
  
> [!NOTE]  
>  O primeiro exemplo de serviço Web lista o conteúdo do servidor de relatório que usa o método <xref:ReportService2006.ReportingService2006.ListChildren%2A>. Para executar essa consulta, você deve criar uma nova fonte de dados e definir a cadeia de caracteres de conexão `http://localhost/reportserver/reportservice2006.asmx`. O <xref:ReportService2006.ReportingService2006.ListChildren%2A> método aceita dois parâmetros: **Item** e **recursiva**. Defina o valor padrão de **Item** para **/** e **Recursive** para **1**.  
  
## <a name="specifying-namespaces"></a>Especificando namespaces  
 Use o elemento **Query** XML para especificar os namespaces usados nos dados XML da fonte de dados. A seguinte consulta XML usa o namespace **sales**. Os nós XML **ElementPath** para `sales:LineItems` e `sales:LineItem` usam o namespace **sales**.  
  
```  
<Query xmlns:sales=  
"http://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      http://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 Para especificar o namespace do provedor de dados para que o namespace padrão permaneça vazio, use **xmldp**. Isso é mostrado no exemplo a seguir.  
  
### <a name="example"></a>Exemplo  
 Os seguintes exemplos usam o documento XML DPNamespace.xml, fornecido para ilustração após a tabela. Essa tabela mostra dois exemplos de sintaxe de ElementPath XML que inclui prefixos de namespace.  
  
|Elemento de consulta XML|Campos resultantes no conjunto de dados|  
|-----------------------|-------------------------------------|  
|\<Consulta / >|Valor r:`http://schemas.microsoft.com/...`<br /><br /> Valor b:`http://schemas.microsoft.com/...`<br /><br /> Valor c:`http://schemas.microsoft.com/...`|  
|`<xmldp:Query xmlns:xmldp="http://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="http://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Valor D<br /><br /> Valor E<br /><br /> Valor F|  
  
#### <a name="xml-document-dpnamespacexml"></a>Documento XML: DPNamespace.xml  
 É possível copiar esse XML e salvá-lo em uma URL disponível do Designer de Relatórios a ser usado como uma fonte de dados XML: por exemplo, http://localhost/DPNamespace.xml.  
  
```  
<Root xmlns:ns="http://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de conexão XML &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
