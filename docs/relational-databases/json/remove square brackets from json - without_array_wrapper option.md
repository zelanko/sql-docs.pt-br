---
title: "Remover os colchetes da sa&#237;da de JSON com a op&#231;&#227;o WITHOUT_ARRAY_WRAPPER (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WITHOUT_ARRAY_WRAPPER"
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Remover os colchetes da sa&#237;da de JSON com a op&#231;&#227;o WITHOUT_ARRAY_WRAPPER (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para remover, por padrão, os colchetes que envolvem a saída JSON da cláusula **FOR JSON**, especifique a opção **WITHOUT_ARRAY_WRAPPER**. Use esta opção para gerar um único objeto JSON como saída.  
  
 Se você não especificar essa opção, a saída JSON será colocada entre colchetes.  
  
## Exemplos  
 O exemplo a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER**.  
  
 **Consulta**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 **Resultado** Com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{ "year":2015, "month":12, "day":15 }  
```  
  
 **Resultado** Sem a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[ { "year":2015, "month":12, "day":15 } ]  
```  
  
 Veja outro exemplo de uma cláusula **FOR JSON** com a opção **WITHOUT_ARRAY_WRAPPER**.  
  
 **Consulta**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 **Resultado** Com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{  
    "SalesOrderNumber":"SO43660",  
    "OrderDate":"2011-05-31T00:00:00",  
    "Status":5  
}  
```  
  
 **Resultado** Sem a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[  
    {  
        "SalesOrderNumber":"SO43660",  
        "OrderDate":"2011-05-31T00:00:00",  
        "Status":5  
    }  
]  
```  
  
## Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  