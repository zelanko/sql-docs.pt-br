---
title: "Função SQLGetDiagField | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetDiagField
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetDiagField
helpviewer_keywords: SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3dbc86d0dd1be8ef4e8ca19f8a7f25147a35fcc6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetdiagfield-function"></a>Função SQLGetDiagField
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetDiagField** retorna o valor atual de um campo de um registro da estrutura de dados de diagnóstico (associada a um identificador especificado) que contém informações de erro, aviso e status.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Um identificador de tipo de identificador que descreve o tipo de identificador para o qual diagnósticos são necessários. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo Gerenciador de Driver e do driver. Aplicativos não devem usar este tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Um identificador para a estrutura de dados de diagnóstico, do tipo indicado pelo *HandleType*. Se *HandleType* é SQL_HANDLE_ENV, *tratar* pode ser um identificador de ambiente não compartilhado ou compartilhado.  
  
 *RecNumber*  
 [Entrada] Indica que o registro de status do qual o aplicativo busca de informações. Registros de status são numerados de 1. Se o *DiagIdentifier* argumento indica qualquer campo do cabeçalho do diagnóstico, *RecNumber* será ignorado. Caso contrário, ele deve ser maior que 0.  
  
 *DiagIdentifier*  
 [Entrada] Indica o campo do diagnóstico cujo valor será retornado. Para obter mais informações, consulte o "*DiagIdentifier* argumento" seção "Comentários".  
  
 *DiagInfoPtr*  
 [Saída] Ponteiro para um buffer no qual retornar as informações de diagnóstico. O tipo de dados depende do valor de *DiagIdentifier*. Se *DiagInfoPtr* é do tipo integer, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função, como alguns drivers só pode gravar o inferior 32 bits ou 16 bits de um buffer e deixe de ordem superior bits inalterados.  
  
 Se *DiagInfoPtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo  *DiagInfoPtr*.  
  
 *BufferLength*  
 [Entrada] Se *DiagIdentifier* é um diagnóstico definidas pelo ODBC e *DiagInfoPtr* aponta para uma cadeia de caracteres ou um buffer binário, este argumento deve ser o comprimento de \* *DiagInfoPtr* . Se *DiagIdentifier* é um campo definido pelo ODBC e \* *DiagInfoPtr* é um inteiro, *BufferLength* será ignorado. Se o valor em  *\*DiagInfoPtr* é uma cadeia de caracteres Unicode (ao chamar **SQLGetDiagFieldW**), o *BufferLength* argumento deve ser um número par.  
  
 Se *DiagIdentifier* é um campo definido pelo driver, o aplicativo indica a natureza do campo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se *DiagInfoPtr* é um ponteiro para uma cadeia de caracteres, *BufferLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *DiagInfoPtr* é um ponteiro para um buffer de binário, os locais de aplicativo o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *DiagInfoPtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou cadeia de caracteres binária, *BufferLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se  *\*DiagInfoPtr* contém um tipo de dados de comprimento fixo, *BufferLength* é SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o número de bytes necessários para o caractere null de terminação) disponíveis para retornar em \* *DiagInfoPtr*, para dados de caracteres. Se o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, o texto em \* *DiagInfoPtr* será truncado para *BufferLength* menos o comprimento de um caractere null de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_NO_DATA.  
  
## <a name="diagnostics"></a>diagnóstico  
 **SQLGetDiagField** não envia registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retorno para relatar o resultado da execução do seu próprio:  
  
-   SQL_SUCCESS: A função retornou com êxito as informações de diagnósticas.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* era muito pequeno para conter o campo de diagnóstico solicitado. Portanto, os dados no campo de diagnóstico foi truncados. Para determinar se ocorreu um truncamento, o aplicativo deve comparar *BufferLength* para o número real de bytes disponíveis, que está escrito em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: O identificador indicado por *HandleType* e *tratar* não era um identificador válido.  
  
-   SQL_ERROR: Uma das opções a seguir ocorreu:  
  
    -   *O DiagIdentifier* argumento não era um dos valores válidos.  
  
    -   *O DiagIdentifier* argumento era SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE ou SQL_DIAG_ROW_COUNT, mas *tratar* não era um identificador de instrução. (O Gerenciador de Driver retorna este diagnóstico.)  
  
    -   *O RecNumber* argumento era negativo ou 0 quando *DiagIdentifier* indicado um campo de um registro de diagnóstico. *RecNumber* é ignorado para campos de cabeçalho.  
  
    -   O valor solicitado era uma cadeia de caracteres e *BufferLength* foi menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona no identificador não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* era maior que o número de registros de diagnóstico que existiam para o identificador especificado no *tratar.* A função também retorna SQL_NO_DATA para qualquer positivo *RecNumber* se não houver nenhum registro de diagnóstico para *tratar*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLGetDiagField** para realizar um dos três objetivos:  
  
