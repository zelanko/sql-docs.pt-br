---
title: True Function (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 646bcb8058a0a4455c71aecd6a4f907c7dd5f332
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740364"
---
# <a name="boolean-constructor-functions---true-xquery"></a>Funções do Construtor Booliano – true (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor xs:boolean True. Isso é equivalente a `xs:boolean("1")`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. Usando a função booliana true() XQuery  
 O exemplo a seguir consulta uma não tipado **xml** variável. A expressão na **Value ()** método retorna um valor booliano **True ()** se "aaa" é o valor do atributo. O **Value ()** método o **xml** converte o valor booliano em um pouco de tipo de dados e o retorna.  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 No exemplo a seguir, a consulta é especificada em relação a um tipado **xml** coluna. A expressão `if` verifica o valor Booliano digitado do elemento <`ROOT`> e retorna o XML construído. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquemas XML que define o elemento <`ROOT`> do tipo xs:boolean.  
  
-   Cria uma tabela com um tipado **xml** coluna usando a coleção de esquemas XML.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções do construtor booliano &#40;XQuery&#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
