---
title: Função SQLValidDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb490b475c5795125d11915729693eb630934eb8
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201455"
---
# <a name="sqlvaliddsn-function"></a>Função SQLValidDSN
**Conformidade com**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLValidDSN** verifica o comprimento e a validade do nome de fonte de dados antes do nome é adicionado às informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome a ser verificado da fonte de dados.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se o nome da fonte de dados é válido. Retornará FALSE se o nome da fonte de dados é inválido ou a falha da chamada de função.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLValidDSN** retornar FALSE, um associado  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. Um  *\*pfErrorCode* é retornado somente se a chamada de função falha, não se falso foi retornado porque o nome da fonte de dados é inválido. A seguinte tabela lista os  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não foi possível executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLValidDSN** é chamado por um driver [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) para verificar o comprimento do nome de fonte de dados e a validade dos caracteres individuais no nome da fonte de dados. Ele verifica se o comprimento do nome é maior que SQL_MAX_DSN_LENGTH, conforme definido em sqlext. h. (O tamanho da fonte de dados também é verificado pela [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** verifica se qualquer um dos seguintes caracteres inválidos são incluídos no nome da fonte de dados:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionar, modificar ou remover uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na configuração de DLL)|  
|Adicionar, modificar ou remover uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Escrever um nome de fonte de dados para as informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
