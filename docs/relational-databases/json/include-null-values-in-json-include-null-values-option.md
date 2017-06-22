---
title: "Incluir valores nulos na opção JSON – INCLUDE_NULL_VALUES | Microsoft Docs"
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
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 2cdb047169569041e3a8f7890d8215fd87284959
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="include-null-values-in-json---includenullvalues-option"></a>Incluir valores nulos na opção JSON – INCLUDE_NULL_VALUES
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para incluir valores nulos na saída JSON da cláusula **FOR JSON** , especifique a opção **INCLUDE_NULL_VALUES** .  
  
 Se você não especificar a opção **INCLUDE_NULL_VALUES** , a saída JSON não inclui propriedades para valores que são nulos nos resultados da consulta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **INCLUDE_NULL_VALUES** .  
  
|Sem a opção **INCLUDE_NULL_VALUES**|Com a opção **INCLUDE_NULL_VALUES**|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 Veja outro exemplo de uma cláusula **FOR JSON** com a opção **INCLUDE_NULL_VALUES** .  
  
 **Consulta**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES    
```  
  
 **Resultado**  
  
```json  
[{
    "name": "John",
    "surname": null
}, {
    "name": "Jane",
    "surname": "Doe"
}] 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para muitas soluções específicas, casos de uso e recomendações, consulte o [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no banco de dados SQL Azure por Jovan Popovic, gerente de programas da Microsoft.  

## <a name="see-also"></a>Consulte também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

