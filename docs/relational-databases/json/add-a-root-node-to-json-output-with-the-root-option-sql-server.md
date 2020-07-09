---
title: Adicionar um nó raiz à saída JSON com a opção ROOT
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- ROOT (FOR JSON)
ms.assetid: b9afa74a-f59f-483e-a178-42be2e9882c9
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 801fd50761c561db67405c5cc47210ba43facdf2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722308"
---
# <a name="add-a-root-node-to-json-output-with-the-root-option-sql-server"></a>Adicionar um nó raiz à saída JSON com a opção ROOT (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Para adicionar um único elemento de nível superior à saída JSON da cláusula **FOR JSON** , especifique a opção **ROOT** .  
  
 Se você não especificar a opção **ROOT** , a saída JSON não incluirá um elemento raiz.  
  
## <a name="examples"></a>Exemplos  
 A tabela a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **ROOT** .  
  
 Os exemplos na tabela a seguir pressupõem que o argumento *RootName* opcional esteja vazio. Se você fornecer um nome para o elemento raiz, esse valor substituirá o valor **root** nos exemplos.  
  
 Sem a opção **ROOT**  
  
```json  
{  
   <<json properties>>  
}  
```  
  
```json  
[  
   <<json array elements>>  
]  
```  
  
 Com a opção **ROOT**  
  
```json  
{   
  "root": {  
   <<json properties>>  
 }  
}  
```  
  
```json  
{   
  "root": [  
   << json array elements >>  
  ]  
}  
```  
  
 Veja outro exemplo de uma cláusula **FOR JSON** com a opção **ROOT** . Este exemplo especifica um valor para o argumento *RootName* opcional.  
  
 **Consulta**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH, ROOT('info')
```  
  
 **Resultado**  
  
```json  
{
    "info": [{
        "Id": 1,
        "FirstName": "Ken",
        "LastName": "Sánchez",
        "Info": {
            "MiddleName": "J"
        }
    }, {
        "Id": 2,
        "FirstName": "Terri",
        "LastName": "Duffy",
        "Info": {
            "MiddleName": "Lee"
        }
    }, {
        "Id": 3,
        "FirstName": "Roberto",
        "LastName": "Tamburello"
    }, {
        "Id": 4,
        "FirstName": "Rob",
        "LastName": "Walters"
    }, {
        "Id": 5,
        "FirstName": "Gail",
        "LastName": "Erickson",
        "Info": {
            "Title": "Ms.",
            "MiddleName": "A"
        }
    }]
}
```  
  
 **Resultado (sem raiz)**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
 
## <a name="see-also"></a>Consulte Também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
