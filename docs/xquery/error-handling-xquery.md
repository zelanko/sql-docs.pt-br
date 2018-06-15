---
title: Erro ao manipular (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c7277c122c76ef2aa9ff6c82b4693faed6b409ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076935"
---
# <a name="error-handling-xquery"></a>Tratamento de erros (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  A especificação de W3C permite que erros de tipo ocorram estática ou dinamicamente, e define erros de tipo, dinâmicos e estáticos.  
  
## <a name="compilation-and-error-handling"></a>Compilação e tratamento de erros  
 Erros de compilação são retornados de expressões Xquery sintaticamente incorretas e instruções XML DML. A fase de compilação verifica a exatidão do tipo estático das expressões XQuery e instruções DML, e usa esquemas XML para inferências de tipo para XML digitado. Erros do tipo estático ocorrem se uma expressão puder falhar no tempo de execução em razão de uma violação de segurança de tipo. Os exemplos de erro estático são: adição de uma cadeia de caracteres a um número inteiro e consulta de um nó inexistente para dados digitados.  
  
 Como uma divergência do padrão de W3C, os erros em tempo de execução Xquery são convertidos em sequências vazias. Essas sequências podem se propagar como XML vazio ou NULL no resultado da consulta, dependendo do contexto da invocação.  
  
 Uma conversão explícita para o tipo correto permite aos usuários solucionar erros estáticos, embora erros de tempo de execução lançados sejam transformados em sequências vazias.  
  
## <a name="static-errors"></a>Erros estáticos  
 Erros estáticos são retornados usando o mecanismo de erro [!INCLUDE[tsql](../includes/tsql-md.md)]. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], os erros de tipo Xquery são retornados estaticamente. Para obter mais informações, consulte [XQuery e digitação estática](../xquery/xquery-and-static-typing.md).  
  
## <a name="dynamic-errors"></a>Erros dinâmicos  
 No XQuery, a maioria dos erros dinâmicos são mapeados para uma sequência vazia ("()"). Entretanto, estas são as duas exceções: condições de estouro nas funções de agregação do XQuery e validação de erros XML-DML. Observe que a maioria dos erros dinâmicos é mapeada para uma sequência vazia. Caso contrário, a execução da consulta que se beneficia dos índices XML pode causar erros inesperados. Portanto, para prover uma execução eficiente sem gerar erros inesperados, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] mapeia erros dinâmicos para ().  
  
 Frequentemente, na situação em que o erro dinâmico aconteceria dentro de um predicado, não causar o erro não é alterar as semânticas, porque () é mapeado para False. No entanto, em alguns casos, retornando () em vez de um erro dinâmico pode causar resultados inesperados. Os exemplos a seguir ilustram isso.  
  
### <a name="example-using-the-avg-function-with-a-string"></a>Exemplo: usando a função avg () com uma cadeia de caracteres  
 No exemplo a seguir, o [função avg](../xquery/aggregate-functions-avg.md) é chamado para calcular a média dos três valores. Um desses valores é uma cadeia de caracteres. Em razão da instância XML nesse caso não ser digitada, todos os dados nela são de um tipo atômico não digitado. O **Avg ()** função converte primeiro esses valores para **xs: Double** antes de calcular a média. No entanto, o valor `"Hello"`, não pode ser convertido em **xs: Double** e cria um erro dinâmico. Nesse caso, em vez de retornar um erro dinâmico, a conversão de `"Hello"` para **xs: Double** faz com que uma sequência vazia. O **Avg ()** função ignora esse valor, calcula a média dos outros dois valores e retorna 150.  
  
```  
DECLARE @x xml  
SET @x=N'<root xmlns:myNS="test">  
 <a>100</a>  
 <b>200</b>  
 <c>Hello</c>  
</root>'  
SELECT @x.query('avg(//*)')  
```  
  
### <a name="example-using-the-not-function"></a>Exemplo: usando a função not  
 Quando você usa o [não funcionar](../xquery/functions-on-boolean-values-not-function.md) em um predicado, por exemplo, `/SomeNode[not(Expression)]`, e a expressão causa um erro dinâmico, uma sequência vazia será retornada em vez de um erro. Aplicando **not ()** para a sequência vazia retorna True, em vez de um erro.  
  
### <a name="example-casting-a-string"></a>Exemplo: convertendo uma cadeia de caracteres  
 No exemplo a seguir, a cadeia de caracteres literal "NaN" é convertida em xs:string, depois em xs:double. O resultado é um conjunto de linhas vazio. Embora a cadeia de caracteres "NaN" não possa ser convertida em xs:double com sucesso, isso não pode ser determinado até que a cadeia de caracteres seja convertida primeiro em xs:string.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double(xs:string("NaN")) ')  
GO  
```  
  
 Neste exemplo, contudo, acontece um erro de tipo estático.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double("NaN") ')  
GO  
```  
  
#### <a name="implementation-limitations"></a>Limitações de implementação  
 O **fn:error()** não há suporte para a função.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Fundamentos de XQuery](../xquery/xquery-basics.md)  
  
  
