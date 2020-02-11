---
title: Escrever instruções Transact-SQL internacionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64dc9129373a57de2924b2983e14266a67d4915e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62873521"
---
# <a name="write-international-transact-sql-statements"></a>Gravar instruções Transact-SQL internacionais
  Os bancos de dados e aplicativos de bancos de dados que usam instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] serão mais portáteis de um idioma para outro, ou darão suporte a vários idiomas, se as diretrizes a seguir forem cumpridas.  
  
-   Substitua todos os usos do `char`, `varchar` e tipos de dados `text` por `nchar`, `nvarchar` e `nvarchar(max)`. Fazendo isto, você não deve considerar assuntos relacionados à conversão de página de código. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](collation-and-unicode-support.md).  
  
-   Ao executar comparações e operações de mês e dia da semana, use as partes de data numérica em vez de cadeias de caracteres de nomes. Configurações de linguagem diferentes retornam nomes diferentes para os meses e dias de semana. Por exemplo, DATENAME(MONTH,GETDATE()) retorna May quando o idioma está definido como inglês dos EUA, retorna Mai quando o idioma é definido como alemão e retorna mai quando o idioma é definido como francês. No lugar, use uma função como DATEPART que usa o número do mês ao invés do nome. Use os nomes DATEPART quando for construir conjuntos de resultados a serem exibidos a um usuário, pois os nomes de datas geralmente são mais significativos que uma representação numérica. Porém, não codifique qualquer lógica que dependa dos nomes exibidos sendo modificados em um idioma específico.  
  
-   Quando especificar datas em comparações ou para entradas nas instruções INSERT ou UPDATE, use as constantes que são interpretadas da mesma maneira de todas as definições de linguagem:  
  
    -   Os aplicativos ODBC, ADO e OLE DB devem usar as cláusulas de fuga ODBC timestamp, data e hora para:  
  
         **{TS '** yyyy**-**_mm_**-**_DDHH_**:**_mm_**:**_SS_[**.** _FFF_] **'}** Como: **{TS '** 1998**-** 09**-** 24 10 **:** 02 **:** 20 **'}**  
  
         **{d '** _aaaa_ **-** _mm_ **-** _DD_ **'}** como: **{d '** 1998**-** 09**-** 24 **'}**  
  
         **{T'** _hh_ **:** _mm_ **:** _SS_ **'}** como: **{T'** 10:02:20 **'}**  
  
    -   Os aplicativos que usam outras APIs ou scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , procedimentos armazenados e gatilhos, devem usar as sequências numéricas de não separadas. Por exemplo, *yyyymmdd* como 19980924.  
  
    -   Os aplicativos que usam outras APIs, [!INCLUDE[tsql](../../includes/tsql-md.md)] ou scripts, procedimentos armazenados e gatilhos devem usar a instrução Convert com um parâmetro de estilo explícito para todas as conversões `time`entre `date`os `smalldate`tipos `datetime`de dados,, `datetimeoffset` ,, **datetime2**e tipo de dados de cadeia de caracteres. Por exemplo, a instrução a seguir é interpretada da mesma maneira para todas configurações de conexão de formato de data ou de linguagem:  
  
        ```  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
         Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
  
