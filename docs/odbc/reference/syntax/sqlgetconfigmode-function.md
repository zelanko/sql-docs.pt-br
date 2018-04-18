---
title: Função SQLGetConfigMode | Microsoft Docs
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
ms.topic: article
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c00416f664f8c4e6049b37ee8c408c7c7563a11f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetconfigmode-function"></a>Função SQLGetConfigMode
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLGetConfigMode** recupera o modo de configuração que indica onde a entrada Odbc.ini listando valores DSN é nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pwConfigMode*  
 [Saída] Ponteiro para o buffer que contém o modo de configuração. (Consulte "Comentários".) O valor em  *\*pwConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLGetConfigMode** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 Essa função é usada para determinar onde a entrada Odbc.ini listando valores DSN é nas informações do sistema. Se  *\*pwConfigMode* é ODBC_USER_DSN, o DSN é um DSN de usuário e a função lê da entrada Odbc.ini em HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN é um DSN de sistema e a função lê da entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usado.  
  
 Por padrão, **SQLGetConfigMode** retorna ODBC_BOTH_DSN. Quando um DSN de usuário ou um DSN de sistema é criado por uma chamada para **SQLConfigDataSource**, a função define o modo de configuração para ODBC_USER_DSN ou ODBC_SYSTEM_DSN para distinguir os DSNs de sistema e de usuário ao modificar um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Definir o modo de configuração|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
