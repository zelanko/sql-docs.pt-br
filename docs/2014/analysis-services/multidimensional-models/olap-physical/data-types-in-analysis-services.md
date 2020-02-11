---
title: Tipos de dados em Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 910be4f4-3010-41cd-9fdc-f0a79a0ce823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ecdc64918e582f25f0e017d263c66e78c0d1bee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62725380"
---
# <a name="data-types-in-analysis-services"></a>Tipos de dados no Analysis Services
  Para todos <xref:Microsoft.AnalysisServices.DataItem> os objetos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , o oferece suporte ao `System.Data.OleDb.OleDbType`seguinte subconjunto de. Para definir ou ler o tipo de dados, use o [tipo de dados DataItem &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl).  
  
## <a name="supported-data-types"></a>Tipos de dados com suporte  
  
|||  
|-|-|  
|BigInt|Um inteiro de 64 bytes com sinal. O tipo de valor *bigint* representa inteiros com valores variando de 9.223.372.036.854.775.808 negativo para positivo 9.223.372.036.854.775.807.|  
|Binário|Um fluxo de dados binários do tipo de **byte** . **Byte** é um tipo de valor que representa inteiros não assinados com valores que variam de 0 a 255.|  
|Boolean|Instâncias desse tipo têm valores de `true` ou `false`.|  
|Moeda|Um valor de *moeda* que varia de-922337203685477,5808 a + 922337203685477,5807 com precisão de dez milésimos de uma unidade monetária (quatro casas decimais).|  
|Data|Dados de data e hora armazenados como um duplo. A parte inteira é o número de dias desde 30 de dezembro de 1899 e a parte fracionária é uma fração de um dia ou hora do dia.|  
|DOUBLE|Um número de ponto flutuante dentro do intervalo de -1,79769313486232E +308 a 1,79769313486232E +308. Um valor Double armazena informações numéricas com até 15 dígitos decimais de precisão.|  
|Integer|Um número inteiro com sinal de 32 bits que representa números inteiros com valores que variam de 2.147.483.648 negativo a 2.147.483.647 positivo.|  
|Single|Um número de ponto flutuante dentro do intervalo de - 3,4028235E +38 a 3,4028235E +38. Um valor Single armazena informações numéricas com até sete dígitos decimais de precisão.|  
|Smallint|Um inteiro com sinal de 16 bits. O tipo de valor *smallint* representa inteiros assinados com valores que variam de 32768 negativos a 32767 positivos.|  
|Tinyint|Um inteiro com sinal de 8 bits. O tipo de valor Tinyint representa inteiros com valores que variam de 128 negativo a 127 positivo.|  
|UnsignedBigInt|Um inteiro não assinado de 64 bits. O tipo de valor *UnsignedBigInt* representa inteiros não assinados com valores variando de 0 a 18446744073709551615.|  
|UnsignedInt|Um inteiro não assinado de 32 bits. O tipo de valor *unsignedInt* representa inteiros não assinados com valores variando de 0 a 4.294.967.295.|  
|UnsignedSmallInt|Um inteiro sem sinal de 16 bits. O tipo de valor *UnsignedSmallInt* representa inteiros não assinados com valores variando de 0 a 65535.|  
|UnsignedTinyInt|Um inteiro sem sinal de 8 bits. O tipo de valor *UnsignedTinyInt* representa inteiros não assinados com valores que variam de 0 a 255|  
|WChar|Um fluxo com terminação nula de caracteres Unicode. Um *WCHAR* é uma coleção sequencial de caracteres Unicode que é usada para representar texto.|  
  
## <a name="amo-validations-on-data-types"></a>Validações de AMO em tipos de dados  
 A tabela a seguir lista as validações extras que o AMO (Objetos de Gerenciamento de Análise) faz para determinadas associações:  
  
|Objeto|Associação|Tipos de dados permitidos|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Todos menos Binary|  
||NameColumn|Apenas WChar|  
||SkippedLevelsColumn|Apenas os tipos inteiros: BigInt, Inteiro, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
||CustomRollupColumn|Apenas WChar|  
||CustomRollupPropertiesColumn|Apenas WChar|  
||UnaryOperatorColumn|Apenas WChar|  
||ValueColumn|Todos|  
|AttributeTranslation|CaptionColumn|Apenas WChar|  
|ScalarMiningStructureColumn|KeyColumns|Todos menos Binary|  
||NameColumn|Apenas WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|Todos menos Binary|  
|MeasureGroupAttribute|KeyColumns|Todos menos Binary|  
|Medidas de contagens distintas|Fonte|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  
