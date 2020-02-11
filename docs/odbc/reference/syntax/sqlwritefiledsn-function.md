---
title: Função SQLWriteFileDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b1ce34074a2326d17a199537b308a9a670d8163
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039432"
---
# <a name="sqlwritefiledsn-function"></a>Função SQLWriteFileDSN
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLWriteFileDSN** grava informações em um DSN de arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 Entrada Ponteiro para o nome do DSN do arquivo. Uma extensão DSN é anexada a todos os nomes de arquivo que ainda não têm uma extensão DSN.  
  
 *lpszAppName*  
 Entrada Ponteiro para o nome do aplicativo. É "ODBC" para a seção ODBC.  
  
 *lpszKeyName*  
 Entrada Ponteiro para o nome da chave a ser lida. Consulte "Comentários" para palavras-chave reservadas.  
  
 *lpszString*  
 Der Apontado para a cadeia de caracteres associada à chave a ser gravada. O comprimento máximo da cadeia de caracteres apontada por esse argumento é de 32.767 bytes.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLWriteFileDSN** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome de arquivo especificado no argumento *lpszFileName* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *lpszAppName*, *lpszKeyName*ou *lpszString* era nulo.|  
  
## <a name="comments"></a>Comentários  
 O ODBC reserva o nome da seção [ODBC] na qual armazenar as informações de conexão. As palavras-chave reservadas para esta seção são as mesmas que as reservadas para uma cadeia de conexão em **SQLDriverConnect**. (Para obter mais informações, consulte a descrição da função [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .)  
  
 Os aplicativos podem usar essas palavras-chave reservadas para gravar informações diretamente em um DSN de arquivo. Se um aplicativo quiser criar ou modificar a cadeia de conexão sem DSN associada a um DSN de arquivo, ele poderá chamar **SQLWriteFileDSN** para qualquer uma das palavras-chave da cadeia de conexão reservada na seção [ODBC].  
  
 Se o argumento *lpszString* for um ponteiro NULL, a palavra-chave apontada pelo argumento *lpszKeyName* será excluída do arquivo. DSN. Se os argumentos *lpszString* e *lpszKeyName* forem ambos ponteiros nulos, a seção apontada pelo argumento *lpszAppName* será excluída do arquivo. DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Lendo informações de DSNs de arquivo|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
