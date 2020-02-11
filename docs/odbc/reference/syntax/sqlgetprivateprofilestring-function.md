---
title: Função SQLGetPrivateProfileString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d58fe69e487b4f61384f9bd146b17c6d9ada9ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061470"
---
# <a name="sqlgetprivateprofilestring-function"></a>Função SQLGetPrivateProfileString
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLGetPrivateProfileString** Obtém uma lista de nomes de valores ou dados correspondentes a um valor das informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszSection*  
 Entrada Aponta para uma cadeia de caracteres terminada em nulo que especifica a seção que contém o nome da chave. Se esse argumento for nulo, a função copiará todos os nomes de seção no arquivo para o buffer fornecido.  
  
 *lpszEntry*  
 Entrada Aponta para a cadeia de caracteres terminada em nulo que contém o nome da chave cuja cadeia de caracteres associada deve ser recuperada. Se esse argumento for nulo, todos os nomes de chave na seção especificada pelo argumento *lpszSection* serão copiados para o buffer especificado pelo argumento *RetBuffer* .  
  
 *lpszDefault*  
 Entrada Aponta para uma cadeia de caracteres terminada em nulo que especifica o valor padrão para a chave fornecida se a chave não puder ser encontrada no arquivo de inicialização. Este argumento não pode ser nulo.  
  
 *RetBuffer*  
 Der Aponta para o buffer que recebe a cadeia de caracteres recuperada.  
  
 *cbRetBuffer*  
 Entrada Especifica o tamanho, em caracteres, do buffer apontado pelo argumento *RetBuffer* .  
  
 *lpszFilename*  
 Entrada Aponta para uma cadeia de caracteres terminada em nulo que nomeia o arquivo de inicialização. Se esse argumento não contiver um caminho completo para o arquivo, o diretório padrão será pesquisado.  
  
## <a name="returns"></a>Retornos  
 **SQLGetPrivateProfileString** retorna um valor inteiro que indica o número de caracteres lidos.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando uma chamada para **SQLGetPrivateProfileString** falha, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 O **SQLGetPrivateProfileString** é fornecido como uma maneira simples de drivers de porta e DLLs de instalação de driver do Microsoft® Windows® para o Microsoft Windows NT®/Windows 2000. Chamadas para **GetPrivateProfileString** que recuperam uma cadeia de caracteres de perfil do arquivo ODBC. ini devem ser substituídas por chamadas para **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** chama funções na API de® do Win32 para recuperar os nomes solicitados de valores ou dados correspondentes a um valor da subchave ODBC. ini das informações do sistema.  
  
 O modo de configuração (conforme definido por **SQLSetConfigMode**) indica onde a entrada ODBC. ini que lista os valores de DSN está nas informações do sistema. Se o DSN for um DSN de usuário (o modo de configuração é USERDSN_ONLY), a função lerá da entrada ODBC. ini no HKEY_CURRENT_USER. Se o DSN for um DSN do sistema (SYSTEMDSN_ONLY), a função lerá da entrada ODBC. ini no HKEY_LOCAL_MACHINE. Se o modo de configuração for BOTHDSN, HKEY_CURRENT_USER será tentado e, se falhar, HKEY_LOCAL_MACHINE será usado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gravando um valor nas informações do sistema|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
