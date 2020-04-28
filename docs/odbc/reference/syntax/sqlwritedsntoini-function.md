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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286956"
---
# <a name="sqlwritedsntoini-function"></a>Função SQLWriteDSNToIni
**Conformidade**  
 Versão introduzida: ODBC 1,0  
  
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
 Entrada Nome da fonte de dados a ser adicionada.  
  
 *lpszDriver*  
 Entrada Descrição do driver (geralmente o nome do DBMS associado) apresentado aos usuários em vez do nome do driver físico.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se for bem-sucedida, FALSE se falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLWriteDSNToIni** retorna false, um valor * \*pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. A tabela a seguir lista os valores de * \*pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O argumento *lpszDSN* continha uma cadeia de caracteres que era inválida para um DSN.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou tradutor inválido|O argumento *lpszDriver* era inválido.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O instalador não pôde criar um DSN no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLWriteDSNToIni** adiciona a fonte de dados à seção [fontes de dados ODBC] das informações do sistema. Em seguida, ele cria uma seção de especificação para a fonte de dados e adiciona uma única palavra-chave (**Driver**) com o nome da dll do driver como seu valor. Se a seção especificação da fonte de dados já existir, o **SQLWriteDSNToIni** removerá a seção antiga antes de criar a nova.  
  
 O chamador dessa função deve adicionar quaisquer palavras-chave e valores específicos do driver à seção especificação da fonte de dados das informações do sistema.  
  
 Se o nome da fonte de dados for padrão, **SQLWriteDSNToIni** também criará a seção de especificação de driver padrão nas informações do sistema.  
  
 Essa função deve ser chamada somente de uma DLL de instalação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(na DLL de instalação)|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Removendo um nome de fonte de dados das informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
