---
title: 'Exemplo: especificando um elemento raiz para o XML gerado por FOR XML | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fcdaa21682f435291c6e491cc1ac0d230831b81e
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>Exemplo: Especificando um elemento raiz para o XML gerado por FOR XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Ao especificar a opção `ROOT` na consulta `FOR XML` , é possível solicitar um único elemento de nível superior para o XML resultante, conforme mostrado nesta consulta. O argumento especificado para a política `ROOT` fornece o nome do elemento raiz.  
  
## <a name="example"></a>Exemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 Este é o resultado:  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
