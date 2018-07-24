---
title: AsBinaryZM (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AsBinaryZM
- AsBinaryZM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM, geography
- AsBinaryZM
ms.assetid: 37246adb-814d-4113-9983-4d336de8182c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d5666547134235dec0cec2ec104c5123946f0a13
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37986233"
---
# <a name="asbinaryzm-geography-data-type"></a>AsBinaryZM (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de **geometry** aumentada com os valores de **Z** (elevação) e **M** (medida) presentes na instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **varbinary(max)**  
  
 Tipo de retorno do CLR: **SqlBytes**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
  
```sql  
DECLARE @g1 GEOGRAPHY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;Tipo de dados geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;Tipo de dados de geografia&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
