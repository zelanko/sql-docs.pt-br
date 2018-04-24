---
title: Point (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Point
- Point_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Point method
- Point (geography Data Type)
ms.assetid: 0dc6f422-7aae-4016-b7f4-3289fa8f989c
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ee7a291dbfc359e15d010484fd4c33dcf645adf0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="point-geography-data-type"></a>Point (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Constrói uma instância de **geography** que representa uma instância de **Point** de seus valores de latitude e de longitude e uma SRID (ID de referência espacial).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Point ( Lat, Long, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Lat*  
 É uma expressão **float** que representa a coordenada X do **Point** que está sendo gerado.  
  
 *Long*  
 É uma expressão **float** que representa a coordenada Y do **Point** gerado. Para obter mais informações sobre os valores válidos de longitude e latitude, confira [Point](../../relational-databases/spatial/point.md).  
  
 *SRID*  
 É uma expressão **int** que representa a SRID da instância de **geography** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
> [!NOTE]  
>  Argumentos para o método Point (tipo de dados geography) têm coordenadas em ordem inversa se comparados a WKT.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Point()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Point(47.65100, -122.34900, 4326)  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
