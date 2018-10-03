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
manager: craigg
ms.openlocfilehash: d520a84d45e3552f5e260778b5cacf2ac91f05a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654374"
---
# <a name="sqlsetconfigmode-function"></a>Função SQLSetConfigMode
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLSetConfigMode** define o modo de configuração que indica onde a entrada ini listando valores DSN é nas informações do sistema.  
  
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
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetConfigMode** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequência de parâmetro inválido|O *wConfigMode* argumento não continha ODBC_USER_DSN, ODBC_SYSTEM_DSN ou ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Comentários  
 Essa função é usada para definir onde a entrada ini listando valores DSN é nas informações do sistema. Se *wConfigMode* é ODBC_USER_DSN, o DSN é um DSN de usuário e a função lê da entrada ini em HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN é um DSN de sistema e a função lê da entrada ini em HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usada.  
  
 Essa função não afeta **SQLCreateDataSource** e **SQLDriverConnect**. O modo de configuração deve ser definida quando um driver lê do registro chamando **SQLGetPrivateProfileString** ou grava no registro chamando **SQLWritePrivateProfileString**. Chamadas para **SQLGetPrivateProfileString** e **SQLWritePrivateProfileString** usar o modo de configuração para saber qual parte do registro no qual operar.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** deve ser chamado somente quando necessário; se o modo for definido incorretamente, o instalador de ODBC podem não funcionar corretamente.  
  
 **SQLSetConfigMode** faz uma modificação do registro direto do modo de configuração. Isso está além do processo de modificar o modo de configuração por uma chamada para **SQLConfigDataSource**. Uma chamada para **SQLConfigDataSource** define o modo de configuração para distinguir os DSNs de sistema e de usuário durante a modificação de um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando uma fonte de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Conectando a uma fonte de dados usando uma caixa de diálogo ou de cadeia de caracteres de conexão|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperando o modo de configuração|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
