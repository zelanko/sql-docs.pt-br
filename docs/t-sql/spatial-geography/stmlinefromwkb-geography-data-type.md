---
title: STMLineFromWKB (tipo de dados geography) | Microsoft Docs
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
- STMLineFromWKB_TSQL
- STMLineFromWKB (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: STMLineFromWKB method
ms.assetid: 05ca6d65-4799-4b9a-9672-cfebae95f23e
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd984f8dee29059c1b99545c94db3e7a04879d0e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stmlinefromwkb-geography-data-type"></a>STMLineFromWKB (Tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um **geographyMultiLineString** instância de uma representação do Open Geospatial Consortium (OGC) Well-Known Binary (WKB).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STMLineFromWKB ( 'WKB_multilinestring' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *WKB_multilinestring*  
 É a representação WKB do **geographyMultiLineString** instância a ser retornada. *WKB_multilinestring* é um **varbinary (max)** expressão.  
  
 *SRID*  
 É um **int** SRID (ID) de fazer referência a expressão que representa o espaciais a **geographyMultiLineString** instância que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
 Tipo OGC: **MultiLineString**  
  
## <a name="remarks"></a>Remarks  
 Este método lança um **FormatException** se a entrada não for bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STMLineFromWKB()` para criar um `geography`instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STMLineFromWKB(0x010500000002000000010200000005000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D3474083C0CAA145965EC04E62105839D44740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D34740010200000005000000022B8716D9965EC0C1CAA145B6D34740022B8716D9965EC06ABC749318D447407593180456965EC06ABC749318D447407593180456965EC03333333333D34740022B8716D9965EC0C1CAA145B6D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [OGC Static Geography Methods](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
