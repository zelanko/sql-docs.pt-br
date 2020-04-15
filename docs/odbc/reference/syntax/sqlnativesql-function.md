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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304717"
---
# <a name="sqlnativesql-function"></a>Função SQLNativeSql
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLNativeSql** retorna a seqüência SQL como modificada pelo driver. **SQLNativeSql** não executa a declaração SQL.  
  
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
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *InstatementText*  
 [Entrada] Seqüência de texto SQL a ser traduzida.  
  
 *Comprimento de texto1*  
 [Entrada] Comprimento em caracteres da seqüência de texto ** InStatementText.*  
  
 *OutStatementText*  
 [Saída] Ponteiro para um buffer no qual retornar a seqüência SQL traduzida.  
  
 Se *OutStatementText* for NULL, *TextLength2Ptr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *OutStatementText*.  
  
 *BufferLength*  
 [Entrada] Número de caracteres no \*buffer *OutStatementText.* Se o valor retornado em * \*InStatementText* for uma seqüência Unicode (ao chamar **SQLNativeSqlW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 *TextLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres \*(excluindo a rescisão nula) disponível para retornar em *OutStatementText*. Se o número de caracteres disponíveis para retornar for maior ou igual \*a *BufferLength,* a seqüência sql traduzida em *OutStatementText* será truncada para *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLNativeSql** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE comumente devolvidos por **SQLNativeSql** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *OutStatementText* não era grande o suficiente para retornar toda a seqüência SQL, de modo que a seqüência SQL foi truncada. O comprimento da seqüência SQL não truncada é devolvido em **TextLength2Ptr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|O *ConnectionHandle* não estava em um estado conectado.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22007|Formato de data-hora inválido|**InStatementText* continha uma cláusula de escape com um valor de data, hora ou carimbo de data inválido.|  
|24.000|Estado de cursor inválido|O cursor referido na declaração foi posicionado antes do início do conjunto de resultados ou após o término do conjunto de resultados. Este erro não pode ser devolvido por um driver que tenha uma implementação nativa do cursor DBMS.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY009|Uso inválido do ponteiro nulo|(DM) **InStatementText* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o *ConnectionHandle* e ainda estava sendo executada quando esta função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O argumento *TextLength1* foi inferior a 0, mas não igual a SQL_NTS.|  
|||(DM) O argumento *BufferLength* era menor que 0 e o argumento *OutStatementText* não era um ponteiro nulo.|  
|HY109|Posição do cursor inválido|A linha atual do cursor tinha sido excluída ou não tinha sido buscada. Este erro não pode ser devolvido por um driver que tenha uma implementação nativa do cursor DBMS.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *ConnectionHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 A seguir, exemplos do que **sqlnativesql** pode retornar para a seqüência SQL de entrada a seguir contendo a função escalar CONVERT. Suponha que a coluna empid seja do tipo INTEGER na fonte de dados:  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Um driver para Microsoft SQL Server pode retornar a seguinte seqüência sql traduzida:  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Um driver para ORACLE Server pode retornar a seguinte seqüência sql traduzida:  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Um driver para Ingres pode retornar a seguinte seqüência sql traduzida:  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 Para obter mais informações, consulte [Execução Direta](../../../odbc/reference/develop-app/direct-execution-odbc.md) e [Execução Preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
 Nenhum.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
