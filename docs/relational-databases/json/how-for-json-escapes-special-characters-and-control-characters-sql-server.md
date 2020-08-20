---
description: Como o FOR JSON ignora os caracteres especiais e os caracteres de controle (SQL Server)
title: Como o FOR JSON ignora os caracteres especiais e os caracteres de controle
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c96ae7e539a4a5783d238d71ff94d9e04f179251
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499228"
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>Como o FOR JSON ignora os caracteres especiais e os caracteres de controle (SQL Server)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este tópico descreve como a cláusula **FOR JSON** de uma instrução **SELECT** do SQL Server ignora os caracteres especiais e representa os caracteres de controle na saída JSON.  

> [!IMPORTANT]
> Esta página descreve o suporte interno para JSON no Microsoft SQL Server. Para obter informações gerais sobre como fazer o escape e a codificação em JSON, consulte a Seção 2.5 da RFC do JSON – [https://www.ietf.org/rfc/rfc4627.txt](https://www.ietf.org/rfc/rfc4627.txt).

## <a name="escaping-of-special-characters"></a>Ignorando os caracteres especiais  
Se os dados de origem contiverem caracteres especiais, a cláusula **FOR JSON** ignorará os caracteres especiais na saída JSON com `\`, conforme mostrado na tabela a seguir. Este escape ocorre nos nomes das propriedades e em seus valores.  
  
|**Caractere especial**|**Saída de escape**|  
|---------------------------|--------------------------|  
|Aspas (")|\\"|  
|Barra invertida (\\)|\\\\|  
|Barra (/)|\\/|  
|Backspace|\b|  
|Avanço de formulário|\f|  
|Nova linha|\n|  
|Retorno de carro|\r|  
|Guia horizontal|\t|  
  
## <a name="control-characters"></a>Caracteres de controle  
Se os dados de origem contiverem caracteres de controle, a cláusula **FOR JSON** fará a codificação na saída JSON no formato `\u<code>`, conforme mostrado na tabela a seguir.  
  
|**Caractere de controle**|**Saída codificada**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>Exemplo  
 Aqui está um exemplo da a saída **FOR JSON** para os dados de origem que inclui caracteres especiais e caracteres de controle.  
  
 Consulta:  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 Resultado:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[Cláusula FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
