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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aeff68aaa4e4901820054a9bf3079efc7d74cebc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818836"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Função SQLWritePrivateProfileString
**Conformidade com**  
 Versão introduziu: ODBC 2.0  
  
 **Resumo**  
 **SQLWritePrivateProfileString** grava um nome de valor e os dados até a subchave ini as informações do sistema.  
  
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
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que contém o nome da seção em que a cadeia de caracteres será copiada. Se a seção não existir, ele é criado. O nome da seção é independente de caso; a cadeia de caracteres pode ser qualquer combinação de letras maiusculas e minúsculas.  
  
 *lpszEntry*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que contém o nome da chave a ser associado uma cadeia de caracteres. Se a chave não existir na seção especificada, ele é criado. Se esse argumento for nulo, a seção inteira, incluindo todas as entradas dentro da seção, é excluída.  
  
 *lpszString*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo a serem gravados no arquivo. Se esse argumento for NULL, a chave apontando para o *lpszEntry* argumento é excluído.  
  
 *lpszFilename*  
 [Saída] Aponta para uma cadeia de caracteres terminada em nulo que nomeia o arquivo de inicialização.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLWritePrivateProfileString** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|Não foi possível gravar as informações solicitadas do sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLWritePrivateProfileString** é fornecido como uma maneira simples de drivers de porta e DLLs de instalação do driver do Microsoft® Windows® para Microsoft Windows/Windows 2000. Chamadas para **WritePrivateProfileString** que gravar uma cadeia de caracteres de perfil para o arquivo ini deve ser substituída por chamadas para **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chama funções na API Win32® para adicionar o nome do valor especificado e os dados até a subchave ini as informações do sistema.  
  
 Um modo de configuração indica em que a entrada ini listando valores DSN é nas informações do sistema. Se o DSN é um DSN de usuário (a variável de estado é USERDSN_ONLY), a função grava a entrada ini em HKEY_CURRENT_USER. Se o DSN é um DSN de sistema (SYSTEMDSN_ONLY), a função grava a entrada ini em HKEY_LOCAL_MACHINE. Se a variável de estado for BOTHDSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usada.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo um valor de informações do sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
