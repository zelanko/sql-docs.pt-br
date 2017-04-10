---
title: "Incluir valores nulos em uma sa&#237;da JSON com a op&#231;&#227;o INCLUDE_NULL_VALUES (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "INCLUDE_NULL_VALUES (FOR JSON)"
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# Incluir valores nulos em uma sa&#237;da JSON com a op&#231;&#227;o INCLUDE_NULL_VALUES (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para incluir valores nulos na saída JSON da cláusula **FOR JSON**, especifique a opção **INCLUDE_NULL_VALUES**.  
  
 Se você não especificar a opção **INCLUDE_NULL_VALUES**, a saída JSON não inclui propriedades para valores que são nulos nos resultados da consulta.  
  
## Exemplos  
 O exemplo a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **INCLUDE_NULL_VALUES**.  
  
|Sem a opção **INCLUDE_NULL_VALUES**|Com a opção **INCLUDE_NULL_VALUES**|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 Veja outro exemplo de uma cláusula **FOR JSON** com a opção **INCLUDE_NULL_VALUES**.  
  
 **Consulta**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES  
```  
  
 **Resultado**  
  
```json  
[   
   {"name": "John",  "surname": null },  
   {"name": "Jane",  "surname": "Doe"}  
]  
```  
  
## Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  