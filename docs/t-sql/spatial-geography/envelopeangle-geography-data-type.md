---
title: EnvelopeAngle (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a0198176abd6d9adad12e892be1734227c14d78
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33060783"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o ângulo máximo entre o ponto retornado pelo método `EnvelopeCenter()` e um ponto na instância de **geography** em graus.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Esse método retorna um ponto na instância de **geography** em graus. Quando usado com EnvelopeCenter(), `EnvelopeAngle()` retorna um círculo delimitador de uma instância de **geography**.  
  
 No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esse método foi estendido para as instâncias de **FullGlobe**.  
  
 A limitação de hemisfério aplicada a `EnvelopeAngle()` no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] foi removida. Porém, para instâncias com ângulos maiores que 90 graus, serão retornados 180 graus. `EnvelopeAngle()` não é preciso para instâncias de **geography** que abrangem mais de um hemisfério.  
  
## <a name="examples"></a>Exemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
