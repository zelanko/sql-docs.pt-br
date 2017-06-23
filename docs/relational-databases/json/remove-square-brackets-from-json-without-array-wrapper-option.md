---
title: "Remover os colchetes da opção do JSON – WITHOUT_ARRAY_WRAPPER | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 36e612b6c3759d968687d8ba35286c399de02a74
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Remover os colchetes da opção do JSON – WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Para remover, por padrão, os colchetes que envolvem a saída JSON da cláusula **FOR JSON** , especifique a opção **WITHOUT_ARRAY_WRAPPER** . Use esta opção com um resultado de linha única para gerar um único objeto JSON como saída em vez de uma matriz com um único elemento.

Se você usar essa opção com um resultado de várias linhas, a saída resultante não é JSON válido devido os vários elementos e os colchetes ausentes.  
  
## <a name="example-single-row-result"></a>Exemplo (resultados de uma linha)  
O exemplo a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Resultado** com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Resultado** (padrão) sem o **WITHOUT_ARRAY_WRAPPER** opção  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>Exemplo (resultados de várias linhas)
Veja outro exemplo de uma cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER** . Este exemplo produz um resultado de várias linhas. A saída não é JSON válido devido os vários elementos e os colchetes ausentes.
  
 **Consulta**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Resultado** com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Resultado** (padrão) sem o **WITHOUT_ARRAY_WRAPPER** opção  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para muitas soluções específicas, casos de uso e recomendações, consulte o [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no banco de dados SQL Azure por Jovan Popovic, gerente de programas da Microsoft.
  
## <a name="see-also"></a>Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

