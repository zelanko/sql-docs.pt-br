---
description: bcp_bind
title: bcp_bind | Microsoft Docs
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_bind
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.reviewer: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edff3154a4385ee87bf7686cf5e2954e026e495f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473657"
---
# <a name="bcp_bind"></a>bcp_bind

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Associa dados de uma variável de programa a uma coluna de tabela para cópia em massa no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="syntax"></a>Sintaxe

```  
  
RETCODE bcp_bind (  
        HDBC hdbc,
        LPCBYTE pData,  
        INT cbIndicator,  
        DBINT cbData,  
        LPCBYTE pTerm,  
        INT cbTerm,  
        INT eDataType,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumentos

 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *pData*  
 É um ponteiro para os dados copiados. Se *eDataType* for SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SqlBinary, SQLNCHAR ou SQLIMAGE, *pData* poderá ser NULL. Um *pData* nulo indica que valores de dados longos serão enviados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em partes usando [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md). O usuário só deve definir *pData* como nulo se a coluna correspondente ao campo associado ao usuário for uma coluna BLOB, caso contrário **bcp_bind** falhará.  
  
 Se houve indicadores presentes nos dados, eles aparecerão na memória diretamente antes dos dados. O parâmetro *pData* aponta para a variável de indicador nesse caso, e a largura do indicador, o parâmetro *cbIndicator* , é usada pela cópia em massa para resolver os dados do usuário corretamente.  
  
 *cbIndicator*  
 É o comprimento, em bytes, de um indicador de comprimento ou nulo para os dados da coluna. Os valores de comprimento de indicador válidos são 0 (quando nenhum indicador é usado), 1, 2, 4 ou 8. Os indicadores aparecem na memória diretamente antes de qualquer dado. Por exemplo, a definição do tipo de estrutura a seguir poderia ser usada para inserir valores inteiros em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a cópia em massa:  
  
```
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 No caso de exemplo, o parâmetro *pData* seria definido como o endereço de uma instância declarada da estrutura, o endereço do membro da estrutura BCPBOUNDINT *iIndicator* . O parâmetro *cbIndicator* seria definido como o tamanho de um inteiro (sizeof (int)) e o parâmetro *cbData* seria definido novamente como o tamanho de um inteiro (sizeof (int)). Para copiar em massa uma linha para o servidor que contém um valor nulo para a coluna associada, o valor do membro *iIndicator* da instância deve ser definido como SQL_NULL_DATA.  
  
 *cbData*  
 É a contagem de bytes de dados na variável de programa, não incluindo o comprimento de qualquer terminador ou indicador de comprimento ou nulo.  
  
 Definir *cbData* como SQL_NULL_DATA significa que todas as linhas copiadas para o servidor contêm um valor nulo para a coluna.  
  
 Definir *cbData* como SQL_VARLEN_DATA indica que o sistema usará um terminador de cadeia de caracteres ou outro método para determinar o comprimento dos dados copiados.  
  
 Para tipos de dados de comprimento fixo, como inteiros, o tipo de dados indica o comprimento dos dados para o sistema. Portanto, para tipos de dados de comprimento fixo, *cbData* pode ser SQL_VARLEN_DATA com segurança ou o comprimento dos dados.  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados Binary e de caractere, *cbData* pode ser SQL_VARLEN_DATA, SQL_NULL_DATA, algum valor positivo ou 0. Se *cbData* for SQL_VARLEN_DATA, o sistema usará um indicador de comprimento/nulo (se presente) ou uma sequência de terminador para determinar o comprimento dos dados. Se os dois forem fornecidos, o sistema irá usar aquele que resulta na menos quantidade de dados sendo copiados. Se *cbData* for SQL_VARLEN_DATA, o tipo de dados da coluna será um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de caractere ou binário e nem um indicador de comprimento nem uma sequência de terminador será especificado, o sistema retornará uma mensagem de erro.  
  
 Se *cbData* for 0 ou um valor positivo, o sistema usará *cbData* como o comprimento dos dados. No entanto, se, além de um valor positivo de *cbData* , um indicador de comprimento ou uma sequência de terminador for fornecida, o sistema determinará o comprimento dos dados usando o método que resultará na menor quantidade de dados sendo copiados.  
  
 O valor do parâmetro *cbData* representa a contagem de bytes de dados. Se os dados de caractere forem representados por caracteres largos Unicode, um valor de parâmetro *cbData* positivo representará o número de caracteres multiplicado pelo tamanho em bytes de cada caractere.  
  
 *pTerm*  
 É um ponteiro para o padrão de bytes, se houver, que marca o fim desta variável de programa. Por exemplo, geralmente, as cadeias de caracteres C ANSI e MBCS têm um terminador com 1 byte (\0).  
  
 Se não houver um terminador para a variável, defina *pTerm* como NULL.  
  
 Você pode usar uma cadeia de caracteres vazia ("") para designar o terminador nulo C como o terminador de variável do programa. Como a cadeia de caracteres vazia terminada em nulo constitui um único byte (o próprio byte do terminador), defina *cbTerm* como 1. Por exemplo, para indicar que a cadeia de caracteres em *szName* é terminada em nulo e que o terminador deve ser usado para indicar o comprimento:  
  
