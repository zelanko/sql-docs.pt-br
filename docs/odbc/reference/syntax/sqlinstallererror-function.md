---
title: Função SQLInstallerError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab9461d87a3df2efc98c38e4c72cee4c247fee7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138034"
---
# <a name="sqlinstallererror-function"></a>Função SQLInstallerError
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLInstallerError** retorna informações de erro ou de status para as funções do ODBC Installer.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *iError*  
 Entrada Número do registro de erro. Os números válidos são de 1 a 8.  
  
 *pfErrorCode*  
 Der Código de erro do instalador. (Para obter mais informações, consulte "Comentários".)  
  
 *lpszErrorMsg*  
 Der Ponteiro para armazenamento do texto da mensagem de erro.  
  
 *cbErrorMsgMax*  
 Entrada Comprimento máximo do buffer *szErrorMsg* . Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos o caractere de terminação nula.  
  
 *cbErrorMsgMax*  
 Entrada Comprimento máximo do buffer *szErrorMsg* . Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos o caractere de terminação nula.  
  
 *pcbErrorMsg*  
 Der Aponta para o número total de bytes (excluindo o caractere de terminação nula) disponível para retornar em *lpszErrorMsg*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbErrorMsgMax*, o texto da mensagem de erro em *lpszErrorMsg* será truncado para *cbErrorMsgMax* menos os bytes de caractere de terminação nula. O argumento *pcbErrorMsg* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLInstallerError** não publica valores de erro para si mesmo. **SQLInstallerError** retorna SQL_NO_DATA quando não é possível recuperar informações de erro (nesse caso, *pfErrorCode* é indefinido). Se **SQLInstallerError** não puder acessar valores de erro por qualquer motivo que normalmente retornasse SQL_ERROR, **SQLInstallerError** retornará SQL_ERROR mas não publicará nenhum valor de erro. Se você não souber o comprimento da cadeia de caracteres de aviso (*lpszErrorMsg*), poderá definir *lpszErrorMsg* como nulo e chamar **SQLInstallerError**. **SQLInstallerError** retornará o comprimento da cadeia de caracteres de aviso em *cbErrorMsgMax*. Se o buffer da mensagem de erro for muito curto, **SQLInstallerError** retornará SQL_SUCCESS_WITH_INFO e retornará o valor de *PfErrorCode* correto para **SQLInstallerError**.  
  
 Para determinar se um truncamento ocorreu na mensagem de erro, um aplicativo pode comparar o valor no argumento *cbErrorMsgMax* com o comprimento real do texto da mensagem gravado no argumento *pcbErrorMsg* . Se ocorrer truncamento, o comprimento de buffer correto deve ser alocado para *lpszErrorMsg* e **SQLInstallerError** deve ser chamado novamente com o registro *iError* correspondente.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo chama **SQLInstallerError** quando uma chamada anterior à função ODBC Installer retorna false. As funções de instalação do instalador ODBC e do driver ou do tradutor só postam zero ou mais erros quando a função falha (retorna FALSE); Portanto, um aplicativo chama **SQLInstallerError** somente depois que uma função ODBC Installer falha.  
  
 A fila de erros do instalador ODBC é liberada toda vez que uma nova função do instalador é chamada. Portanto, um aplicativo não pode esperar a recuperação de erros para funções que não sejam da última chamada de função do instalador.  
  
 Para recuperar vários erros de uma chamada de função, um aplicativo chama **SQLInstallerError** várias vezes.  
  
 Quando não há nenhuma informação adicional, **SQLInstallerError** retorna SQL_NO_DATA, o argumento *pfErrorCode* é indefinido, o argumento *pcbErrorMsg* é igual a 0 e o argumento *lpszErrorMsg* contém um único caractere de terminação nula (a menos que o argumento *cbErrorMsgMax* seja igual a 0).
