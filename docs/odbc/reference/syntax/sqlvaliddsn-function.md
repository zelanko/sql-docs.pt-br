---
title: "Função SQLValidDSN | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 473670a87ede935267c91537f301589b94666acf
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlvaliddsn-function"></a>Função SQLValidDSN
**Conformidade**  
 Versão introduzidas: ODBC 2.0  
  
 **Resumo**  
 **SQLValidDSN** verifica o comprimento e a validade do nome de fonte de dados antes do nome é adicionado às informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome a ser verificada da fonte de dados.  
  
## <a name="returns"></a>Retorna  
 A função retornará TRUE se o nome da fonte de dados é válido. Retornará FALSE se o nome da fonte de dados é inválido ou a falha da chamada de função.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLValidDSN** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. Um  *\*pfErrorCode* é retornado somente se a chamada de função falhar, não se FALSE retornado porque o nome da fonte de dados é inválido. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLValidDSN** é chamado por um driver [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) para verificar se o comprimento do nome de fonte de dados e a validade dos caracteres no nome da fonte de dados individuais. Ele verifica se o comprimento do nome é maior que SQL_MAX_DSN_LENGTH, conforme definido em Sqlext.h. (O comprimento do nome de fonte de dados também é verificado por [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** verifica se qualquer um dos seguintes caracteres inválidos são incluídas no nome de fonte de dados:  
  
 [ ] { } ( ) , ; ? * = ! @ \  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na configuração de DLL)|  
|Adicionar, modificar ou remover uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Escrevendo um nome de fonte de dados para as informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|

