---
title: Função SQLNativeSql | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e233d9742ea7bd9aa5de56962e1d785be78b8066
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlnativesql-function"></a>Função SQLNativeSql
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLNativeSql** retorna a cadeia de caracteres SQL conforme modificado pelo driver. **SQLNativeSql** não executa a instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador da conexão*  
 [Entrada] Identificador de Conexão.  
  
 *InStatementText*  
 [Entrada] Cadeia de texto SQL a ser convertido.  
  
 *TextLength1*  
 [Entrada] Comprimento em caracteres de **InStatementText* cadeia de caracteres de texto.  
  
 *OutStatementText*  
 [Saída] Ponteiro para um buffer no qual retornar a cadeia de caracteres traduzida do SQL.  
  
 Se *OutStatementText* for NULL, *TextLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere null de terminação para dados de caractere) disponível no buffer de retorno apontada pelo *OutStatementText*.  
  
 *BufferLength*  
 [Entrada] Número de caracteres a \* *OutStatementText* buffer. Se o valor retornado em  *\*InStatementText* é uma cadeia de caracteres Unicode (ao chamar **SQLNativeSqlW**), o *BufferLength* argumento deve ser um número par.  
  
 *TextLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto null de terminação) disponíveis para retornar em \* *OutStatementText*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, o convertido a cadeia de caracteres SQL em \* *OutStatementText* será truncado para  *BufferLength* menos o comprimento de um caractere null de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLNativeSql** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* SQL_HANDLE_DBC e um *tratar* de *identificador da conexão*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLNativeSql** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *OutStatementText* não era grande o suficiente para retornar a cadeia de caracteres inteira do SQL, para que a cadeia de caracteres SQL foi truncada. O comprimento da cadeia de caracteres SQL completo é retornado em **TextLength2Ptr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|O *identificador da conexão* não estava em um estado conectado.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22007|Formato de datetime inválido|**InStatementText* continha uma cláusula de escape com um valor de data, hora ou carimbo de hora inválido.|  
|24000|Estado de cursor inválido|O cursor referenciado na instrução foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados. Esse erro não pode ser retornado por um driver com uma implementação de cursor nativa do DBMS.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|(DM) **InStatementText* foi um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o *identificador da conexão* e ainda estava em execução quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o argumento *TextLength1* era menor que 0, mas não igual a SQL_NTS.|  
|||(DM) o argumento *BufferLength* foi menor que 0 e o argumento *OutStatementText* não era um ponteiro nulo.|  
|HY109|Posição de cursor inválido|A linha atual do cursor foi excluída ou não tinha sido buscada. Esse erro não pode ser retornado por um driver com uma implementação de cursor nativa do DBMS.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *identificador da conexão* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 Os seguintes são exemplos do que **SQLNativeSql** pode retornar para a seguinte entrada SQL cadeia de caracteres que contém a função escalar CONVERT. Suponha que a coluna empid é do tipo inteiro na fonte de dados:  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Um driver do Microsoft SQL Server pode retornar a cadeia de caracteres traduzida por SQL seguinte:  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Um driver para o servidor ORACLE pode retornar a cadeia de caracteres traduzida por SQL seguinte:  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 Um driver para Ingres pode retornar a cadeia de caracteres traduzida por SQL seguinte:  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 Para obter mais informações, consulte [execução direta](../../../odbc/reference/develop-app/direct-execution-odbc.md) e [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
 Nenhum.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
