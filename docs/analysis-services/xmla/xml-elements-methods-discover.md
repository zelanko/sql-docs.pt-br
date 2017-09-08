---
title: "Método Discover (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Discover Method
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60a101afa2953d62e2910b4523a0213e4e786490
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---methods---discover"></a>Elementos XML - métodos - descobrir
  Recupera informações, como a lista de bancos de dados disponíveis ou detalhes sobre um objeto específico, de uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os dados recuperados com o método **Discover** dependem dos valores dos parâmetros configurados.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|Nenhuma|  
|Elementos filho|[Propriedades](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md), [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md), [restrições](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O **Discover** método solicita metadados sobre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instâncias e objetos. Metadados são retornados usando o XMLA [linhas](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) tipo de dados.  
 
> [!TIP] 
> Se você estiver familiarizado com os comandos XML, clique em modelo de consulta XMLA no **consulta** barra de ferramentas no Management Studio, para criar a consulta e adicione os parâmetros. Para obter mais informações, consulte [Usar modelos do Analysis Services no SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md). 
  
## <a name="example"></a>Exemplo  
 No exemplo de código a seguir, o cliente envia o **Discover** chamada para solicitar uma lista de cubos das [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] exemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Executar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Métodos &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Conjuntos de linhas do esquema do Analysis Services](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

