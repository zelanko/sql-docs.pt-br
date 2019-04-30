---
title: Ponto | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Point geometry subtype [SQL Server]
- geometry data type [SQL Server], spatial data
ms.assetid: 2a596ec4-8b2f-4962-bcb4-e5c8f77edad5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c680f40a27f0a0ba450d061dae3127872d1262a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191944"
---
# <a name="point"></a>Ponto
  Em dados espaciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um `Point` é um objeto dimensional zero que representa um único local e pode conter valores Z (elevação) e M (medida).  
  
## <a name="geography-data-type"></a>Tipo de dados de geografia  
 O tipo de Ponto para o tipo de dados geography representa um único local em que *Lat* representa latitude e *Long* representa longitude. Os valores de latitude e longitude são medidos em graus. Valores para latitude sempre estão no intervalo [-90, 90] e os valores inseridos fora desse intervalo gerarão uma exceção. Os valores de longitude estão sempre no intervalo (-180, 180]; e os valores inseridos fora desse intervalo são ajustados para caberem nesse intervalo. Por exemplo, se 190 for inserido para longitude, ele será ajustado para o valor -170. *SRID* representa a ID de referência espacial da instância **geography** que você deseja retornar.  
  
## <a name="geometry-data-type"></a>Tipo de dados geometry  
 O tipo de Ponto para o tipo de dados geometry representa um único local onde *X* representa a coordenada X do Ponto que é gerado e *Y* representa a coordenada de Y do Ponto que é gerado. *SRID* representa a ID de referência espacial da instância **geometry** que você deseja retornar.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `geometry Point`que representa o ponto (3, 4) com um SRID de 0.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT (3 4)', 0);  
```  
  
 O próximo exemplo cria uma instância de `geometry``Point` que representa o ponto (3, 4) com um valor Z (elevação) de 7, um valor M (medida) de 2,5 e o SRID padrão de 0.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 7 2.5)');  
```  
  
 O exemplo final retorna os valores X, Y, Z e M para a instância `geometry``Point` .  
  
```  
SELECT @g.STX;  
SELECT @g.STY;  
SELECT @g.Z;  
SELECT @g.M;  
```  
  
 Podem ser especificados valores Z e M como NULL, conforme mostrado no exemplo a seguir.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POINT(3 4 NULL NULL)');  
```  
  
## <a name="see-also"></a>Consulte também  
 [MultiPoint](multipoint.md)   
 [STX &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)   
 [STY &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/sty-geometry-data-type)   
 [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
