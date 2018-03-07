---
title: Filtro (tipo de dados geometry) | Microsoft Docs
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
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 3d629a39-157e-4159-a3ca-a3c2e0ed4160
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e09f4ac5d6d4ecaf32f6b500aee9a3a50c772c02
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="filter-geometry-data-type"></a>Filter (tipo de dados de geometria)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Um método que oferece um método de interseção rápido, somente de índice para determinar se um **geometria** instância intercepta outra **geometria** instância, supondo que um índice está disponível.
  
Retornará 1 se uma **geometria** instância intercepta potencialmente outra **geometria** instância. Esse método pode gerar um retorno de falso positivo e o resultado exato poderá depender do plano. Retorna um valor 0 preciso (retorno verdadeiro negativo) se não houver nenhuma intersecção de **geometria** instâncias encontradas.
  
Em casos em que um índice não está disponível ou não é usado, o método retornará os mesmos valores **stintersects ()** quando chamado com os mesmos parâmetros.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Filter ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra **geometria** instância a ser comparada com a instância na qual Filter() é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [STIntersects &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
  

