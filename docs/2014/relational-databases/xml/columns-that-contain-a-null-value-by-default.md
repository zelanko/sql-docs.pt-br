---
title: Colunas que contêm um valor nulo por padrão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ada1d2f79b74455a8fcd885362c9efc3fb286e71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116324"
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
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo PATH com FOR XML](use-path-mode-with-for-xml.md)  
  
  