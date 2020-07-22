---
title: Long (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7c3a5096426aa6fbfa69da1eacab3d0cd80f72ed
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556162"
---
# <a name="long-geography-data-type"></a>Long (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  A propriedade de longitude retorna a instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Long  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-value"></a>Valor retornado  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 No modelo OpenGIS, Long é definido apenas em instâncias de **geography** compostas por um único ponto. Essa propriedade retornará NULL se instâncias de **geography** contiverem mais de um ponto. Essa propriedade é exata e somente leitura.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo cria uma instância de **Point** e recupera a longitude do ponto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
