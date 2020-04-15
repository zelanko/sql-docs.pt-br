---
title: Função SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d8260dd285fb3f5bbb9fcdaeaaebf1586090179
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282916"
---
# <a name="sqltableprivileges-function"></a>Função SQLTablePrivileges
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLTablePrivileges** retorna uma lista de tabelas e os privilégios associados a cada tabela. O motorista retorna as informações como resultado definido na declaração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *Catalogname*  
 [Entrada] Catálogo de mesas. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Padrão de busca de cordas para nomes de esquemas. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem esquemas.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Tablename*  
 [Entrada] Padrão de pesquisa de cordas para nomes de tabela.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *O Nome da Tabela* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLTablePrivileges** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLTablePrivileges** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função **SQLTablePrivileges** foi chamada e antes de concluir a execução, **sqlCancelou** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função **SQLTablePrivileges** foi chamada novamente no *StatementHandle*.<br /><br /> A função **SQLTablePrivileges** foi chamada e, antes de concluir a execução, **o SQLCancel** ou **o SQLCancelHandle** foram chamados para o *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* ou *TableName* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLTablePrivileges** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento do nome foi inferior a 0, mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o qualificador ou nome correspondente.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [A função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um esquema foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> Um padrão de pesquisa de seqüência foi especificado para o esquema da tabela, nome da tabela ou nome da coluna, e a fonte de dados não suporta padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Os argumentos *SchemaName* e *TableName* aceitam padrões de pesquisa. Para obter mais informações sobre padrões de pesquisa [válidos,](../../../odbc/reference/develop-app/pattern-value-arguments.md)consulte Argumentos de valor de padrão .  
  
 **O SQLTablePrivileges** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_CAT, TABLE_SCHEM, TABLE_NAME, PRIVILEGE e GRANTEE.  
  
 Para determinar os comprimentos reais das colunas de TABLE_CAT, TABLE_SCHEM e TABLE_NAME, um aplicativo pode chamar **sqlGetInfo** com as opções de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_TABLE_NAME_LEN.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As seguintes colunas foram renomeadas para ODBC *3.x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|Coluna ODBC *3.x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 7 (IS_GRANTABLE) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo; NULL se não aplicável à fonte de dados. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema; NULL se não aplicável à fonte de dados. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não É NULO|Nome da tabela.|  
|GRANTOR (ODBC 1.0)|4|Varchar|Nome do usuário que concedeu o privilégio; NULL se não aplicável à fonte de dados.<br /><br /> Para todas as linhas em que o valor na coluna GRANTEE é o proprietário do objeto, a coluna GRANTOR será "_SYSTEM".|  
|BENEFICIÁRIO (ODBC 1.0)|5|Varchar não É NULO|Nome do usuário a quem o privilégio foi concedido.|  
|PRIVILÉGIO (ODBC 1.0)|6|Varchar não É NULO|O privilégio da mesa. Pode ser um dos seguintes ou um privilégio específico da fonte de dados.<br /><br /> SELECT: O beneficiário pode recuperar dados de uma ou mais colunas da tabela.<br /><br /> INSIRA: O beneficiário pode inserir novas linhas contendo dados para uma ou mais colunas na tabela.<br /><br /> ATUALIZAÇÃO: O beneficiário pode atualizar os dados em uma ou mais colunas da tabela.<br /><br /> EXCLUSão: O beneficiário pode excluir linhas de dados da tabela.<br /><br /> REFERÊNCIAS: O beneficiário pode consultar uma ou mais colunas da tabela dentro de uma restrição (por exemplo, uma restrição única, referencial ou de verificação de tabela).<br /><br /> O escopo de ação permitido ao beneficiário por um determinado privilégio de tabela é dependente da fonte de dados. Por exemplo, o privilégio UPDATE pode permitir que o beneficiário atualize todas as colunas em uma tabela em uma fonte de dados e apenas as colunas para as quais o concededor tem o privilégio UPDATE em outra fonte de dados.|  
|IS_GRANTABLE (ODBC 1.0)|7|Varchar|Indica se o beneficiário pode conceder o privilégio a outros usuários; "SIM", "NÃO" ou NULO se desconhecido ou não aplicável à fonte de dados.<br /><br /> Um privilégio é concedido ou não pode ser concedido, mas não ambos. O conjunto de resultados retornado pelo **SQLColumnPrivileges** nunca conterá duas linhas para as quais todas as colunas, exceto a coluna IS_GRANTABLE contêm o mesmo valor.|  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolvendo privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Retornando as colunas em uma tabela ou tabela|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Estatísticas e índices da tabela de retorno|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Retornando uma lista de tabelas em uma fonte de dados|[Função SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
