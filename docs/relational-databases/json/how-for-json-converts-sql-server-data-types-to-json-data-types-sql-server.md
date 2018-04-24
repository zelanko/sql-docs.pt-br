---
title: Como FOR JSON converte tipos de dados do SQL Server para tipos de dados JSON (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: 11
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 37ce8117a1e21778f5a35cff09a4cd71bf9f2f61
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>Como FOR JSON converte tipos de dados do SQL Server para tipos de dados JSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  A cláusula **FOR JSON** usa as regras a seguir para converter os tipos de dados do SQL Server em tipos JSON na saída JSON.  
  
|Categoria|Tipo de dados do SQL Server|Tipo de dados JSON|  
|--------------|--------------|---------------|  
|Tipos de cadeia de caracteres e caracteres|char, nchar, varchar, nvarchar|cadeia de caracteres|  
|Tipos numéricos|int, bigint, float, decimal, numeric|number|  
|Tipo de Bit|bit|Booliano (verdadeiro ou falso)|  
|Tipos de data e hora|date, datetime, datetime2, time, datetimeoffset|cadeia de caracteres|  
|Tipos binários|varbinary, binary, image, timestamp, rowversion|Cadeia de caracteres codificada em BASE64|  
|Tipos CLR|geometria, geografia, outros tipos CLR|Sem suporte. Estes tipos retornam um erro.<br /><br /> Na instrução SELECT, use CAST ou CONVERT ou use um método ou propriedade CLR para converter os dados de origem em um tipo de dados do SQL Server que pode ser convertido com êxito em um tipo JSON. Por exemplo, use **STAsText()** para o tipo de geometria ou **ToString()** para qualquer tipo CLR. O tipo do valor de saída JSON é derivado do tipo de retorno da conversão aplicada na instrução SELECT.|  
|Outros tipos|uniqueidentifier, money|cadeia de caracteres|  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-blog-posts"></a>Postagens no blog da Microsoft  
  
Para ver soluções específicas, casos de uso e recomendações, consulte as [postagens no blog](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre o suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure.  

### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
