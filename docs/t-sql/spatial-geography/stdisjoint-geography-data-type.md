---
title: STDisjoint (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDisjoint (geography Data Type)
- STDisjoint_TSQL
dev_langs: TSQL
helpviewer_keywords: STDisjoint
ms.assetid: 98328a02-e018-47d6-aa93-de162b8aef62
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a81d42abbc9a15068e1d58d5bb7222defbfc8042
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="stdisjoint-geography-data-type"></a>STDisjoint (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retornará 1 se uma **geografia** instância está espacialmente separada de outra **geografia** instância. Retornará 0 se não estiver.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STDisjoint ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância a ser comparada com a instância na qual STDisjoint() é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Dois **geografia** instâncias são não contíguas se a interseção de seus conjuntos de pontos estiver vazia.  
  
 Esse método sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geografia** instâncias não coincidem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STDisjoint()` para testar duas instâncias `geography` a fim de confirmar se elas estão espacialmente separadas.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
