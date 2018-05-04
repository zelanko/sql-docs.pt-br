---
title: True Function (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
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
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7f66609682a91aac4d4b28aaa67412137069d7bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="boolean-constructor-functions---true-xquery"></a>Funções do construtor Boolianas - true (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor xs:boolean True. Isso é equivalente a `xs:boolean("1")`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em instâncias XML que são armazenados em várias **xml** colunas de tipo de banco de dados AdventureWorks.  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. Usando a função booliana true() XQuery  
 O exemplo a seguir consulta sem um tipo **xml** variável. A expressão no **Value ()** método retorna um valor booleano **verdadeiro ()** se "aaa" é o valor do atributo. O **Value ()** método o **xml** converte o valor booliano em algum tipo de dados e o retorna.  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 No exemplo a seguir, a consulta é especificada em relação a um tipo **xml** coluna. A expressão `if` verifica o valor Booliano digitado do elemento <`ROOT`> e retorna o XML construído. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquemas XML que define o elemento <`ROOT`> do tipo xs:boolean.  
  
-   Cria uma tabela com um tipo **xml** coluna por meio da coleção de esquema XML.  
  
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
  
  
