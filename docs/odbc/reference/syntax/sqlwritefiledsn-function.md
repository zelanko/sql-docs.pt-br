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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039432"
---
# <a name="sqlwritefiledsn-function"></a>Função SQLWriteFileDSN
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLWriteFileDSN** grava informações de um DSN de arquivo.  
  
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
 [Entrada] Ponteiro para o nome do DSN de arquivo. Uma extensão DSN é anexada a todos os nomes de arquivo que ainda não tiver uma extensão DSN.  
  
 *lpszAppName*  
 [Entrada] Ponteiro para o nome do aplicativo. Isso é "ODBC" para a seção ODBC.  
  
 *lpszKeyName*  
 [Entrada] Ponteiro para o nome da chave a ser lido. Consulte "Comentários" para palavras-chave reservadas.  
  
 *lpszString*  
 [Saída] Apontada para a cadeia de caracteres associada com a chave a ser gravado. O comprimento máximo da cadeia de caracteres apontada por esse argumento é 32.767 bytes.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLWriteFileDSN** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome do arquivo especificado na *lpszFileName* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *lpszAppName*, *lpszKeyName*, ou *lpszString* argumento era nulo.|  
  
## <a name="comments"></a>Comentários  
 ODBC reserva o nome da seção [ODBC] no qual deseja armazenar as informações de conexão. As palavras-chave reservadas para essa seção são os mesmos reservado para uma cadeia de caracteres de conexão no **SQLDriverConnect**. (Para obter mais informações, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.)  
  
 Aplicativos podem usar essa palavras-chave reservadas para gravar informações diretamente em um DSN de arquivo. Se um aplicativo quiser criar ou modificar a cadeia de conexão sem DSN associada a um DSN de arquivo, ele poderá chamar **SQLWriteFileDSN** para qualquer as palavras-chave de cadeia de caracteres reservados de conexão na seção [ODBC].  
  
 Se o *lpszString* argumento for um ponteiro nulo, a palavra-chave apontada para o *lpszKeyName* argumento será excluído do arquivo. DSN. Se o *lpszString* e *lpszKeyName* argumentos forem nulos, a seção apontada pelo *lpszAppName* argumento será excluído do arquivo. DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Ler as informações de DSNs de arquivos|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
