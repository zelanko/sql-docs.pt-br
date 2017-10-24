---
title: "Sequência de expressões (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- expressions [XQuery], sequence
- filtering sequences [XQuery]
ms.assetid: 41e18b20-526b-45d2-9bd9-e3b7d7fbce4e
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 99e7d41d829f9ef651b51306fc34754ef2e161c9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sequence-expressions-xquery"></a>Expressões de sequência (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferece suporte aos operadores XQuery usados para construir, filtrar e combinar uma sequência de itens. Um item pode ser um valor atômico ou um nó.  
  
## <a name="constructing-sequences"></a>Construindo sequências  
 Você pode usar o operador vírgula para construir uma sequência que concatena itens em uma única sequência.  
  
 Uma sequência pode conter valores duplicados. As sequências aninhadas, uma sequência dentro de uma sequência, são recolhidas. Por exemplo, a sequência (1, 2, (3, 4, (5))) se torna (1, 2, 3, 4, 5). Estes são exemplos de construção de sequências.  
  
### <a name="example-a"></a>Exemplo A  
 A consulta a seguir retorna uma sequência de cinco valores atômicos:  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3,4,5)')  
go  
-- result 1 2 3 4 5  
```  
  
 A consulta a seguir retorna uma sequência de dois nós:  
  
```  
-- sequence of 2 nodes  
declare @x xml  
set @x=''  
select @x.query('(<a/>, <b/>)')  
go  
-- result  
<a />  
<b />  
```  
  
 A consulta a seguir retorna um erro, pois você está construindo uma sequência de valores atômicos e nós. Esta é uma sequência heterogênea e sem-suporte.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1, 2, <a/>, <b/>)')  
go  
```  
  
### <a name="example-b"></a>Exemplo B  
 A consulta a seguir constrói uma sequência de valores atômicos combinando quatro sequências de comprimento diferente em uma única sequência.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2),10,(),(4, 5, 6)')  
go  
-- result = 1 2 10 4 5 6  
```  
  
 Você pode classificar a sequência usando FLOWR e ORDER BY:  
  
```  
declare @x xml  
set @x=''  
select @x.query('for $i in ((1,2),10,(),(4, 5, 6))  
                  order by $i  
                  return $i')  
go  
```  
  
 Você pode contar os itens na sequência usando o **fn:count()** função.  
  
```  
declare @x xml  
set @x=''  
select @x.query('count( (1,2,3,(),4) )')  
go  
-- result = 4  
```  
  
### <a name="example-c"></a>Exemplo C  
 A consulta a seguir é especificada na coluna AdditionalContactInfo do **xml** tipo na tabela Contact. Essa coluna armazena informações adicionais do contato, como um ou mais números de telefone, números de pager e endereços. O \<telephoneNumber >, \<pager >, e outros nós podem aparecer em qualquer lugar no documento. A consulta constrói uma sequência que contém todos os a \<telephoneNumber > filhos do nó de contexto, seguido de \<pager > filhos. Observe o uso do operador de sequência vírgula na expressão de retorno, `($a//act:telephoneNumber, $a//act:pager)`.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo   
   return ($a//act:telephoneNumber, $a//act:pager)  
') As Result  
FROM Person.Contact  
WHERE ContactID=3  
```  
  
 Este é o resultado:  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:pager xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>999-555-1244</act:number>  
  <act:SpecialInstructions>  
Page only in case of emergencies.  
</act:SpecialInstructions>  
</act:pager>  
```  
  
## <a name="filtering-sequences"></a>Filtrando sequências  
 Você pode filtrar a sequência retornada por uma expressão adicionando um predicado à expressão. Para obter mais informações, consulte [expressões de caminho &#40; XQuery &#41; ](../xquery/path-expressions-xquery.md). Por exemplo, a consulta a seguir retorna uma sequência de três nós do elemento <`a`>:  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a')  
```  
  
 Este é o resultado:  
  
```  
<a attrA="1">111</a>  
<a />  
<a />  
```  
  
 Para recuperar apenas os elementos <`a`> que têm o atributo attrA, especifique um filtro no predicado. A sequência resultante terá só um elemento <`a`>.  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a[@attrA]')  
```  
  
 Este é o resultado:  
  
```  
<a attrA="1">111</a>  
```  
  
 Para obter mais informações sobre como especificar predicados em uma expressão de caminho, consulte [especificando predicados em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-predicates.md).  
  
 O exemplo a seguir constrói uma expressão de sequência de subárvores e depois aplica um filtro à sequência.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
<c>top level c</c>  
<d></d>  
'  
```  
  
 A expressão em `(/a, /b)` constrói uma sequência com subárvores `/a` e `/b` e da sequência resultante a expressão filtra o elemento `<c>`.  
  
```  
SELECT @x.query('  
  (/a, /b)/c  
')  
```  
  
 Este é o resultado:  
  
```  
<c>C under a</c>  
<c>C under b</c>  
```  
  
 O exemplo a seguir aplica um filtro de predicado. A expressão localiza os elementos <`a`> e <`b`> que contêm o elemento <`c`>.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
  
<c>top level c</c>  
<d></d>  
'  
SELECT @x.query('  
  (/a, /b)[c]  
')  
```  
  
 Este é o resultado:  
  
```  
<a>  
  <c>C under a</c>  
</a>  
<b>  
  <c>C under b</c>  
</b>  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Não há suporte para a expressão de intervalo XQuery.  
  
-   As sequências devem ser homogêneas. Especificamente, todos os itens em uma sequência devem ser nós ou valores atômicos. Isso é verificado estaticamente.  
  
-   Não há suporte para a combinação de sequências de nó usando operadores de união, intersecção ou exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  

