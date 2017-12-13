---
title: Tipo de elemento (MiningStructureColumn) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Type Element (MiningStructureColumn)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TYPE
helpviewer_keywords: Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15c18862d04cd5e50bd80238fcb3d649a3d835cd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="type-element-miningstructurecolumn-assl"></a>Elemento Type (MiningStructureColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o tipo do [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Longas*|Um inteiro de 64 bytes com sinal. Esse tipo de dados mapeado para o **Int64** no tipo de dados a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] de tipo do .NET Framework e os dados DBTYPE_I8 no OLE DB.|  
|*Boolean*|Um valor booliano. Esse tipo de dados mapeado para o **booliano** tipo de dados no .NET Framework e o tipo de dados DBTYPE_BOOL no OLE DB.|  
|*Texto*|Um fluxo com terminação nula de caracteres Unicode. Esse tipo de dados mapeado para o **cadeia de caracteres** tipo de dados no .NET Framework e o tipo de dados DBTYPE_WSTR no OLE DB.|  
|*Duplo*|Um número de ponto flutuante de precisão dupla dentro do intervalo de -1.79E +308 a 1.79E +308. Esse tipo de dados mapeado para o **duplo** tipo de dados no .NET Framework e o tipo de dados DBTYPE_R8 no OLE DB.|  
|*Data*|Dados de data, armazenados como um número de ponto flutuante de precisão dupla. A parte inteira é o número de dias desde 30 de dezembro de 1899, enquanto a parte fracionária é uma fração de um dia. Esse tipo de dados mapeado para o **DateTime** tipo de dados no .NET Framework e o tipo de dados DBTYPE_DATE no OLE DB.|  
|*Table*|Uma tabela aninhada. Este tipo de dados mapeia para o tipo de dados DBTYPE_HCHAPTER em OLE DB.<br /><br /> Observação: As colunas de tabela no .NET Framework não tem um tipo de dados intrínseco equivalente, mas são suportadas pelo **DataReader** classe.|  
  
 A enumeração que corresponde aos valores permitidos para **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>.  
  
 O elemento que corresponde ao pai do **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
