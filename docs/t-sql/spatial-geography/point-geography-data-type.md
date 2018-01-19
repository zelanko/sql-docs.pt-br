---
title: Point (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
- Point
- Point_TSQL
dev_langs: TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1a5a32fd3b25d4e68c07a69e0945335ca9d712b9
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="point-geography-data-type"></a>Point (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Constrói um **geografia** instância representando um **ponto** instância de seus valores de latitude e longitude e um SRID (ID) de referência espacial.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Lat*  
 É um **float** expressão que representa a coordenada x do **ponto** que está sendo gerado.  
  
 *Longo*  
 É um **float** expressão que representa a coordenada y do **ponto** que está sendo gerado. Para obter mais informações sobre valores de longitude e latitude válido, consulte [ponto](../../relational-databases/spatial/point.md).  
  
 *SRID*  
 É um **int** expressão que representa a SRID do **geografia** instância que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
> [!NOTE]  
>  Argumentos para o método Point (tipo de dados geography) têm coordenadas em ordem inversa se comparados a WKT.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Point()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
