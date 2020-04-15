---
title: Executando consultas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93984308c9b661af8e7263ed1c3c0a54e1b35eab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297986"
---
# <a name="executing-queries-odbc"></a>Executando consultas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Depois que um aplicativo ODBC inicializa um identificador de conexão e conecta-se a uma fonte de dados, ele aloca um ou mais identificadores de instrução no identificador de conexão. O aplicativo pode, então, executar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instruções na alça da instrução. A sequência geral de eventos na execução de uma instrução SQL é:  
  
1.  Definir quaisquer atributos de instrução necessários.  
  
2.  Construir a instrução.  
  
3.  Executar a instrução.  
  
4.  Recuperar quaisquer conjuntos de resultados.  
  
 Depois que um aplicativo recuperar todas as linhas em todos os conjuntos de resultados retornados pela instrução SQL, ele pode executar outra consulta no mesmo identificador de instrução. Se um aplicativo determinar que não é necessário recuperar todas as linhas em um determinado conjunto de resultados, ele poderá cancelar o resto do resultado definido ligando para [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) ou [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md).  
  
 Se você precisar executar a mesma instrução SQL várias vezes com dados diferentes em um aplicativo ODBC, use um marcador de parâmetros indicado por um ponto de interrogação (?) na construção de uma instrução SQL:  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 Cada marcador de parâmetro pode então ser vinculado a uma variável de programa chamando [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md).  
  
 Depois que todas as instruções SQL forem executadas e seus conjuntos de resultados forem processados, o aplicativo liberará a alça de instrução.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver Cliente Nativo ODBC suporta várias alças de declaração por cabo de conexão. As transações são gerenciadas no nível da conexão. Dessa forma, todo o trabalho realizado em todos os identificadores de instrução em um único identificador de conexão é gerenciado como parte da mesma transação.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Alocando um identificador de instrução](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [Construindo uma Declaração SQL &#40;o&#41;da ODBC](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [Construindo instruções SQL para cursores](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [Usando parâmetros de instrução](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [Execução de Declarações &#40;&#41;Da ODBC](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [Liberando um identificador de instrução](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
