---
title: Escrever instruções Transact-SQL internacionais | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2019
ms.prod: sql
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4cbc237ad0df16dbb854fb5bd062d7d37375294f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70913554"
---
# <a name="write-international-transact-sql-statements"></a>Gravar instruções Transact-SQL internacionais
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Os bancos de dados e aplicativos de bancos de dados que usam instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] serão mais portáteis de um idioma para outro, ou darão suporte a vários idiomas, se as diretrizes a seguir forem cumpridas.  

-   Começando no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], use:
    -   Os tipos de dados **char**, **varchar** e **varchar (max)** com uma ordenação habilitada para [UTF-8](../../relational-databases/collations/collation-and-unicode-support.md#utf8) e os dados são codificados usando o UTF-8.
    -   Os tipos de dados **nchar**, **nvarchar** e **nvarchar(max)** com a ordenação habilitada para [SC (caractere suplementar)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) e os dados são codificados usando UTF-16. O uso de uma ordenação não SC resulta na codificação de dados usando o UCS-2.      

    Isso evita problemas de conversão de página de código. Para acessar outras considerações, confira [Diferenças de armazenamento entre UTF-8 e UTF-16](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences).  

-   Até [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], substitua todos os usos dos tipos de dados **char**, **varchar** e **varchar (max)** por **nchar**, **nvarchar** e **nvarchar (max)** . Se você estiver usando uma ordenação habilitada para [SC (caractere suplementar)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters), os dados serão codificados usando UTF-16. O uso de uma ordenação não SC resulta na codificação de dados usando o UCS-2. Isso evita problemas de conversão de página de código. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md). 

    > [!IMPORTANT]
    > O tipo de dados **texto** foi preterido e não deve ser usado em novos trabalhos de desenvolvimento. Planeje converter dados de **texto** em **varchar(max)** .
  
-   Ao realizar comparações e operações de mês e dia da semana, use as partes de data numérica em vez de cadeias de caracteres de nomes. Configurações de linguagem diferentes retornam nomes diferentes para os meses e dias de semana. Por exemplo, `DATENAME(MONTH,GETDATE())` retorna `May` quando o idioma é definido como inglês dos EUA, retorna `Mai` quando o idioma é definido como alemão e retorna `mai` quando o idioma é definido como francês. No lugar, use uma função como [DATEPART](../../t-sql/functions/datepart-transact-sql.md) que usa o número do mês ao invés do nome. Use os nomes DATEPART quando for construir conjuntos de resultados a serem exibidos a um usuário, pois os nomes de datas geralmente são mais significativos que uma representação numérica. Porém, não codifique nenhuma lógica que dependa dos nomes exibidos sendo modificados em um idioma específico.  
  
-   Quando especificar datas em comparações ou para entradas nas instruções INSERT ou UPDATE, use as constantes que são interpretadas da mesma maneira de todas as definições de linguagem:  
  
    -   Os aplicativos ODBC, ADO e OLE DB devem usar as cláusulas de fuga ODBC timestamp, data e hora para:  
  
         **{ ts'** _yyyy_ **-** _mm_ **-** _dd_ _hh_ **:** _mm_ **:** _ss_ [ **.** _fff_] **'}** como: **{ ts'1998-09-24 10:02:20'}**  
  
         **{ d'** _yyyy_ **-** _mm_ **-** _dd_ **'}** como: **{ d'1998-09-24'}**
  
         **{ t'** _hh_ **:** _mm_ **:** _ss_ **'}** como: **{ t'10:02:20'}**  
  
    -   Os aplicativos que usam outras APIs ou scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , procedimentos armazenados e gatilhos, devem usar as sequências numéricas de não separadas. Por exemplo, *yyyymmdd* como 19980924.  
  
    -   Os aplicativos que usam outras APIs ou que usam scripts, procedimentos armazenados e gatilhos [!INCLUDE[tsql](../../includes/tsql-md.md)] devem usar a instrução [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) com um parâmetro de estilo explícito para todas as conversões entre os tipos de dados **time**, **date**, **smalldate**, **datetime**, **datetime2** e **datetimeoffset** e os tipos de dados da cadeia de caracteres. Por exemplo, a instrução a seguir é interpretada da mesma maneira para todas configurações de conexão de formato de data ou de linguagem:  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)      
