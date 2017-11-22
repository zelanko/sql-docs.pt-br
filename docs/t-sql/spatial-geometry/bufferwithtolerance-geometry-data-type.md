---
title: BufferWithTolerance (tipo de dados geometry) | Microsoft Docs
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
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs: TSQL
helpviewer_keywords: BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a6a932ffe43e978bdc9e06f96cac300d45a035b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna valores de um objeto geométrico que representa a união de todos os pontos cuja distância de uma **geometria** instância é menor ou igual ao valor especificado, permitindo uma tolerância especificada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distância*  
 É um **float** expressão que especifica a distância entre o **geometria** instância em torno da qual calcular o buffer.  
  
 *tolerância*  
 É um **float** expressão que especifica a tolerância da distância do buffer.  
  
 *Tolerância* refere-se à variação máxima na distância ideal do buffer para a aproximação linear retornada.  
  
 Por exemplo, a distância ideal de buffer de um ponto é um círculo, mas deve ser aproximado por um polígono. Quanto menor a tolerância, mais pontos o polígono terá, o que aumenta a complexidade do resultado, mas diminui o erro.  
  
 *relativo*  
 É um **bit** especificando se o *tolerância* valor é relativo ou absoluto. Se 'TRUE' ou 1, em seguida, tolerância será relativa e calculada como o produto do *tolerância* parâmetro e o diâmetro da caixa delimitadora da instância. Se 'FALSE' ou 0, tolerância será absoluta e o *tolerância* valor é a variação máxima absoluta na distância ideal do buffer para a aproximação linear retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geometry**  
  
 Tipo de retorno CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 O *tolerância* parâmetro deve ser maior que zero. Se *tolerância* < = 0, um `System.ArgumentOutOfRangeException` é gerada.  
  
> [!NOTE]  
>  Como *tolerância* é um **float** tipo, um `System.Runtime.InteropServices.COMException` pode ser gerada se o valor atribuído à tolerância for muito pequeno devido a problemas de arredondamento com tipos de ponto flutuante.  
  
## <a name="remarks"></a>Comentários  
 Quando *distância* > 0, uma um **polígono** ou **MultiPolygon** instância será retornada.  
  
> [!NOTE]  
>  Como a distância é um **float**, um valor extremamente pequeno pode equivaler a zero nos cálculos. Quando isso ocorre, uma cópia da chamada **geometria** instância será retornada. Consulte [float e real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Quando *distância* = 0, uma cópia da chamada **geometria** instância será retornada.  
  
 Quando *distância* < 0 então  
  
-   vazio **GeometryCollection** instância é retornada quando as dimensões da instância são 0 ou 1.  
  
-   Um buffer negativo é retornado quando as dimensões da instância são 2 ou mais.  
  
    > [!NOTE]  
    >  Um buffer negativo também pode criar um vazio **GeometryCollection** instância.  
  
 Um buffer negativo remove todos os pontos dentro da distância determinada do limite do **geometria** instância.  
  
 O erro entre o buffer teórico e calculado é max (tolerância, extensões \* 1. e-7) onde a tolerância é o valor da *tolerância* parâmetro. Para obter mais informações sobre extensões, consulte [referência de método do tipo de dados geometry](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` e usa `BufferWithTolerance()` para obter um buffer grosseiro à sua volta.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [STBuffer &#40; tipo de dados geometry &#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

