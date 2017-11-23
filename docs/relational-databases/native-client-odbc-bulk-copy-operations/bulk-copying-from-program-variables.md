---
title: "Cópia em massa de variáveis de programa | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 935fad0a9e40cd85b9ec13a62d6c28cd8e215d64
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="bulk-copying-from-program-variables"></a>Cópia em massa de variáveis do programa
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Você pode fazer cópias em massa diretamente de variáveis de programa. Depois de alocar variáveis para manter os dados de uma linha e chamar [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para iniciar a cópia em massa, chame [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para cada coluna especificar o local e o formato da variável de programa a ser associado com a coluna. Preenchimento de cada variável de dados, em seguida, chame [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para enviar uma linha de dados para o servidor. Repita o processo de encher as variáveis e chamar **bcp_sendrow** até que todas as linhas foram enviadas para o servidor, em seguida, chame [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) para especificar que a operação foi concluída.  
  
 O **bcp_bind***pData* parâmetro contém o endereço da variável que está sendo associada à coluna. Os dados de cada coluna podem ser armazenados de uma destas duas formas:  
  
-   Aloque uma variável para manter os dados.  
  
-   Aloque uma variável de indicador seguida imediatamente pela variável de dados.  
  
 A variável de indicador indica o comprimento dos dados para colunas de comprimento variável e também indica valores NULL se a coluna permitir NULLs. Se apenas uma variável de dados for usada, então o endereço dessa variável será armazenado no **bcp_bind***pData* parâmetro. Se uma variável de indicador for usada, o endereço da variável de indicador é armazenado no **bcp_bind***pData* parâmetro. As funções de cópia em massa calculam o local da variável de dados, adicionando o **bcp_bind***cbIndicator* e *pData* parâmetros.  
  
 **bcp_bind** dá suporte a três métodos para lidar com dados de comprimento variável:  
  
-   Use *cbData* com apenas uma variável de dados. Coloque o comprimento dos dados de *cbData*. Cada vez que o comprimento dos dados em massa de ser copiado alterações, chame [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)redefinir *cbData*. Se um dos outros dois métodos estiver sendo usado, especifique SQL_VARLEN_DATA para *cbData*. Se todos os valores de dados que são fornecidos para uma coluna forem NULL, especifique SQL_NULL_DATA para *cbData*.  
  
-   Use variáveis de indicador. Como cada valor de dados novo é movido na variável de dados, armazene o comprimento do valor na variável de indicador. Se um dos outros dois métodos estiver sendo usado, especifique 0 para *cbIndicator*.  
  
-   Use ponteiros de terminador. Carga de **bcp_bind***pTerm* parâmetro com o endereço do padrão de bit que finaliza os dados. Se um dos outros dois métodos estiver sendo usado, especifique NULL para *pTerm*.  
  
 Todos os três métodos podem ser usados no mesmo **bcp_bind** chamada, caso em que a especificação que resulte na menor quantidade de dados sendo copiados é usada.  
  
 O **bcp_bind***tipo* identificadores de tipo de dados do parâmetro usa DB-Library, não ODBC identificadores de tipo de dados. Identificadores de tipo de dados DB-Library são definidos em SQLNCLI. h para uso com o ODBC **bcp_bind** função.  
  
 As funções de cópia em massa não têm suporte para todos os tipos de dados do ODBC C. Por exemplo, as funções de cópia em massa não dão suporte à estrutura ODBC SQL_C_TYPE_TIMESTAMP, portanto, use [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) ou [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para converter dados do ODBC SQL_TYPE_TIMESTAMP a uma variável SQL_C_CHAR. Se você usar **bcp_bind** com um *tipo* parâmetro sqlcharacter para associar a variável para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** coluna, as funções de cópia em massa convertem o cláusula de escape de carimbo de hora na variável de caractere para o formato de data e hora adequado.  
  
 A tabela a seguir lista os tipos de dados recomendado para usar mapeando de um tipo de dados SQL ODBC para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados.  
  
|Tipo de dados do ODBC SQLz|Tipos de dados do ODBC C|bcp_bind *tipo* parâmetro|Tipo de dados do SQL Server|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**caractere**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **variável de caractere**<br /><br /> **char variados**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**texto**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **DEC**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (assinado)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (sem-sinal)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (assinado)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (sem-sinal)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **inteiro**|  
|SQL_INTEGER (assinado)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **inteiro**|  
|SQL_INTEGER (não assinado)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **DEC**|  
|SQL_BIGINT (assinado e sem-sinal)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **a variável binário**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**imagem**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não entraram **tinyint**sem sinal **smallint**, ou não assinado **int** tipos de dados. Para evitar a perda de valores de dados ao migrar estes tipos de dados, crie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela com o próximo tipo de dados inteiro maior. Para impedir que os usuários adicionem posteriormente valores fora da faixa permitida pelo tipo de dados original, aplique uma regra à coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fim de restringir os valores permitidos para a faixa com suporte do tipo de dados na fonte original:  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não dá suporte para tipos de dados de intervalo diretamente. Um aplicativo pode, no entanto, armazenar sequências de escape de intervalo como cadeias de caracteres em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna de caracteres. O aplicativo pode lê-los para uso posterior, mas eles não podem ser usados em instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 As funções de cópia em massa podem ser usadas para carregar rapidamente dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenham sido lidos de uma fonte de dados ODBC. Use [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) para associar as colunas de um conjunto de resultados para variáveis de programa, em seguida, use **bcp_bind** para associar as mesmas variáveis de programa para uma operação de cópia em massa. Chamando [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) ou **SQLFetch** busca uma linha de dados da fonte de dados ODBC em variáveis de programa e chamar [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) copia os dados em massa as variáveis de programa para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Um aplicativo pode usar o [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) função sempre que precisar alterar o endereço da variável de dados especificada originalmente no **bcp_bind** *pData* parâmetro. Um aplicativo pode usar o [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) função sempre que precisar alterar o comprimento de dados especificado originalmente no **bcp_bind***cbData* parâmetro.  
  
 Você não pode ler dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em variáveis de programa usando a cópia em massa; há nada como uma função "bcp_readrow". Você só pode enviar dados do aplicativo para o servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
