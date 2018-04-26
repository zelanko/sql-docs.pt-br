---
title: Expressões primárias (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- variable references [XQuery]
- primary expressions [XQuery]
- function calls [XQuery]
- expressions [XQuery], primary
- literals [XQuery]
- context item expressions [XQuery]
ms.assetid: d4183c3e-12b5-4ca0-8413-edb0230cb159
caps.latest.revision: 20
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ee901d54e5cf68eb5de1e20c448289eab83dbfb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="primary-expressions-xquery"></a>Expressões primárias (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  As expressões primárias do XQuery incluem literais, referências variáveis, expressões de item de contexto, construtores e chamadas de função.  
  
## <a name="literals"></a>Literais  
 Os literais do XQuery podem ser literais numéricos ou da cadeia de caracteres. Um literal da cadeia de caracteres pode incluir referências de entidade predefinidas; uma referência de entidade é uma sequência de caracteres. A sequência inicia com um E comercial que representa um único caractere, que, de outra forma, poderia ter significância sintática. A seguir, são apresentadas as referências de entidade predefinidas para XQuery.  
  
|Referência de entidade|Representa|  
|----------------------|----------------|  
|&lt;|\<|  
|&gt;|>|  
|&amp;|&|  
|&quot;|"|  
|&apos;|'|  
  
 Um literal da cadeia de caracteres também pode conter uma referência de caractere, uma referência de estilo XML para um caractere Unicode, que é identificado por seu ponto de código decimal ou hexadecimal. Por exemplo, o símbolo do Euro pode ser representado pela referência de caractere, "&\#8364;".  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa a versão XML 1.0 como a base da análise.  
  
### <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram o uso de literais e também referências de entidade e caractere.  
  
 Esse código retorna um erro, pois os caracteres `<'` e `'>` têm significado especial.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 Se, em vez disso, você usar uma referência de entidade, a consulta funcionará.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 O exemplo a seguir ilustra o uso de uma referência de caractere para representar o símbolo de Euro.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <a>€12.50</a>')  
```  
  
 Este é o resultado.  
  
 `<a>€12.50</a>`  
  
 No exemplo a seguir, a consulta é delimitada por apóstrofos. Portanto, o apóstrofo no valor da cadeia de caracteres é representado por dois apóstrofos adjacentes.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>I don''t know</a>')  
Go  
```  
  
 Este é o resultado.  
  
 `<a>I don't know</a>`  
  
 As funções booleanas internas, **verdadeiro ()** e **False ()**, pode ser usado para representar valores booleanos, conforme mostrado no exemplo a seguir.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>{true()}</a>')  
GO  
```  
  
 O construtor de elemento direto especifica uma expressão em colchetes. Isso é substituído por seu valor no XML resultante.  
  
 Este é o resultado.  
  
 `<a>true</a>`  
  
## <a name="variable-references"></a>Referências variáveis  
 Uma referência variável no XQuery é um QName precedido por um sinal de $. Essa implementação oferece suporte somente a referências variáveis sem-prefixo. Por exemplo, a consulta a seguir define a variável `$i` na expressão FLWOR.  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
 for $i in /root return data($i)')  
GO  
```  
  
 A consulta a seguir não funcionará, pois um prefixo de namespace é adicionado ao nome da variável.  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
DECLARE namespace x="http://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 Você pode usar a função de extensão do SQL: Variable para se referir a variáveis SQL, conforme mostrado na consulta a seguir.  
  
```  
DECLARE @price money  
SET @price=2500  
DECLARE @x xml  
SET @x = ''  
SELECT @x.query('<value>{sql:variable("@price") }</value>')  
```  
  
 Este é o resultado.  
  
 `<value>2500</value>`  
  
#### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações de implementação:  
  
-   Não é oferecido suporte a variáveis com prefixos de namespace.  
  
-   Não é oferecido suporte à importação de módulo.  
  
-   Não é oferecido suporte a declarações de variáveis externas. Uma solução para isso é usar o [função SQL: Variable](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="context-item-expressions"></a>Expressões de item de contexto  
 O item de contexto é o item sendo processado atualmente no contexto de uma expressão de caminho. Ele é inicializado em uma instância de tipo de dados XML não NULL com o nó de documento. Ele também pode ser alterado pelo método Nodes (), no contexto de expressões XPath ou predicados [].  
  
 O item de contexto é retornado por uma expressão que contém um ponto (.). Por exemplo, a consulta a seguir avalia cada elemento <`a`> para a presença do atributo `attr`. Se o atributo estiver presente, o elemento será retornado. Observe que a condição no predicado especifica que o nó de contexto é especificado por um único ponto.  
  
```  
DECLARE @var XML  
SET @var = '<ROOT>  
<a>1</a>  
<a attr="1">2</a>  
</ROOT>'  
SELECT @var.query('/ROOT[1]/a[./@attr]')  
```  
  
 Este é o resultado.  
  
 `<a attr="1">2</a>`  
  
## <a name="function-calls"></a>Chamadas de função  
 Você pode chamar funções XQuery internas e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] funções Variable () e SQL: Column. Para obter uma lista de funções implementadas, consulte [funções XQuery em relação ao tipo de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md).  
  
#### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações de implementação:  
  
-   Não é oferecido suporte à declaração de função no prólogo do XQuery.  
  
-   Não é oferecido suporte à importação de função.  
  
## <a name="see-also"></a>Consulte também  
 [Construção XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
