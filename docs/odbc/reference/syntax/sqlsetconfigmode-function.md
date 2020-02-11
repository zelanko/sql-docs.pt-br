---
title: Função SQLSetConfigMode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2f2bcd3fef2946e5b983c1bbdeee1efe4776512
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018923"
---
# <a name="sqlsetconfigmode-function"></a>Função SQLSetConfigMode
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLSetConfigMode** define o modo de configuração que indica onde a entrada ODBC. ini que lista os valores de DSN está nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *wConfigMode*  
 Entrada O modo de configuração do instalador (consulte "Comentários"). O valor em *wConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLSetConfigMode** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetros inválida|O argumento *wConfigMode* não continha ODBC_USER_DSN, ODBC_SYSTEM_DSN ou ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Comentários  
 Essa função é usada para definir onde a entrada ODBC. ini que lista os valores de DSN está nas informações do sistema. Se *wConfigMode* for ODBC_USER_DSN, o DSN será um DSN de usuário e a função lerá da entrada ODBC. ini no HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN será um DSN de sistema e a função lerá da entrada ODBC. ini no HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER será tentado e, se falhar, HKEY_LOCAL_MACHINE será usado.  
  
 Essa função não afeta **SQLCreateDataSource** e **SQLDriverConnect**. O modo de configuração deve ser definido quando um driver lê do registro chamando **SQLGetPrivateProfileString** ou grava no registro chamando **SQLWritePrivateProfileString**. Chamadas para **SQLGetPrivateProfileString** e **SQLWritePrivateProfileString** usam o modo de configuração para saber em qual parte do registro operar.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** deve ser chamado somente quando necessário; Se o modo estiver definido incorretamente, o instalador ODBC poderá falhar ao funcionar corretamente.  
  
 O **SQLSetConfigMode** faz uma modificação direta do registro do modo de configuração. Isso está além do processo de modificar o modo de configuração por uma chamada para **SQLConfigDataSource**. Uma chamada para **SQLConfigDataSource** define o modo de configuração para distinguir os DSNs do usuário e do sistema ao modificar um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando uma fonte de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Conectando-se a uma fonte de dados usando uma cadeia de conexão ou caixa de diálogo|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperando o modo de configuração|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
