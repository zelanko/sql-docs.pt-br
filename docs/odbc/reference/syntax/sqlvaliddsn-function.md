---
description: Função SQLValidDSN
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4919887a6e0bad4526959d0cd31205019a597a0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421020"
---
# <a name="sqlvaliddsn-function"></a>Função SQLValidDSN
**Conformidade**  
 Versão introduzida: ODBC 2,0  
  
 **Resumo**  
 **SQLValidDSN** verifica o comprimento e a validade do nome da fonte de dados antes que o nome seja adicionado às informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 Entrada Nome da fonte de dados a ser verificado.  
  
## <a name="returns"></a>Retornos  
 A função retornará TRUE se o nome da fonte de dados for válido. Ele retornará FALSE se o nome da fonte de dados for inválido ou a chamada de função falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLValidDSN** retorna false, um valor * \* pfErrorCode* associado pode ser obtido chamando **SQLInstallerError**. Um * \* pfErrorCode* será retornado somente se a chamada de função falhar, e não se false for retornado porque o nome da fonte de dados é inválido. A tabela a seguir lista os valores de * \* pfErrorCode* que podem ser retornados por **SQLInstallerError** e explica cada um no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral do instalador|Ocorreu um erro para o qual não havia nenhum erro do instalador específico.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido à falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **SQLValidDSN** é chamado pelo [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) de um driver para verificar o comprimento do nome da fonte de dados e a validade dos caracteres individuais no nome da fonte de dados. Ele verifica se o comprimento do nome é maior que SQL_MAX_DSN_LENGTH, conforme definido em sqlext. h. (O comprimento do nome da fonte de dados também é verificado por [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** verifica se algum dos seguintes caracteres inválidos está incluído no nome da fonte de dados:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na DLL de instalação)|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Gravando um nome de fonte de dados para as informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
