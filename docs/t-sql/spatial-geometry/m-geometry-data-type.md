---
title: M (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geometry Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b8d0c4dd1b813ce5da8f0272a0c2e19e7beab1c6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555623"
---
# <a name="m-geometry-data-type"></a>M (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  O valor **M** (medida) da instância de **geometry**. As semânticas do valor de medida são definidas pelo usuário.  

## <a name="syntax"></a>Sintaxe  
  
```  
  
.M  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 O valor dessa propriedade será nulo se a instância de **geometry** não for um **Point**, bem como para qualquer instância de **Point** para a qual ele não foi definido.  
  
 Essa propriedade é somente leitura.  
  
 Os valores de **M** não são usados nos cálculos feitos pela biblioteca e não serão usados em nenhum cálculo de biblioteca.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Point` com valores Z (elevação) e M (medida) e usa `M` para buscar o valor M da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

