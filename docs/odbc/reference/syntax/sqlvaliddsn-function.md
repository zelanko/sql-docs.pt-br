---
title: Função SQLvaliddSN | Microsoft Docs
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
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286966"
---
# <a name="sqlvaliddsn-function"></a>Função SQLValidDSN
**Conformidade**  
 Versão introduzida: ODBC 2.0  
  
 **Resumo**  
 **SQLValidDSN** verifica o comprimento e a validade do nome de origem dos dados antes que o nome seja adicionado às informações do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nome da fonte de dados a ser verificado.  
  
## <a name="returns"></a>Retornos  
 A função retorna TRUE se o nome da fonte de dados for válido. Ele retorna FALSO se o nome da fonte de dados for inválido ou a chamada de função falhar.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLValidDSN** retorna FALSE, um valor * \*pfErrorCode* associado pode ser obtido ligando para **SQLInstallerError**. Um * \*pfErrorCode* é retornado somente se a chamada de função falhar, não se FALSE foi devolvido porque o nome de origem dos dados é inválido. A tabela a * \** seguir lista os valores pfErrorCode que podem ser retornados pelo **SQLInstallerError** e explica cada um no contexto desta função.  
  
|*\*pfErrorCode*|Erro|Descrição|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro do instalador geral|Ocorreu um erro para o qual não houve erro específico do instalador.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não conseguiu executar a função por falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **O SQLValidDSN** é chamado pelo [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) de um driver para verificar o comprimento do nome de origem dos dados e a validade dos caracteres individuais no nome de origem dos dados. Ele verifica se o comprimento do nome é maior do que SQL_MAX_DSN_LENGTH, como definido em Sqlext.h. (O comprimento do nome de origem dos dados também é verificado por [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **O SQLValidDSN** verifica se algum dos seguintes caracteres inválidos está incluído no nome de origem dos dados:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Adicionando, modificando ou removendo uma fonte de dados|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (na DLL de configuração)|  
|Adicionando, modificando ou removendo uma fonte de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Escrevendo um nome de origem de dados para as informações do sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
