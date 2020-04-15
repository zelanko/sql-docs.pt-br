---
title: Função SQLWritefileDSN | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e781f1be79e0079f33b3d0800c665f5f5e9fda4d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286876"
---
# <a name="sqlwritefiledsn-function"></a>Função SQLWriteFileDSN
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLWriteFileDSN** grava informações em um Arquivo DSN.  
  
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
 [Entrada] Ponteiro para o nome do Arquivo DSN. Uma extensão DSN é anexada a todos os nomes de arquivo que ainda não possuem uma extensão DSN.  
  
 *lpszAppName*  
 [Entrada] Ponteiro para o nome da aplicação. Aqui é "ODBC" para a seção ODBC.  
  
 *lpszKeyName*  
 [Entrada] Ponteiro para o nome da chave a ser lida. Consulte "Comentários" para palavras-chave reservadas.  
  
 *lpszString*  
 [Saída] Apontou para a corda associada à chave a ser escrita. O comprimento máximo da string apontado por este argumento é de 32.767 bytes.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLWriteFileDSN** retorna FALSO, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome do arquivo especificado no argumento *lpszFileName* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *lpszAppName*, *lpszKeyName*ou *lpszString* foi NULO.|  
  
## <a name="comments"></a>Comentários  
 A ODBC reserva o nome da seção [ODBC] para armazenar as informações de conexão. As palavras-chave reservadas para esta seção são as mesmas reservadas para uma seqüência de conexão no **SQLDriverConnect**. (Para obter mais informações, consulte a descrição da função [SQLDriverConnect.)](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
 Os aplicativos podem usar essas palavras-chave reservadas para escrever informações diretamente em um DSN de arquivo. Se um aplicativo quiser criar ou modificar a seqüência de conexão sem DSN associada a um DSN de arquivo, ele pode chamar **SQLWriteFileDSN** para qualquer uma das palavras-chave de seqüência de conexão reservada na seção [ODBC].  
  
 Se o argumento *lpszString* for um ponteiro nulo, a palavra-chave apontada pelo argumento *lpszKeyName* será excluída do arquivo .dsn. Se os *argumentos lpszString* e *lpszKeyName* forem ambos ponteiros nulos, a seção apontada pelo argumento *lpszAppName* será excluída do arquivo .dsn.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Leitura de informações de DSNs de arquivo|[SQlReadfiledsn](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
