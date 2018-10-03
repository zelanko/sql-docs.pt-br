---
title: Point (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4de164536b75684d8c019a9f93db4a9b21415650
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759804"
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
  
  
