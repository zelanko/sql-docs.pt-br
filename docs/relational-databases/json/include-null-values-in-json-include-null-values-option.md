---
title: Incluir valores nulos na opção JSON – INCLUDE_NULL_VALUES | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0c2046a1fb1e3dfb2abfdfe113ebc45be78f729e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32936301"
---
# <a name="include-null-values-in-json---includenullvalues-option"></a>Incluir valores nulos na opção JSON – INCLUDE_NULL_VALUES
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-blog-posts"></a>Postagens no blog da Microsoft  
  
Para ver soluções específicas, casos de uso e recomendações, consulte as [postagens no blog](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre o suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure.  

### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

## <a name="see-also"></a>Consulte Também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
