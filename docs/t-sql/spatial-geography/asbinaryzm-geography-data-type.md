---
title: AsBinaryZM (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c617d4303593588b6e86a5b9b7662a5ec690c577
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67948071"
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
  
## <a name="remarks"></a>Comentários  
  
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
  
  
