---
title: STLength (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f5b7a075d562731f986c0f85db505c81315acbd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stlength-geography-data-type"></a>STLength (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna o comprimento total dos elementos em uma instância de **geography** ou nas instâncias de **geografia** em uma **GeometryCollection**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Se uma instância de **geography** for fechada, seu comprimento será calculado como o comprimento total em torno da instância. O comprimento de qualquer polígono é seu perímetro, e o comprimento de um ponto é 0. O comprimento de uma **GeometryCollection** é encontrado calculando a soma dos comprimentos de todas as instâncias de **geografia** contidas dentro da coleção.  
  
 STLength () funciona em LineStrings válidos e inválidos. Em geral, um LineString é inválido devido aos segmentos sobrepostos, que podem ser causados por anomalias como rastreamentos de GPS imprecisos. STLength () não remove segmentos sobrepostos ou inválidos. Ele inclui segmentos sobrepostos e inválidos no valor de comprimento que ele retorna. O método MakeValid () pode remover segmentos sobrepostos de um LineString.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STLength()` para encontrar o comprimento da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
