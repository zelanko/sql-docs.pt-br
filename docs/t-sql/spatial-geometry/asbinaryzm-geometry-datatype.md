---
title: "AsBinaryZM (DataType Geométrico) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
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
helpviewer_keywords: AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0c250cae7bce041e858b71b21f0f0a140560604
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM (DataType geométrico)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna a representação do Open Geospatial Consortium (OGC) Well-Known Binary (WKB) de um **geometria** instância aumentada com qualquer **Z** (elevação) e **M** (medida) valores transportados pela instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **varbinary (max)**  
  
 Tipo de retorno CLR: **SqlBytes**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
  
```sql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

