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
manager: craigg
ms.openlocfilehash: a0ae475ba4dc290f57eadf94d1e45e8a203a7ce5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536594"
---
# <a name="sqlinstallererror-function"></a>Função SQLInstallerError
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallerError** retorna informações de status ou erro para as funções do instalador ODBC.  
  
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
 [Entrada] Número de registro de erro. Números válidos são de 1 a 8.  
  
 *pfErrorCode*  
 [Saída] Código de erro do instalador. (Para obter mais informações, consulte "Comentários".)  
  
 *lpszErrorMsg*  
 [Saída] Ponteiro para o armazenamento para o texto da mensagem de erro.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento máximo do *szErrorMsg* buffer. Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos do caractere nulo de terminação.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento máximo do *szErrorMsg* buffer. Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos do caractere nulo de terminação.  
  
 *pcbErrorMsg*  
 [Saída] Ponteiro para o número total de bytes (exceto o caractere nulo de terminação) disponíveis para retornar na *lpszErrorMsg*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbErrorMsgMax*, o texto da mensagem de erro na *lpszErrorMsg* será truncado com *cbErrorMsgMax* menos o bytes de caractere de finalização null. O *pcbErrorMsg* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLInstallerError** não poste os valores de erro para si mesmo. **SQLInstallerError** retorna SQL_NO_DATA quando não for possível recuperar qualquer informação de erro (caso em que *pfErrorCode* é indefinido). Se **SQLInstallerError** não é possível acessar os valores de erro por qualquer motivo que normalmente retornaria SQL_ERROR, **SQLInstallerError** retornará SQL_ERROR, mas não postar quaisquer valores de erro. Se você não souber o comprimento da cadeia de caracteres de aviso (*lpszErrorMsg*), você pode definir *lpszErrorMsg* como NULL e chame **SQLInstallerError**. **SQLInstallerError** será, em seguida, retornar o comprimento da cadeia de caracteres de aviso no *cbErrorMsgMax*. Se o buffer para a mensagem de erro é curto demais **SQLInstallerError** retorna SQL_SUCCESS_WITH_INFO e retorna a correta *pfErrorCode* valor para **SQLInstallerError**.  
  
 Para determinar se ocorreu um truncamento na mensagem de erro, um aplicativo pode comparar o valor na *cbErrorMsgMax* argumento para o comprimento real do texto da mensagem gravado para o *pcbErrorMsg* argumento. Se ocorrer o truncamento, o comprimento do buffer correto deve ser alocado para *lpszErrorMsg* e **SQLInstallerError** deve ser chamado novamente com a correspondente *iError*registro.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo chama **SQLInstallerError** quando uma chamada anterior para a função do instalador ODBC retorna FALSE. Funções de instalação instalador e o driver ou conversor ODBC lançar zero ou mais erros somente quando a função falhar (retorna FALSE); Portanto, um aplicativo chama **SQLInstallerError** somente depois que uma função do instalador ODBC falha.  
  
 A fila de erros do instalador ODBC é liberada sempre que uma nova função do instalador é chamada. Portanto, um aplicativo não pode esperar recuperar os erros para as funções que da última chamada de função do instalador.  
  
 Para recuperar vários erros para uma chamada de função, um aplicativo chama **SQLInstallerError** várias vezes.  
  
 Quando não há nenhuma informação adicional, **SQLInstallerError** retorne SQL_NO_DATA, o *pfErrorCode* argumento é indefinido, o *pcbErrorMsg* argumento for igual a 0, e o *lpszErrorMsg* argumento contém um único caractere de terminação null (a menos que o *cbErrorMsgMax* argumento for igual a 0).
