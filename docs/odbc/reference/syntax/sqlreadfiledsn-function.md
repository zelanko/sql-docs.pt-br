---
title: Função SQLReadFileDSN | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad1e3dc4901fc7251528e6040b9250469f8fef6c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053657"
---
# <a name="sqlreadfiledsn-function"></a>Função SQLReadFileDSN
**Conformidade**  
 Versão introduzida: ODBC 3,0  
  
 **Resumo**  
 **SQLReadFileDSN** lê informações de um DSN de arquivo.  
  
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
 Entrada Ponteiro para o buffer de dados que contém o nome do arquivo. DSN. Uma extensão. DSN é anexada a todos os nomes de arquivo que ainda não têm uma extensão. DSN. O valor em * \*lpszFileName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszAppName*  
 Entrada Ponteiro para o buffer de dados que contém o nome do aplicativo. É "ODBC" para a seção ODBC. O valor em * \*lpszAppName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszKeyName*  
 Entrada Ponteiro para o buffer de dados que contém o nome da chave a ser lida. Consulte "Comentários" para palavras-chave reservadas. O valor em * \*lpszAppName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszString*  
 Der Ponteiro para o buffer de dados que contém a cadeia de caracteres associada à chave a ser lida.  
  
 Se * \*lpszFileName* for um nome de arquivo. DSN válido, mas o argumento *lpszAppName* for um ponteiro nulo e o argumento *lpszKeyName* for um ponteiro NULL, * \*lpszString* conterá uma lista de aplicativos válidos. Se * \*lpszFileName* for um nome de arquivo. DSN válido e * \*lpszAppName* for um nome de aplicativo válido, mas o argumento *lpszKeyName* for um ponteiro NULL, * \*lpszString* conterá uma lista de palavras-chave reservadas válidas na seção apropriada do arquivo DSN, delimitada por ponto-e-vírgula. Se * \*lpszFileName* for um nome de arquivo. DSN válido, mas * \*lpszAppName* for um ponteiro nulo e o argumento *lpszKeyName* for um ponteiro NULL, * \*lpszString* conterá uma lista das seções no arquivo DSN, delimitada por ponto-e-vírgula.  
  
 *cbString*  
 Entrada Comprimento do buffer * \*lpszString* .  
  
 *pcbString*  
 Der Número total de bytes disponíveis para retornar em * \*lpszString*. Se o número de bytes disponíveis para retornar for maior ou igual a *cbString*, a cadeia de caracteres de saída em * \*lpszString* será truncada para *cbString* menos o caractere de terminação nula. O argumento *pcbString* pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLReadFileDSN** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O argumento *lpszString* era nulo.<br /><br /> O argumento *cbString* era menor ou igual a 0.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome de arquivo especificado no argumento *lpszFileName* era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O argumento *lpszAppName* era nulo, enquanto o argumento *lpszKeyName* era válido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Cadeia de caracteres de saída truncada|A cadeia de caracteres retornada em * \*lpszString* foi truncada porque o valor em *cbString* era menor ou igual ao valor em * \*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|A palavra-chave não existia no DSN do arquivo.|  
  
## <a name="comments"></a>Comentários  
 O ODBC reserva o nome da seção [ODBC] na qual armazenar as informações de conexão. As palavras-chave reservadas para esta seção são as mesmas que as reservadas para uma cadeia de conexão em **SQLDriverConnect**. (Para obter mais informações, consulte a descrição da função [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .)  
  
 Os aplicativos podem usar essas palavras-chave reservadas para ler as informações em um DSN de arquivo. Se um aplicativo quiser descobrir a cadeia de conexão sem DSN associada a um DSN de arquivo, ele poderá chamar **SQLReadFileDSN** para qualquer uma das palavras-chave da cadeia de conexão reservada na seção [ODBC]. A cadeia de conexão completa passada em uma conexão sem DSN é uma combinação de todas as palavras-chave (reservadas e específicas de driver) na seção [ODBC].  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gravando informações em um DSN de arquivo|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
