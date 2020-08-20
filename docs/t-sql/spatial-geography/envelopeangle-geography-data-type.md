---
description: EnvelopeAngle (tipo de dados geography)
title: EnvelopeAngle (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c72459ec22208dfebbe234430ba49a4e94cb06a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479363"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o ângulo máximo entre o ponto retornado pelo método `EnvelopeCenter()` e um ponto na instância de **geography** em graus.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeAngle( )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de retorno do CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
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
  
  
