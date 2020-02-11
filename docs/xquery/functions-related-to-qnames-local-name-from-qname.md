---
title: local-name-from-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
author: rothja
ms.author: jroth
ms.openlocfilehash: 765d412b9f3f0395a9bca6fd52c74135ddde3ff4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68004563"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>Funções Relacionadas a QNames – local-name-from-QName
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um xs: NCNAME que representa a parte local de QName especificada por *$ARG*. O resultado será uma sequência vazia se *$ARG* for a sequência vazia.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 É do QName que o nome local deveria ser extraído.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML que são **** armazenadas em várias colunas de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] tipo XML no banco de dados.  
  
 O exemplo a seguir usa a função **local-name-from-QName ()** para recuperar o nome local e as partes de URI de namespace de um valor de tipo QName. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquemas XML.  
  
-   Cria uma tabela com uma coluna do tipo xml. O tipo xml é digitado usando a coleção de esquemas XML.  
  
-   Armazena uma instância XML de exemplo na tabela. Usando o método **Query ()** do tipo de dados XML, a expressão de consulta é executada para recuperar a parte do nome local do valor do tipo QName da instância.  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<root xmlns="QNameXSD" xmlns:a="https://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrieve namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = https://someURI  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções relacionadas a QNames &#40;&#41;XQuery](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
