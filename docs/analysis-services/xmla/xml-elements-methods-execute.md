---
title: Método Execute (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c47a3c1a297bd636c64e52fcb83fda6a2b7bad5
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574928"
---
# <a name="xml-elements---methods---execute"></a>Elementos XML - métodos - executar
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Envia o XML para comandos Analysis (XMLA) para uma instância do Analysis Services. Isso inclui solicitações que envolvem transferência de dados, como a recuperação ou a atualização dos dados no servidor.  
  
 **Namespace** urn:schemas-microsoft-com:xml-analysis  
  
 **Ação SOAP** "urn: schemas-microsoft-com: XML-análise: executar"  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Execute>  
   <Command>...</Command>  
   <Properties>...</Properties>  
   <Parameters>...</Parameters>  
</Execute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|Nenhum|  
|Elementos filho|[Comando](../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md), [parâmetros](../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md), [propriedades](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **Execute** método executa comandos XMLA fornecidos no **comando** elemento e retorna qualquer dado resultante usando o XMLA [linhas](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) tipo de dados (para resultados de tabela Define) ou o XMLA [MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) de tipo de dados (para conjuntos de resultados multidimensional).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir é um exemplo de um **Execute** chamada do método que contém uma instrução SELECT do MDX (Multidimensional Expressions).  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Statement>  
         SELECT [Measures].MEMBERS ON COLUMNS FROM [Adventure Works]  
      </Statement>  
   </Command>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Multidimensional</Format>  
         <AxisFormat>ClusterFormat</AxisFormat>  
      </PropertyList>  
   </Properties>  
</Execute>  
```  
  
## <a name="see-also"></a>Confira também
 [Tipos de dados XML &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Método Discover &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Métodos &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Conjuntos de linhas de esquema do Analysis Services](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
