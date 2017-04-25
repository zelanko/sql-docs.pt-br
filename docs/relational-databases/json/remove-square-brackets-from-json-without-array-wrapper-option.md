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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea60d5a74c680e9c2aba571a76815f77913da471
ms.lasthandoff: 04/11/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Remover os colchetes da opção do JSON – WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para remover, por padrão, os colchetes que envolvem a saída JSON da cláusula **FOR JSON** , especifique a opção **WITHOUT_ARRAY_WRAPPER** . Use essa opção para gerar um único objeto JSON como saída em vez de uma matriz.  
  
 Se você não especificar essa opção, a saída JSON será colocada entre colchetes.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```tsql  
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
  
 **Resultado** sem a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  
  
 Veja outro exemplo de uma cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Resultado** com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Resultado** sem a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  
  
## <a name="see-also"></a>Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

