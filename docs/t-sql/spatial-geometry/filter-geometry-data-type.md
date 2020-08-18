---
description: Filter (tipo de dados de geometria)
title: Filter (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 11092f892c9e6e756849f368a44db3ec7f3d0a61
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88359252"
---
# <a name="filter-geometry-data-type"></a>Filter (tipo de dados de geometria)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Um método que oferece um maneira de interseção rápida e somente de índice para determinar se uma instância de **geometry** intersecciona outra instância de **geometry**, considerando que um índice esteja disponível.
  
Retornará 1 se uma instância de **geometry** possivelmente interseccionar outra instância de **geometry**. Esse método pode gerar um retorno falso positivo e o resultado exato poderá depender do plano. Retornará um valor 0 preciso (retorno verdadeiro negativo) se não for localizada nenhuma intersecção de instâncias de **geometria**.
  
Nos casos em que um índice não estiver disponível ou não for usado, o método retornará os mesmos valores que **STIntersects()** quando for chamado com os mesmos parâmetros.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Filter ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *other_geometry*  
 É outra instância de **geometry** a ser comparada com a instância na qual Filter() é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Esse método não é determinista e não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Filter()` para determinar se há interseção entre duas instâncias de `geometry`.  
  
```  
CREATE TABLE sample (id int primary key, g geometry);  
GO  
INSERT INTO sample VALUES  
   (0, geometry::Point(0, 0, 0)),  
   (1, geometry::Point(0, 1, 0)),  
   (2, geometry::Point(0, 2, 0)),  
   (3, geometry::Point(0, 3, 0)),  
   (4, geometry::Point(0, 4, 0));  
  
CREATE SPATIAL INDEX sample_idx ON sample(g)  
WITH (bounding_box = (-8000, -8000, 8000, 8000));  
GO  
SELECT id  
FROM sample   
WHERE g.Filter(geometry::Parse('POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))')) = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

