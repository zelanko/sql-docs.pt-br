---
title: EnvelopeCenter (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: da1c2fd6f1e6732f28f79196b433b8e46a595a85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066434"
---
# <a name="envelopecenter-geography-data-type"></a>EnvelopeCenter (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna um ponto que você pode usar como o centro de um círculo delimitador para a instância de **geography**.  
  
Cada ponto na instância é descrito como um vetor. Para descobrir o círculo delimitador, o vetor se estende do centro da Terra ao ponto na superfície da Terra. O ponto central do círculo delimitador é calculado com média de todos os vetores. No caso de loops próximos, em uma instância de **Polygon** ou em uma instância de **LineString**, o primeiro e o último ponto são usados apenas uma vez.  
  
Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
Esse método retorna um **point**. Quando usado com `EnvelopeAngle()`, `EnvelopeCenter()` retorna um círculo delimitador de uma instância **geography**.  
  
> [!NOTE]  
>  `EnvelopeCenter()` retorna um círculo delimitador para uma instância de **geography**, mas os resultados não têm a garantia de produzir o círculo delimitador mínimo. Em contrapartida, o método `STEnvelope()` de tipo de dados **geometry** retorna certamente uma caixa delimitadora mínima quando aplicado a uma instância de **geometry**.  
  
No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, ele retorna o centro do círculo que representa o envelope dessa instância como um **point**. Para todos os objetos grandes conforme definidos por `EnvelopeAngle()` = 180, `EnvelopeCenter()` retornará (90,0).  
  
Esse método não oferece precisão.  
  
## <a name="examples"></a>Exemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
[Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
[EnvelopeAngle &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
