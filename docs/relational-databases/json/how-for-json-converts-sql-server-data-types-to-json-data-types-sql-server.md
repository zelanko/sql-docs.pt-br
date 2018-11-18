---
title: Como FOR JSON converte tipos de dados do SQL Server para tipos de dados JSON (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/07/2016
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 80bf0fa78d101f853b04793c1084a69a6f6bdd00
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661171"
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
  
Para ver soluções específicas, casos de uso e recomendações, consulte as [postagens no blog](https://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre o suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure.  

### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
