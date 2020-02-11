---
title: Função SQLGetConfigMode | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14fb43015db9113262320f78f0bae53f8a168f95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044548"
---
# <a name="sqlgetconfigmode-function"></a>Função SQLGetConfigMode
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLGetConfigMode** recupera o modo de configuração que indica onde a entrada ODBC. ini que lista os valores de DSN está nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 Der Ponteiro para o buffer que contém o modo de configuração. (Consulte "Comentários".) O valor em * \*pwConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetConfigMode** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Essa função é usada para determinar onde a entrada ODBC. ini que lista os valores de DSN está nas informações do sistema. Se * \*pwConfigMode* for ODBC_USER_DSN, o DSN será um DSN de usuário e a função lerá da entrada ODBC. ini no HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN será um DSN de sistema e a função lerá da entrada ODBC. ini no HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER será tentado e, se falhar, HKEY_LOCAL_MACHINE será usado.  
  
 Por padrão, **SQLGetConfigMode** retorna ODBC_BOTH_DSN. Quando um DSN de usuário ou um DSN de sistema é criado por uma chamada para **SQLConfigDataSource**, a função define o modo de configuração como ODBC_USER_DSN ou ODBC_SYSTEM_DSN para distinguir os DSNs do usuário e do sistema ao modificar um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Definindo o modo de configuração|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
