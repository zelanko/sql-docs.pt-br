---
title: Sintaxe de Consulta XML para dados de relatório XML | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dd1bccb6bff8f19e9abb779310033f4685b31f67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081352"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>Sintaxe de consulta XML para dados de relatório XML (SSRS)
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é possível criar conjuntos de dados para fontes de dados XML. Após definir uma fonte de dados, crie uma consulta para o conjunto de dados. Dependendo do tipo de dados XML apontado pela fonte de dados, a consulta do conjunto de dados é criada incluindo uma **Query** XML ou um caminho de elemento. Uma **Consulta** XML é iniciada com uma marcação **\<Query>** e inclui namespaces e elementos XML que variam de acordo com a fonte de dados. Um caminho de elemento não depende do namespace e especifica quais nós e atributos de nós devem ser usados nos dados XML subjacentes com uma sintaxe do tipo XPath. Para obter mais informações sobre os caminhos de elemento, consulte [Sintaxe do caminho de elemento para dados de relatório XML &#40;SSRS&#41;](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md).  
  
 É possível criar uma fonte de dados XML para os seguintes tipos de dados XML:  
  
-   Documentos Xml apontados por uma URL que usa protocolo http  
  
-   Pontos de extremidade do serviço Web que retornam dados XML  
  
-   Dados XML inseridos  
  
 Como especificar uma **Query** XML ou um caminho de elemento no tipo de dados XML.  
  
 Para um documento XML, a **Query** XML é opcional. Se ela for incluída, poderá conter um **ElementPath**XML opcional. O valor do **ElementPath** XML usa a sintaxe de caminho de elemento. A **Query** XML e o **ElementPath** XML são incluídos para processar namespaces corretamente quando exigidos pelos dados XML da fonte de dados.  
  
 Para um ponto de extremidade de serviço Web apontado por uma URL de cadeia de conexão, a **Query** XML define o método de serviço Web, a ação SOAP ou ambos. O provedor de dados XML cria uma solicitação de serviço Web que recupera dados XML a serem usados no relatório.  
  
> [!NOTE]  
>  Quando um namespace de serviço Web inclui um caractere de barra ( **/)** , inclua o método de serviço Web e a ação SOAP de modo que a extensão de processamento de dados XML possa derivar o namespace corretamente.  
  
 Para um documento XML inserido, a **Query** XML define os dados XML inseridos a serem usados, inclui espaços para nome opcionais e contém um **ElementPath**XML opcional.  
  
## <a name="specifying-query-parameters-for-xml-data"></a>Especificando parâmetros de consulta para dados XML  
 É possível especificar parâmetros de consulta para documentos XML.  
  
-   Para solicitações de URL, os parâmetros de consulta são incluídos como parâmetros de URL padrão.  
  
-   Para solicitações de serviço Web, os parâmetros de consulta são passados para o método de serviço Web. Para definir um parâmetro de consulta, use a página **Parâmetros** da caixa de diálogo **Propriedades do Conjunto de Dados** . 
  
### <a name="example"></a>Exemplo  
 Os exemplos na seguinte tabela ilustram como recuperar dados do serviço Web Servidor de Relatórios, de um documento XML e de dados XML inseridos.  
  
|Fonte de dados XML|Exemplo de consulta|  
|---------------------|-------------------|  
|Dados XML de serviço Web do método <xref:ReportService2010.ReportingService2010.ListChildren%2A> .|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="https://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|Dados XML de serviço Web do SoapAction.|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>https://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|Documento XML ou dados XML inseridos que usam namespaces.<br /><br /> Elemento de consulta que especifica namespaces para um caminho de elemento.|`<Query xmlns:es="https://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML inserido.|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML que usa padrão.|*Nenhuma consulta*.<br /><br /> O caminho de elemento deriva do próprio documento XML e independe do namespace.|  
  
> [!NOTE]  
>  O primeiro exemplo de serviço Web lista o conteúdo do servidor de relatório que usa o método <xref:ReportService2006.ReportingService2006.ListChildren%2A> . Para executar essa consulta, é necessário criar uma nova fonte de dados e definir a cadeia de conexão como `https://localhost/reportserver/reportservice2006.asmx`. O método <xref:ReportService2006.ReportingService2006.ListChildren%2A> usa dois parâmetros: **Item** e **Recursivo**. Defina o valor padrão de **Item** para **/** e **Recursive** para **1**.  
  
## <a name="specifying-namespaces"></a>Especificando namespaces  
 Use o elemento **Query** XML para especificar os namespaces usados nos dados XML da fonte de dados. A seguinte consulta XML usa o namespace **sales**. Os nós XML **ElementPath** para `sales:LineItems` e `sales:LineItem` usam o namespace **sales**.  
  
```  
<Query xmlns:sales=  
"https://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      https://schemas.microsoft.com/SalesWebService/ListOrders   
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
|\<Query/>|Valor A: `https://schemas.microsoft.com/...`<br /><br /> Valor B: `https://schemas.microsoft.com/...`<br /><br /> Valor C: `https://schemas.microsoft.com/...`|  
|`<xmldp:Query xmlns:xmldp="https://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="https://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Valor D<br /><br /> Valor E<br /><br /> Valor F|  
  
#### <a name="xml-document-dpnamespacexml"></a>Documento XML: DPNamespace.xml  
 É possível copiar esse XML e salvá-lo em uma URL disponível do Designer de Relatórios a ser usado como uma fonte de dados XML: por exemplo, https://localhost/DPNamespace.xml.  
  
```  
<Root xmlns:ns="https://schemas.microsoft.com/...">  
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
  
## <a name="see-also"></a>Consulte Também  
 [Tipo de conexão XML &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
