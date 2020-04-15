---
title: Função sqlinstallerError | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e749237cf87c5054b8273f38531d9336d316e040
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302097"
---
# <a name="sqlinstallererror-function"></a>Função SQLInstallerError
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLInstallerError** retorna informações de erro ou status para as funções do instalador ODBC.  
  
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
 [Entrada] Número do registro de erro. Os números válidos são de 1 a 8.  
  
 *pfErrorCode*  
 [Saída] Código de erro do instalador. (Para obter mais informações, consulte "Comentários").)  
  
 *lpszErrorMsg*  
 [Saída] Ponteiro para armazenamento para o texto da mensagem de erro.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento máximo do buffer *szErrorMsg.* Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos o caractere de rescisão nula.  
  
 *cbErrorMsgMax*  
 [Entrada] Comprimento máximo do buffer *szErrorMsg.* Isso deve ser menor ou igual a SQL_MAX_MESSAGE_LENGTH menos o caractere de rescisão nula.  
  
 *pcbErrorMsg*  
 [Saída] Ponteiro para o número total de bytes (excluindo o caractere de rescisão nula) disponível para retornar em *lpszErrorMsg*. Se o número de bytes disponíveis para retornar for maior ou igual ao *cbErrorMsgMax,* o texto da mensagem de erro no *lpszErrorMsg* será truncado para *cbErrorMsgMax* menos os bytes de caractere de rescisão nula. O *argumento pcbErrorMsg* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA ou SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLInstallerError** não posta valores de erro para si mesmo. **SQLInstallerError** retorna SQL_NO_DATA quando não consegue recuperar qualquer informação de erro (nesse *caso, pfErrorCode* está indefinido). Se **o SQLInstallerError** não puder acessar valores de erro por qualquer motivo que normalmente retorne SQL_ERROR, **o SQLInstallerError** retorna SQL_ERROR mas não publica nenhum valor de erro. Se você não souber o comprimento da seqüência de avisos *(lpszErrorMsg),* você pode definir *lpszErrorMsg* para NULL e chamar **SQLInstallerError**. **SQLInstallerError** retornará o comprimento da seqüência de avisos no *cbErrorMsgMax*. Se o buffer da mensagem de erro for muito curto, **o SQLInstallerError** retorna SQL_SUCCESS_WITH_INFO e retorna o valor correto *pfErrorCode* para **SQLInstallerError**.  
  
 Para determinar se uma truncação ocorreu na mensagem de erro, um aplicativo pode comparar o valor no argumento *cbErrorMsgMax* com o comprimento real do texto da mensagem escrito para o argumento *pcbErrorMsg.* Se a truncação ocorrer, o comprimento de buffer correto deve ser alocado para *lpszErrorMsg* e **SQLInstallerError** deve ser chamado novamente com o registro *iError* correspondente.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo chama **SQLInstallerError** quando uma chamada anterior para a função instalador oDBC retorna FALSA. Funções de instalação e configuração do instalador e do driver ou tradutor do ODBC postam zero ou mais erros somente quando a função falha (retorna FALSE); portanto, um aplicativo chama **SQLInstallerError** somente após a falha de uma função do instalador ODBC.  
  
 A fila de erro do instalador ODBC é lavada cada vez que uma nova função de instalador é chamada. Portanto, um aplicativo não pode esperar recuperar erros para funções que não a partir da chamada de função do último instalador.  
  
 Para recuperar vários erros para uma chamada de função, um aplicativo chama **SQLInstallerError** várias vezes.  
  
 Quando não há informações adicionais, **o SQLInstallerError** retorna SQL_NO_DATA, o argumento *pfErrorCode* é indefinido, o argumento *pcbErrorMsg* é igual a 0 e o argumento *lpszErrorMsg* contém um único caractere de rescisão nula (a menos que o argumento *cbErrorMsgMax* seja igual a 0).
