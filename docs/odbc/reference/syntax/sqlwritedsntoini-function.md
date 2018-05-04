---
title: Função SQLWriteDSNToIni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1fd8998194331719535b16b6d9ae9a0aada8d36
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlwritedsntoini-function"></a>Função SQLWriteDSNToIni
**Conformidade**  
 Versão introduzidas: ODBC 1.0  
  
 **Resumo**  
 **SQLWriteDSNToIni** adiciona uma fonte de dados para as informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome da fonte de dados para adicionar.  
  
 *lpszDriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico do driver.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLWriteDSNToIni** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O *lpszDSN* argumento continha uma cadeia de caracteres que era inválida para um DSN.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszDriver* argumento era inválido.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O instalador não conseguiu criar um DSN no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLWriteDSNToIni** adiciona a fonte de dados à seção [fontes de dados ODBC] as informações do sistema. Em seguida, cria uma seção de especificação para a fonte de dados e adiciona uma única palavra-chave (**Driver**) com o nome do driver DLL como seu valor. Se a seção de especificação de fonte de dados já existir, **SQLWriteDSNToIni** remove a seção antiga antes de criar um novo.  
  
 O chamador dessa função deve adicionar quaisquer palavras-chave específicas de driver e os valores para a seção de especificação de fonte de dados as informações do sistema.  
  
 Se o nome da fonte de dados é o padrão, **SQLWriteDSNToIni** também cria a seção de especificação de driver padrão nas informações do sistema.  
  
 Essa função deve ser chamada apenas de uma DLL de instalação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(na configuração de DLL)|  
|Adicionar, modificar ou remover uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Remover um nome de fonte de dados das informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
