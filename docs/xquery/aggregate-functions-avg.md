---
title: Função AVG (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
ms.openlocfilehash: b659aa13a8704a060be12bb015bd0de0fd126562
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985999"
---
# <a name="aggregate-functions---avg"></a>Funções de Agregação – avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a média de uma sequência de números.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 A sequência de valores atômicos cuja média é calculada.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores atomizados que são passados para **Avg ()** precisa ser um subtipo de exatamente um dos três tipos de base numéricos internos ou XDT: untypedatomic. Eles não podem ser uma combinação disso. Valores do tipo xdt:untypedAtomic são tratados como xs:double. O resultado de **Avg ()** recebe o tipo base dos tipos passados como xs: Double no caso de XDT: untypedatomic.  
  
 Se a entrada estiver estaticamente vazia, vazio será implícito e um erro estático será gerado.  
  
 O **Avg ()** função retorna a média dos números calculados. Por exemplo:  
  
 **Soma (** *$arg* **) div count (** *$arg* **)**  
  
 Se *$arg* é uma sequência vazia, a sequência vazia será retornada.  
  
 Se um valor XDT: untypedatomic não puder ser convertido em xs: Double, o valor será desconsiderado na sequência de entrada *$arg*.  
  
 Em todos os outros casos, a função retorna um erro estático.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. Usando a função avg() XQuery para localizar locais do centro de trabalho no processo de fabricação no qual as horas de trabalho são maiores que a média de todos os locais do centro de trabalho.  
 Você pode reescrever a consulta fornecida na [função min (XQuery)](../xquery/aggregate-functions-min.md) usar o **Avg ()** função.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   O **Avg ()** função mapeia todos os números inteiros para xs: decimal.  
  
-   O **Avg ()** não há suporte para a função em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
