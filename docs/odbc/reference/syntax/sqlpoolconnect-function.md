---
title: Função SQLPoolConnect | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dda69fa741555f4402bded930f68260b154fd30
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404851"
---
# <a name="sqlpoolconnect-function"></a>Função SQLPoolConnect
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3,8 ODBC: ODBC  
  
 **Resumo**  
 **SQLPoolConnect** é usado para criar uma nova conexão, se nenhuma conexão no pool pode ser reutilizado.  
  
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
 [Saída] Ponteiro para um buffer para a cadeia de caracteres de conexão concluído. Após a conexão bem-sucedida à fonte de dados de destino, esse buffer contém a cadeia de conexão concluído. Aplicativos devem alocar pelo menos 1.024 caracteres para esse buffer.  
  
 Se *wszOutConnectString* for NULL, *cchConnectStringLen* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar o buffer apontado por *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Entrada] Comprimento do **wszOutConnectString* buffer em caracteres.  
  
 *cchConnectStringLen*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto o caractere nulo de terminação) disponíveis para retornar na \* *wszOutConnectString*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *cchConnectStringBuffer*, o concluída a cadeia de caracteres de conexão no \* *wszOutConnectString* será truncado com *cchConnectStringBuffer* menos o comprimento de um caractere nulo de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Semelhante ao [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) para qualquer erro de validação de entrada, exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **manipular** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 O Gerenciador de Driver garante que o pai HENV tratar dos *hDbc* e *hDbcInfoToken* são os mesmos.  
  
 Diferentemente [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), não há nenhuma *DriverCompletion* argumento para solicitar aos usuários inserir informações de conexão. Uma caixa de diálogo solicitando que não é permitida no cenário de pooling.  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Sempre que um driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de Driver retorna o erro para o aplicativo (no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornará SQL_SUCCESS_WITH_INFO, o Gerenciador de Driver obterá as informações de diagnóstico da *hDbcInfoToken*e retornar SQL_SUCCESS_WITH_INFO para o aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Quando um aplicativo usa [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* será um buffer nulo (os três últimos parâmetros serão tudo definidos como NULL, 0, NULL). Caso contrário, o driver deve retornar a cadeia de conexão de saída, que será retornada ao aplicativo [função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) chamar.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
