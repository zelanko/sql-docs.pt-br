---
title: Tipo de elemento (MiningStructureColumn) (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe90c1b870129df1e03d7fc36270463334508069
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-miningstructurecolumn-assl"></a>Elemento Type (MiningStructureColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém o tipo do [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) elemento.  
  
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
|*Longo*|Um inteiro de 64 bytes com sinal. Esse tipo de dados mapeado para o **Int64** no tipo de dados a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] de tipo do .NET Framework e os dados DBTYPE_I8 no OLE DB.|  
|*Boolean*|Um valor booliano. Esse tipo de dados mapeado para o **booliano** tipo de dados no .NET Framework e o tipo de dados DBTYPE_BOOL no OLE DB.|  
|*Texto*|Um fluxo com terminação nula de caracteres Unicode. Esse tipo de dados mapeado para o **cadeia de caracteres** tipo de dados no .NET Framework e o tipo de dados DBTYPE_WSTR no OLE DB.|  
|*Double*|Um número de ponto flutuante de precisão dupla dentro do intervalo de -1.79E +308 a 1.79E +308. Esse tipo de dados mapeado para o **duplo** tipo de dados no .NET Framework e o tipo de dados DBTYPE_R8 no OLE DB.|  
|*Data*|Dados de data, armazenados como um número de ponto flutuante de precisão dupla. A parte inteira é o número de dias desde 30 de dezembro de 1899, enquanto a parte fracionária é uma fração de um dia. Esse tipo de dados mapeado para o **DateTime** tipo de dados no .NET Framework e o tipo de dados DBTYPE_DATE no OLE DB.|  
|*Table*|Uma tabela aninhada. Este tipo de dados mapeia para o tipo de dados DBTYPE_HCHAPTER em OLE DB.<br /><br /> Observação: As colunas de tabela no .NET Framework não tem um tipo de dados intrínseco equivalente, mas são suportadas pelo **DataReader** classe.|  
  
 A enumeração que corresponde aos valores permitidos para **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>.  
  
 O elemento que corresponde ao pai do **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
