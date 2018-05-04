---
title: Função SQLInstallerError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e786d2b1fa8136c4745b8ee3a91b91069a79e873
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstallererror-function"></a>Função SQLInstallerError
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallerError** retorna informações de erro ou de status para as funções do instalador ODBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *IERRO*  
 [Entrada] Número de registro de erro. Números válidos são de 1 a 8.  
  
 *pfErrorCode*  
 [Saída] Código de erro do instalador. (Para obter mais informações, consulte "Comentários".)  
  
 *lpszErrorMsg*  
 [Saída] Ponteiro para o armazenamento para o texto da mensagem de erro.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento máximo do *szErrorMsg* buffer. Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos o caractere null de terminação.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento máximo do *szErrorMsg* buffer. Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos o caractere null de terminação.  
  
 *pcbErrorMsg*  
 [Saída] Ponteiro para o número total de bytes (excluindo o caractere null de terminação) disponíveis para retornar em *lpszErrorMsg*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbErrorMsgMax*, o texto da mensagem de erro no *lpszErrorMsg* será truncado para *cbErrorMsgMax* menos de bytes de caractere NULL de terminação. O *pcbErrorMsg* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA ou SQL_ERROR.  
  
## <a name="diagnostics"></a>diagnóstico  
 **SQLInstallerError** não lançar valores de erro para si mesmo. **SQLInstallerError** retorna SQL_NO_DATA quando não é possível recuperar informações de erro (nesse caso *pfErrorCode* é indefinido). Se **SQLInstallerError** não é possível acessar os valores de erro por qualquer motivo que normalmente retornaria SQL_ERROR, **SQLInstallerError** retornará SQL_ERROR, mas não envia os valores de erro. Se você não souber o comprimento da cadeia de caracteres de aviso (*lpszErrorMsg*), você pode definir *lpszErrorMsg* como NULL e chame **SQLInstallerError**. **SQLInstallerError** será, em seguida, retornar o comprimento da cadeia de caracteres de aviso em *cbErrorMsgMax*. Se o buffer para a mensagem de erro é muito curto, **SQLInstallerError** retorna SQL_SUCCESS_WITH_INFO e retorna o correto *pfErrorCode* valor para **SQLInstallerError**.  
  
 Para determinar se ocorreu um truncamento na mensagem de erro, um aplicativo pode comparar o valor de *cbErrorMsgMax* argumento para o comprimento real do texto da mensagem gravado o *pcbErrorMsg* argumento. Se o truncamento ocorrer, o tamanho do buffer correto deve ser alocado para *lpszErrorMsg* e **SQLInstallerError** deve ser chamado novamente com a correspondente *IERRO*registro.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo chama **SQLInstallerError** quando uma chamada anterior para a função do instalador ODBC retorna FALSE. Funções da instalação do instalador e driver ou conversor ODBC lançar zero ou mais erros somente quando a função falha (retorna FALSE); Portanto, um aplicativo chama **SQLInstallerError** somente depois que uma função do instalador ODBC falha.  
  
 A fila de erros do instalador ODBC é liberada sempre que uma nova função de instalador é chamada. Portanto, um aplicativo não se pode esperar recuperar os erros de funções que na última chamada de função do instalador.  
  
 Para recuperar vários erros de uma chamada de função, um aplicativo chama **SQLInstallerError** várias vezes.  
  
 Quando não houver nenhuma informação adicional, **SQLInstallerError** retorna SQL_NO_DATA, o *pfErrorCode* argumento será indefinido, o *pcbErrorMsg* argumento for igual a 0, e o *lpszErrorMsg* argumento contém um único caractere null de terminação (a menos que o *cbErrorMsgMax* argumento for igual a 0).
