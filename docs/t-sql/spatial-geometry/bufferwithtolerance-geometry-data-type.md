---
title: BufferWithTolerance (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 409fdd3fe05b4dc5b0baabe0d60e871efd028c29
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729994"
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (tipo de dados geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um objeto geométrico que representa a união de todos os valores de pontos cuja distância de uma instância de **geometry** é menor ou igual a um valor especificado, permitindo uma tolerância especificada.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumentos  
 *distance*  
 É uma expressão **float** que especifica a distância da instância de **geometry** em torno da qual o buffer deve ser calculado.  
  
 *tolerance*  
 É uma expressão **float** que especifica a tolerância da distância do buffer.  
  
 *Tolerância* refere-se à variação máxima na distância ideal do buffer para a aproximação linear retornada.  
  
 Por exemplo, a distância ideal de buffer de um ponto é um círculo, mas deve ser aproximado por um polígono. Quanto menor a tolerância, mais pontos o polígono terá, o que aumenta a complexidade do resultado, mas diminui o erro.  
  
 *relative*  
 É um **bit** que especifica se o valor de *tolerance* é relativo ou absoluto. Se for 'TRUE' ou 1, a tolerância será relativa e será calculada como o produto entre o parâmetro *tolerance* e o diâmetro da caixa delimitadora da instância. Se for 'FALSE' ou 0, a tolerância será absoluta e o valor de *tolerance* será a variação máxima absoluta na distância ideal do buffer para a aproximação linear retornada.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 O parâmetro *tolerância* precisa ser maior que zero. Se *tolerância* <= 0, uma `System.ArgumentOutOfRangeException` será gerada.  
  
> [!NOTE]  
>  Como *tolerance* é um tipo **float** uma `System.Runtime.InteropServices.COMException` poderá ser gerada se o valor atribuído à tolerância for muito pequeno devido a problemas de arredondamento com tipos de ponto flutuante.  
  
## <a name="remarks"></a>Remarks  
 Quando a *distância* for > 0, uma instância de **polígono** ou **MultiPolygon** será retornada.  
  
> [!NOTE]  
>  Como a distância é um **float**, um valor extremamente pequeno poderá equivaler a zero nos cálculos. Quando isso ocorrer, uma cópia da instância de **geometry** de chamada será retornada. Consulte [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Quando a *distância* for = 0, uma cópia da instância de **geometry** de chamada será retornada.  
  
 Quando a *distância* for < 0  
  
-   Uma instância de **GeometryCollection** vazia será retornada quando as dimensões da instância forem 0 ou 1.  
  
-   Um buffer negativo é retornado quando as dimensões da instância são 2 ou mais.  
  
    > [!NOTE]  
    >  Um buffer negativo também pode criar uma instância de **GeometryCollection** vazia.  
  
 Um buffer negativo remove todos os pontos dentro da distância determinada do limite da instância de **geometry**.  
  
 O erro entre o buffer teórico e o calculado é max(tolerance, extents \* 1.E-7), em que a tolerância é o valor do parâmetro *tolerance*. Para obter mais informações sobre extensões, confira [Referência de método do tipo de dados geometry](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `Point` e usa `BufferWithTolerance()` para obter um buffer grosseiro à sua volta.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STBuffer &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

