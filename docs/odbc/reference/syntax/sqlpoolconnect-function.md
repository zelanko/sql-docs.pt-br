---
title: Função SQLPOOLConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306897"
---
# <a name="sqlpoolconnect-function"></a>Função SQLPoolConnect
**Conformidade**  
 Versão introduzida: ODBC 3.8 Standards Compliance: ODBC  
  
 **Resumo**  
 **O SQLPoolConnect** é usado para criar uma nova conexão se nenhuma conexão no pool puder ser reutilizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hdbc*  
 [Entrada] A alça de conexão.  
  
 *hDbcInfoToken*  
 [Entrada] A alça de token para a nova solicitação de conexão do aplicativo.  
  
 *wszOutConnectstring*  
 [Saída] Ponteiro para um buffer para a seqüência de conexão concluída. Após a conexão bem-sucedida com a fonte de dados de destino, este buffer contém a seqüência de conexões concluída. Os aplicativos devem alocar pelo menos 1.024 caracteres para este buffer.  
  
 Se *wszOutConnectString* for NULL, *cchConnectStringLen* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponível para retornar no buffer apontado por *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Entrada] Comprimento do buffer ** wszOutConnectString,* em caracteres.  
  
 *cchConnectStringLen*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de rescisão nula) disponível para retornar em \* *wszOutConnectString*. Se o número de caracteres disponíveis para retornar for maior ou igual \*a *cchConnectStringBuffer,* a seqüência de caracteres de conexão concluída no *wszOutConnectString* será truncada para *cchConnectStringBuffer* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Semelhante ao [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) para qualquer erro de validação de entrada, exceto que o Driver Manager usará um **HandleType** of SQL_HANDLE_DBC_INFO_TOKEN e uma **alça** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 O Driver Manager garante que a alça HENV pai do *hDbc* e *hDbcInfoToken* são as mesmas.  
  
 Ao contrário [do SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md)não há argumento *de DriverComplet* para solicitar aos usuários que insiram informações de conexão. Um diálogo de solicitação é proibido no cenário de pooling.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Driver Manager retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Driver Manager obterá as informações de diagnóstico do *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [no SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Quando um aplicativo usa [SQLConnect,](../../../odbc/reference/syntax/sqlconnect-function.md) *wszOutConnectString* será um buffer NULL (os três últimos parâmetros serão definidos como NULL, 0, NULL). Caso contrário, o driver deve retornar a seqüência de conexão de saída, que será devolvida à chamada [sqldriverconnect function](../../../odbc/reference/syntax/sqldriverconnect-function.md) do aplicativo.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
