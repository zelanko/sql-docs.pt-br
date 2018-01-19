---
title: STWithin (tipo de dados geography) | Microsoft Docs
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
dev_langs: TSQL
helpviewer_keywords: STWithin method (geography)
ms.assetid: 6fc745cc-7976-418a-a89a-c267e64ab3a2
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2fe7e1e315b9465b5df0814dbda78c75ef279e12
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="stwithin-geography-data-type"></a>STWithin (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retornará 1 se uma **geografia** instância está espacialmente dentro de outra **geografia** instância; caso contrário, retornará 0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STWithin ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância a ser comparada com a instância na qual `STWithin()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Esse método sempre retornará nulo se as IDs de referência espaciais (SRIDs) da **geografia** instâncias não coincidem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STWithin()` para testar duas instâncias  `geography` para verificar se a primeira instância está completamente dentro da segunda.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STWithin(@h);  
```  
  
  
