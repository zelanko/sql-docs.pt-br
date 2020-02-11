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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
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
 Todos os tipos dos valores atomos que são passados para **AVG ()** precisam ser um subtipo de exatamente um dos três tipos base numéricos internos ou xdt: untypedAtomic. Eles não podem ser uma combinação disso. Valores do tipo xdt:untypedAtomic são tratados como xs:double. O resultado de **AVG ()** recebe o tipo base do passado em tipos, como xs: Double no caso de xdt: untypedAtomic.  
  
 Se a entrada estiver estaticamente vazia, Empty será implícito e um erro estático será gerado.  
  
 A função **AVG ()** retorna a média dos números computados. Por exemplo:  
  
 **contagem de div Sum (** *$arg* **) (** *$ARG* **)**  
  
 Se *$ARG* for uma sequência vazia, a sequência vazia será retornada.  
  
 Se um valor de xdt: untypedAtomic não puder ser convertido em xs: Double, o valor será desconsiderado na sequência de entrada, *$ARG*.  
  
 Em todos os outros casos, a função retorna um erro estático.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>a. Usando a função avg() XQuery para localizar locais do centro de trabalho no processo de fabricação no qual as horas de trabalho são maiores que a média de todos os locais do centro de trabalho.  
 Você pode reescrever a consulta fornecida na [função mín (XQuery)](../xquery/aggregate-functions-min.md) para usar a função **AVG ()** .  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **AVG ()** mapeia todos os inteiros para xs: decimal.  
  
-   Não há suporte para a função **AVG ()** em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
