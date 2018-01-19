---
title: EnvelopeAngle (tipo de dados geography) | Microsoft Docs
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
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs: TSQL
helpviewer_keywords: EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b7eaef8384500d63acee0d5fae1183d4928bcca
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o ângulo máximo entre o ponto retornado por `EnvelopeCenter()` e um ponto de **geografia** instância em graus.  
  
 Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **float**  
  
 Tipo de retorno CLR: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Este método retorna um ponto de **geografia** instância em graus. Quando usado com EnvelopeCenter(), `EnvelopeAngle()` retorna um círculo delimitador de um **geografia** instância.  
  
 Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esse método foi estendido para **FullGlobe** instâncias.  
  
 A limitação de hemisfério aplicada a `EnvelopeAngle()` na [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] foi removido. Porém, para instâncias com ângulos maiores que 90 graus, serão retornados 180 graus. `EnvelopeAngle()`não é preciso para **geografia** instâncias que se estendem por mais de um hemisfério.  
  
## <a name="examples"></a>Exemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
