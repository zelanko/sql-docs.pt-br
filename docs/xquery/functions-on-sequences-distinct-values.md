---
title: Função DISTINCT-values (XQuery) | Microsoft Docs
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
ms.openlocfilehash: d2f856c9b351c776651f08e66f90c7f567a5dcfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223731"
---
# <a name="functions-on-sequences---distinct-values"></a>Funções em Sequências – distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove valores duplicados da sequência especificada por *$arg*. Se *$arg* é uma sequência vazia, a função retornará a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Sequência de valores atômicos.  
  
## <a name="remarks"></a>Comentários  
 Todos os tipos de valores atomizados que são passados para **distinct-values()** têm que ser subtipos do mesmo tipo base. Tipos base aceitos são os tipos que oferecem suporte a **eq** operação. Esses tipos incluem os três tipos base numéricos internos, os tipos base de data/hora, xs:string, xs:boolean e xdt:untypedAtomic. Os valores do tipo xdt:untypedAtomic são convertidos em xs:string. Se houver uma mistura desses tipos, ou se outros valores de outros tipos forem passados, será gerado um erro estático.  
  
 O resultado de **distinct-values()** recebe o tipo base dos tipos passados como xs: string no caso de XDT: untypedatomic, com a cardinalidade original. Se a entrada estiver estaticamente vazia, vazio será implícito e um erro estático será gerado.  
  
 Os valores de xs:string são comparados à ordenação de ponto de código Unicode padrão XQuery.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Usando a função distinct-values() para remover valores duplicados da sequência  
 Neste exemplo, uma instância XML que contém os números de telefone é atribuída a um **xml** variável de tipo. O XQuery especificado contra essa variável usa o **distinct-values()** função para compilar uma lista de números de telefone que não contêm duplicatas.  
  
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
  
 Esse é o resultado:  
  
```  
111-111-1111 222-222-2222    
```  
  
 Na consulta a seguir, uma sequência de números (1, 1, 2) é passada para o **distinct-values()** função. A função remove então a duplicata na sequência e retorna as outras duas.  
  
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
  
-   O **distinct-values()** função mapeia os valores inteiros para xs: decimal.  
  
-   O **distinct-values()** função apenas suporta os tipos mencionados anteriormente e não suporta a combinação de tipos base.  
  
-   O **distinct-values()** não há suporte para a função nos valores xs: Duration.  
  
-   Não há suporte para opção sintática que fornece ordenação.  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
