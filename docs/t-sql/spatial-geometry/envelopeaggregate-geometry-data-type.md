---
title: EnvelopeAggregate (tipo de dados geometry) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geometry)
ms.assetid: c4c15abe-0fe9-441d-9d42-6572e264869c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16c46ec5f18dde104a66d4fcf405f81ce59b2d6f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="envelopeaggregate-geometry-data-type"></a>EnvelopeAggregate (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma caixa delimitadora para um determinado conjunto de **geometria** objetos.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_operand*  
 É um **geometria** coluna de tipo de tabela que representa o conjunto de **geometria** objetos.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
## <a name="exceptions"></a>Exceções  
 Gera uma `FormatException` quando há valores de entrada que não são válidos. Consulte [STIsValid &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 Método retornará **nulo** quando a entrada estiver vazia ou tiver SRIDs diferentes. Consulte [Spatial Reference Identifiers &#40; SRIDs &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Método ignora **nulo** entradas.  
  
> [!NOTE]  
>  Método retornará **nulo** se todos os valores inseridos forem **nulo**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma caixa delimitadora para um conjunto de objetos em uma coluna de variável de tabela.  
  
 ```
 -- Setup table variable for EnvelopeAggregate example 
DECLARE @Geom TABLE 
( 
shape geometry, 
shapeType nvarchar(50) 
) 
INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'), 
('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle'); 
-- Perform EnvelopeAggregate on @Geom.shape column 
SELECT geometry::EnvelopeAggregate(shape).ToString() 
FROM @Geom;
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

