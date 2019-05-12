---
title: SQLWriteDSNToIni Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5a36be7a98a39cab8b9df428b8d4bd9a1d399a1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536786"
---
# <a name="sqlwritedsntoini-function"></a>Função SQLWriteDSNToIni
**Conformidade com**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLWriteDSNToIni** adiciona uma fonte de dados para as informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome da fonte de dados para adicionar.  
  
 *lpszDriver*  
 [Entrada] Descrição do driver (geralmente o nome do DBMS associado) apresentada aos usuários em vez do nome físico de driver.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLWriteDSNToIni** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O *lpszDSN* argumento continha uma cadeia de caracteres que era inválida para um DSN.|  
|ODBC_ERROR_INVALID_NAME|Nome inválido de driver ou conversor|O *lpszDriver* argumento era inválido.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O instalador não conseguiu criar um DSN no registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLWriteDSNToIni** adiciona a fonte de dados para a seção [fontes de dados ODBC] as informações do sistema. Em seguida, cria uma seção de especificação para a fonte de dados e adiciona uma única palavra-chave (**Driver**) com o nome do driver DLL como seu valor. Se a seção de especificação de fonte de dados já existir, **SQLWriteDSNToIni** remove a seção antiga antes de criar um novo.  
  
 O chamador dessa função deve adicionar os valores e palavras-chave específicas de driver para a seção de especificação de fonte de dados de informações do sistema.  
  
 Se o nome da fonte de dados é o padrão, **SQLWriteDSNToIni** também cria a seção de especificação de driver padrão nas informações do sistema.  
  
 Essa função deve ser chamada apenas de uma DLL de instalação.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(na configuração de DLL)|  
|Adicionar, modificar ou remover uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Removendo um nome de fonte de dados de informações do sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
