---
title: Filter (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7cf00adcfb11249dc2465d2afd7532dc4d4dc093
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937840"
---
# <a name="filter-geography-data-type"></a>Filter (tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Um método que oferece um método rápido de interseção somente de índice para determinar se uma instância de **geography** é interseccionada por outra instância de **geography**, supondo que um índice esteja disponível.  
  
 Retorna 1 se uma instância de **geography** intercepta potencialmente outra instância de **geography**. Esse método pode gerar um retorno de falso positivo e o resultado exato poderá ser dependente de plano. Retorna um valor 0 preciso (retorno negativo verdadeiro) se nenhuma intersecção de instâncias de **geography** é encontrada.  
  
 Nos casos em que um índice não estiver disponível ou não for usado, o método retornará os mesmos valores que **STIntersects()** quando for chamado com os mesmos parâmetros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geography*  
 É outra instância de **geography** para comparação com a instância na qual Filter() é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
