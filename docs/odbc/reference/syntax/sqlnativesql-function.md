---
title: SQLNativeSql Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab39d1fca288196dcf42da70083dad323c406ba0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465952"
---
# <a name="sqlnativesql-function"></a>Função SQLNativeSql
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
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
 *ConnectionHandle*  
 [Entrada] Identificador de Conexão.  
  
 *InStatementText*  
 [Entrada] Cadeia de texto SQL a ser traduzido.  
  
 *TextLength1*  
 [Entrada] Comprimento em caracteres de **InStatementText* cadeia de caracteres de texto.  
  
 *OutStatementText*  
 [Saída] Ponteiro para um buffer no qual retornar a cadeia de caracteres traduzida do SQL.  
  
 Se *OutStatementText* for NULL, *TextLength2Ptr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontada por *OutStatementText*.  
  
 *BufferLength*  
 [Entrada] Número de caracteres a \* *OutStatementText* buffer. Se o valor retornado em  *\*InStatementText* é uma cadeia de caracteres Unicode (ao chamar **SQLNativeSqlW**), o *BufferLength* argumento deve ser um número par.  
  
 *TextLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto a finalização null) disponíveis para retornar na \* *OutStatementText*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, o convertidos de cadeia de caracteres SQL na \* *OutStatementText* será truncado para  *BufferLength* menos o comprimento de um caractere nulo de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLNativeSql** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* SQL_HANDLE_DBC e uma *manipular* dos *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLNativeSql** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *OutStatementText* não era grande o suficiente para retornar a cadeia de caracteres inteira do SQL, portanto, a cadeia de caracteres SQL foi truncada. O comprimento da cadeia de caracteres SQL completo é retornado no **TextLength2Ptr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexão não aberta|O *ConnectionHandle* não estava em um estado conectado.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22007|Formato de data/hora inválido|**InStatementText* continha uma cláusula de escape com um valor de data, hora ou carimbo de hora inválido.|  
|24000|Estado de cursor inválido|O conhecido na instrução de cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados. Esse erro não pode ser retornado por um driver de ter uma implementação nativa de cursor do DBMS.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|(DM) **InStatementText* é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o *ConnectionHandle* e ainda estava em execução quando essa função foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o argumento *TextLength1* era menor que 0, mas não é igual a SQL_NTS.|  
|||(DM) o argumento *BufferLength* era menor que 0 e o argumento *OutStatementText* não era um ponteiro nulo.|  
|HY109|Posição do cursor inválida|A linha atual do cursor tivesse sido excluída ou não tinha sido buscada. Esse erro não pode ser retornado por um driver de ter uma implementação nativa de cursor do DBMS.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *ConnectionHandle* não suporta a função.|  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
