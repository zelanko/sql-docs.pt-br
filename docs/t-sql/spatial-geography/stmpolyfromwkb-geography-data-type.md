---
title: STMPolyFromWKB (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPolyFromWKB (geography Data Type)
- STMPolyFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromWKB method
ms.assetid: c4d0e649-0abb-4343-a3f0-3a702c8bbbdb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: bb3ad4cf2da399c32af4ccdcb183ebebc393dbe5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120942"
---
# <a name="stmpolyfromwkb-geography-data-type"></a>STMPolyFromWKB (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma instância de **geographyMultiPolygon** de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STMPolyFromWKB ( 'WKB_multipolygon' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_multipolygon*  
 É a representação WKB da instância de **geographyMultiPolygon** que você deseja retornar. *WKB_multipolygon* é uma expressão **varbinary(max)** .  
  
 *SRID*  
 É uma expressão **int** que representa a SRID (ID de referência espacial) da instância de **geographyMultiPolygon** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
 Tipo OGC: **MultiPolygon**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STMPolyFromWKB()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STMPolyFromWKB(0x01060000000200000001030000000100000004000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D34740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D3474001030000000100000004000000E7FBA9F1D2955EC08716D9CEF7D34740E7FBA9F1D2955EC0F853E3A59BD447405839B4C876965EC0F853E3A59BD44740E7FBA9F1D2955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OGC Static Geography Methods](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
