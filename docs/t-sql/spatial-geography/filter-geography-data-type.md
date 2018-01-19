---
title: Filtro (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9d659875d2d34ff1bfecefd05356760949addd40
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="filter-geography-data-type"></a>Filter (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Um método que oferece um método de interseção rápido, somente de índice para determinar se um **geografia** instância intercepta outra **geografia** instância, supondo que um índice está disponível.  
  
 Retornará 1 se uma **geografia** instância intercepta potencialmente outra **geografia** instância. Esse método pode gerar um retorno de falso positivo e o resultado exato poderá ser dependente de plano. Retorna um valor 0 preciso (retorno verdadeiro negativo) se não houver nenhuma intersecção de **geografia** instâncias encontradas.  
  
 Em casos em que um índice não está disponível ou não é usado, o método retornará os mesmos valores **stintersects ()** quando chamado com os mesmos parâmetros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra **geografia** instância a ser comparada com a instância na qual Filter() é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **bits**  
  
 Tipo de retorno CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Esse método não é determinista e não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `Filter()` para determinar se há interseção entre duas instâncias de `geography`.  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
