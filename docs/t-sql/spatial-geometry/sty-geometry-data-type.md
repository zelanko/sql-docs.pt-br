---
title: STY (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STY_TSQL
- STY (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STY (geometry Data Type)
ms.assetid: f72e0eaa-7d1d-4052-88fd-a172d8cb0d71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 05f4ddd6366fbb09b4c5f0c9dd186f415fdc16ea
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066140"
---
# <a name="sty-geometry-data-type"></a>STY (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

A propriedade de coordenada Y de uma instância de **Point**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STY  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 O valor dessa propriedade será nulo se a instância de **geometry** for um ponto. Essa propriedade é somente leitura.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` e usa `STY` para recuperar a coordenada Y da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STY;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STX &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STSrid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

