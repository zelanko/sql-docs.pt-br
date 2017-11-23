---
title: EnvelopeCenter (tipo de dados geography) | Microsoft Docs
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
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs: TSQL
helpviewer_keywords: EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4557189ecd06bca2abe0ce9348f00cc191b66a53
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (Tipo de dados de geografia)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um ponto que pode ser usado como o Centro de um círculo delimitador para o **geografia** instância.  
  
 Para determinar o círculo delimitador, cada ponto na instância é descrito como um vetor do centro da Terra a um ponto na superfície da Terra. O ponto central do círculo delimitador é calculado com média de todos os vetores. Loops fechado, em um **polígono** instância ou um **linestring** instância, o primeiro e último ponto é usado apenas uma vez.  
  
 Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **geografia**  
  
 Tipo de retorno CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentários  
 Este método retorna um **ponto**. Quando usado com `EnvelopeAngle()`, `EnvelopeCenter()` retorna um círculo delimitador de um **geografia** instância.  
  
> [!NOTE]  
>  `EnvelopeCenter()`Retorna um círculo delimitador para um **geografia** instância, mas os resultados não são garantidos para produzir círculos delimitadores mínimos. Em contraste, o **geometria** método de tipo de dados `STEnvelope()` é garantido para retornar da caixa delimitadora mínima quando ele é aplicado a um **geometria** instância.  
  
 Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e superior, retorna o centro do círculo que representa o envelope dessa instância como um **ponto**. Para todos os objetos grandes conforme definidos por `EnvelopeAngle()` = 180, `EnvelopeCenter()` retornará (90,0).  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos estendidos em instâncias de Geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40; tipo de dados geography &#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
