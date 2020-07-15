---
title: Especificar um elemento raiz para uso com FOR XML | Microsoft Docs
description: Veja um exemplo de consulta que especifica a opção RAIZ da cláusula FOR XML para solicitar somente um elemento de nível superior no XML resultante.
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: cf32be608e844036893b7c7dbf42ba76db0c203f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632647"
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>Exemplo: Especificando um elemento raiz para o XML gerado pela FOR XML
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Ao especificar a opção `ROOT` na consulta `FOR XML` , é possível solicitar um único elemento de nível superior para o XML resultante, conforme mostrado nesta consulta. O argumento especificado para a política `ROOT` fornece o nome do elemento raiz.  
  
## <a name="example"></a>Exemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
GO
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
 [Usar o modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
