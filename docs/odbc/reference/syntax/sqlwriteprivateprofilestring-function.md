---
description: Função SQLWritePrivateProfileString
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
ms.openlocfilehash: b1110b60d6dc0ba079804ba8a9f21c06f0c1f78d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420950"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Função SQLWritePrivateProfileString
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLWritePrivateProfileString** grava um nome de valor e dados na subchave Odbc.ini das informações do sistema.  
  
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
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLWritePrivateProfileString** retorna false, um valor * \* pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \* pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|Não foi possível gravar as informações do sistema solicitadas.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 O **SQLWritePrivateProfileString** é fornecido como uma maneira simples de drivers de porta e DLLs de instalação de driver do Microsoft® Windows® para o Microsoft Windows NT®/Windows 2000. Chamadas para **WritePrivateProfileString** que gravam uma cadeia de caracteres de perfil para o arquivo de Odbc.ini devem ser substituídas por chamadas para **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chama funções na API de® do Win32 para adicionar o nome de valor e os dados especificados à subchave Odbc.ini das informações do sistema.  
  
 Um modo de configuração indica onde os valores de DSN da listagem de Odbc.ini de entrada estão nas informações do sistema. Se o DSN for um DSN de usuário (a variável de estado é USERDSN_ONLY), a função gravará na entrada de Odbc.ini no HKEY_CURRENT_USER. Se o DSN for um DSN do sistema (SYSTEMDSN_ONLY), a função gravará na entrada de Odbc.ini no HKEY_LOCAL_MACHINE. Se a variável de estado for BOTHDSN, HKEY_CURRENT_USER for tentado e, se falhar, HKEY_LOCAL_MACHINE será usado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo um valor das informações do sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
