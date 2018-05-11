---
title: Método Discover (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4bc359e24664f97db41acd87914194731c37e325
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---methods---discover"></a>Elementos XML - métodos - descobrir
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
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
 [Tipos de dados XML & #40; XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Método Execute &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Métodos &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [Elementos XML & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Conjuntos de linhas do esquema do Analysis Services](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
