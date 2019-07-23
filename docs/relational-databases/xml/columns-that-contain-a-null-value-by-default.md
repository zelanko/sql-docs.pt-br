---
title: Colunas que contêm um valor nulo por padrão | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0fb8b86daedb73f62396e1dc13a06a5a4e2a7bb3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113076"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>Colunas que contêm um valor nulo por padrão

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Por padrão, um valor nulo em uma coluna é mapeado para a ausência do atributo, nó ou elemento. Esse comportamento padrão pode ser substituído com o uso da frase de palavra-chave ELEMENTS XSINIL. Essa frase solicita o XML centrado em elemento. Isso significa que os valores nulos são explicitamente indicados nos resultados retornados. Esses elementos não terão nenhum valor.

A frase ELEMENTS XSINIL é mostrada no exemplo de Transact-SQL SELECT a seguir.

```sql
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
  AND  E.EmployeeID=1
FOR XML PATH, ELEMENTS XSINIL;
```  
  
 O resultado é mostrado a seguir. Observe que se XSINIL não for especificado, o elemento <`Middle`> estará ausente.  
  
```xml
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
