---
title: "Usar OPENJSON com um esquema explícito (SQL Server) | Microsoft Docs"
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
- OPENJSON, with explicit schema
ms.assetid: 9c1c3bfb-e1ad-4659-b94f-722b0848d5a2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9909c0d9d42e40e09517d60bb23906a49c8e9161
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="use-openjson-with-an-explicit-schema-sql-server"></a>Usar OPENJSON com um esquema explícito (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use **OPENJSON** com um esquema explícito para retornar uma tabela formatada como especificado na cláusula WITH.  
  
 Aqui estão alguns exemplos que usam **OPENJSON** com um esquema explícito. Para obter mais informações e mais exemplos, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="example---use-the-with-clause-to-format-the-output"></a>Exemplo - Usar a cláusula WITH para formatar a saída  
 A consulta a seguir retorna os resultados mostrados na tabela a seguir. Observe como a cláusula AS JSON faz com que valores sejam retornados como objetos JSON em vez de valores escalares em col5 e array_element.  
  
```tsql  
DECLARE @json NVARCHAR(MAX) =
N'{"someObject":   
    {"someArray":  
      [  
          {"k1": 11, "k2": null, "k3": "text"},  
          {"k1": 21, "k2": "text2", "k4": { "data": "text4" }},  
          {"k1": 31, "k2": 32},  
          {"k1": 41, "k2": null, "k4": { "data": false }}     
       ]  
    }  
 }'  
   
SELECT * FROM  
 OPENJSON(@json, N'lax $.someObject.someArray')  
WITH ( k1 int,   
        k2 varchar(100),  
        col3 varchar(6) N'$.k3',  
        col4 varchar(10) N'lax $.k4.data',  
        col5 nvarchar(MAX) N'lax $.k4' AS JSON, 
        array_element nvarchar(MAX) N'$' AS JSON  
 )  
```  
  
 **Resultados**  
  
|k1|k2|col3|col4|col5|array_element|  
|--------|--------|----------|----------|----------|--------------------|  
|11|*NULL*|"texto"|*NULL*|*NULL*|{"k1": 11, "k2": nulo, "k3": "texto"}|  
|21|"texto2"|*NULL*|"texto4"|{ "dados": "texto4" }|{"k1": verdadeiro, "k2": "texto2", "k4": { "dados": "texto4" } }|  
|31|"32"|*NULL*|*NULL*|*NULL*|{"k1": 31, "k2": 32 }|  
|41|*NULL*|*NULL*|false|{ "dados": falso }|{"k1": 41, "k2": nulo,       "k4": { "dados": falso }    }|  
  
## <a name="example---load-json-into-a-includessnoversionincludesssnoversion-mdmd-table"></a>Exemplo – Carregar o objeto JSON em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 O exemplo a seguir carrega um objeto JSON inteiro em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```tsql  
DECLARE @json NVARCHAR(MAX) = '{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50))  
```  
  
## <a name="see-also"></a>Consulte também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

