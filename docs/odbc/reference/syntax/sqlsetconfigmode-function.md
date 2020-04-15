---
title: Função SQLSetConfigmode | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293276"
---
# <a name="sqlsetconfigmode-function"></a>Função SQLSetConfigMode
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLSetConfigMode** define o modo de configuração que indica onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argumentos  
 *wConfigMode*  
 [Entrada] O modo de configuração do instalador (consulte "Comentários"). O valor no *wConfigMode* pode ser:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetConfigMode** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Seqüência de parâmetros inválidos|O argumento *wConfigMode* não continha ODBC_USER_DSN, ODBC_SYSTEM_DSN ou ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Comentários  
 Esta função é usada para definir onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema. Se *o wConfigMode* estiver ODBC_USER_DSN, o DSN é um DSN do usuário e a função será lida a partir da entrada Odbc.ini em HKEY_CURRENT_USER. Se for ODBC_SYSTEM_DSN, o DSN é um Sistema DSN e a função é lida a partir da entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se for ODBC_BOTH_DSN, HKEY_CURRENT_USER é tentado, e se falhar, HKEY_LOCAL_MACHINE é usado.  
  
 Esta função não afeta **sqlCreateDataSource** e **SQLDriverConnect**. O modo de configuração deve ser definido quando um driver lê do registro ligando para **SQLGetPrivateProfileString** ou grava ndo para o registro, chamando **SQLWritePrivateProfileString**. Chamadas para **SQLGetPrivateProfileString** e **SQLWritePrivateProfileString** usam o modo de configuração para saber em qual parte do registro operar.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** deve ser chamado somente quando necessário; se o modo estiver configurado incorretamente, o Instalador ODBC pode não funcionar corretamente.  
  
 **SQLSetConfigMode** faz uma modificação direta do registro do modo de configuração. Isso é diferente do processo de modificação do modo de configuração por uma chamada para **SQLConfigDataSource**. Uma chamada para **SQLConfigDataSource** define o modo de configuração para distinguir DSNs do usuário e do sistema ao modificar um DSN. Antes de retornar, **SQLConfigDataSource** redefine o modo de configuração para BOTHDSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando uma fonte de dados|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Conectando-se a uma fonte de dados usando uma seqüência de conexão ou caixa de diálogo|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperando o modo de configuração|[Modo SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
