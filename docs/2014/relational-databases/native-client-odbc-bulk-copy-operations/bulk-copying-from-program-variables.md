---
title: Cópia em massa de variáveis de programa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5473d741f5144338c99627e1057c51ce116093d6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130286"
---
# <a name="bulk-copying-from-program-variables"></a>Cópia em massa de variáveis do programa
  Você pode fazer cópias em massa diretamente de variáveis de programa. Depois de alocar variáveis para armazenar os dados para uma linha e chamar [bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para iniciar a cópia em massa, chame [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para cada coluna especificar o local e o formato da variável de programa a ser associado com a coluna. Preencher cada variável de dados, em seguida, chame [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para enviar uma linha de dados para o servidor. Repita o processo de encher as variáveis e chamar **bcp_sendrow** até que todas as linhas foram enviadas para o servidor, em seguida, chame [bcp_done](../native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) para especificar que a operação foi concluída.  
  
 O **bcp_bind**_pData_ parâmetro contém o endereço da variável que está sendo associada à coluna. Os dados de cada coluna podem ser armazenados de uma destas duas formas:  
  
-   Aloque uma variável para manter os dados.  
  
-   Aloque uma variável de indicador seguida imediatamente pela variável de dados.  
  
 A variável de indicador indica o comprimento dos dados para colunas de comprimento variável e também indica valores NULL se a coluna permitir NULLs. Se apenas uma variável de dados for usada, em seguida, o endereço dessa variável é armazenado na **bcp_bind**_pData_ parâmetro. Se uma variável de indicador for usada, o endereço da variável de indicador é armazenado na **bcp_bind**_pData_ parâmetro. As funções de cópia em massa calculam o local da variável de dados, adicionando os **bcp_bind**_cbIndicator_ e *pData* parâmetros.  
  
 **bcp_bind** dá suporte a três métodos para lidar com dados de comprimento variável:  
  
-   Use *cbData* com apenas uma variável de dados. Coloque o comprimento dos dados no *cbData*. Cada vez que o comprimento dos dados em massa de ser copiado de alterações, chame [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)redefinir *cbData*. Se um dos outros dois métodos estiver sendo usado, especifique SQL_VARLEN_DATA para *cbData*. Se todos os valores de dados que está sendo fornecidos para uma coluna forem NULL, especifique SQL_NULL_DATA para *cbData*.  
  
-   Use variáveis de indicador. Como cada valor de dados novo é movido na variável de dados, armazene o comprimento do valor na variável de indicador. Se um dos outros dois métodos estiver sendo usado, especifique 0 para *cbIndicator*.  
  
-   Use ponteiros de terminador. Carga do **bcp_bind**_pTerm_ parâmetro com o endereço do padrão de bit que finaliza os dados. Se um dos outros dois métodos estiver sendo usado, especifique NULL para *pTerm*.  
  
 Todos os três métodos que podem ser usados no mesmo **bcp_bind** chamar, caso em que a especificação que resulte na menor quantidade de dados sendo copiados é usada.  
  
 O **bcp_bind**_tipo_ identificadores de tipo de dados do parâmetro usa DB-Library, não ODBC identificadores de tipo de dados. Identificadores de tipo de dados DB-Library são definidos em SQLNCLI. h para uso com o ODBC **bcp_bind** função.  
  
 As funções de cópia em massa não têm suporte para todos os tipos de dados do ODBC C. Por exemplo, as funções de cópia em massa não dão suporte à estrutura ODBC SQL_C_TYPE_TIMESTAMP, portanto, use [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) ou [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para converter dados do ODBC SQL_TYPE_TIMESTAMP a uma variável SQL_C_CHAR. Se você usar **bcp_bind** com um *tipo* parâmetro SQLCHARACTER para associar a variável a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** as funções de cópia em massa de coluna, convertem o cláusula de escape de carimbo de hora na variável de caractere para o formato de data e hora adequado.  
  
 A tabela seguinte lista os tipos de dados indicados para usar mapeando de um tipo de dados do ODBC SQL para um tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tipo de dados do ODBC SQLz|Tipos de dados do ODBC C|bcp_bind *tipo* parâmetro|Tipo de dados do SQL Server|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**character**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **a variável de caractere**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**text**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (assinado)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (sem-sinal)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (assinado)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (sem-sinal)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **inteiro**|  
|SQL_INTEGER (assinado)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **inteiro**|  
|SQL_INTEGER (não assinado)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**|  
|SQL_BIGINT (assinado e sem-sinal)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **a variável binária**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**image**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não entraram **tinyint**sem sinal **smallint**, ou sem sinal **int** tipos de dados. Para impedir a perda de valores de dados ao migrar estes tipos de dados, crie a tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o próximo tipo de dados de inteiro maior. Para impedir que os usuários adicionem posteriormente valores fora da faixa permitida pelo tipo de dados original, aplique uma regra à coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fim de restringir os valores permitidos para a faixa com suporte do tipo de dados na fonte original:  
  
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
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte a tipos de dados de intervalo diretamente. Porém, um aplicativo pode armazenar sequências de escape de intervalo como cadeias de caracteres em uma coluna de caractere do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O aplicativo pode lê-los para uso posterior, mas eles não podem ser usados em instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 As funções de cópia em massa podem ser usadas para carregar dados que tenham sido lidos de uma fonte de dados ODBC rapidamente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para associar as colunas de um conjunto de resultados para variáveis de programa, em seguida, use **bcp_bind** para associar as mesmas variáveis de programa para uma operação de cópia em massa. Chamando [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md) ou **SQLFetch** , em seguida, busca uma linha de dados da fonte de dados ODBC em variáveis de programa e chamar [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) copia os dados em massa as variáveis de programa para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Um aplicativo pode usar o [bcp_colptr](../native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) funcionar sempre que precisar alterar o endereço da variável de dados especificado originalmente na **bcp_bind** _pData_ parâmetro. Um aplicativo pode usar o [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) funcionar sempre que precisar alterar o comprimento de dados especificado originalmente na **bcp_bind**_cbData_ parâmetro.  
  
 Você não pode ler dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em variáveis de programa que usam cópia em massa; não há nada como uma função "bcp_readrow". Você só pode enviar dados do aplicativo para o servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
