---
title: "Função SQLSetConfigMode | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8919f758c486e6569b9620fcaa7bcf76f4dac0f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconfigmode-function"></a>Função SQLSetConfigMode
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLSetConfigMode** define o modo de configuração que indica onde a entrada Odbc.ini listando valores DSN é nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *wConfigMode*  
 [Entrada] O modo de configuração do instalador (consulte "Comentários"). O valor em *wConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLSetConfigMode** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetro inválido|O *wConfigMode* argumento não continha ODBC_USER_DSN, ODBC_SYSTEM_DSN ou ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Comentários  
 Essa função é usada para definir onde a entrada Odbc.ini listando valores DSN é nas informações do sistema. Se *wConfigMode* é ODBC_USER_DSN, o DSN é um DSN de usuário e a função lê da entrada Odbc.ini em HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN é um DSN de sistema e a função lê da entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usado.  
  
 Essa função não afeta **SQLCreateDataSource** e **SQLDriverConnect**. O modo de configuração deve ser definida quando um driver lê o registro chamando **SQLGetPrivateProfileString** ou grava o registro chamando **SQLWritePrivateProfileString**. Chamadas para **SQLGetPrivateProfileString** e **SQLWritePrivateProfileString** usar o modo de configuração para saber qual parte do registro para operar.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** deve ser chamado somente quando necessário; se o modo for definido incorretamente, o instalador de ODBC podem não funcionar corretamente.  
  
 **SQLSetConfigMode** faz com que uma modificação de registro direto do modo de configuração. Isso está além do processo de modificar o modo de configuração por uma chamada para **SQLConfigDataSource**. Uma chamada para **SQLConfigDataSource** define o modo de configuração para distinguir os DSNs de sistema e de usuário ao modificar um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criar uma fonte de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Conectando a uma fonte de dados usando uma caixa de diálogo ou cadeia de caracteres de conexão|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperando o modo de configuração|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|

