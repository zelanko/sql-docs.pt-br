---
title: STPointN (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15a196cf9ac1c5f560a2eeee3d0262829f88480b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stpointn-geography-data-type"></a>STPointN (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o ponto especificado em uma **geografia** instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É um **int** expressão entre 1 e o número de pontos de **geografia** instância.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
 Abra o tipo Geospatial Consortium (OGC): **ponto**  
  
## <a name="remarks"></a>Comentários  
 Se um **geografia** instância é criada pelo usuário, STPointN() retorna o ponto especificado por *expressão* ordenando os pontos na ordem em que eles foram originalmente de entrada.  
  
 Se um **geografia** instância é criada pelo sistema, STPointN() retorna o ponto especificado por *expressão* ordenando todos os pontos na mesma ordem, eles seriam saída: primeiro por  **Geografia** instância, depois pelo anel dentro da instância (se apropriado) e, em seguida, pelo ponto dentro do anel. Essa ordem é determinística.  
  
 Se esse método for chamado com um valor menor que 1, ele lança uma **ArgumentOutOfRangeException**.  
  
 Se esse método for chamado com um valor maior que o número de pontos na instância, retornará nulo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STPointN()` para recuperar o segundo o ponto na descrição da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  

