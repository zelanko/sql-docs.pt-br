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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053657"
---
# <a name="sqlreadfiledsn-function"></a>Função SQLReadFileDSN
**Conformidade com**  
 Versão introduzida: ODBC 3.0  
  
 **Resumo**  
 **SQLReadFileDSN** lê as informações de um DSN de arquivo.  
  
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
 [Entrada] Ponteiro para o buffer de dados que contém o nome do arquivo. DSN. Uma extensão. DSN é anexada a todos os nomes de arquivo que ainda não tiver uma extensão. DSN. O valor em  *\*lpszFileName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszAppName*  
 [Entrada] Ponteiro para o buffer de dados que contém o nome do aplicativo. Isso é "ODBC" para a seção ODBC. O valor em  *\*lpszAppName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszKeyName*  
 [Entrada] Ponteiro para o buffer de dados que contém o nome da chave a ser lido. Consulte "Comentários" para palavras-chave reservadas. O valor em  *\*lpszAppName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszString*  
 [Saída] Ponteiro para o buffer de dados que contém a cadeia de caracteres associada com a chave a ser lido.  
  
 Se  *\*lpszFileName* é um nome de arquivo. DSN válido, mas o *lpszAppName* argumento for um ponteiro nulo e o *lpszKeyName* argumento for um ponteiro nulo, em seguida,  *\*lpszString* contém uma lista de aplicativos válidos. Se  *\*lpszFileName* é um nome de arquivo. DSN válido e  *\*lpszAppName* é um nome de aplicativo válido, mas o *lpszKeyName* argumento é um valor nulo em seguida, ponteiro  *\*lpszString* contém uma lista de válido palavras-chave reservadas na seção apropriada do arquivo DSN, delimitado por ponto e vírgula. Se  *\*lpszFileName* é um nome de arquivo. DSN válido, mas  *\*lpszAppName* for um ponteiro nulo e o *lpszKeyName* argumento for um ponteiro nulo, em seguida  *\*lpszString* contém uma lista das seções no arquivo DSN, delimitados por ponto e vírgula.  
  
 *cbString*  
 [Entrada] Comprimento do  *\*lpszString* buffer.  
  
 *pcbString*  
 [Saída] Número total de bytes disponíveis para retornar na  *\*lpszString*. Se o número de bytes disponíveis para retornar for maior que ou igual a *cbString*, a cadeia de caracteres de saída na  *\*lpszString* será truncado com *cbString* menos o caractere nulo de terminação. O *pcbString* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLReadFileDSN** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszString* argumento era nulo.<br /><br /> O *cbString* argumento era menor que ou igual a 0.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome do arquivo especificado na *lpszFileName* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *lpszAppName* argumento era nulo, enquanto o *lpszKeyName* argumento era válido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Cadeia de caracteres de saída truncada|A cadeia de caracteres retornada na  *\*lpszString* foi truncado porque o valor na *cbString* era menor que ou igual ao valor na  *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|A palavra-chave não existia no arquivo DSN.|  
  
## <a name="comments"></a>Comentários  
 ODBC reserva o nome da seção [ODBC] no qual deseja armazenar as informações de conexão. As palavras-chave reservadas para essa seção são os mesmos reservado para uma cadeia de caracteres de conexão no **SQLDriverConnect**. (Para obter mais informações, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.)  
  
 Aplicativos podem usar essa palavras-chave reservadas para ler as informações em um DSN de arquivo. Se desejar obter um aplicativo descobrir a cadeia de conexão sem DSN associada a um DSN de arquivo, ele pode chamar **SQLReadFileDSN** para qualquer as palavras-chave de cadeia de caracteres reservados de conexão na seção [ODBC]. A cadeia de caracteres de conexão completa passada em uma conexão sem DSN é uma combinação de todas as palavras-chave (reservadas e específicos de driver) na seção [ODBC].  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gravar informações em um DSN de arquivo|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
