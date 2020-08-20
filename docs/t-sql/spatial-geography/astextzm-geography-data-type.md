---
description: AsTextZM (tipo de dados geography)
title: AsTextZM (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 49857a94c95240386893854408d2b26cba533815
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479408"
---
# <a name="astextzm-geography-data-type"></a>AsTextZM (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de **geography**, aumentada com os valores de **Z** (elevação) e de **M** (medida) presentes na instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsTextZM ()  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de retorno do CLR: **SqlChars**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Point` que contém valores de **Z** (elevação) e **M** (medida). `STAsText()` seleciona os valores de WKT, (-122.34900 47.65100); `AsTextZM()` seleciona os mesmos valores de WKT e também retorna os valores de **Z** e **M**, resultando em (-122.34900 47.65100 10.3 12).  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;Tipo de dados geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;Tipo de dados de geografia&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
