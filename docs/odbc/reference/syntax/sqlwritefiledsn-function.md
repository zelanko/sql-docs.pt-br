---
title: Função SQLWriteFileDSN | Microsoft Docs
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d317d0c4bd4097a5fd5ba9040497977c6fe75199
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlwritefiledsn-function"></a>Função SQLWriteFileDSN
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLWriteFileDSN** grava informações de um DSN de arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 [Entrada] Ponteiro para o nome do arquivo DSN. Uma extensão DSN é acrescentada a todos os nomes de arquivo que ainda não tiver uma extensão DSN.  
  
 *lpszAppName*  
 [Entrada] Ponteiro para o nome do aplicativo. Isso é "ODBC" para a seção ODBC.  
  
 *lpszKeyName*  
 [Entrada] Ponteiro para o nome da chave a ser lido. Consulte "Comentários" para palavras-chave reservadas.  
  
 *lpszString*  
 [Saída] Apontada para a cadeia de caracteres associada com a chave a ser gravado. O comprimento máximo da cadeia de caracteres apontada por esse argumento é 32.767 bytes.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLWriteFileDSN** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome do arquivo especificado no *lpszFileName* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *lpszAppName*, *lpszKeyName*, ou *lpszString* argumento era nulo.|  
  
## <a name="comments"></a>Comentários  
 ODBC reserva o nome da seção [ODBC] no qual deseja armazenar as informações de conexão. Palavras-chave reservadas para essa seção são os mesmos reservado para uma cadeia de conexão na **SQLDriverConnect**. (Para obter mais informações, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.)  
  
 Aplicativos podem usar essa palavras-chave reservadas para gravar informações diretamente em um DSN de arquivo. Se um aplicativo precisar criar ou modificar a cadeia de conexão sem DSN associada a um DSN de arquivo, ele pode chamar **SQLWriteFileDSN** para qualquer as palavras-chave de cadeia de caracteres reservados de conexão na seção [ODBC].  
  
 Se o *lpszString* argumento é um ponteiro nulo, a palavra-chave apontada para o *lpszKeyName* argumento será excluído do arquivo. DSN. Se o *lpszString* e *lpszKeyName* argumentos são ambos os ponteiros nulos, a seção apontada pelo *lpszAppName* argumento será excluído do arquivo. DSN.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Ler as informações de DSNs de arquivos|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
