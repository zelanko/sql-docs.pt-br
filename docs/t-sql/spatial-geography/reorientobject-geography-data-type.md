---
title: ReorientObject (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6865a5246f7bb0afa7dd280041e98fada88c3099
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555170"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geography** com regiões interiores e exteriores intercambiadas.  
  
Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ReorientObject (geography)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
_geografia_  
É outra instância de **geography** na qual `ReorientObject()` é invocado.  
  
## <a name="return-value"></a>Valor retornado  
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
Esse método altera a orientação do anel de todos os **Polygons** em uma **GeometryCollection**, mas não remove nem altera **Points** ou **LineStrings** na coleção especificada.  
  
Se você passar uma **GeometryCollection** para esse método, cada instância na coleção será orientada novamente como resultado, mas a coleção como um todo não será orientada novamente.  
  
## <a name="examples"></a>Exemplos  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>Consulte Também  
[Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
