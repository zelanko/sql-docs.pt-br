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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7a76f86f1be8012e0df2ed80960095eb83d6882e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021445"
---
# <a name="bulk-copying-from-program-variables"></a>Cópia em massa de variáveis do programa
  Você pode fazer cópias em massa diretamente de variáveis de programa. Depois de alocar variáveis para manter os dados de uma linha e chamar [bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para iniciar a cópia em massa, chame [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para cada coluna para especificar o local e o formato da variável de programa a ser associada à coluna. Preencha cada variável com os dados e, em seguida, chame [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para enviar uma linha de dados para o servidor. Repita o processo de preenchimento das variáveis e a chamada de **bcp_sendrow** até que todas as linhas tenham sido enviadas ao servidor e, em seguida, chame [bcp_done](../native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) para especificar que a operação foi concluída.  
  
 O parâmetro **bcp_bind**_pData_ contém o endereço da variável que está sendo associada à coluna. Os dados de cada coluna podem ser armazenados de uma destas duas formas:  
  
-   Aloque uma variável para manter os dados.  
  
-   Aloque uma variável de indicador seguida imediatamente pela variável de dados.  
  
 A variável de indicador indica o comprimento dos dados para colunas de comprimento variável e também indica valores NULL se a coluna permitir NULLs. Se apenas uma variável de dados for usada, o endereço dessa variável será armazenado no parâmetro **bcp_bind**_pData_ . Se uma variável de indicador for usada, o endereço da variável de indicador será armazenado no parâmetro **bcp_bind**_pData_ . As funções de cópia em massa calculam o local da variável de dados adicionando os parâmetros **bcp_bind**_cbIndicator_ e *pData* .  
  
 o **bcp_bind** dá suporte a três métodos para lidar com dados de comprimento variável:  
  
-   Use *cbData* com apenas uma variável de dados. Coloque o comprimento dos dados em *cbData*. Cada vez que o comprimento dos dados a serem copiados em massa é alterado, chame [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)para redefinir *cbData*. Se um dos outros dois métodos estiver sendo usado, especifique SQL_VARLEN_DATA para *cbData*. Se todos os valores de dados que estão sendo fornecidos para uma coluna forem nulos, especifique SQL_NULL_DATA para *cbData*.  
  
-   Use variáveis de indicador. Como cada valor de dados novo é movido na variável de dados, armazene o comprimento do valor na variável de indicador. Se um dos outros dois métodos estiver sendo usado, especifique 0 para *cbIndicator*.  
  
-   Use ponteiros de terminador. Carregue o parâmetro **bcp_bind**_pTerm_ com o endereço do padrão de bit que encerra os dados. Se um dos outros dois métodos estiver sendo usado, especifique NULL para *pTerm*.  
  
 Todos esses três métodos podem ser usados na mesma chamada de **bcp_bind** ; nesse caso, a especificação que resulta na menor quantidade de dados sendo copiados é usada.  
  
 O parâmetro de_tipo_ **bcp_bind**usa identificadores de tipo de dados de biblioteca DB, não identificadores de tipo de dados ODBC. Os identificadores de tipo de dados da biblioteca DB são definidos em sqlncli. h para uso com a função ODBC **bcp_bind** .  
  
 As funções de cópia em massa não têm suporte para todos os tipos de dados do ODBC C. Por exemplo, as funções de cópia em massa não dão suporte à estrutura de SQL_C_TYPE_TIMESTAMP ODBC, portanto, use [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) ou [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para converter dados ODBC SQL_TYPE_TIMESTAMP em uma variável SQL_C_CHAR. Se você usar **bcp_bind** com um parâmetro de *tipo* de SQLCHARACTER para associar a variável a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna **DateTime** , as funções de cópia em massa converterão a cláusula de escape timestamp na variável Character para o formato DateTime adequado.  
  
 A tabela seguinte lista os tipos de dados indicados para usar mapeando de um tipo de dados do ODBC SQL para um tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tipo de dados do ODBC SQLz|Tipos de dados do ODBC C|parâmetro de *tipo* de bcp_bind|Tipo de dados do SQL Server|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**espaço**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **character varying**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**text**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dez**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (assinado)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (sem-sinal)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (assinado)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (sem-sinal)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **inteiro**|  
|SQL_INTEGER (assinado)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **inteiro**|  
|SQL_INTEGER (não assinado)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dez**|  
|SQL_BIGINT (assinado e sem-sinal)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **binary varying**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**imagem**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Não **tem os tipos** de dados **tinyint**, **smallint**não assinados ou sem assinatura. Para impedir a perda de valores de dados ao migrar estes tipos de dados, crie a tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o próximo tipo de dados de inteiro maior. Para impedir que os usuários adicionem posteriormente valores fora da faixa permitida pelo tipo de dados original, aplique uma regra à coluna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fim de restringir os valores permitidos para a faixa com suporte do tipo de dados na fonte original:  
  
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
  
 As funções de cópia em massa podem ser usadas para carregar dados que tenham sido lidos de uma fonte de dados ODBC rapidamente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para associar as colunas de um conjunto de resultados às variáveis de programa e, em seguida, use **bcp_bind** para associar as mesmas variáveis de programa a uma operação de cópia em massa. Chamar [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md) ou **SQLFetch** , em seguida, busca uma linha de dados da fonte de dados ODBC nas variáveis do programa e chamar [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) copia em massa os dados das variáveis do programa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Um aplicativo pode usar a função [bcp_colptr](../native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) sempre que precisar alterar o endereço da variável de dados especificada originalmente no parâmetro **bcp_bind** _pData_ . Um aplicativo pode usar a função [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) sempre que precisar alterar o comprimento dos dados originalmente especificado no parâmetro **bcp_bind**_cbData_ .  
  
 Você não pode ler dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em variáveis de programa que usam cópia em massa; não há nada como uma função "bcp_readrow". Você só pode enviar dados do aplicativo para o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando operações de cópia em massa &#40;&#41;ODBC](performing-bulk-copy-operations-odbc.md)  
  
  
