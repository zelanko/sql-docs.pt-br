---
title: Elemento DropOnlyMode (DTA)
description: No utilitário dta, o elemento DropOnlyMode especifica que o Orientador de Otimização do Mecanismo de Banco de Dados considera apenas descartar índices, exibições indexadas ou partições existentes.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: b8335b68b684f5ca9688542a30919c05397b6c65
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831535"
---
# <a name="droponlymode-element-dta"></a>Elemento DropOnlyMode (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica que o Orientador de Otimização do Mecanismo de Banco de Dados deve apenas considerar descartar índices, exibições indexadas ou partições existentes durante a sessão de ajuste. Nenhuma nova estrutura de design físico é considerada quando esta opção de ajuste é especificada.  
  
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
  
 **Ocorrência**: Opcional. Pode-se usar apenas uma vez para cada elemento **TuningOptions** . Não poderá ser usado se os elementos seguintes forem especificados no elemento de **TuningOptions** :  
  
-   [Elemento FeatureSet &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Elemento Partitioning &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   O [Elemento KeepExisting &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md) é definido como **ALL**  
  
## <a name="element-relationships"></a>Relações do elemento  
 **Elemento pai**: [Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
