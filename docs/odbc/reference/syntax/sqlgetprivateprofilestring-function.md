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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061470"
---
# <a name="sqlgetprivateprofilestring-function"></a>Função SQLGetPrivateProfileString
**Conformidade com**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLGetPrivateProfileString** obtém uma lista de nomes de valores ou dados que correspondem a um valor de informações do sistema.  
  
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
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que especifica a seção que contém o nome da chave. Se esse argumento for nulo, a função copia todos os nomes de seção no arquivo para o buffer fornecido.  
  
 *lpszEntry*  
 [Entrada] Aponta para a cadeia de caracteres terminada em nulo que contém o nome da chave cuja cadeia de caracteres associada deve ser recuperado. Se esse argumento for NULL, todos os nomes de chave de na seção especificada o *lpszSection* argumento são copiados para o buffer especificado pelo *RetBuffer* argumento.  
  
 *lpszDefault*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que especifica o valor padrão para a chave especificada se a chave não pode ser encontrada no arquivo de inicialização. Esse argumento não pode ser NULL.  
  
 *RetBuffer*  
 [Saída] Aponta para o buffer que recebe a cadeia de caracteres recuperada.  
  
 *cbRetBuffer*  
 [Entrada] Especifica o tamanho, em caracteres, do buffer apontado pela *RetBuffer* argumento.  
  
 *lpszFilename*  
 [Entrada] Aponta para uma cadeia de caracteres terminada em nulo que nomeia o arquivo de inicialização. Se esse argumento não contiver um caminho completo para o arquivo, o diretório padrão é pesquisado.  
  
## <a name="returns"></a>Retorna  
 **SQLGetPrivateProfileString** retorna um valor inteiro que indica o número de caracteres lidos.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando uma chamada para **SQLGetPrivateProfileString** falhar, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetPrivateProfileString** é fornecido como uma maneira simples de drivers de porta e DLLs de instalação do driver do Microsoft® Windows® para Microsoft Windows/Windows 2000. Chamadas para **GetPrivateProfileString** que recuperar uma cadeia de caracteres de perfil do arquivo ini deve ser substituída por chamadas para **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** chama funções na API Win32® para recuperar os nomes solicitados de valores ou dados correspondentes a um valor da subchave ini as informações do sistema.  
  
 O modo de configuração (conforme definido pela **SQLSetConfigMode**) indica em que a entrada ini listando valores DSN é nas informações do sistema. Se o DSN é um DSN de usuário (o modo de configuração é USERDSN_ONLY), a função lê da entrada ini em HKEY_CURRENT_USER. Se o DSN é um DSN de sistema (SYSTEMDSN_ONLY), a função lê da entrada ini em HKEY_LOCAL_MACHINE. Se o modo de configuração for BOTHDSN, HKEY_CURRENT_USER é tentada e se ele falhar, HKEY_LOCAL_MACHINE é usada.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Gravação de um valor para as informações do sistema|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
