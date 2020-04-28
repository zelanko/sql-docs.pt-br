---
title: Função SQLNativeSql | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9666bc767affb3b6bb624c416614079193d4b921
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304717"
---
# <a name="sqlnativesql-function"></a>Função SQLNativeSql
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLNativeSql** retorna a cadeia de caracteres SQL como modificada pelo driver. **SQLNativeSql** não executa a instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *InStatementText*  
 Entrada Cadeia de texto SQL a ser convertida.  
  
 *TextLength1*  
 Entrada Comprimento em caracteres de **InStatementText* cadeia de caracteres de texto.  
  
 *OutStatementText*  
 Der Ponteiro para um buffer no qual retornar a cadeia de caracteres SQL convertida.  
  
 Se *OutStatementText* for NULL, *TextLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *OutStatementText*.  
  
 *BufferLength*  
 Entrada Número de caracteres no \*buffer *OutStatementText* . Se o valor retornado em * \*InStatementText* for uma cadeia de caracteres Unicode (ao chamar **SQLNativeSqlW**), o argumento *BufferLength* deverá ser um número par.  
  
 *TextLength2Ptr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo a terminação nula) disponíveis para retornar \*em *OutStatementText*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength*, a cadeia de caracteres SQL traduzida em \* *OutStatementText* será truncada para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLNativeSql** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLNativeSql** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O buffer \* *OutStatementText* não era grande o suficiente para retornar a cadeia de caracteres SQL inteira, portanto, a cadeia de caracteres SQL foi truncada. O comprimento da cadeia de caracteres SQL não truncada é retornado em **TextLength2Ptr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|O *ConnectionHandle* não estava em um estado conectado.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22007|Formato de data e hora inválido|**InStatementText* continha uma cláusula escape com um valor de data, hora ou timestamp inválido.|  
|24.000|Estado de cursor inválido|O cursor referido na instrução foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados. Esse erro não pode ser retornado por um driver que tem uma implementação de cursor do DBMS nativo.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|(DM) **InStatementText* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o argumento *TextLength1* era menor que 0, mas não é igual a SQL_NTS.|  
|||(DM) o argumento *BufferLength* era menor que 0 e o argumento *OutStatementText* não era um ponteiro nulo.|  
|HY109|Posição do cursor inválida|A linha atual do cursor foi excluída ou não foi buscada. Esse erro não pode ser retornado por um driver que tem uma implementação de cursor do DBMS nativo.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *ConnectionHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Veja a seguir exemplos de o que **SQLNativeSql** pode retornar para a seguinte cadeia de caracteres SQL de entrada que contém a função escalar Convert. Suponha que a coluna empid seja do tipo inteiro na fonte de dados:  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Um driver para Microsoft SQL Server pode retornar a seguinte cadeia de caracteres SQL traduzida:  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Um driver para o servidor ORACLE pode retornar a seguinte cadeia de caracteres SQL convertida:  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Um driver para entrada pode retornar a seguinte cadeia de caracteres SQL traduzida:  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 Para obter mais informações, consulte [execução direta](../../../odbc/reference/develop-app/direct-execution-odbc.md) e [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
 Nenhum.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
