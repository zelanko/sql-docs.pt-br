---
title: Função SQLReadfileDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abda956ee7682c9ac49270e8bf69fb039641790
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303947"
---
# <a name="sqlreadfiledsn-function"></a>Função SQLReadFileDSN
**Conformidade**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLReadFileDSN** lê informações de um Arquivo DSN.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszFileName*  
 [Entrada] Ponteiro para o buffer de dados contendo o nome do arquivo .dsn. Uma extensão .dsn é anexada a todos os nomes de arquivo que ainda não possuem uma extensão .dsn. O valor em * \*lpszFileName* deve ser uma seqüência de seqüência sumida.  
  
 *lpszAppName*  
 [Entrada] Ponteiro para o buffer de dados contendo o nome do aplicativo. Aqui é "ODBC" para a seção ODBC. O valor em * \*lpszAppName* deve ser uma seqüência de terminadas por nulidade.  
  
 *lpszKeyName*  
 [Entrada] Ponteiro para o buffer de dados contendo o nome da chave a ser lida. Consulte "Comentários" para palavras-chave reservadas. O valor em * \*lpszAppName* deve ser uma seqüência de terminadas por nulidade.  
  
 *lpszString*  
 [Saída] Ponteiro para o buffer de dados contendo a seqüência associada com a chave a ser lida.  
  
 Se * \*lpszFileName* é um nome de arquivo .dsn válido, mas o argumento *lpszAppName* é um ponteiro nulo e o argumento *lpszKeyName* é um ponteiro nulo, então * \*lpszString* contém uma lista de aplicativos válidos. Se * \*lpszFileName* é um nome de arquivo .dsn válido e * \*lpszAppName* é um nome de aplicativo válido, mas o argumento *lpszKeyName* é um ponteiro nulo, então * \*lpszString* contém uma lista de palavras-chave reservadas válidas na seção apropriada do arquivo DSN, delimitada por ponto e vírgula. Se * \*lpszFileName* é um nome de arquivo .dsn válido, mas * \*lpszAppName* é um ponteiro nulo e o argumento *lpszKeyName* é um ponteiro nulo, então * \*lpszString* contém uma lista das seções no arquivo DSN, delimitada por ponto e vírgula.  
  
 *cbString*  
 [Entrada] Comprimento do * \*buffer lpszString.*  
  
 *pbString*  
 [Saída] Número total de bytes disponíveis para retornar em * \*lpszString*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbString,* a seqüência de saída no * \*lpszString* será truncada para *cbString* menos o caractere de rescisão nula. O argumento *pcbString* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sQLReadFileDSN** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszString* foi NULO.<br /><br /> O argumento *cbString* foi menor ou igual a 0.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome do arquivo especificado no argumento *lpszFileName* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválida|O argumento *lpszAppName* era NULO, enquanto o argumento *lpszKeyName* era válido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Cadeia de saída truncada|A seqüência retornada em * \*lpszString* foi truncada porque o valor em *cbString* era menor ou igual ao valor em * \*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|A palavra-chave não existia no arquivo DSN.|  
  
## <a name="comments"></a>Comentários  
 A ODBC reserva o nome da seção [ODBC] para armazenar as informações de conexão. As palavras-chave reservadas para esta seção são as mesmas reservadas para uma seqüência de conexão no **SQLDriverConnect**. (Para obter mais informações, consulte a descrição da função [SQLDriverConnect.)](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
 Os aplicativos podem usar essas palavras-chave reservadas para ler as informações em um DSN de arquivo. Se um aplicativo quiser descobrir a seqüência de conexão sem DSN associada a um DSN de arquivo, ele pode chamar **SQLReadFileDSN** para qualquer uma das palavras-chave de seqüência de conexão reservada na seção [ODBC]. A seqüência de conexão completa passada em uma conexão sem DSN é uma combinação de todas as palavras-chave (reservadas e específicas do driver) na seção [ODBC].  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Escrever informações para um Arquivo DSN|[SQLWritefileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
