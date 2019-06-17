---
title: Tipos de dados no Analysis Services | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62725380"
---
# <a name="data-types-in-analysis-services"></a>Tipos de dados no Analysis Services
  Para todos os <xref:Microsoft.AnalysisServices.DataItem> objetos, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte ao seguinte subconjunto de `System.Data.OleDb.OleDbType`. Para definir ou ler o tipo de dados, use [tipos de dados DataItem &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl).  
  
## <a name="supported-data-types"></a>Tipos de dados com suporte  
  
|||  
|-|-|  
|BigInt|Um inteiro de 64 bytes com sinal. O *BigInt* tipo de valor representa inteiros com valores que variam de 9.223.372.036.854.775.808 negativo a 9.223.372.036.854.775.807 positivo.|  
|Binary|Um fluxo de dados binários da **bytes** tipo. **Bytes** é um tipo de valor que representa inteiros sem sinal com valores que variam de 0 a 255.|  
|Booliano|Instâncias desse tipo têm valores de `true` ou `false`.|  
|Currency|Um *moeda* valor variando de -922.337.203.685.477,5808 a + 922.337.203.685.477,5807 com precisão de dez milésimos de uma unidade de moeda (quatro casas decimais).|  
|Date|Dados de data e hora armazenados como um duplo. A parte inteira é o número de dias desde 30 de dezembro de 1899 e a parte fracionária é uma fração de um dia ou hora do dia.|  
|Double|Um número de ponto flutuante dentro do intervalo de -1,79769313486232E +308 a 1,79769313486232E +308. Um valor Double armazena informações numéricas com até 15 dígitos decimais de precisão.|  
|Integer|Um número inteiro com sinal de 32 bits que representa números inteiros com valores que variam de 2.147.483.648 negativo a 2.147.483.647 positivo.|  
|Single|Um número de ponto flutuante dentro do intervalo de - 3,4028235E +38 a 3,4028235E +38. Um valor Single armazena informações numéricas com até sete dígitos decimais de precisão.|  
|Smallint|Um inteiro com sinal de 16 bits. O *Smallint* tipo de valor representa inteiros com sinal com valores que variam de 32768 negativo a 32767 positivo.|  
|Tinyint|Um inteiro com sinal de 8 bits. O tipo de valor Tinyint representa inteiros com valores que variam de 128 negativo a 127 positivo.|  
|UnsignedBigInt|Um inteiro não assinado de 64 bits. O *UnsignedBigInt* tipo de valor representa inteiros sem sinal com valores que variam de 0 a 18.446.744.073.709.551.615.|  
|UnsignedInt|Um inteiro não assinado de 32 bits. O *UnsignedInt* tipo de valor representa inteiros sem sinal com valores que variam de 0 a 4.294.967.295.|  
|UnsignedSmallInt|Um inteiro sem sinal de 16 bits. O *UnsignedSmallInt* tipo de valor representa inteiros sem sinal com valores que variam de 0 a 65535.|  
|UnsignedTinyInt|Um inteiro sem sinal de 8 bits. O *UnsignedTinyInt* tipo de valor representa inteiros sem sinal com valores que variam de 0 a 255|  
|WChar|Um fluxo com terminação nula de caracteres Unicode. Um *WChar* é uma coleção sequencial de caracteres Unicode que é usada para representar texto.|  
  
## <a name="amo-validations-on-data-types"></a>Validações de AMO em tipos de dados  
 A tabela a seguir lista as validações extras que o AMO (Objetos de Gerenciamento de Análise) faz para determinadas associações:  
  
|Object|Associação|Tipos de dados permitidos|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Todos menos Binary|  
||NameColumn|Apenas WChar|  
||SkippedLevelsColumn|Somente tipos de inteiros: BigInt, Integer, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
||CustomRollupColumn|Apenas WChar|  
||CustomRollupPropertiesColumn|Apenas WChar|  
||UnaryOperatorColumn|Apenas WChar|  
||ValueColumn|Todos|  
|AttributeTranslation|CaptionColumn|Apenas WChar|  
|ScalarMiningStructureColumn|KeyColumns|Todos menos Binary|  
||NameColumn|Apenas WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|Todos menos Binary|  
|MeasureGroupAttribute|KeyColumns|Todos menos Binary|  
|Medidas de contagens distintas|`Source`|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  
