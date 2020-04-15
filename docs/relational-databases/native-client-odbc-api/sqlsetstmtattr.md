---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2fc3bf094504415cc2ec27c6c472cce747b53481
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301872"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não dá suporte ao modelo de cursor misto (conjunto de chaves/dinâmico). As tentativas de definir o tamanho do conjunto de chaves usando SQL_ATTR_KEYSET_SIZE falhará se o valor definido não for igual a 0.  
  
 O aplicativo define SQL_ATTR_ROW_ARRAY_SIZE em todas as instruções para declarar o número de linhas retornadas em uma chamada de função **SQLFetchOu** ou [SQLFetchScroll.](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) Em instruções que indicam um cursor de servidor, o driver usa SQL_ATTR_ROW_ARRAY_SIZE para determinar o tamanho do bloco de linhas que o servidor gera para satisfazer uma solicitação de busca do cursor. No tamanho do bloco de um cursor dinâmico, a ordenação e a associação de linhas serão fixas se o nível de isolamento da transação for suficiente para assegurar leituras repetidas de transações confirmadas. O cursor é completamente dinâmico fora do bloco indicado por esse valor. O tamanho do bloco de cursor de servidor é completamente dinâmico e pode ser alterado a qualquer momento do processamento de busca.  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr e parâmetros com valor de tabela  
 SQLSetStmtAttr pode ser usado para definir SQL_SOPT_SS_PARAM_FOCUS no descritor de parâmetros de aplicativo (APD) antes de acessar campos descritores para colunas de parâmetros de valor de tabela.  
  
 Se for feita uma tentativa de definir SQL_SOPT_SS_PARAM_FOCUS à ordinal de um parâmetro que não seja um parâmetro de valor de tabela, o SQLSetStmtAttr retorna SQL_ERROR e um registro de diagnóstico é criado com SQLSTATE = HY024 e a mensagem "Valor de atributo inválido". SQL_SOPT_SS_PARAM_FOCUS não é alterado quando SQL_ERROR é retornado.  
  
 A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o acesso a registros de descritor para parâmetros.  
  
 SQLSetStmtAttr também pode ser usado para definir SQL_SOPT_SS_NAME_SCOPE. Para obter mais informações, consulte a seção SQL_SOPT_SS_NAME_SCOPE posteriormente neste tópico.  
  
 Para obter mais informações, consulte [Metadados de parâmetros avaliados em tabela para declarações preparadas](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Para obter mais informações sobre parâmetros avaliados em tabela, consulte [Parâmetros valorizados em tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>SQLSetStmtAttr Suporte para colunas esparsas  
 SQLSetStmtAttr pode ser usado para definir SQL_SOPT_SS_NAME_SCOPE. Para obter mais informações, consulte a seção SQL_SOPT_SS_NAME_SCOPE, mais tarde neste tópico. Para obter mais informações sobre colunas esparsas, consulte [Colunas esparsas suporte &#40;o ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="statement-attributes"></a>Atributos de instrução  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client também dá suporte aos seguintes atributos de instrução específicos do driver.  
  
### <a name="sql_sopt_ss_cursor_options"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 O atributo SQL_SOPT_SS_CURSOR especifica se o driver usará opções de desempenho específicas do driver em cursores. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) não é permitido quando essas opções são definidas. A configuração padrão é SQL_CO_OFF. O valor *ValuePtr* é do tipo SQLLEN.  
  
|*ValorDoValorPtr*|Descrição|  
|----------------------|-----------------|  
|SQL_CO_OFF|Padrão. Desabilita cursores rápidos somente para frente, somente leitura e autofetch, habilita **o SQLGetData** em cursores somente para uso avançado e somente leitura. Quando SQL_SOPT_SS_CURSOR_OPTIONS for definido como SQL_CO_OFF, o tipo de cursor não será alterado. Ou seja, o cursor somente de avanço rápido permanecerá um cursor somente de avanço rápido. Para alterar o tipo de cursor, o aplicativo deve agora definir um tipo de cursor diferente usando **SQLSetStmtAttr**/SQL_ATTR_CURSOR_TYPE.|  
|SQL_CO_FFO|Habilita cursores rápidos somente para frente e somente leitura, desativa **o SQLGetData** em cursores somente para uso e leitura.|  
|SQL_CO_AF|Habilita a opção autofetch em qualquer tipo de cursor. Quando esta opção estiver definida para uma alça de declaração, **o SQLExecute** ou **o SQLExecDirect** gerarão um **SQLFetchScroll** implícito (SQL_FIRST). O cursor é aberto e o primeiro lote de linhas é retornado em uma única viagem de ida e volta ao servidor.|  
|SQL_CO_FFO_AF|Habilita cursores somente de avanço rápido com a opção autofetch. É igual a se SQL_CO_AF e SQL_CO_FFO forem especificados.|  
  
 Quando essas opções são definidas, o servidor fecha o cursor automaticamente ao detectar que a última linha foi buscada. O aplicativo ainda deve ligar para [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) ou [SQLCloseCursor,](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)mas o driver não precisa enviar a notificação de proximidade ao servidor.  
  
 Se a lista selecionada contiver uma coluna **de texto,** **ntext**ou **imagem,** o cursor somente para encaminhamento rápido será convertido em um cursor dinâmico e **o SQLGetData** será permitido.  
  
### <a name="sql_sopt_ss_defer_prepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 O atributo SQL_SOPT_SS_DEFER_PREPARE determina se a declaração é preparada imediatamente ou diferida até que **SQLExecute,** [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) ou [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md) sejam executados. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 e anteriores, essa propriedade é ignorada (sem adiamento da preparação). O valor *ValuePtr* é do tipo SQLLEN.  
  
|*ValorDoValorPtr*|Descrição|  
|----------------------|-----------------|  
|SQL_DP_ON|Padrão. Depois de chamar [sqlPrepare function](https://go.microsoft.com/fwlink/?LinkId=59360), a preparação da declaração é adiada até **que o SQLExecute** seja chamado ou a operação de metapropriedade **(SQLDescribeCol** ou **SQLDescribeParam**) seja executada.|  
|SQL_DP_OFF|A declaração é preparada assim que **o SQLPrepare** for executado.|  
  
### <a name="sql_sopt_ss_regionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 O atributo SQL_SOPT_SS_REGIONALIZE é usado para determinar a conversão de dados no nível de instrução. O atributo faz o driver respeitar a configuração de localidade do cliente ao converter valores de data, hora, e moeda em cadeias de caracteres. A conversão ocorre somente de tipos de dados nativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cadeias de caracteres.  
  
 O valor *ValuePtr* é do tipo SQLLEN.  
  
|*ValorDoValorPtr*|Descrição|  
|----------------------|-----------------|  
|SQL_RE_OFF|Padrão. O driver não converte dados de data, hora e moeda em dados de cadeia de caracteres usando a configuração de localidade do cliente.|  
|SQL_RE_ON|O driver usa a configuração de localidade do cliente ao converter dados de data, hora e moeda em dados de cadeia de caracteres.|  
  
 As configurações regionais de conversão se aplicam a tipos de dados de moeda, numéricos e de data e hora. A configuração da conversão é aplicável somente a conversões de saída quando valores de moeda, numéricos, de data ou de hora são convertidos em cadeias de caracteres.  
  
> [!NOTE]  
>  Quando a opção de instrução SQL_SOPT_SS_REGIONALIZE está ativa, o driver usa as configurações do Registro de localidade do usuário atual. O driver não honra a localização do segmento atual se o aplicativo defini-lo por, por exemplo, chamando **SetThreadLocale**.  
  
 A alteração do comportamento regional de uma fonte de dados pode fazer o aplicativo falhar. Um aplicativo que analisa cadeias de caracteres de data e espera que cadeias de caracteres de data sejam exibidas conforme definido pelo ODBC poderia ser afetado adversamente pela alteração desse valor.  
  
### <a name="sql_sopt_ss_textptr_logging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 O SQL_SOPT_SS_TEXTPTR_LOGGING atribui o registro de operações em colunas que contenham dados de **texto** ou **imagem.** O valor *ValuePtr* é do tipo SQLLEN.  
  
|*ValorDoValorPtr*|Descrição|  
|----------------------|-----------------|  
|SQL_TL_OFF|Desativa o registro de operações realizadas em dados de **texto** e **imagem.**|  
|SQL_TL_ON|Padrão. Permite o registro de operações realizadas em dados de **texto** e **imagem.**|  
  
### <a name="sql_sopt_ss_hidden_columns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 O atributo SQL_SOPT_SS_HIDDEN_COLUMNS expõe, no conjunto de resultados, colunas ocultas em uma instrução [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE. Por padrão, o driver não expõe estas colunas. O valor *ValuePtr* é do tipo SQLLEN.  
  
|*ValorDoValorPtr*|Descrição|  
|----------------------|-----------------|  
|SQL_HC_OFF|Padrão. As colunas FOR BROWSE são ocultadas do conjunto de resultados.|  
|SQL_HC_ON|Expõe colunas FOR BROWSE.|  
  
### <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 O atributo SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT retorna o texto de mensagem para a solicitação de notificação de consulta.  
  
### <a name="sql_sopt_ss_querynotification_options"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 O atributo SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS especifica as opções usadas para a solicitação de notificação de consulta. Elas são especificadas em uma cadeia de caracteres com a sintaxe `name=value` conforme especificado a seguir. O aplicativo é responsável por criar o serviço e ler as notificações da fila.  
  
 A sintaxe da cadeia de caracteres das opções de notificação de consulta é:  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 Por exemplo:  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sql_sopt_ss_querynotification_timeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 O atributo SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT especifica o número de segundos que a notificação de consulta deve permanecer ativa. O valor padrão é 432.000 segundos (5 dias). O valor *ValuePtr* é do tipo SQLLEN.  
  
### <a name="sql_sopt_ss_param_focus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 O atributo SQL_SOPT_SS_PARAM_FOCUS especifica o foco para chamadas SQLBindParameter subseqüentes, SQLGetDescField, SQLSetDescField, SQLGetDescRec e SQLSetDescRec.  
  
 O tipo para SQL_SOPT_SS_PARAM_FOCUS é SQLULEN.  
  
 O padrão é 0, o que significa que estas chamadas são endereçadas a parâmetros que correspondem a marcadores de parâmetro na instrução SQL. Quando definido como o número de um parâmetro com valor de tabela, estas chamadas são endereçadas a colunas desse parâmetro com valor de tabela. Quando definido como um valor que não é o número de um parâmetro com valor de tabela, estas chamadas retornam o erro IM020: "O foco do parâmetro não se refere a um parâmetro com valor de tabela".  
  
### <a name="sql_sopt_ss_name_scope"></a>SQL_SOPT_SS_NAME_SCOPE  
 O atributo SQL_SOPT_SS_NAME_SCOPE especifica o escopo de nome para chamadas de função de catálogo subsequentes. O conjunto de resultados retornado por SQLColumns depende da configuração de SQL_SOPT_SS_NAME_SCOPE.  
  
 O tipo para SQL_SOPT_SS_NAME_SCOPE é SQLULEN.  
  
|*ValorDoValorPtr*|Descrição|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|Padrão.<br /><br /> Ao usar parâmetros com valor de tabela, indica que metadados de tabelas reais devem ser retornados.<br /><br /> Ao usar o recurso colunas esparsas, o SQLColumns retornará apenas colunas que não são membros do **column_set**esparso .|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|Indica que o aplicativo exige metadados para um tipo de tabela, em vez de uma tabela real (funções de catálogo devem retornar metadados para tipos de tabela). Em seguida, o aplicativo passa o TYPE_NAME do parâmetro avaliado em tabela como parâmetro *TableName.*|  
|SQL_SS_NAME_SCOPE_EXTENDED|Ao usar o recurso colunas esparsas, o SQLColumns retorna todas as colunas, independentemente de **column_set** a adesão.|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|Ao usar o recurso colunas esparsas, o SQLColumns retorna apenas colunas que são membros do **column_set**esparso .|  
|SQL_SS_NAME_SCOPE_DEFAULT|Igual a SQL_SS_NAME_SCOPE_TABLE.|  
  
 SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME são usados com os parâmetros *CatalogName* e *SchemaName,* respectivamente, para identificar o catálogo e o esquema para o parâmetro avaliado em tabela. Quando um aplicativo concluir a recuperação de metadados para parâmetros com valor de tabela, ele deve definir SQL_SOPT_SS_NAME_SCOPE novamente com seu valor padrão SQL_SS_NAME_SCOPE_TABLE.  
  
 Quando SQL_SOPT_SS_NAME_SCOPE for definido como SQL_SS_NAME_SCOPE_TABLE, as consultas a servidores vinculados irão falhar. Chamadas para SQLColumns ou SQLPrimaryKeys com um catálogo que contém um componente de servidor falharão.  
  
 Se você tentar definir SQL_SOPT_SS_NAME_SCOPE com um valor inválido, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE HY024 e a mensagem "Valor de atributo inválido".  
  
 Se uma função de catálogo, então SQLTables, SQLColumns ou SQLPrimaryKeys for chamada quando SQL_SOPT_SS_NAME_SCOPE tiver um valor diferente SQL_SS_NAME_SCOPE_TABLE, SQL_ERROR é retornada. Um registro de diagnóstico é gerado com SQLSTATE HY010 e a mensagem "Erro de sequência de função (SQL_SOPT_SS_NAME_SCOPE não está definido como SQL_SS_NAME_SCOPE_TABLE)".  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLGetStsttAttr](https://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
