---
title: bcp_bind | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_bind
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 711c82bb627ca9ad1620cf1e11fdbc9dfa5f4351
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140566"
---
# <a name="bcpbind"></a>bcp_bind
  Associa dados de uma variável de programa a uma coluna de tabela para cópia em massa no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_bind (  
HDBC   
hdbc  
,   
LPCBYTE   
pData  
,  
INT   
cbIndicator  
,  
DBINT   
cbData  
,  
LPCBYTE   
pTerm  
,  
INT   
cbTerm  
,  
INT   
eDataType  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *pData*  
 É um ponteiro para os dados copiados. Se *eDataType* for SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR ou SQLIMAGE, *pData* pode ser NULL. Um valor nulo *pData* indica que os valores de dados longos serão enviados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em partes usando [bcp_moretext](bcp-moretext.md). O usuário só deve definir *pData* como NULL se a coluna correspondente ao campo associado ao usuário for uma coluna BLOB caso contrário **bcp_bind** falhará.  
  
 Se houve indicadores presentes nos dados, eles aparecerão na memória diretamente antes dos dados. O *pData* parâmetro aponta para a variável de indicador nesse caso, e a largura do indicador, o *cbIndicator* parâmetro, é usada pela cópia em massa para endereçar dados de usuário corretamente.  
  
 *cbIndicator*  
 É o comprimento, em bytes, de um indicador de comprimento ou nulo para os dados da coluna. Os valores de comprimento de indicador válidos são 0 (quando nenhum indicador é usado), 1, 2, 4 ou 8. Os indicadores aparecem na memória diretamente antes de qualquer dado. Por exemplo, a definição do tipo de estrutura a seguir poderia ser usada para inserir valores inteiros em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a cópia em massa:  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 No caso de exemplo, o *pData* parâmetro seria definido para o endereço de uma instância declarada da estrutura, o endereço do BCPBOUNDINT *iIndicator* membro da estrutura. O *cbIndicator* parâmetro seria definido como o tamanho de um número inteiro (sizeof e o *cbData* parâmetro seria novamente definido para o tamanho de um inteiro (sizeof. Para o valor de uma linha para o servidor que contém um valor nulo na coluna associada, o valor da instância de cópia em massa *iIndicator* membro deve ser definido como SQL_NULL_DATA.  
  
 *cbData*  
 É a contagem de bytes de dados na variável de programa, não incluindo o comprimento de qualquer terminador ou indicador de comprimento ou nulo.  
  
 Definindo *cbData* como SQL_NULL_DATA significa que todas as linhas copiadas no servidor contêm um valor NULL da coluna.  
  
 Definindo *cbData* como SQL_VARLEN_DATA indica que o sistema usará um terminador de cadeia de caracteres ou outro método para determinar o comprimento dos dados copiados.  
  
 Para tipos de dados de comprimento fixo, como inteiros, o tipo de dados indica o comprimento dos dados para o sistema. Portanto, para tipos de dados de comprimento fixo *cbData* com segurança pode ser SQL_VARLEN_DATA ou o comprimento dos dados.  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caractere e tipos de dados binários *cbData* pode ser SQL_VARLEN_DATA, SQL_NULL_DATA, algum valor positivo ou 0. Se *cbData* for SQL_VARLEN_DATA, o sistema usa um indicador de comprimento/nulo (se presente) ou uma sequência de terminador para determinar o comprimento dos dados. Se os dois forem fornecidos, o sistema irá usar aquele que resulta na menos quantidade de dados sendo copiados. Se *cbData* for SQL_VARLEN_DATA, o tipo de dados da coluna é uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caractere ou tipo binário e nem um indicador de comprimento nem uma sequência de terminador for especificada, o sistema retornará uma mensagem de erro.  
  
 Se *cbData* for 0 ou um valor positivo, o sistema usará *cbData* como o comprimento de dados. No entanto, se, além de um positivo *cbData* valor, uma sequência de terminador ou de indicador de comprimento é fornecida, o sistema determinará o comprimento de dados usando o método que resulta na menor quantidade de dados sendo copiados.  
  
 O *cbData* valor do parâmetro representa a contagem de bytes de dados. Se os dados de caractere forem representados por caracteres que abrangem Unicode, um positivo *cbData* valor do parâmetro representa o número de caracteres multiplicado pelo tamanho em bytes de cada caractere.  
  
 *pTerm*  
 É um ponteiro para o padrão de bytes, se houver, que marca o fim desta variável de programa. Por exemplo, geralmente, as cadeias de caracteres C ANSI e MBCS têm um terminador com 1 byte (\0).  
  
 Se houver um terminador para a variável, defina *pTerm* como NULL.  
  
 Você pode usar uma cadeia de caracteres vazia ("") para designar o terminador nulo C como o terminador de variável do programa. Como a cadeia de caracteres de vazia terminada em nulo constitui um único byte (o próprio byte do terminador), defina *cbTerm* como 1. Por exemplo, para indicar que a cadeia de caracteres em *szName* é terminada em nulo e que o terminador deve ser usado para indicar o comprimento:  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 Uma forma não terminada desse exemplo poderia indicar que 15 caracteres copiadas do *szName* variável para a segunda coluna da tabela associada:  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 A API de cópia em massa executa a conversão de caracteres Unicode em MBCS conforme necessário. Verifique se a cadeia de caracteres de bytes de terminador e o comprimento da cadeia de caracteres de bytes estão definidos corretamente. Por exemplo, para indicar que a cadeia de caracteres em *szName* é uma cadeia de caracteres largos Unicode, finalizada pelo valor de terminador nulo Unicode:  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Se o limite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a coluna é o caractere largo, nenhuma conversão é executada na [bcp_sendrow](bcp-sendrow.md). Se a coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for do tipo caractere do MBCS, a conversão de caracteres largo em caracteres multibyte será executada conforme os dados são enviados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *cbTerm*  
 É a contagem de bytes presentes no terminador da variável de programa, se houver. Se houver um terminador para a variável, defina *cbTerm* como 0.  
  
 *eDataType*  
 É o tipo de dados C da variável de programa. Os dados na variável de programa são convertidos para o tipo da coluna do banco de dados. Se esse parâmetro for 0, nenhuma conversão será executada.  
  
 O *eDataType* parâmetro é enumerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tokens de tipo de dados em SQLNCLI. h, não os enumeradores de tipo de dados ODBC C. Por exemplo, você pode especificar um inteiro de dois bytes, ODBC tipo SQL_C_SHORT, usando o tipo SQLINT2 específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o suporte para tokens de tipo de dados SQLXML e SQLUDT na *`eDataType`* parâmetro.  
  
 *idxServerCol*  
 É a posição ordinal da coluna na tabela do banco de dados na qual os dados são copiados. A primeira coluna em uma tabela é a coluna 1. A posição ordinal de uma coluna é relatada por [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Use **bcp_bind** de uma maneira rápida e eficiente copiar dados de uma variável de programa em uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Chame [bcp_init](bcp-init.md) antes de chamar essa ou qualquer outra função de cópia em massa. Chamando **bcp_init** define o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela de destino para cópia em massa. Ao chamar **bcp_init** para uso com **bcp_bind** e [bcp_sendrow](bcp-sendrow.md), o **bcp_init** _szDataFile_parâmetro, que indica o arquivo de dados é definido como NULL; o **bcp_init**_eDirection_ parâmetro for definido como DB_IN.  
  
 Tornar um separado **bcp_bind** chamar para cada coluna no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela na qual você deseja copiar. Depois que o necessário **bcp_bind** chamadas foram feitas, em seguida, chame **bcp_sendrow** para enviar uma linha de dados de suas variáveis de programa para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Reassociar uma coluna não tem suporte.  
  
 Sempre que desejar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para confirmar as linhas já recebidas, chame [bcp_batch](bcp-batch.md). Por exemplo, chamar **bcp_batch** uma vez para cada 1000 linhas inseridas ou em qualquer outro intervalo.  
  
 Quando não houver nenhum mais linhas a serem inseridas, chame [bcp_done](bcp-done.md). Caso isso não seja feito, será gerado um erro.  
  
 Controlar as configurações de parâmetro especificadas com [bcp_control](bcp-control.md), não têm nenhum efeito **bcp_bind** transferências de linha.  
  
 Se *pData* de uma coluna é definida como nulo porque seu valor será fornecido por chamadas para [bcp_moretext](bcp-moretext.md), todas as colunas subsequentes com *eDataType* definido como SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR ou SQLIMAGE também deve ser associado com *pData* definido como NULL, e seus valores também devem ser fornecidos por chamadas para `bcp_moretext`.  
  
 Para novos tipos de valor grande, como `varchar(max)`, `varbinary(max)`, ou `nvarchar(max)`, você pode usar SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY e SQLNCHAR como indicadores de tipo no *eDataType* parâmetro.  
  
 Se *cbTerm* é não em 0, qualquer valor (1, 2, 4 ou 8) é válido para o prefixo (*cbIndicator*). Nessa situação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client irá pesquisar o terminador, calcular o comprimento dos dados em relação ao terminador de (*eu*) e defina o *cbData* com o menor valor de i e o valor de prefixo.  
  
 Se *cbTerm* é 0 e *cbIndicator* (o prefixo) não é 0, *cbIndicator* deve ser 8. O prefixo de 8 bytes pode ter os seguintes valores:  
  
-   0xFFFFFFFFFFFFFFFF significa um valor nulo para o campo  
  
-   0xFFFFFFFFFFFFFFFE é tratado como um valor de prefixo especial usado para enviar dados em partes para o servidor de forma eficiente. O formato dos dados com este prefixo especial é:  
  
-   < SPECIAL_PREFIX > \<0 ou mais partes de dados >< ZERO_CHUNK > onde:  
  
-   SPECIAL_PREFIX é 0xFFFFFFFFFFFFFFFE  
  
-   DATA_CHUNK é um prefixo de 4 bytes que contém o comprimento da parte, seguido dos dados reais cujo comprimento é especificado no prefixo de 4 bytes.  
  
-   ZERO_CHUNK é um valor de 4 bytes que contém todos os zeros (00000000) que indicam o final dos dados.  
  
-   Qualquer outro comprimento de 8 bytes válido é tratado como um comprimento de dados normal.  
  
 Chamando [bcp_columns](bcp-columns.md) ao usar **bcp_bind** resulta em um erro.  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>Suporte do bcp_bind a recursos aprimorados de data e hora  
 Para obter informações sobre os tipos usados com o *eDataType* parâmetro para tipos de data/hora, consulte [alterações de cópia em massa para tipos aprimorada de data e hora &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
