---
title: Função true (XQuery) | Microsoft Docs
description: Saiba mais sobre a função XQuery true () que retorna o valor booliano true.
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 8dc3582cb34c80f488005f5a2eaf1c6022c5e1be
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035789"
---
# <a name="boolean-constructor-functions---true-xquery"></a>Funções do Construtor Booliano – true (XQuery)
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  Retorna o valor xs:boolean True. Isso é equivalente a `xs:boolean("1")`.  
  
## <a name="syntax"></a>Syntax  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são armazenadas em várias colunas de tipo **XML** no banco de dados AdventureWorks.  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>a. Usando a função booliana true() XQuery  
 O exemplo a seguir consulta uma variável **XML** não tipada. A expressão no método **Value ()** retorna booliano **true ()** se "AAA" for o valor do atributo. O método **Value ()** do tipo de dados **XML** converte o valor booliano em um bit e o retorna.  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 No exemplo a seguir, a consulta é especificada em uma coluna **XML** com tipo. A `if` expressão verifica o valor booliano digitado do `ROOT` elemento <> e retorna o XML construído, de acordo. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquema XML que define o <`ROOT` elemento> do tipo xs: Boolean.  
  
-   Cria uma tabela com uma coluna **XML** com tipo usando a coleção de esquema XML.  
  
-   Salva uma instância XML na coluna e a consulta.  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de Construtor boolianas &#40;&#41;XQuery ](./xquery-functions-against-the-xml-data-type.md)  
  
