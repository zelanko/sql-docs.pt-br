---
title: bcp_moretext | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_moretext
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30ddae53cc452796de0617bb5718d04156dcda41
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430175"
---
# <a name="bcpmoretext"></a>bcp_moretext
  Envia parte de um valor de tipo de dados longo, de tamanho variável, para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_moretext (  
HDBC   
hdbc  
,  
DBINT   
cbData  
,  
LPCBYTE   
pData  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *cbData*  
 É o número de bytes de dados sendo copiados para o SQL Server dos dados referenciado pelo *pData*. Um valor igual a SQL_NULL_DATA indica NULL.  
  
 *pData*  
 É um ponteiro da parte de dados de tamanho variável, longa, para a qual há suporte a ser enviado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 Essa função pode ser usada em conjunto com [bcp_bind](bcp-bind.md) e [bcp_sendrow](bcp-sendrow.md) longos e copiar os valores de dados de comprimento variável para o SQL Server em um número de partes menores. **bcp_moretext** pode ser usado com colunas que têm os seguintes tipos de dados do SQL Server: `text`, `ntext`, `image`, `varchar(max)`, `nvarchar(max)`, `varbinary(max)`, tipo definido pelo usuário (UDT) e XML. **bcp_moretext** não não conversões de dados de suporte, os dados fornecidos devem corresponder ao tipo de dados da coluna de destino.  
  
 Se **bcp_bind** for chamado com um nonNULL *pData* parâmetro para tipos de dados que são suportados pelo **bcp_moretext**, `bcp_sendrow` envia o valor de inteiro de dados, independentemente de comprimento. Se, no entanto, **bcp_bind** tem um valor nulo *pData* parâmetro para tipos de dados com suporte **bcp_moretext** pode ser usado para copiar dados logo após um retorno bem-sucedido de `bcp_sendrow` que indica se todas as colunas associadas aos dados presentes foram processadas.  
  
 Se você usar **bcp_moretext** para enviar uma coluna de tipo de dados com suporte em uma linha, você deve também usá-lo para enviar todas as outras colunas de tipo de dados com suporte na linha. Nenhuma coluna pode ser ignorada. Os tipos de dados para os quais há suporte são SQLTEXT, SQLNTEXT, SQLIMAGE, SQLUDT e SQLXML. SQLCHARACTER, SQLVARCHAR, SQNCHAR, SQLBINARY e SQLVARBINARY também se encontram nessa categoria caso a coluna seja varchar(max), nvarchar(max) ou varbinary(max), respectivamente.  
  
 Chamar **bcp_bind** ou [bcp_collen](bcp-collen.md) define o comprimento total de todas as partes de dados a serem copiados para a coluna do SQL Server. Uma tentativa de enviar ao SQL Server mais bytes que o especificado na chamada para **bcp_bind** ou `bcp_collen` gera um erro. Esse erro surgiria, por exemplo, em um aplicativo que usou `bcp_collen` para definir o comprimento dos dados disponíveis para o SQL Server `text` , em seguida, chamado de coluna como 4500 **bcp_moretext** cinco vezes enquanto indicava em cada chamada Se os dados de tamanho do buffer tinha 1.000 bytes.  
  
 Se uma linha copiada contenha mais de uma coluna longa e de comprimento variável, **bcp_moretext** primeiro envia seus dados para a menor coluna numerada ordinalmente, seguida da próxima menor coluna numerada ordinalmente e assim por diante. A configuração correta do comprimento total dos dados esperados é importante. Não há nenhuma forma de sinalizar, fora da configuração de comprimento, que todos os dados de uma coluna foram recebidos pela cópia em massa.  
  
 Quando `var(max)` os valores são enviados ao servidor usando bcp_sendrow e bcp_moretext, não é necessário chamar bcp_collen para definir o comprimento da coluna. Em vez disso, somente para esses tipos, o valor é terminado por chamada bcp_sendrow com um comprimento de zero.  
  
 Um aplicativo normalmente chama `bcp_sendrow` e **bcp_moretext** em loops enviar um número de linhas de dados. Aqui está uma descrição de como fazer isso para uma tabela que contém dois `text` colunas:  
  
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
 Este exemplo mostra como usar **bcp_moretext** com **bcp_bind** e `bcp_sendrow`:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
