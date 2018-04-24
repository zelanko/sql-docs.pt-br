---
title: EnvelopeCenter (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f72f27b98f97cfe15d853a961d194cfb7d1f25ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (Tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um ponto que pode ser usado como o centro de um círculo delimitador para a instância de **geography**.  
  
 Para determinar o círculo delimitador, cada ponto na instância é descrito como um vetor do centro da Terra a um ponto na superfície da Terra. O ponto central do círculo delimitador é calculado com média de todos os vetores. No caso de loops próximos, em uma instância de **polygon** ou em uma instância de **linestring**, o primeiro e o último ponto são usados apenas uma vez.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Esse método retorna um **point**. Quando usado com `EnvelopeAngle()`, `EnvelopeCenter()` retorna um círculo delimitador de uma instância **geography**.  
  
> [!NOTE]  
>  `EnvelopeCenter()` retorna um círculo delimitador para uma instância de **geography**, mas os resultados não têm a garantia de produzir o círculo delimitador mínimo. Em contrapartida, o método `STEnvelope()` de tipo de dados **geometry** retorna certamente uma caixa delimitadora mínima quando aplicado a uma instância de **geometry**.  
  
 No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, ele retorna o centro do círculo que representa o envelope dessa instância como um **point**. Para todos os objetos grandes conforme definidos por `EnvelopeAngle()` = 180, `EnvelopeCenter()` retornará (90,0).  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
