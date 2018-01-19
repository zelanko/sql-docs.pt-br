---
title: M (tipo de dados geometry) | Microsoft Docs
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
f1_keywords:
- M (geometry Data Type)
- M_TSQL
dev_langs: TSQL
helpviewer_keywords: M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e1e51e478e2929f5c458568ceaae1966990ef95
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="m-geometry-data-type"></a>M (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O **M** (medida) valor da **geometria** instância. As semânticas do valor de medida são definidas pelo usuário.  

## <a name="syntax"></a>Sintaxe  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 O valor dessa propriedade é null se o **geometria** instância não é um **ponto**, bem como para qualquer **ponto** instância para que ele não está definido.  
  
 Esta propriedade é somente leitura.  
  
 **M** valores não são usados nos cálculos feitos pela biblioteca e não serão executados em qualquer cálculo de biblioteca.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Point` com valores Z (elevação) e M (medida) e usa `M` para buscar o valor M da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

