---
title: UnionAggregate (tipo de dados geometry) | Microsoft Docs
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
- UnionAggregate method (geometry)
ms.assetid: dc7929cc-55ca-4a2c-a4b9-f5452f95bde8
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f4fd01821e8f432d39905fb0bca974c155a151af
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066135"
---
# <a name="unionaggregate-geometry-data-type"></a>UnionAggregate (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Executa uma operação de união em um conjunto de objetos de geometria.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UnionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_operand*  
 É uma coluna de tabela do tipo **geometria** que contém o conjunto de objetos de **geometria** no qual uma operação de união deve ser executada.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
## <a name="exceptions"></a>Exceções  
 Gera uma `FormatException` quando há valores de entrada que não são válidos. Confira [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Comentários  
 O método retornará **nulo** quando a entrada estiver vazia ou tiver SRIDs diferentes. Confira [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 O método ignora entradas **nulas**.  
  
> [!NOTE]  
>  O método retornará **nulo** se todos os valores inseridos forem **nulos**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a união de um conjunto de objetos de **geometria** em uma variável de tabela.  
 ```
 -- Setup table variable for UnionAggregate example 
 DECLARE @Geom TABLE 
 ( 
 shape geometry, 
 shapeType nvarchar(50) 
 ); 
 INSERT INTO @Geom(shape,shapeType) 
 VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'), 
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle'); 
 -- Perform UnionAggregate on @Geom.shape column 
 SELECT geometry::UnionAggregate(shape).ToString() 
 FROM @Geom;
``` 
  
## <a name="see-also"></a>Consulte Também  
 [Métodos geometry estáticos estendidos](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

