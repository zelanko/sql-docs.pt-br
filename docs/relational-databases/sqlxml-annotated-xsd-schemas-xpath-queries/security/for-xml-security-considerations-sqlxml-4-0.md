---
title: Considerações sobre segurança de FOR XML (SQLXML)
description: Saiba mais sobre as considerações de segurança importantes ao especificar o modo FOR XML AUTO no SQLXML 4,0.
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4f09792ba8f6747cfec97b065a9bc40ebc143217
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689418"
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>Considerações de segurança de FOR XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O modo FOR XML AUTO gera uma hierarquia de XML na qual os nomes de elemento mapeiam para nomes de tabela e nomes de atributo mapeiam para nomes de coluna. Dessa forma, a tabela e as informações de coluna do banco de dados são expostas. Você pode ocultar as informações do banco de dados quando usar modo AUTO (formatação no lado de servidor) especificando aliases de coluna e da tabela na consulta. Esses aliases são retornados no documento XML resultante como nomes de elemento e atributos.  
  
 Por exemplo, a seguinte consulta especifica o modo de AUTO; portanto, a formatação XML é feita no servidor:  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 No documento XML resultante, os aliases são usados para nomes do elemento e do atributo:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 Quando você usar modo NESTED (formatação no lado do cliente), só são retornados aliases para atributos no documento XML resultante. Os nomes das tabelas base são sempre retornados como nomes de elemento. Por exemplo, a seguinte consulta especifica o modo NESTED:  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 No documento XML resultante, os nomes das tabelas base são retornados como nomes de elemento, e os aliases da tabela não são usados:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
