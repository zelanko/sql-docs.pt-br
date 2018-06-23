---
title: Escrever instruções Transact-SQL internacionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
caps.latest.revision: 35
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cbd8342f74668ba52ff837336bd9b245480f489f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122852"
---
# <a name="write-international-transact-sql-statements"></a>Gravar instruções Transact-SQL internacionais
  Os bancos de dados e aplicativos de bancos de dados que usam instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] serão mais portáteis de um idioma para outro, ou darão suporte a vários idiomas, se as diretrizes a seguir forem cumpridas.  
  
-   Substitua todos os usos do `char`, `varchar` e tipos de dados `text` por `nchar`, `nvarchar` e `nvarchar(max)`. Fazendo isto, você não deve considerar assuntos relacionados à conversão de página de código. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](collation-and-unicode-support.md).  
  
-   Ao executar comparações e operações de mês e dia da semana, use as partes de data numérica em vez de cadeias de caracteres de nomes. Configurações de linguagem diferentes retornam nomes diferentes para os meses e dias de semana. Por exemplo, DATENAME(MONTH,GETDATE()) retorna May quando o idioma está definido como inglês dos EUA, retorna Mai quando o idioma é definido como alemão e retorna mai quando o idioma é definido como francês. No lugar, use uma função como DATEPART que usa o número do mês ao invés do nome. Use os nomes DATEPART quando for construir conjuntos de resultados a serem exibidos a um usuário, pois os nomes de datas geralmente são mais significativos que uma representação numérica. Porém, não codifique qualquer lógica que dependa dos nomes exibidos sendo modificados em um idioma específico.  
  
-   Quando especificar datas em comparações ou para entradas nas instruções INSERT ou UPDATE, use as constantes que são interpretadas da mesma maneira de todas as definições de linguagem:  
  
    -   Os aplicativos ODBC, ADO e OLE DB devem usar as cláusulas de fuga ODBC timestamp, data e hora para:  
  
         **{ ts'** aaaa**-***mm***-***dd**hh ***:*** mm ***:*** ss *[**.***fff*] **'}** tal como: **{ ts'** 1998**-** 09**-** 24 10 **:** 02 **:** 20 **' }**  
  
         **{ d'** *yyyy* **-** *mm* **-** *dd* **'}** como: **{ d'** 1998**-** 09**-** 24 **'}**  
  
         **{ t'** *hh* **:** *mm* **:** *ss* **'}** como: **{ t'** 10:02:20 **'}**  
  
    -   Os aplicativos que usam outras APIs ou scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , procedimentos armazenados e gatilhos, devem usar as sequências numéricas de não separadas. Por exemplo, *yyyymmdd* como 19980924.  
  
    -   Aplicativos que usam outras APIs ou [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts, procedimentos armazenados e gatilhos devem usar a instrução CONVERT com um parâmetro de estilo explícito para todas as conversões entre o `time`, `date`, `smalldate`, `datetime`, **datetime2**, e `datetimeoffset` tipos de dados e tipos de dados de cadeia de caracteres. Por exemplo, a instrução a seguir é interpretada da mesma maneira para todas configurações de conexão de formato de data ou de linguagem:  
  
        ```  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
         Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
  
