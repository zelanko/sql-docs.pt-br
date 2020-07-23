---
title: Função de valores distintos (XQuery) | Microsoft Docs
description: Saiba como usar a função de valores distintos em um XQuery para remover valores duplicados de uma sequência.
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
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
ms.openlocfilehash: 39b5db61e3709d8d9f1d9859f15d9e6c271b5e05
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917963"
---
# <a name="functions-on-sequences---distinct-values"></a>Funções em Sequências – distinct-values
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  Remove valores duplicados da sequência especificada por *$ARG*. Se *$ARG* for uma sequência vazia, a função retornará a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de valores atômicos.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores Atom que são passados para **valores distintos ()** devem ser subtipos do mesmo tipo base. Os tipos base que são aceitos são os tipos que oferecem suporte à operação **EQ** . Esses tipos incluem os três tipos base numéricos internos, os tipos base de data/hora, xs:string, xs:boolean e xdt:untypedAtomic. Os valores do tipo xdt:untypedAtomic são convertidos em xs:string. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, será gerado um erro estático.  
  
 O resultado de **valores distintos ()** recebe o tipo base do passado em tipos, como xs: String no caso de xdt: untypedAtomic, com a cardinalidade original. Se a entrada estiver estaticamente vazia, Empty será implícito e um erro estático será gerado.  
  
 Os valores de xs:string são comparados à ordenação de ponto de código Unicode padrão XQuery.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>a. Usando a função distinct-values() para remover valores duplicados da sequência  
 Neste exemplo, uma instância XML que contém números de telefone é atribuída a uma variável de tipo **XML** . O XQuery especificado nessa variável usa a função de **valores distintos ()** para compilar uma lista de números de telefone que não contêm duplicatas.  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 Este é o resultado:  
  
```  
111-111-1111 222-222-2222    
```  
  
 Na consulta a seguir, uma sequência de números (1, 1, 2) é passada para a função de **valores distintos ()** . A função remove então a duplicata na sequência e retorna as outras duas.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 A consulta retorna 1 2.  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   A função **distinct-values ()** mapeia valores inteiros para xs: decimal.  
  
-   A função **distinct-values ()** dá suporte apenas aos tipos mencionados anteriormente e não oferece suporte à combinação de tipos base.  
  
-   Não há suporte para a função de **valores distintos ()** em valores xs: Duration.  
  
-   Não há suporte para opção sintática que fornece ordenação.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
