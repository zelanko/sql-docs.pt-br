---
title: Elemento DropOnlyMode (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8798a084ab6762781e2445700c0f0e4f51d2f617
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="droponlymode-element-dta"></a>Elemento DropOnlyMode (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Especifica que o orientador de otimização do mecanismo de banco de dados deve apenas considerar descartar índices existentes, exibições indexadas ou partições durante a sessão de ajuste. Nenhuma nova estrutura de design físico é considerada quando esta opção de ajuste é especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
 **Comprimento e tipo de dados**  
  
 **Valor padrão**  
  
 **Ocorrência**: opcional. Pode-se usar apenas uma vez para cada elemento **TuningOptions** . Não poderá ser usado se os elementos seguintes forem especificados no elemento de **TuningOptions** :  
  
-   [Elemento FeatureSet &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Elemento Partitioning &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   O [Elemento KeepExisting &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md) é definido como **ALL**  
  
## <a name="element-relationships"></a>Relações do elemento  
 **Elemento pai**: [elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
 **Elementos filho**  
  
## <a name="example"></a>Exemplo  
 O exemplo seguinte mostra a seção **TuningOptions** de um arquivo de entrada do Orientador de Otimização do Mecanismo de Banco de Dados XML onde o **DropOnlyMode** é especificado. Nesse exemplo a hora de ajuste é limitada a 24 horas (1440 minutos) e todos os índices clusterizados e não clusterizados existentes serão considerados para o descarte:  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
