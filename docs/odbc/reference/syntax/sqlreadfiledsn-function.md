---
title: Função SQLReadFileDSN | Microsoft Docs
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
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1db13b239a2cf9e1f121336e792333b70f042ed8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlreadfiledsn-function"></a>Função SQLReadFileDSN
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **SQLReadFileDSN** lê as informações de um DSN de arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Ponteiro para o buffer de dados que contém o nome do arquivo. DSN. Uma extensão. DSN é acrescentada a todos os nomes de arquivo que não têm uma extensão. DSN. O valor em  *\*lpszFileName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszAppName*  
 [Entrada] Ponteiro para o buffer de dados que contém o nome do aplicativo. Isso é "ODBC" para a seção ODBC. O valor em  *\*lpszAppName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszKeyName*  
 [Entrada] Ponteiro para o buffer de dados que contém o nome da chave a ser lido. Consulte "Comentários" para palavras-chave reservadas. O valor em  *\*lpszAppName* deve ser uma cadeia de caracteres terminada em nulo.  
  
 *lpszString*  
 [Saída] Ponteiro para o buffer de dados que contém a cadeia de caracteres associada com a chave a ser lido.  
  
 Se  *\*lpszFileName* é um nome de arquivo. DSN válido, mas o *lpszAppName* argumento é um ponteiro nulo e o *lpszKeyName* argumento é um ponteiro nulo, em seguida,  *\*lpszString* contém uma lista de aplicativos válidos. Se  *\*lpszFileName* é um nome de arquivo. DSN válido e  *\*lpszAppName* é um nome de aplicativo válido, mas o *lpszKeyName* argumento é nulo ponteiro, em seguida,  *\*lpszString* contém uma lista de válido palavras-chave reservadas na seção apropriada do arquivo DSN, delimitada por ponto e vírgula. Se  *\*lpszFileName* é um nome de arquivo. DSN válido, mas  *\*lpszAppName* é um ponteiro nulo e o *lpszKeyName* argumento é um ponteiro nulo, em seguida,  *\*lpszString* contém uma lista das seções no arquivo DSN, delimitada por ponto e vírgula.  
  
 *cbString*  
 [Entrada] Comprimento do  *\*lpszString* buffer.  
  
 *pcbString*  
 [Saída] Número total de bytes disponíveis para retornar em  *\*lpszString*. Se o número de bytes disponíveis para retornar é maior que ou igual a *cbString*, a cadeia de caracteres de saída em  *\*lpszString* será truncado para *cbString* menos o caractere null de terminação. O *pcbString* argumento pode ser um ponteiro nulo.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLReadFileDSN** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Comprimento de buffer inválido|O *lpszString* argumento era nulo.<br /><br /> O *cbString* argumento era menor ou igual a 0.|  
|ODBC_ERROR_INVALID_PATH|Caminho de instalação inválido|O caminho do nome do arquivo especificado no *lpszFileName* argumento era inválido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitação inválido|O *lpszAppName* argumento era nulo, enquanto o *lpszKeyName* argumento era válido.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Cadeia de caracteres de saída truncada|A cadeia de caracteres retornada em  *\*lpszString* foi truncado porque o valor em *cbString* era menor ou igual ao valor no  *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|A palavra-chave não existe no arquivo DSN.|  
  
## <a name="comments"></a>Comentários  
 ODBC reserva o nome da seção [ODBC] no qual deseja armazenar as informações de conexão. Palavras-chave reservadas para essa seção são os mesmos reservado para uma cadeia de conexão na **SQLDriverConnect**. (Para obter mais informações, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.)  
  
 Aplicativos podem usar essa palavras-chave reservadas para ler as informações em um DSN de arquivo. Se desejar que um aplicativo descobrir a cadeia de conexão sem DSN associada a um DSN de arquivo, ele pode chamar **SQLReadFileDSN** para qualquer as palavras-chave de cadeia de caracteres reservados de conexão na seção [ODBC]. A cadeia de caracteres de conexão completa passada em uma conexão sem DSN é uma combinação de todas as palavras-chave (reservadas e específicos de driver) na seção [ODBC].  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gravar informações em um DSN de arquivo|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
