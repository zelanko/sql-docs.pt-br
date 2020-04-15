---
title: Função SQLGetConfigmode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc11bec24ede3352dd43f3645fb8c720b77fdabe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285686"
---
# <a name="sqlgetconfigmode-function"></a>Função SQLGetConfigMode
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLGetConfigMode** recupera o modo de configuração que indica onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 [Saída] Ponteiro para o buffer contendo o modo de configuração. (Veja "Comentários".) O valor em * \*pwConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetConfigMode** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Esta função é usada para determinar onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema. Se * \*o pwConfigMode* estiver ODBC_USER_DSN, o DSN é um DSN do usuário e a função será lida a partir da entrada Odbc.ini em HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN é um Sistema DSN e a função é lida a partir da entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER é tentado, e se falhar, HKEY_LOCAL_MACHINE é usado.  
  
 Por padrão, **SQLGetConfigMode** retorna ODBC_BOTH_DSN. Quando um DSN do usuário ou um DSN do sistema é criado por uma chamada para **SQLConfigDataSource,** a função define o modo de configuração para ODBC_USER_DSN ou ODBC_SYSTEM_DSN para distinguir DSNs do usuário e do sistema enquanto modifica um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Definindo o modo de configuração|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
