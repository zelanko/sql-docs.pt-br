---
title: máximo de função (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a53b02bc682bf7b3c918a02d5a16dc326ca3a594
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077853"
---
# <a name="aggregate-functions---max"></a>Funções de agregação - max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna de uma sequência de valores atômicos, *$arg*, o item cujo valor é maior do que todos os outros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de valores atômicos do qual deve ser retornado o valor máximo.  
  
## <a name="remarks"></a>Remarks  
 Todos os tipos de valores atomizados que são passados para **Max ()** precisam ser subtipos do mesmo tipo base. Tipos base aceitos são os tipos que oferecem suporte a **gt** operação. Esses tipos incluem os três tipos base numéricos internos, os tipos base de data/hora, xs:string, xs:boolean e xdt:untypedAtomic. Valores do tipo xdt:untypedAtomic são convertidos em xs:double. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, será gerado um erro estático.  
  
 O resultado de **Max ()** recebe o tipo base dos tipos passados como xs: Double no caso de XDT: untypedatomic. Se a entrada estiver estaticamente vazia, vazio será implícito e um erro estático será gerado.  
  
 O **Max ()** função retorna o valor na sequência que é maior do que qualquer outro na sequência de entrada. Para valores xs:string, o agrupamento de ponto de código Unicode padrão está sendo usado. Se um valor XDT: untypedatomic não pode ser convertido em xs: Double, o valor será ignorado na sequência de entrada, *$arg*. Se a entrada for uma sequência vazia calculada dinamicamente, a sequência vazia será retornada.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. Usando a função max() XQuery para localizar locais de centro de trabalho no processo de fabricação que têm grande parte das horas de trabalho  
 A consulta fornecida na [função min (XQuery)](../xquery/aggregate-functions-min.md) pode ser reescrita para usar o **Max ()** função.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **max (**) função mapeia todos os inteiros para xs: decimal.  
  
-   O **Max ()** não há suporte para a função em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
-   Não há suporte para opção sintática que fornece agrupamento.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
