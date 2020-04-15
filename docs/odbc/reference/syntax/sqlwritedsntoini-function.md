---
title: Função SQLWriteDSNToIni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bb141c8f54c49ca3a5c6fc4bc15d434f91795c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286956"
---
# <a name="sqlwritedsntoini-function"></a>Função SQLWriteDSNToIni
**Conformidade**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLWriteDSNToIni** adiciona uma fonte de dados às informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome da fonte de dados para adicionar.  
  
 *Lpszdriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do motorista físico.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se for bem sucedida, FALSA se falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sQLWriteDSNToIni** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O argumento *lpszDSN* continha uma string que era inválida para um DSN.|  
|ODBC_ERROR_INVALID_NAME|Nome de motorista ou tradutor inválido|O argumento *lpszDriver* era inválido.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O instalador não conseguiu criar um DSN no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLWriteDSNToIni** adiciona a fonte de dados à seção [Fontes de dados ODBC] das informações do sistema. Em seguida, cria uma seção de especificação para a fonte de dados e adiciona uma única palavra-chave **(Driver**) com o nome do driver DLL como seu valor. Se a seção de especificação de origem de dados já existir, **o SQLWriteDSNToIni** removerá a seção antiga antes de criar a nova.  
  
 O chamador desta função deve adicionar quaisquer palavras-chave e valores específicos do driver à seção de especificação de origem de dados das informações do sistema.  
  
 Se o nome da fonte de dados for Padrão, **SQLWriteDSNToIni** também criará a seção de especificação de driver padrão nas informações do sistema.  
  
 Esta função deve ser chamada apenas a partir de uma configuração DLL.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(na DLL de configuração)|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Removendo um nome de origem de dados das informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
