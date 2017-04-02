---
title: "Como o FOR JSON ignora os caracteres especiais e os caracteres de controle (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, caracteres especiais"
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Como o FOR JSON ignora os caracteres especiais e os caracteres de controle (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este tópico descreve como a cláusula **FOR JSON** ignora os caracteres especiais e representa os caracteres de controle na saída JSON.  
  
## Ignorando os caracteres especiais  
 A cláusula **FOR JSON** ignora os caracteres especiais na saída JSON com `\`, conforme mostrado na tabela a seguir. Este escape ocorre nos nomes das propriedades e em seus valores.  
  
|**Caractere especial**|**Sequência codificada**|  
|---------------------------|--------------------------|  
|Aspas (")|\\"|  
|Barra invertida (\\)|\\\|  
|Barra (/)|\\/|  
|Backspace|\b|  
|Avanço de formulário|\f|  
|Linha nova|\n|  
|Retorno de carro|\r|  
|Guia horizontal|\t|  
  
## Caracteres de controle  
 A cláusula **FOR JSON** representa os caracteres de controle na saída JSON no formato `\u<code>`, conforme mostrado na tabela a seguir.  
  
|**Caractere de controle**|**Sequência codificada**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## Exemplo  
 Aqui está um exemplo de uma cláusula **FOR JSON** que inclui caracteres de escape e controle.  
  
 Consulta:  
  
```tsql  
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
   "KEY\\\t\/\"":"VALUE\\\t\/\r\n\"",  
   "0":"\u0000",  
   "1":"\u0001",  
  "31":"\u001f“  
}  
```  
  
## Consulte também  
 [Formatar os resultados da consulta como JSON com o FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  