```
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```

 Um formulário não finalizado deste exemplo pode indicar que 15 caracteres sejam copiados da variável *szName* para a segunda coluna da tabela vinculada:  

```
bcp_bind(hdbc, szName, 0, 15,
   NULL, 0, SQLCHARACTER, 2)  
```

 A API de cópia em massa executa a conversão de caracteres Unicode em MBCS conforme necessário. Verifique se a cadeia de caracteres de bytes de terminador e o comprimento da cadeia de caracteres de bytes estão definidos corretamente. Por exemplo, para indicar que a cadeia de caracteres em *szName* é uma cadeia de caracteres Unicode largo, terminada pelo valor de terminador NULL Unicode:  
  
```  
bcp_bind(hdbc, szName, 0,
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna associada for um caractere largo, nenhuma conversão será executada em [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md). Se a coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for do tipo caractere do MBCS, a conversão de caracteres largo em caracteres multibyte será executada conforme os dados são enviados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *cbTerm*  
 É a contagem de bytes presentes no terminador da variável de programa, se houver. Se não houver um terminador para a variável, defina *cbTerm* como 0.  

*eDataType* É o tipo de dados C da variável do programa. Os dados na variável de programa são convertidos para o tipo da coluna do banco de dados. Se esse parâmetro for 0, nenhuma conversão será executada.  

O parâmetro *eDataType* é enumerado pelos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tokens de tipo de dados em sqlncli. h, não os enumeradores de tipo de dados ODBC C. Por exemplo, você pode especificar um inteiro de dois bytes, ODBC tipo SQL_C_SHORT, usando o tipo SQLINT2 específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o suporte para os tokens de tipo de dados SQLXML e SQLUDT no parâmetro **_eDataType_** .  

A tabela a seguir lista os tipos de dados enumerados válidos e os tipos de dados ODBC C correspondentes.

|eDataType|Tipo de C|
|-----------------------|------------|  
|SQLTEXT|char *|  
|SQLNTEXT|wchar_t *|  
|SQLCHARACTER|char *|  
|SQLBIGCHAR|char *|  
|SQLVARCHAR|char *|  
|SQLBIGVARCHAR|char *|  
|SQLNCHAR|wchar_t *|  
|SQLNVARCHAR|wchar_t *|  
|SQLBINARY|unsigned char *|  
|SQLBIGBINARY|unsigned char *|  
|SQLVARBINARY|unsigned char *|  
|SQLBIGVARBINARY|unsigned char *|  
|SQLBIT|char|  
|SQLBITN|char|  
|SQLINT1|char|  
|SQLINT2|short int|  
|SQLINT4|INT|  
|SQLINT8|_int64|  
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|  
|SQLFLT4|FLOAT|  
|SQLFLT8|FLOAT|  
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|  
|SQLDECIMALN|SQL_NUMERIC_STRUCT|  
|SQLNUMERICN|SQL_NUMERIC_STRUCT|  
|SQLMONEY|DBMONEY|  
|SQLMONEY4|DBMONEY4|  
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|  
|SQLTIMEN|SQL_SS_TIME2_STRUCT|  
|SQLDATEN|SQL_DATE_STRUCT|  
|SQLDATETIM4|DBDATETIM4|  
|SQLDATETIME|DBDATETIME|  
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|  
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|  
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|  
|SQLIMAGE|unsigned char *|  
|SQLUDT|unsigned char *|  
|SQLUNIQUEID|SQLGUID|  
|SQLVARIANT|*Qualquer tipo de dados, exceto:*<br />–   text<br />–   ntext<br />–   image<br />–   varchar(max)<br />–   varbinary(max)<br />–   nvarchar(max)<br />–   xml<br />–   timestamp|  
|SQLXML|*Tipos de dados C compatíveis:*<br />–   char*<br />–   wchar_t *<br />–   unsigned char *|  

*idxServerCol* É a posição ordinal da coluna na tabela de banco de dados para a qual os dados são copiados. A primeira coluna em uma tabela é a coluna 1. A posição ordinal de uma coluna é relatada por [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Retornos

 SUCCEED ou FAIL.

## <a name="remarks"></a>Comentários

Use **bcp_bind** para uma maneira rápida e eficiente de copiar dados de uma variável de programa para uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

Chame [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) antes de chamar esta ou qualquer outra função de cópia em massa. Chamar **bcp_init** define a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela de destino para cópia em massa. Ao chamar **bcp_init** para uso com **bcp_bind** e [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), o parâmetro **bcp_init** _szDataFile_ , que indica o arquivo de dados, é definido como nulo; o parâmetro **bcp_init**_eDirection_ é definido como DB_IN.  

Faça uma chamada de **bcp_bind** separada para cada coluna na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela na qual você deseja copiar. Depois que as chamadas de **bcp_bind** necessárias tiverem sido feitas, chame **bcp_sendrow** para enviar uma linha de dados de suas variáveis de programa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Reassociar uma coluna não tem suporte.

Sempre que você quiser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confirmar as linhas já recebidas, chame [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md). Por exemplo, chame **bcp_batch** uma vez para cada 1000 linhas inseridas ou em qualquer outro intervalo.  

Quando não houver mais linhas a serem inseridas, chame [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). Caso isso não seja feito, será gerado um erro.

As configurações de parâmetro de controle, especificadas com [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md), não têm efeito sobre transferências de linha **bcp_bind** .  

Se *pData* para uma coluna for definido como NULL porque seu valor será fornecido por chamadas para [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md), qualquer coluna subsequente com *eDataType* definida como SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SqlBinary, SQLNCHAR ou SQLIMAGE também deverá ser associada a *pData* definido como NULL e seus valores também deverão ser fornecidos por chamadas para **bcp_moretext**.  

Para novos tipos de valor grande, como **varchar (max)**, **varbinary (max)** ou **nvarchar (max)**, você pode usar sqldigit, SQLVARCHAR, SQLVARBINARY, SqlBinary e SQLNCHAR como indicadores de tipo no parâmetro *eDataType* .  

Se *cbTerm* não for 0, qualquer valor (1, 2, 4 ou 8) será válido para o prefixo (*cbIndicator*). Nessa situação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pesquisará o terminador, calculará o comprimento dos dados em relação ao terminador (*i*) e definirá *cbData* como o valor menor de i e o valor do prefixo.  

Se *cbTerm* for 0 e *cbIndicator* (o prefixo) não for 0, *cbIndicator* deverá ser 8. O prefixo de 8 bytes pode ter os seguintes valores:  

- 0xFFFFFFFFFFFFFFFF significa um valor nulo para o campo  

- 0xFFFFFFFFFFFFFFFE é tratado como um valor de prefixo especial, que é usado para enviar com eficiência dados em partes para o servidor. O formato dos dados com este prefixo especial é:  

- <SPECIAL_PREFIX> \<0 or more  DATA CHUNKS> <ZERO_CHUNK> em que:  

- SPECIAL_PREFIX é 0xFFFFFFFFFFFFFFFE  

- DATA_CHUNK é um prefixo de 4 bytes contendo o comprimento da parte, seguido pelos dados reais cujo comprimento é especificado no prefixo de 4 bytes.  

- ZERO_CHUNK é um valor de 4 bytes que contém todos os zeros (00000000) indicando o fim dos dados.  

- Qualquer outro comprimento de 8 bytes válido é tratado como um comprimento de dados regular.  

 Chamar [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) ao usar **bcp_bind** resulta em um erro.  
  
## <a name="bcp_bind-support-for-enhanced-date-and-time-features"></a>Suporte do bcp_bind a recursos aprimorados de data e hora

Para obter informações sobre os tipos usados com o parâmetro *eDataType* para tipos de data/hora, consulte [alterações de cópia em massa para tipos de data e hora aprimorados &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  

Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  

## <a name="example"></a>Exemplo
  
```
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>Consulte Também

 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)
