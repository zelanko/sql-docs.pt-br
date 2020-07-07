---
title: bcp_exec | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_exec
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb159b403b132610894a92f0906ca5cc37b29cae
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000595"
---
# <a name="bcp_exec"></a>bcp_exec
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Executa uma cópia em massa completa dos dados entre uma tabela de banco de dados e um arquivo de usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_exec (  
        HDBC hdbc,  
        LPDBINT pnRowsProcessed);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *pnRowsProcessed*  
 É um ponteiro para um DBINT. A função **bcp_exec** preenche esse DBINT com o número de linhas copiadas com êxito. Se *pnRowsProcessed* for NULL, ele será ignorado por **bcp_exec**.  
  
## <a name="returns"></a>Retornos  
 SUCCEED, SUCCEED_ASYNC ou FAIL. Os lucros de função **bcp_exec** retornarão SUCCEED se todas as linhas forem copiadas. **bcp_exec** retornará SUCCEED_ASYNC se uma operação de cópia em massa assíncrona ainda estiver pendente. **bcp_exec** retornará FAIL se uma falha completa ocorrer, ou se o número de linhas que geram erros alcançar o valor especificado para BCPMAXERRS usando [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md). O padrão de BCPMAXERRS é definido como 10. A opção BCPMAXERRS afeta somente os erros de sintaxe detectados pelo provedor ao ler as linhas do arquivo de dados (e não as linhas enviadas para o servidor). O servidor anula o lote ao detectar um erro com uma linha. Verifique o parâmetro *pnRowsProcessed* para o número de linhas copiadas com êxito.  
  
## <a name="remarks"></a>Comentários  
 Esta função copia os dados de um arquivo de usuário para uma tabela de banco de dados ou vice-versa, dependendo do valor do parâmetro *eDirection* em [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md).  
  
 Antes de chamar **bcp_exec**, chame **bcp_init** com um nome de arquivo de usuário válido. Caso isso não seja feito, será gerado um erro.  
  
 **bcp_exec** é a única função de cópia em massa que provavelmente ficará pendente para qualquer duração de tempo. Portanto, é a única função de cópia em massa que suporta o modo assíncrono. Para definir o modo assíncrono, use [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para definir SQL_ATTR_ASYNC_ENABLE como SQL_ASYNC_ENABLE_ON antes de chamar **bcp_exec**. Para testar se houve a conclusão, chame **bcp_exec** com os mesmos parâmetros. Se a cópia em massa ainda não tiver sido concluída, **bcp_exec** retornará SUCCEED_ASYNC. Retornará também em *pnRowsProcessed* uma contagem de status do número de linhas que foram enviadas para o servidor. As linhas enviadas para o servidor não serão confirmadas até que o fim de um lote seja atingido.  
  
 Para obter informações sobre uma alteração significativa na cópia em massa a partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , consulte [executando operações de cópia em massa &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar **bcp_exec**:  
  
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
if (bcp_init(hdbc, _T("pubs..authors"), _T("authors.sav"), NULL, DB_OUT)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Now, execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   if (nRowsProcessed == -1)  
      {  
      printf_s("No rows processed on bulk copy execution.\n");  
      }  
   else  
      {  
      printf_s("Incomplete bulk copy.   Only %ld row%s copied.\n",  
         nRowsProcessed, (nRowsProcessed == 1) ? "": "s");  
      }  
   return;  
   }  
  
printf_s("%ld rows processed.\n", nRowsProcessed);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
