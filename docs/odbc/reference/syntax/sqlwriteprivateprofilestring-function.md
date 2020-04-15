---
title: SQLWritePrivateProfileString function | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286879"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Função SQLWritePrivateProfileString
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLWritePrivateProfileString** grava um nome de valor e dados para o subchave Odbc.ini das informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Lpszsection*  
 [Entrada] Aponta para uma seqüência de terminação nula contendo o nome da seção para a qual a seqüência será copiada. Se a seção não existe, ela é criada. O nome da seção é independente de caso; a seqüência pode ser qualquer combinação de letras maiúsculas e minúsculas.  
  
 *Lpszentry*  
 [Entrada] Aponta para uma seqüência de terminadas nula contendo o nome da chave a ser associada a uma string. Se a chave não existir na seção especificada, ela será criada. Se esse argumento for NULO, toda a seção, incluindo todas as entradas dentro da seção, será excluída.  
  
 *lpszString*  
 [Entrada] Aponta para uma seqüência de terminadas nula a ser escrita no arquivo. Se esse argumento for NULO, a chave apontada pelo argumento *lpszEntry* será excluída.  
  
 *lpszNome de arquivo*  
 [Saída] Aponta para uma seqüência de terminadas nula que nomeia o arquivo de inicialização.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLWritePrivateProfileString** retorna FALSO, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|As informações solicitadas do sistema não puderam ser escritas.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **O SQLWritePrivateProfileString** é fornecido como uma maneira simples de portar drivers e DLLs de configuração de drivers da Microsoft® Windows® para Microsoft Windows NT®/Windows 2000. Chamadas para **WritePrivateProfileString** que gravar uma seqüência de perfil no arquivo Odbc.ini deve ser substituída por chamadas para **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chama funções na API Win32® para adicionar o nome de valor e os dados especificados à subchave Odbc.ini das informações do sistema.  
  
 Um modo de configuração indica onde os valores de DSN de listagem de entrada Odbc.ini estão nas informações do sistema. Se o DSN for um DSN do usuário (a variável estado é USERDSN_ONLY), a função será escrita para a entrada Odbc.ini em HKEY_CURRENT_USER. Se o DSN for um Sistema DSN (SYSTEMDSN_ONLY), a função será escrita para a entrada Odbc.ini em HKEY_LOCAL_MACHINE. Se a variável de estado for BOTHDSN, HKEY_CURRENT_USER é tentado e, se falhar, HKEY_LOCAL_MACHINE é usado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo um valor a partir das informações do sistema|[SqlGetPrivateProfilestring](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
