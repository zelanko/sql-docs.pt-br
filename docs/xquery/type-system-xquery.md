---
title: Tipo de sistema (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c0c11fc81be9e8a5b34548e22a7f2feb43a441b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="type-system-xquery"></a>Sistema de tipos (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery é uma linguagem com rigidez de tipos para esquemas digitados, e uma linguagem fraca em tipos para dados não digitados. Os tipos predefinidos de XQuery incluem o seguinte:  
  
-   Tipos internos de esquema XML no **http://www.w3.org/2001/XMLSchema** namespace.  
  
-   Tipos definidos no **http://www.w3.org/2004/07/xpath-datatypes** namespace.  
  
 Este tópico também descreve o seguinte:  
  
-   O valor digitado contra o valor da cadeia de caracteres de um nó.  
  
-   O [dados função &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) e [Function &#40; de cadeia de caracteres XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md).  
  
-   Correspondendo o tipo de sequência retornado por uma expressão.  
  
## <a name="built-in-types-of-xml-schema"></a>Tipos internos do esquema XML  
 Os tipos internos do esquema XML têm um prefixo de namespace predefinido de xs. Alguns desses tipos incluem **xs: Integer** e **xs: string**. Há suporte para todos esses tipos internos. Você pode usar esses tipos ao criar uma coleção de esquemas XML.  
  
 Ao consultar XML digitado, o tipo estático e dinâmico dos nós é determinado pela coleção de esquemas XML associada à coluna ou variável sendo consultada. Para obter mais informações sobre os tipos estáticos e dinâmicos, consulte [contexto de expressão e avaliação de consulta &#40; XQuery &#41; ](../xquery/expression-context-and-query-evaluation-xquery.md). Por exemplo, a consulta a seguir é especificada em relação a um tipo **xml** coluna (`Instructions`). A expressão usa `instance of` para verificar se o valor digitado do atributo `LotSize` retornado é do tipo `xs:decimal`.  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Essas informações digitadas são fornecidas pela coleção de esquemas XML associada à coluna.  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>Tipos definidos no namespace XPath Data Types  
 Os tipos definidos no **http://www.w3.org/2004/07/xpath-datatypes** namespace têm um prefixo predefinido de **xdt**. O seguinte se aplica a esses tipos:  
  
-   Você não pode usar esses tipos ao criar uma coleção de esquemas XML. Esses tipos são usados no sistema de tipos XQuery e são usados para [XQuery e digitação estática](../xquery/xquery-and-static-typing.md). Você pode converter os tipos atômicos, por exemplo, **XDT: untypedatomic**, além de **xdt** namespace.  
  
-   Ao consultar o XML não digitado, o tipo estático e dinâmico de nós de elemento é **xdt: sem tipo**, e o tipo de valores de atributo é **XDT: untypedatomic**. O resultado de uma **Query ()** método gera XML não digitado. Isso significa que os nós XML são retornados como **xdt: sem tipo** e **XDT: untypedatomic**, respectivamente.  
  
-   O **XDT: daytimeduration** e **XDT: yearmonthduration** tipos não têm suporte.  
  
 No exemplo a seguir, a consulta é especificada em uma coluna XML não digitada. A expressão, `data(/a[1]`), retorna uma sequência de um valor atômico. A função `data()` retorna o valor digitado do elemento `<a>`. Como o XML sendo consultado não é digitado, o tipo do valor retornado é `xdt:untypedAtomic`. Portanto, `instance of` retorna true.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 Em vez de recuperar o valor digitado, a expressão (`/a[1]`) no exemplo a seguir retorna uma sequência de um elemento, o elemento `<a>`. A expressão `instance of` usa o teste de elemento para verificar se o valor retornado pela expressão é um nó de elemento `xdt:untyped type`.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  Quando você está consultando uma instância XML digitada e a expressão de consulta inclui o eixo pai, as informações do tipo estática dos nós resultantes não estarão mais disponíveis. Porém, o tipo dinâmico ainda está associado com os nós.  
  
## <a name="typed-value-vs-string-value"></a>Valor com tipo versus valor de cadeia de caracteres  
 Todo nó tem um valor digitado e um valor de cadeia de caracteres. Para os dados XML digitados, o tipo do valor digitado é fornecido pela coleção de esquemas XML associada à coluna ou variável sendo consultada. Para dados XML não digitados, o tipo do valor digitado é **XDT: untypedatomic**.  
  
 Você pode usar o **Data ()** ou **String ()** função para recuperar o valor de um nó:  
  
-   O [dados função &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) retorna o valor digitado de um nó.  
  
-   O [Function &#40; de cadeia de caracteres XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md) retorna o valor de cadeia de caracteres do nó.  
  
 Na coleção de esquemas XML a seguir, o elemento <`root`> do tipo inteiro é definida:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 No exemplo a seguir, a expressão primeiro recupera o valor digitado de `/root[1]` e depois adiciona `3` a ela.  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 No próximo exemplo, a expressão falha, pois a `string(/root[1])` na expressão retorna um valor do tipo de cadeia de caracteres. Esse valor é então passado para um operador aritmético que só considera valores de tipo numéricos como seus operandos.  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 O exemplo a seguir calcula o total dos atributos de `LaborHours`. O `data()` função recupera os valores digitados de `LaborHours` todos os atributos de <`Location`> elementos de um modelo de produto. De acordo com o esquema XML associado a `Instruction` coluna, `LaborHours` é de **xs: decimal** tipo.  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 Essa consulta retorna 12.75 como resultado.  
  
> [!NOTE]  
>  O uso explícito do **Data ()** função neste exemplo é apenas para fins ilustrativos. Se não for especificado, **SUM ()** implicitamente se aplica a **Data ()** função para extrair os valores digitados de nós.  
  
## <a name="see-also"></a>Consulte também  
 [Modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Fundamentos de XQuery](../xquery/xquery-basics.md)  
  
  
