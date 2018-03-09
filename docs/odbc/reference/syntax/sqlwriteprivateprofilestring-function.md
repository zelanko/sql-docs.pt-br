---
title: "Função SQLWritePrivateProfileString | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLWritePrivateProfileString
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLWritePrivateProfileString
helpviewer_keywords: SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 081d91ac2c257fbaa60b93de24dd134ea698bcd9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlwriteprivateprofilestring-function"></a>Função SQLWritePrivateProfileString
**Conformidade**  
 Versão introduzidas: ODBC 2.0  
  
 **Resumo**  
 **SQLWritePrivateProfileString** grava um nome de valor e os dados até a subchave Odbc.ini as informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszSection*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que contém o nome da seção para que a cadeia de caracteres será copiada. Se a seção não existir, ele será criado. O nome da seção é independente de caso; a cadeia de caracteres pode ser qualquer combinação de letras maiusculas e minúsculas.  
  
 *lpszEntry*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que contém o nome da chave a ser associado uma cadeia de caracteres. Se a chave não existe na seção especificada, ele será criado. Se esse argumento for nulo, a seção inteira, incluindo todas as entradas na seção, é excluída.  
  
 *lpszString*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo para ser gravado no arquivo. Se esse argumento for nulo, a chave aponta para o *lpszEntry* argumento é excluído.  
  
 *lpszFilename*  
 [Saída] Aponta para uma cadeia de caracteres terminada em nulo que nomeia o arquivo de inicialização.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLWritePrivateProfileString** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|Não foi possível gravar as informações solicitadas do sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLWritePrivateProfileString** é fornecido como uma maneira simples de drivers de porta e DLLs de instalação do driver do Microsoft® Windows® para Microsoft Windows/Windows 2000. Chamadas para **WritePrivateProfileString** que gravar uma cadeia de caracteres de perfil para o arquivo Odbc.ini deve ser substituída por chamadas para **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chama funções na API Win32® para adicionar o nome do valor especificado e os dados até a subchave Odbc.ini as informações do sistema.  
  
 Um modo de configuração indica onde a entrada Odbc.ini listando valores DSN é nas informações do sistema. Se o DSN é um DSN de usuário (a variável de estado é USERDSN_ONLY), a função grava a entrada Odbc.ini em HKEY_CURRENT_USER. Se o DSN é um DSN de sistema (SYSTEMDSN_ONLY), a função grava a entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se a variável de estado é BOTHDSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obter um valor das informações do sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
