---
title: STLength (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength_TSQL
- STLength (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STLength (geometry Data Type)
ms.assetid: e34dc620-2a65-4248-b099-fff91830ab98
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2b42f879a238e1c1e9a44c92c8683a91c9021600
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030861"
---
# <a name="stlength-geometry-data-type"></a>STLength (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o comprimento total dos elementos em uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Se uma instância de **geometry** for fechada, seu comprimento será calculado como o comprimento total ao redor da instância. O comprimento de qualquer polígono é seu perímetro e o comprimento de um ponto é 0. O comprimento de qualquer tipo de **geometrycollection** é a soma dos comprimentos de suas instâncias de **geometry** independentes.  
  
 STLength () funciona em LineStrings válidos e inválidos. Em geral, um LineString é inválido devido aos segmentos sobrepostos, que podem ser causados por anomalias como rastreamentos de GPS imprecisos. STLength () não remove segmentos sobrepostos ou inválidos. Ele inclui segmentos sobrepostos e inválidos no valor de comprimento que ele retorna. O método MakeValid () pode remover segmentos sobrepostos de um LineString.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STLength()` para encontrar o comprimento da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

