---
title: Colunas que contêm um valor nulo por padrão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3aaa7cc6fb40c2f600e734cb3e2250a40e15d63e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717296"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>Colunas que contêm um valor nulo por padrão
  Por padrão, um valor nulo em uma coluna é mapeado para a ausência do atributo, nó ou elemento. Esse comportamento padrão pode ser substituído solicitando XML centrado em elemento usando a diretiva ELEMENTS e especificando XSINIL para solicitar a adição de elementos para valores NULL, conforme mostrado na consulta a seguir:  
  
```  
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 O resultado é mostrado a seguir. Observe que se XSINIL não for especificado, o elemento <`Middle`> estará ausente.  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](use-path-mode-with-for-xml.md)  
  
  
