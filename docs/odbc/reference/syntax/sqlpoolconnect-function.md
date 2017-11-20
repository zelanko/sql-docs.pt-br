---
title: "Função SQLPoolConnect | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c0a82eecc733223442bc1cebf6da111397bca99
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlpoolconnect-function"></a>Função SQLPoolConnect
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.8 ODBC: ODBC  
  
 **Resumo**  
 **SQLPoolConnect** é usado para criar uma nova conexão se nenhuma conexão no pool pode ser reutilizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbc*  
 [Entrada] O identificador de conexão.  
  
 *hDbcInfoToken*  
 [Entrada] O identificador de token para a nova solicitação de conexão do aplicativo.  
  
 *wszOutConnectString*  
 [Saída] Ponteiro para um buffer de cadeia de caracteres de conexão concluído. Após a conexão bem-sucedida à fonte de dados de destino, esse buffer contém a cadeia de conexão concluído. Aplicativos devem alocar pelo menos 1.024 caracteres para esse buffer.  
  
 Se *wszOutConnectString* for NULL, *cchConnectStringLen* ainda retornará o número total de caracteres (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Entrada] Comprimento do **wszOutConnectString* buffer, em caracteres.  
  
 *cchConnectStringLen*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere null de terminação) disponíveis para retornar em \* *wszOutConnectString*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *cchConnectStringBuffer*, a concluir a cadeia de caracteres de conexão em \* *wszOutConnectString* será truncado para *cchConnectStringBuffer* menos o comprimento de um caractere null de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Semelhante ao [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) para qualquer erro de validação de entrada, exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e um **tratar** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 O Gerenciador de Driver garante que o pai HENV tratar de *hDbc* e *hDbcInfoToken* são os mesmos.  
  
 Ao contrário de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), não há nenhum *DriverCompletion* argumento para solicitar aos usuários inserir informações de conexão. Uma caixa de diálogo de solicitação não é permitida no cenário do pool.  
  
 Aplicativos não devem chamar esta função diretamente. Um driver ODBC que oferece suporte ao pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retorna SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO para o aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Quando um aplicativo usa [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* será um buffer nulo (os três últimos parâmetros serão todos definidos como NULL, 0, NULL). Caso contrário, o driver deve retornar a cadeia de caracteres de conexão de saída, que será retornada ao aplicativo [função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) chamar.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

