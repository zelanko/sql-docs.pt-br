---
title: Método Discover (XMLA) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 921afc6d17a0eddcba48e5a6a6064810a3b3b6ef
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979098"
---
# <a name="xml-elements---methods---discover"></a>Elementos XML – métodos – descobrir
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Recupera informações, como a lista de bancos de dados disponíveis ou detalhes sobre um objeto específico, de uma instância do Analysis Services. Os dados recuperados com o método **Discover** dependem dos valores dos parâmetros configurados.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
 **SOAP Action** "urn:schemas-microsoft-com:xml-analysis:Discover"  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Discover>  
   <RequestType>...</RequestType>  
   <Restrictions>...</Restrictions>  
   <Properties>...</Properties>  
</Discover>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|Nenhum|  
|Elementos filho|[As propriedades](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md), [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md), [restrições](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **Discover** método solicita metadados sobre instâncias e objetos. Metadados são retornados usando o XMLA [conjunto de linhas](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) tipo de dados.  
 
> [!TIP] 
> Se você estiver familiarizado com os comandos XML, clique no modelo de consulta XMLA na **consulta** barra de ferramentas no Management Studio, para criar a consulta e adicionar parâmetros. Para obter mais informações, consulte [Usar modelos do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md). 
  
## <a name="example"></a>Exemplo  
 No exemplo de código a seguir, o cliente envia o **Discover** chamada para solicitar uma lista de cubos das [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] banco de dados de exemplo do Analysis Services:  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>MDSCHEMA_CUBES</RequestType>  
   <Restrictions>  
      <RestrictionList>  
         <CATALOG_NAME>Adventure Works DW Multidimensional 2012</CATALOG_NAME>  
      </RestrictionList>  
   </Restrictions>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Tabular</Format>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="see-also"></a>Confira também
 [Tipos de dados XML &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Executar o método &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Métodos &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Conjuntos de linhas de esquema do Analysis Services](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
