---
title: Função SQLWritePrivateProfileString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286879"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Função SQLWritePrivateProfileString
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLWritePrivateProfileString** grava um nome de valor e dados na subchave ODBC. ini das informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszSection*  
 Entrada Aponta para uma cadeia de caracteres terminada em nulo que contém o nome da seção para a qual a cadeia de caracteres será copiada. Se a seção não existir, ela será criada. O nome da seção diferencia maiúsculas de minúsculas; a cadeia de caracteres pode ser qualquer combinação de letras maiúsculas e minúsculas.  
  
 *lpszEntry*  
 Entrada Aponta para uma cadeia de caracteres terminada em nulo que contém o nome da chave a ser associada a uma cadeia de caracteres. Se a chave não existir na seção especificada, ela será criada. Se esse argumento for nulo, a seção inteira, incluindo todas as entradas dentro da seção, será excluída.  
  
 *lpszString*  
 Entrada Aponta para uma cadeia de caracteres terminada em nulo a ser gravada no arquivo. Se esse argumento for nulo, a chave apontada pelo argumento *lpszEntry* será excluída.  
  
 *lpszFilename*  
 Der Aponta para uma cadeia de caracteres terminada em nulo que nomeia o arquivo de inicialização.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLWritePrivateProfileString** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|Não foi possível gravar as informações do sistema solicitadas.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 O **SQLWritePrivateProfileString** é fornecido como uma maneira simples de drivers de porta e DLLs de instalação de driver do Microsoft® Windows® para o Microsoft Windows NT®/Windows 2000. Chamadas para **WritePrivateProfileString** que gravam uma cadeia de caracteres de perfil no arquivo ODBC. ini devem ser substituídas por chamadas para **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chama funções na API de® do Win32 para adicionar o nome de valor e os dados especificados à subchave ODBC. ini das informações do sistema.  
  
 Um modo de configuração indica onde a entrada ODBC. ini que lista os valores de DSN está nas informações do sistema. Se o DSN for um DSN de usuário (a variável de estado é USERDSN_ONLY), a função gravará na entrada ODBC. ini em HKEY_CURRENT_USER. Se o DSN for um DSN do sistema (SYSTEMDSN_ONLY), a função gravará na entrada ODBC. ini no HKEY_LOCAL_MACHINE. Se a variável de estado for BOTHDSN, HKEY_CURRENT_USER for tentado e, se falhar, HKEY_LOCAL_MACHINE será usado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo um valor das informações do sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
