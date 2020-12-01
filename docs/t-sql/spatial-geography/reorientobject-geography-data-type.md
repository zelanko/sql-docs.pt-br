---
description: ReorientObject (tipo de dados geography)
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
ms.openlocfilehash: 9d4f8bf9f9b8409f9ab46af0b1fd0a728e80e505
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88417022"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (tipo de dados geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geography** com regiões interiores e exteriores intercambiadas.  
  
Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
.ReorientObject (geography)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
_geografia_  
É outra instância de **geography** na qual `ReorientObject()` é invocado.  
  
## <a name="return-value"></a>Valor Retornado  
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
  
