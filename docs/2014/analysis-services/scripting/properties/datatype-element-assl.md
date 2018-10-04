---
title: Elemento DataType (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataType
helpviewer_keywords:
- DataType element
ms.assetid: efe6f717-8288-4ca2-85ed-9b63d27c02d8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92c3981344d0425c46ef283fa8792de942d6193b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191036"
---
# <a name="datatype-element-assl"></a>Elemento DataType (ASSL)
  Define o tipo de dados do elemento associado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem> <!-- or Measure -->  
   ...  
   <DataType>...</DataType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DataItem](../data-type/dataitem-data-type-assl.md), [medidas](../objects/measure-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 Os valores para `DataType` estão definidos na enumeração `System.Data.OleDb.OleDbType`. Porém, só os valores de enumeração na tabela a seguir são válidos no elemento `DataType`.  
  
|Valor|Description|  
|-----------|-----------------|  
|*BigInt*|Um inteiro de 64 bytes com sinal. Esse tipo de dados é mapeado para o `Int64` tipo de dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] de tipo do .NET Framework e os dados DBTYPE_I8 no OLE DB.|  
|*bool*|Um valor booliano. Este tipo de dados mapeia para o tipo de dados `Boolean` no .NET Framework e o tipo de dados DBTYPE_BOOL no OLE DB.|  
|*moeda*|Um valor de moeda variando de -2<sup>63</sup> (ou -922.337.203.685.477,5808) a 2<sup>63</sup>-1 (ou + 922.337.203.685.477,5807) com uma precisão de dez milésimos de uma unidade monetária. Este tipo de dados mapeia para o tipo de dados `Decimal` no .NET Framework e o tipo de dados DBTYPE_CY no OLE DB.|  
|*Data*|Dados de data, armazenados como um número de ponto flutuante de precisão dupla. A parte inteira é o número de dias desde 30 de dezembro de 1899, enquanto a parte fracionária é uma fração de um dia. Este tipo de dados mapeia para o tipo de dados `DateTime` no .NET Framework e o tipo de dados DBTYPE_DATE no OLE DB.|  
|*Double*|Número de ponto flutuante de precisão dupla dentro do intervalo de - 1,79E 1,79E + 308 + 308. Este tipo de dados mapeia para o tipo de dados `Double` no .NET Framework e o tipo de dados DBTYPE_R8 no OLE DB.|  
|*Integer*|Um inteiro de 32 bytes com sinal. Esse tipo de dados mapeia para o tipo de dados `Int32` no .NET Framework e o tipo de dados DBTYPE_I4 no OLE DB.|  
|*Single*|Número de um ponto flutuante de precisão simples dentro do intervalo de - 3,40E + 38 a 3,40E + 38. Esse tipo de dados mapeia para o tipo de dados `Single` no .NET Framework e o tipo de dados DBTYPE_R4 no OLE DB.|  
|*SmallInt*|Um inteiro com sinal de 16 bits. Esse tipo de dados mapeia para o tipo de dados `Int16` no .NET Framework e o tipo de dados DBTYPE_I2 no OLE DB.|  
|*TinyInt*|Um inteiro com sinal de 8 bits. Esse tipo de dados mapeia para o tipo de dados `SByte` no .NET Framework e o tipo de dados DBTYPE_I1 no OLE DB.|  
|*UnsignedBigInt*|Um inteiro não assinado de 64 bits. Esse tipo de dados mapeia para o tipo de dados `UInt64` no .NET Framework e o tipo de dados DBTYPE_UI8 no OLE DB.|  
|*unsignedInt*|Um inteiro não assinado de 32 bits. Esse tipo de dados mapeia para o tipo de dados `UInt32` no .NET Framework e o tipo de dados DBTYPE_UI4 no OLE DB.|  
|*UnsignedSmallInt*|Um inteiro sem sinal de 16 bits. Esse tipo de dados mapeia para o tipo de dados `UInt16` no .NET Framework e o tipo de dados DBTYPE_UI2 no OLE DB.|  
|*WChar*|Um fluxo com terminação nula de caracteres Unicode. Este tipo de dados mapeia para o tipo de dados `String` no .NET Framework e o tipo de dados DBTYPE_WSTR no OLE DB.|  
|*Herdado*|O tipo de dados a `DataItem` contidos na [código-fonte](source-element-measure-assl.md) elemento do `Measure` elemento. **Observação:** aplicável somente ao `Measure` elementos.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
