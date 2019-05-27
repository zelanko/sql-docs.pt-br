---
title: ConvexHullAggregate (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ConvexHullAggregate method (geometry)
ms.assetid: ca3d3b55-e02d-4599-8817-a54f5e047db8
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7eba3aaddb88e0be74bc1b131a3e554ee3c5d225
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938222"
---
# <a name="convexhullaggregate-geometry-data-type"></a>ConvexHullAggregate (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Retorna uma envoltória convexa para um determinado conjunto de objetos de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ConvexHullAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_operand*  
 É uma coluna de tabela do tipo **geometry** que representa um conjunto de objetos de geometria.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
## <a name="exception"></a>Exceção  
 Gera uma `FormatException` quando há valores de entrada que não são válidos. Confira [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 O método retornará **nulo** quando a entrada estiver vazia ou tiver SRIDs diferentes. Confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 O método ignora entradas **nulas**.  
  
> [!NOTE]  
>  O método retornará **nulo** se todos os valores inseridos forem **nulos**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma forma convexa do conjunto de objetos geometry em uma coluna de variável de tabela.  
  
 ```
 -- Setup table variable for ConvexHullAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform ConvexHullAggregate on @Geom.shape column  
 SELECT geometry::ConvexHullAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