1.  Para obter informações de aviso ou erro específico quando uma chamada de função retornou SQL_ERROR ou SQL_SUCCESS_WITH_INFO (ou SQL_NEED_DATA para o **SQLBrowseConnect** função).  
  
2.  Para determinar o número de linhas na fonte de dados que foram afetadas quando executadas operações update, delete ou insert com uma chamada para **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, ou **SQLSetPos** (no campo de cabeçalho SQL_DIAG_ROW_COUNT), ou para determinar o número de linhas que existem no cursor aberto atual, se o driver pode fornecer essas informações (da Campo de cabeçalho SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Para determinar qual função foi executada por uma chamada para **SQLExecDirect** ou **SQLExecute** (dos campos de cabeçalho SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Qualquer função ODBC pode postar zero ou mais registros de diagnóstico toda vez que ele é chamado, para que um aplicativo pode chamar **SQLGetDiagField** após qualquer chamada de função ODBC. Não há nenhum limite para o número de registros de diagnóstico que podem ser armazenados em qualquer momento. **SQLGetDiagField** recupera apenas as informações de diagnósticas mais recentemente associadas com a estrutura de dados de diagnóstico especificada no *tratar* argumento. Se o aplicativo chama uma função ODBC que **SQLGetDiagField** ou **SQLGetDiagRec**, qualquer informação de diagnóstica de uma chamada anterior com o mesmo identificador é perdida.  
  
 Um aplicativo pode verificar todos os registros de diagnósticos, incrementando *RecNumber*, contanto que **SQLGetDiagField** retorna SQL_SUCCESS. O número de registros de status é indicado no campo de cabeçalho SQL_DIAG_NUMBER. Chamadas para **SQLGetDiagField** são destrutivos nos campos de cabeçalho e o registro. O aplicativo pode chamar **SQLGetDiagField** novamente mais tarde para recuperar um campo de um registro, como uma função diferente de funções de diagnóstico não foi chamada nesse ínterim, que seria lançar registros no identificador do mesmo.  
  
 Um aplicativo pode chamar **SQLGetDiagField** para retornar qualquer campo diagnóstico a qualquer momento, exceto para SQL_DIAG_CURSOR_ROW_COUNT ou SQL_DIAG_ROW_COUNT, que retornará SQL_ERROR se *tratar* não é um Identificador de instrução. Se qualquer outro campo de diagnóstico será indefinido, a chamada para **SQLGetDiagField** retornará SQL_SUCCESS (desde que nenhum outro diagnóstico for encontrado) e um valor indefinido será retornado para o campo.  
  
 Para obter mais informações, consulte [usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [SQLGetDiagRec implementando e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente daquele que está sendo executada de forma assíncrona gerará HY010 "Erro de sequência de função". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona é concluída.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador pode ter informações de diagnóstico associadas a ele. O *HandleType* argumento indica o tipo de identificador de *tratar*.  
  
 Alguns campos de cabeçalho e o registro não podem ser retornados para o ambiente, a conexão, a instrução e descritor de identificadores. Os identificadores de um campo não é aplicável para o qual são indicadas nas seções "Campos de cabeçalho" e "Campos do Registro" a seguir.  
  
 Se *HandleType* é SQL_HANDLE_ENV, *tratar* pode ser um identificador de ambiente não compartilhado ou compartilhado.  
  
 Não há campos de diagnóstico de cabeçalho específico do driver devem ser associados um identificador de ambiente.  
  
 Os campos de cabeçalho somente diagnóstico que são definidos para um indicador de descritor são SQL_DIAG_NUMBER e SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argumento DiagIdentifier  
 Esse argumento indica o identificador do campo obrigatório da estrutura de dados de diagnóstico. Se *RecNumber* é maior que ou igual a 1, os dados no campo descrevem as informações de diagnóstico retornadas por uma função. Se *RecNumber* for 0, o campo no cabeçalho da estrutura de dados de diagnóstico e, portanto, contém dados que pertencem a chamada de função que retornou informações de diagnóstico, não para informações específicas.  
  
 Drivers podem definir o cabeçalho específico do driver e campos de registro na estrutura de dados de diagnóstico.  
  
 Um ODBC 3*. x* aplicativo trabalhando com um ODBC 2*. x* driver poderá chamar **SQLGetDiagField** somente com um *DiagIdentifier* argumento de SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME ou SQL_DIAG_SQLSTATE. Todos os outros campos de diagnósticos retornará SQL_ERROR.  
  
## <a name="header-fields"></a>Campos de cabeçalho  
 Os campos de cabeçalho listados na tabela a seguir podem ser incluídos no *DiagIdentifier* argumento.  
  
|DiagIdentifier|Tipo de retorno|Retorna|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Este campo contém a contagem de linhas no cursor. Sua semântica dependem de **SQLGetInfo** tipos de informações SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 e SQL_STATIC_CURSOR_ATTRIBUTES2, que indicam qual as contagens de linha estão disponíveis para cada tipo de cursor (em bits SQL_CA2_CRC_EXACT e SQL_CA2_CRC_APPROXIMATE).<br /><br /> O conteúdo deste campo é definido apenas para identificadores de instrução e só depois **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado. Chamando **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_CURSOR_ROW_COUNT em que não seja uma instrução identificador retornará SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Isso é uma cadeia de caracteres que descreve a instrução SQL executada a função subjacente. (Consulte "Valores dos campos de função dinâmico," nesta seção, para valores específicos). O conteúdo deste campo é definido apenas para identificadores de instrução e só depois de uma chamada para **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults**. Chamando **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION em que não seja uma instrução identificador retornará SQL_ERROR. O valor desse campo é indefinido antes de uma chamada para **SQLExecute** ou **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Este é um código numérico que descreve a instrução SQL que foi executada pela função subjacente. (Consulte "Valores da função campos dinâmicos," nesta seção, para um valor específico). O conteúdo deste campo é definido apenas para identificadores de instrução e só depois de uma chamada para **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults**. Chamando **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION_CODE em que não seja uma instrução identificador retornará SQL_ERROR. O valor desse campo é indefinido antes de uma chamada para **SQLExecute** ou **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|O número de registros de status que estão disponíveis para o identificador especificado.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Código de retorno retornado pela função. Para obter uma lista de códigos de retorno, consulte [códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md). O driver não precisa implementar SQL_DIAG_RETURNCODE; ele sempre é implementado pelo Gerenciador de Driver. Se nenhuma função tiver sido chamada ainda no *tratar*, retornará SQL_SUCCESS para SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|O número de linhas afetadas por uma insert, delete ou update executada pelo **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos**. Ele é definido pelo driver após um *especificação de cursor* foi executado. O conteúdo deste campo é definido apenas para identificadores de instrução. Chamando **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_ROW_COUNT em que não seja uma instrução identificador retornará SQL_ERROR. Os dados nesse campo também são retornados o *RowCountPtr* argumento de **SQLRowCount**. Os dados nesse campo são redefinidos após cada chamada de função nondiagnostic, enquanto que a contagem de linhas retornado por **SQLRowCount** permanecerá o mesmo até que a instrução é redefinida para o estado preparado ou alocado.|  
  
## <a name="record-fields"></a>Campos de registro  
 Os campos de registro listados na tabela a seguir podem ser incluídos no *DiagIdentifier* argumento.  
  
|DiagIdentifier|Tipo de retorno|Retorna|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Uma cadeia de caracteres que indica o documento que define a parte de classe do valor SQLSTATE nesse registro. Seu valor é "ISO 9075" para todos os SQLSTATEs definidos pela interface de nível de chamada ISO e Open Group. Para SQLSTATEs de ODBC específico (aqueles cuja classe SQLSTATE é "Mi"), seu valor é "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Se o campo SQL_DIAG_ROW_NUMBER é um número válido de linha em um conjunto de linhas ou um conjunto de parâmetros, este campo contém o valor que representa o número de coluna no conjunto de resultados ou o número do parâmetro no conjunto de parâmetros. Conjunto de resultados números sempre começam com 1; Se este registro de status pertence a uma coluna de indicador, o campo pode ser zero. Parâmetro números começam em 1. Ele tem o valor SQL_NO_COLUMN_NUMBER se o registro de status não está associado um número de coluna ou o número do parâmetro. Se o driver não pode determinar o número de coluna ou parâmetro que este registro está associado, este campo tem o valor SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> O conteúdo deste campo é definido apenas para identificadores de instrução.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Uma cadeia de caracteres que indica o nome de conexão que o registro de diagnóstico está relacionado a. Este campo é definido pelo driver. Para estruturas de dados de diagnóstico associadas com o identificador de ambiente e os diagnósticos não estão relacionados a qualquer conexão, esse campo é uma cadeia de caracteres de comprimento zero.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Uma mensagem informativa sobre o erro ou aviso. Esse campo é formatado conforme descrito em [mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md). Não há nenhum tamanho máximo para o texto da mensagem de diagnóstico.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Um código de erro nativo específico de fonte de dados/driver. Se não houver nenhum código de erro nativo, o driver retornará 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Este campo contém o número da linha no conjunto de linhas ou o número do parâmetro no conjunto de parâmetros, ao qual o registro de status está associado. Números de linha e parâmetro começam com 1. Este campo tem o valor SQL_NO_ROW_NUMBER se este registro de status não está associado um número de linha ou o número do parâmetro. Se o driver não pode determinar o número de linhas ou parâmetro que este registro está associado, este campo tem o valor SQL_ROW_NUMBER_UNKNOWN.<br /><br /> O conteúdo deste campo é definido apenas para identificadores de instrução.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Uma cadeia de caracteres que indica o nome do servidor de registro de diagnóstico relacionadas ao. É o mesmo que o valor retornado para uma chamada para **SQLGetInfo** com a opção SQL_DATA_SOURCE_NAME. Para estruturas de dados de diagnóstico associadas com o identificador de ambiente e os diagnósticos não estão relacionados a qualquer servidor, esse campo é uma cadeia de caracteres de comprimento zero.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Um código de diagnóstico de SQLSTATE de cinco caracteres. Para obter mais informações, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Uma cadeia de caracteres com o mesmo formato e os valores válidos como SQL_DIAG_CLASS_ORIGIN, que identifica a parte de definição da parte do código SQLSTATE subclasse. Os SQLSTATES de ODBC específico para o qual será retornado "ODBC 3.0" incluem o seguinte:<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valores dos campos de função dinâmico  
 A tabela a seguir descreve os valores de SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE que se aplicam a cada tipo de instrução SQL executada por uma chamada para **SQLExecute** ou **SQLExecDirect**. O driver pode adicionar valores definidos pelo driver para aqueles listados.  
  
|instrução SQL<br /><br /> executado|Valor de<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valor de<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*instrução ALTER de domínio*|"ALTER DOMÍNIO"|SQL_DIAG_ALTER_DOMAIN|  
|*instrução ALTER de tabela*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*definição de declaração*|"CRIAR A DECLARAÇÃO"|SQL_DIAG_CREATE_ASSERTION|  
|*definição de conjunto de caracteres*|"CRIAR O CONJUNTO DE CARACTERES"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*definição de agrupamento*|"CRIAR O AGRUPAMENTO"|SQL_DIAG_CREATE_COLLATION|  
|*instrução CREATE de índice*|"CRIAR O ÍNDICE"|SQL_DIAG_CREATE_INDEX|  
|*instrução CREATE de tabela*|"CRIAR A TABELA"|SQL_DIAG_CREATE_TABLE|  
|*instrução CREATE de exibição*|"CRIAR MODO DE EXIBIÇÃO"|SQL_DIAG_CREATE_VIEW|  
|*especificação de cursor*|"SELECIONE CURSOR"|SQL_DIAG_SELECT_CURSOR|  
|*posição de instrução de exclusão*|"CURSOR DE EXCLUSÃO DINÂMICA"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*pesquisa de instrução de exclusão*|"DELETE ONDE"|SQL_DIAG_DELETE_WHERE|  
n-definição *|"CRIAR DOMÍNIO"|SQL_DIAG_CREATE_DOMAIN|  
|*instrução de asserção de drop*|"DROP ASSERÇÃO"|SQL_DIAG_DROP_ASSERTION|  
|*soltar caracteres-conjunto stmt*|"CONJUNTO DE CARACTERES DE SOLTAR"|SQL_DIAG_DROP_CHARACTER_SET|  
|*instrução de drop-agrupamento*|"AGRUPAMENTO DE SOLTAR"|SQL_DIAG_DROP_COLLATION|  
|*instrução de drop-domínio*|"DOMÍNIO SOLTAR"|SQL_DIAG_DROP_DOMAIN|  
|*descarte de índice de instrução*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*instrução drop-schema*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*instrução drop-table*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*descarte de conversão de instrução*|"CONVERSÃO DE SOLTAR"|SQL_DIAG_DROP_TRANSLATION|  
|*instrução drop-view*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
-instrução *|"GRANT"|SQL_DIAG_GRANT|  
|*instrução INSERT*|"INSERIR"|SQL_DIAG_INSERT|  
|*Extensão do procedimento de ODBC*|"CHAMADA"|CHAMADA DE SQL_DIAG_|  
|*Instrução REVOKE*|"REVOKE"|SQL_DIAG_REVOKE|  
|*definição de esquema*|"CRIAR O ESQUEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*definição de tradução*|"CRIAR TRADUÇÃO"|SQL_DIAG_CREATE_TRANSLATION|  
|*posição da instrução de atualização*|"A ATUALIZAÇÃO DINÂMICA CURSOR"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*pesquisa de instrução de atualização*|"ONDE A ATUALIZAÇÃO"|SQL_DIAG_UPDATE_WHERE|  
|Unknown (desconhecido)|*cadeia de caracteres vazia*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>Sequência de registros de Status  
 Registros de status são posicionados em uma sequência com base no número de linha e o tipo do diagnóstico. O Gerenciador de Driver determina a ordem final para retornar registros de status que ele gera. O driver determina a ordem final para retornar registros de status que ele gera.  
  
 Se os registros de diagnóstico são lançados pelo Gerenciador de Driver e o driver, o Gerenciador de Driver é responsável por ordená-los.  
  
 Se houver dois ou mais registros de status, a sequência de registros é determinada pela primeira vez pelo número da linha. As seguintes regras se aplicam a determinar a sequência de registros de diagnóstico por linha:  
  
-   Os registros que não correspondem a qualquer linha aparecem na frente de registros que correspondem a uma linha específica, porque SQL_NO_ROW_NUMBER é definido como -1.  
  
-   Registros para o qual o número de linhas é desconhecido aparecem na frente de todos os outros registros porque SQL_ROW_NUMBER_UNKNOWN está definido para ser – 2.  
  
-   Para todos os registros que pertencem às linhas específicas, os registros são classificados pelo valor no campo SQL_DIAG_ROW_NUMBER. Todos os erros e avisos da primeira linha afetados são listados e, em seguida, todos os erros e avisos da próxima linha afetada e assim por diante.  
  
> [!NOTE]  
>  O ODBC 3*. x* Gerenciador de Driver não solicitar registros de status na fila de diagnóstico se SQLSTATE 01S01 (erro na linha) é retornado por um ODBC 2*. x* driver ou se SQLSTATE 01S01 (linha) será retornado pelo ODBC 3*. x* driver quando **SQLExtendedFetch** é chamado ou **SQLSetPos** é chamado em um cursor que tenha sido posicionado com **SQLExtendedFetch** .  
  
 Em cada linha, ou para todos os registros que não correspondem a uma linha ou para o qual o número de linhas é desconhecido, ou para todos os registros com um número de linhas igual a SQL_NO_ROW_NUMBER, o primeiro registro listado é determinado por meio de um conjunto de regras de classificação. Após o primeiro registro, a ordem dos outros registros que afeta uma linha é indefinida. Um aplicativo não pode assumir que os erros precedem avisos após o primeiro registro. Examine a estrutura de dados de diagnóstico completo para obter informações completas sobre uma chamada bem-sucedida para uma função de aplicativos.  
  
 As regras a seguir são usadas para determinar o primeiro registro dentro de uma linha. O registro com a classificação mais alta é o primeiro registro. A fonte de um registro (Gerenciador de Driver, driver, gateway e assim por diante) não é considerada quando registros de classificação.  
  
-   **Erros** registros de Status que descrevem erros têm a classificação mais alta. As seguintes regras são aplicadas para classificar os erros:  
  
    -   Os registros que indicam uma falha de transação ou a falha na transação possíveis outrank todos os outros registros.  
  
    -   Se dois ou mais registros descrevem a mesma condição de erro, SQLSTATEs definidas pela especificação de CLI do grupo aberto (classes 03 por meio de HZ) outrank SQLSTATEs ODBC-definidos pelo driver.  
  
-   **Os valores de dados não definido pela implementação** registros de Status que descrevem os valores de dados não definidos pelo driver (classe 02) têm a segunda classificação mais alta.  
  
-   **Avisos** registros de Status que descreve os avisos (classe 01) têm a classificação mais baixa. Se dois ou mais registros descrevem a mesma condição de aviso, aviso, em seguida, SQLSTATEs definidas pela especificação de CLI do grupo aberto outrank SQLSTATEs definidas pelo ODBC e definidos pelo driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obter vários campos de uma estrutura de dados de diagnóstico|[Função SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
