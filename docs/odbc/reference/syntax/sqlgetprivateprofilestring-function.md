---
title: SQLGetPrivateProfilestring function | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c12fc8d08535960cbb239c14e017b2ad5faa6c0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303288"
---
# <a name="sqlgetprivateprofilestring-function"></a>Função SQLGetPrivateProfileString
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLGetPrivateProfileString** recebe uma lista de nomes de valores ou dados correspondentes a um valor das informações do sistema.  
  
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
 *Lpszsection*  
 [Entrada] Aponta para uma seqüência de terminadas nula que especifica a seção que contém o nome da chave. Se esse argumento for NULO, a função copiará todos os nomes de seção no arquivo para o buffer fornecido.  
  
 *Lpszentry*  
 [Entrada] Aponta para a seqüência de terminadas nula contendo o nome da chave cuja seqüência associada deve ser recuperada. Se esse argumento for NULO, todos os nomes-chave na seção especificada pelo argumento *lpszSection* serão copiados para o buffer especificado pelo argumento *RetBuffer.*  
  
 *lpszDefault*  
 [Entrada] Aponta para uma seqüência de terminadas nula que especifica o valor padrão para a chave dada se a chave não puder ser encontrada no arquivo de inicialização. Este argumento não pode ser NULO.  
  
 *RetBuffer*  
 [Saída] Aponta para o buffer que recebe a seqüência recuperada.  
  
 *cbRetBuffer*  
 [Entrada] Especifica o tamanho, em caracteres, do buffer apontado pelo argumento *RetBuffer.*  
  
 *lpszNome de arquivo*  
 [Entrada] Aponta para uma seqüência de terminadas nula que nomeia o arquivo de inicialização. Se esse argumento não contiver um caminho completo para o arquivo, o diretório padrão será pesquisado.  
  
## <a name="returns"></a>Retornos  
 **SQLGetPrivateProfileString** retorna um valor inteiro que indica o número de caracteres lidos.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando uma chamada para **SQLGetPrivateProfileString** falha, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **O SQLGetPrivateProfileString** é fornecido como uma maneira simples de portar drivers e DLLs de configuração de drivers da Microsoft® Windows® para Microsoft Windows NT®/Windows 2000. Chamadas para **GetPrivateProfileString** que recuperam uma seqüência de perfil do arquivo Odbc.ini devem ser substituídas por chamadas para **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** chama funções na API Win32® para recuperar os nomes de valores ou dados solicitados correspondentes a um valor da subchave Odbc.ini das informações do sistema.  
  
 O modo de configuração (conforme definido por **SQLSetConfigMode**) indica onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema. Se o DSN for um DSN do usuário (o modo de configuração é USERDSN_ONLY), a função será lida da entrada Odbc.ini em HKEY_CURRENT_USER. Se o DSN for um Sistema DSN (SYSTEMDSN_ONLY), a função será lida da entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se o modo de configuração for BOTHDSN, HKEY_CURRENT_USER for tentado e se falhar, HKEY_LOCAL_MACHINE será usado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Escrevendo um valor para as informações do sistema|[SQLWritePrivateProfilestring](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
