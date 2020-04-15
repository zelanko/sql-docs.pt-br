---
title: Função SQLRemoveDSNFromIni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301795"
---
# <a name="sqlremovedsnfromini-function"></a>Função SQLRemoveDSNFromIni
**Conformidade**  
 Versão introduzida: ODBC 1.0  
  
 **Resumo**  
 **SQLRemoveDSNFromIni** remove uma fonte de dados das informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome da fonte de dados para remover.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se remover a fonte de dados ou a fonte de dados não estiver no arquivo Odbc.ini. Ele retorna FALSO se não remover a fonte de dados.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **sQLRemoveDSNFromIni** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN inválido|O argumento *lpszDSN* era inválido.|  
|ODBC_ERROR_REQUEST_FAILED|Falha na solicitação|O instalador não pôde remover as informações do DSN do registro.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLRemoveDSNFromIni** remove o nome de origem dos dados da seção [Fontes de dados oDBC] das informações do sistema. Também remove a seção de especificação da fonte de dados das informações do sistema.  
  
 Esta função deve ser chamada apenas a partir de uma biblioteca de configuração de driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[Configdsn](../../../odbc/reference/syntax/configdsn-function.md)|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Removendo a fonte de dados padrão|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Adicionando um nome de origem de dados às informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
