---
title: CollectionAggregate (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba8de4fd1dbdf4d7eee55b12c60da7156f512679
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36245718"
---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate (Tipo de Dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Cria uma instância de **GeometryCollection** de um conjunto de tipos de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_operand*  
 É uma coluna da tabela do tipo **geometria** que representa um conjunto de objetos **geometria** a ser listado na instância de **GeometryCollection**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
## <a name="exceptions"></a>Exceções  
 Gera uma `FormatException` quando há valores de entrada que não são válidos. Confira [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 O método retornará **nulo** quando a entrada estiver vazia ou tiver SRIDs diferentes. Confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 O método ignora entradas **nulas**.  
  
> [!NOTE]  
>  O método retornará **nulo** se todos os valores inseridos forem **nulos**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma instância `GeometryCollection` que contém um `CurvePolygon` e um `Polygon`.  
  
 ```
 -- Setup table variable for CollectionAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform CollectionAggregate on @Geom.shape column  
 SELECT geometry::CollectionAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

