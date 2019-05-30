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
manager: craigg
ms.openlocfilehash: c15802d4cf60f507b02733d9b85684576c38774f
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937543"
---
# <a name="m-geometry-data-type"></a>M (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O valor **M** (medida) da instância de **geometry**. As semânticas do valor de medida são definidas pelo usuário.  

## <a name="syntax"></a>Sintaxe  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 O valor dessa propriedade será nulo se a instância de **geometry** não for um **Point**, bem como para qualquer instância de **Point** para a qual ele não foi definido.  
  
 Esta propriedade é somente leitura.  
  
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
  
  

