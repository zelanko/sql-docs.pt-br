---
title: Função Max (XQuery) | Microsoft Docs
description: Saiba mais sobre a função XQuery Max () que retorna um item em uma sequência cujo valor é maior do que o de todos os outros.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: caf736973d288a89bec287aff3cb1c1993e3b0dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726779"
---
# <a name="aggregate-functions---max"></a>Funções de Agregação – max
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Retorna de uma sequência de valores atômicos, *$ARG*, um item cujo valor é maior do que o de todos os outros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de valores atômicos do qual deve ser retornado o valor máximo.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores Atom que são passados para **Max ()** precisam ser subtipos do mesmo tipo base. Os tipos base que são aceitos são os tipos que dão suporte à operação **gt** . Esses tipos incluem os três tipos base numéricos internos, os tipos base de data/hora, xs:string, xs:boolean e xdt:untypedAtomic. Valores do tipo xdt:untypedAtomic são convertidos em xs:double. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, um erro estático será gerado.  
  
 O resultado de **Max ()** recebe o tipo base do passado em tipos, como xs: Double no caso de xdt: untypedAtomic. Se a entrada estiver estaticamente vazia, Empty será implícito e um erro estático será gerado.  
  
 A função **Max ()** retorna um valor na sequência que é maior que qualquer outro na sequência de entrada. Para valores xs:string, a ordenação de ponto de código Unicode padrão está sendo usada. Se um valor de xdt: untypedAtomic não puder ser convertido em xs: Double, o valor será ignorado na sequência de entrada, *$ARG*. Se a entrada for uma sequência vazia calculada dinamicamente, a sequência vazia será retornada.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>a. Usando a função max() XQuery para localizar locais de centro de trabalho no processo de fabricação que têm grande parte das horas de trabalho  
 A consulta fornecida na [função mín (XQuery)](../xquery/aggregate-functions-min.md) pode ser reescrita para usar a função **Max ()** .  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **Max (**) mapeia todos os inteiros para xs: decimal.  
  
-   Não há suporte para a função **Max ()** em valores do tipo xs: Duration.  
  
-   Não há suporte para sequências que misturam tipos, atravessando os limites de tipo base.  
  
-   Não há suporte para opção sintática que fornece ordenação.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
