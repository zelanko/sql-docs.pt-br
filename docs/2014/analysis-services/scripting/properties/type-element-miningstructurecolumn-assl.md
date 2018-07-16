---
title: Tipo de elemento (MiningStructureColumn) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (MiningStructureColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ce9327fb28e9f452e643ded604f2a8dd72a084
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304236"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Elemento Type (MiningStructureColumn) (ASSL)
  Contém o tipo dos [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Long*|Um inteiro de 64 bytes com sinal. Este tipo de dados mapeia para o tipo de dados `Int64` em .NET Framework do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e o tipo de dados DBTYPE_I8 em OLE DB.|  
|*Boolean*|Um valor booliano. Este tipo de dados mapeia para o tipo de dados `Boolean` no .NET Framework e o tipo de dados DBTYPE_BOOL no OLE DB.|  
|*Texto*|Um fluxo com terminação nula de caracteres Unicode. Este tipo de dados mapeia para o tipo de dados `String` no .NET Framework e o tipo de dados DBTYPE_WSTR no OLE DB.|  
|*Dupla*|Um número de ponto flutuante de precisão dupla dentro do intervalo de -1.79E +308 a 1.79E +308. Este tipo de dados mapeia para o tipo de dados `Double` no .NET Framework e o tipo de dados DBTYPE_R8 no OLE DB.|  
|*Data*|Dados de data, armazenados como um número de ponto flutuante de precisão dupla. A parte inteira é o número de dias desde 30 de dezembro de 1899, enquanto a parte fracionária é uma fração de um dia. Este tipo de dados mapeia para o tipo de dados `DateTime` no .NET Framework e o tipo de dados DBTYPE_DATE no OLE DB.|  
|*Table*|Uma tabela aninhada. Este tipo de dados mapeia para o tipo de dados DBTYPE_HCHAPTER em OLE DB. **Observação:** colunas da tabela no .NET Framework não tem um tipo de dados intrínseco equivalente, mas em vez disso, são compatíveis com o `DataReader` classe.|  
  
 A enumeração que corresponde aos valores permitidos para `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>.  
  
 O elemento que corresponde ao pai de `Type` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.MiningStructureColumn>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
