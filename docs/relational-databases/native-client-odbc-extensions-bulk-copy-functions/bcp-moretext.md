---
title: bcp_moretext | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_moretext
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 100646ffb50ac0cb187881a99678c6d366b8922b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010073"
---
# <a name="bcp_moretext"></a>bcp_moretext
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Envia parte de um valor de tipo de dados longo, de tamanho variável, para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_moretext (  
        HDBC hdbc,  
        DBINT cbData,  
        LPCBYTE pData);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *cbData*  
 É o número de bytes de dados que estão sendo copiados para SQL Server dos dados referenciados por *pData*. Um valor igual a SQL_NULL_DATA indica NULL.  
  
 *pData*  
 É um ponteiro da parte de dados de tamanho variável, longa, para a qual há suporte a ser enviado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Essa função pode ser usada em conjunto com [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) e [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para copiar valores de dados longos e de comprimento variável para SQL Server em um número de partes menores. **bcp_moretext** pode ser usado com colunas que têm os seguintes tipos de dados de SQL Server: **Text**, **ntext**, **Image**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, tipo definido pelo usuário (UDT) e XML. **bcp_moretext** não oferece suporte a conversões de dados, os dados fornecidos devem corresponder ao tipo de dados da coluna de destino.  
  
 Se **bcp_bind** for chamado com um parâmetro *pData* não nulo para tipos de dados com suporte pelo **bcp_moretext**, **bcp_sendrow** enviará o valor de dados inteiro, independentemente do comprimento. No entanto, se **bcp_bind** tiver um parâmetro *pData* nulo para tipos de dados com suporte, **bcp_moretext** poderá ser usado para copiar dados imediatamente após um retorno bem-sucedido de **bcp_sendrow** indicando que todas as colunas associadas com os dados presentes foram processadas.  
  
 Se você usar **bcp_moretext** para enviar uma coluna de tipo de dados com suporte em uma linha, você também deverá usá-la para enviar todas as outras colunas de tipo de dados com suporte na linha. Nenhuma coluna pode ser ignorada. Os tipos de dados para os quais há suporte são SQLTEXT, SQLNTEXT, SQLIMAGE, SQLUDT e SQLXML. SQLCHARACTER, SQLVARCHAR, SQNCHAR, SQLBINARY e SQLVARBINARY também se encontram nessa categoria caso a coluna seja varchar(max), nvarchar(max) ou varbinary(max), respectivamente.  
  
 Chamar **bcp_bind** ou [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) define o tamanho total de todas as partes de dados a serem copiadas para a coluna SQL Server. Uma tentativa de enviar SQL Server mais bytes do que o especificado na chamada para **bcp_bind** ou **bcp_collen** gera um erro. Esse erro ocorreria, por exemplo, em um aplicativo que usava **bcp_collen** para definir o comprimento dos dados disponíveis para uma coluna de **texto** de SQL Server como 4500 e, em seguida, chamado **bcp_moretext** cinco vezes ao indicar em cada chamada que o comprimento do buffer de dados era de 1000 bytes.  
  
 Se uma linha copiada contiver mais de uma coluna de comprimento variável longa, **bcp_moretext** primeiro envia seus dados para a coluna numerada ordinal mais baixa, seguida pela próxima coluna numerada ordinal mais baixa e assim por diante. A configuração correta do comprimento total dos dados esperados é importante. Não há nenhuma forma de sinalizar, fora da configuração de comprimento, que todos os dados de uma coluna foram recebidos pela cópia em massa.  
  
 Quando os valores **var (max)** são enviados ao servidor usando bcp_sendrow e bcp_moretext, não é necessário chamar bcp_collen para definir o comprimento da coluna. Em vez disso, somente para esses tipos, o valor é encerrado chamando bcp_sendrow com um comprimento de zero.  
  
 Normalmente, um aplicativo chama **bcp_sendrow** e **bcp_moretext** em loops para enviar um número de linhas de dados. Aqui está uma descrição de como fazer isso para uma tabela que contém duas colunas de **texto** :  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como usar **bcp_moretext** com **bcp_bind** e **bcp_sendrow**:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
