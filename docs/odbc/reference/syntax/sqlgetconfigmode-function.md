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
manager: craigg
ms.openlocfilehash: 54c8dbed5599952778ca7651acbdb55a21b8f876
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206575"
---
# <a name="sqlgetconfigmode-function"></a>Função SQLGetConfigMode
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLGetConfigMode** recupera o modo de configuração que indica onde a entrada ini listando valores DSN é nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 [Saída] Ponteiro para o buffer que contém o modo de configuração. (Consulte "Comentários".) O valor em  *\*pwConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetConfigMode** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Essa função é usada para determinar onde está a entrada ini listando valores DSN nas informações do sistema. Se  *\*pwConfigMode* é ODBC_USER_DSN, o DSN é um DSN de usuário e a função lê da entrada ini em HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN é um DSN de sistema e a função lê da entrada ini em HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usada.  
  
 Por padrão, **SQLGetConfigMode** retorna ODBC_BOTH_DSN. Quando um DSN de usuário ou um DSN de sistema é criado por uma chamada para **SQLConfigDataSource**, a função define o modo de configuração como ODBC_USER_DSN ou ODBC_SYSTEM_DSN para distinguir os DSNs de sistema e de usuário ao modificar um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Definindo o modo de configuração|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
