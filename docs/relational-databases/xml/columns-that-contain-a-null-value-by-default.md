---
title: Colunas que contêm um valor nulo por padrão | Microsoft Docs
description: Saiba como trabalhar com colunas que contêm um valor nulo por padrão usando a frase de palavra-chave ELEMENTS XSINIL no SQL.
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
ms.openlocfilehash: d6962f6117a857ed5875d503c259b4d54e8dd84d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775606"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>Colunas que contêm um valor nulo por padrão

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
  
  
