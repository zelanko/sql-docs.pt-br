---
title: Sequência e QNames (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
caps.latest.revision: 22
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 30d463050f129bbc232c0261f1d6af481744ef93
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37990005"
---
# <a name="sequence-and-qnames-xquery"></a>Sequência e QNames (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve os seguintes conceitos fundamentais do XQuery:  
  
-   Sequência  
  
-   QNames e namespaces predefinidos  
  
## <a name="sequence"></a>Sequência  
 No XQuery, o resultado de uma expressão é uma sequência constituída de uma lista de nós e instâncias XML de tipos atômicos XSD. Uma entrada individual em uma sequência é chamada de item. Um item em uma sequência pode ser qualquer um dos seguintes:  
  
-   Um nó como um elemento, atributo, texto, instrução de processamento, comentário ou documento  
  
-   Um valor atômico como uma instância de um tipo simples de XSD  
  
 Por exemplo, a consulta a seguir constrói uma sequência de dois itens de nós do elemento:  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 Este é o resultado:  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 Na consulta anterior, a vírgula (`,`) no fim da construção `<step1>` é o construtor de sequência e é necessária. Os espaços em branco nos resultados são introduzidos apenas para fins ilustrativos e são inclusos em todos os resultados dos exemplos nessa documentação.  
  
 A seguir são apresentadas informações adicionais de seu interesse sobre sequências:  
  
-   Se uma consulta resultar em uma sequência que contém outra sequência, a sequência contida é simplificada na sequência de contêiner. Por exemplo, a sequência ((1,2, (3,4,5)),6) é simplificada no modelo de dados como (1, 2, 3, 4, 5, 6).  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   Uma sequência vazia é uma sequência que não contém nenhum item. Ela é representada como "()".  
  
-   Uma sequência com apenas um item pode ser tratada como um valor atômico, e vice-versa. Ou seja, (1) = 1.  
  
 Nessa implementação, a sequência deve ser homogênea. Ou seja, ou você tem uma sequência de valores atômicos ou uma sequência de nós. Por exemplo, as seguintes são sequências válidas:  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 A consulta a seguir retorna um erro, porque não há suporte para sequências heterogêneas.  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 Todo identificador em um XQuery é um QName. Um QName é constituído de um prefixo de namespace e de um nome local. Nessa implementação, os nomes de variáveis no XQuery são QNames e eles não podem ter prefixos.  
  
 Considere o exemplo a seguir em que uma consulta é especificada em relação a uma não tipado **xml** variável:  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 Na expressão (`/Root/a`), `Root` e `a` são QNames.  
  
 No exemplo a seguir, uma consulta é especificada em relação a um tipado **xml** coluna. A consulta itera em todos os \<etapa > elementos no primeiro local de centro de trabalho.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Na expressão da consulta, observe o seguinte:  
  
-   `AWMI root`, `AWMI:Location`, `AWMI:step`e `$Step` são todos QNames. `AWMI` é um prefixo, e `root`, `Location` e `Step` são todos nomes de locais.  
  
-   A variável `$step` é um QName e não tem um prefixo.  
  
 Os namespaces a seguir são predefinidos para uso com suporte do Xquery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|Prefixo|URI|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(nenhum prefixo)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|http://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`http://www.w3.org/XML/1998/namespace`|  
|(nenhum prefixo)|`http://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 Cada banco de dados que você cria tem o **sys** coleção de esquemas XML. Ele reserva esses esquemas para que eles possam ser acessados de qualquer coleção de esquemas XML criadas pelo usuário.  
  
> [!NOTE]  
>  Esta implementação não oferece suporte a `local` prefixo conforme descrito na especificação do XQuery em http://www.w3.org/2004/07/xquery-local-functions.  
  
## <a name="see-also"></a>Consulte também  
 [Fundamentos de XQuery](../xquery/xquery-basics.md)  
  
  
