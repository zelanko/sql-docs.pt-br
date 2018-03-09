---
title: bcp_readfmt | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_readfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a41672417cc9c7b34c23f4edceb9d404c0162147
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="bcpreadfmt"></a>bcp_readfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Lê uma definição de formato do arquivo de dados do arquivo de formato especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_readfmt (  
        HDBC hdbc,  
        LPCTSTR szFormatFile);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *szFormatFile*  
 É o caminho e o nome do arquivo que contém os valores de formato para o arquivo de dados.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 Depois de **bcp_readfmt** lê os valores de formato, fará as chamadas apropriadas aos [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) e [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md). Não há necessidade de você analisar um arquivo de formato e fazer essas chamadas.  
  
 Para manter um arquivo de formato, chame [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md). As chamadas de **bcp_readfmt** podem referenciar formatos salvos. Para obter mais informações, consulte [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md).  
  
 Como alternativa, o utilitário de cópia em massa (**bcp**) pode salvar formatos de dados definidos pelo usuário em arquivos que podem ser referenciados por **bcp_readfmt**. Para obter mais informações sobre o **bcp** utility e a estrutura de **bcp** arquivos de formato de dados, consulte [importação e exportação de dados &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 O **BCPDELAYREADFMT** valor o *eOption* parâmetro [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) modifica o comportamento de bcp_readfmt.  
  
> [!NOTE]  
>  O arquivo de formato deve ter sido gerado pela versão 4.2 ou posterior do utilitário **bcp** .  
  
## <a name="example"></a>Exemplo  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
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
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
