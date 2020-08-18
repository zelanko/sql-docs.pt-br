---
description: Função SQLGetDiagField
title: Função SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92043f5deb505d60ebe168a9c219c4d37a304ed5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461021"
---
# <a name="sqlgetdiagfield-function"></a>Função SQLGetDiagField

**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetDiagField** retorna o valor atual de um campo de um registro da estrutura de dados de diagnóstico (associada a um identificador especificado) que contém informações de erro, de aviso e de status.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp

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
 Entrada Um identificador de tipo de identificador que descreve o tipo de identificador para o qual o diagnóstico é necessário. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 O identificador de SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo driver e pelo Gerenciador de driver. Os aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 Entrada Um identificador para a estrutura de dados de diagnóstico, do tipo indicado por *HandleType*. Se *HandleType* for SQL_HANDLE_ENV, o *identificador* poderá ser um identificador de ambiente compartilhado ou não compartilhado.  
  
 *RecNumber*  
 Entrada Indica o registro de status do qual o aplicativo busca informações. Os registros de status são numerados a partir de 1. Se o argumento *DiagIdentifier* indicar qualquer campo do cabeçalho de diagnóstico, *RecNumber* será ignorado. Caso contrário, deve ser maior que 0.  
  
 *DiagIdentifier*  
 Entrada Indica o campo do diagnóstico cujo valor deve ser retornado. Para obter mais informações, consulte a seção "argumento*DiagIdentifier* " em "Comentários".  
  
 *DiagInfoPtr*  
 Der Ponteiro para um buffer no qual as informações de diagnóstico são retornadas. O tipo de dados depende do valor de *DiagIdentifier*. Se *DiagInfoPtr* for um tipo inteiro, os aplicativos deverão usar um buffer de SQLULEN e inicializar o valor como 0 antes de chamar essa função, pois alguns drivers só podem gravar o menor 32 bits ou 16 bits de um buffer e deixar o bit de ordem superior inalterado.  
  
 Se *DiagInfoPtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *DiagInfoPtr*.  
  
 *BufferLength*  
 Entrada Se *DiagIdentifier* for um diagnóstico definido pelo ODBC e o *DiagInfoPtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o comprimento de \* *DiagInfoPtr*. Se *DiagIdentifier* for um campo definido pelo ODBC e \* *DiagInfoPtr* for um inteiro, *BufferLength* será ignorado. Se o valor em * \* DiagInfoPtr* for uma cadeia de caracteres Unicode (ao chamar **SQLGetDiagFieldW**), o argumento *BufferLength* deverá ser um número par.  
  
 Se *DiagIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength* . *BufferLength* pode ter os seguintes valores:  
  
-   Se *DiagInfoPtr* for um ponteiro para uma cadeia de caracteres, *BufferLength* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *DiagInfoPtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *DiagInfoPtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *BufferLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se * \* DiagInfoPtr* contiver um tipo de dados de comprimento fixo, *BufferLength* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de bytes (exceto o número de bytes necessários para o caractere de terminação nula) disponível para retornar em \* *DiagInfoPtr*, para dados de caractere. Se o número de bytes disponíveis para retornar for maior ou igual a *BufferLength*, o texto em \* *DiagInfoPtr* será truncado para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLGetDiagField** não publica registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retorno para relatar o resultado de sua própria execução:  
  
-   SQL_SUCCESS: a função retornou informações de diagnóstico com êxito.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* era muito pequeno para manter o campo de diagnóstico solicitado. Portanto, os dados no campo de diagnóstico foram truncados. Para determinar que ocorreu um truncamento, o aplicativo deve comparar *BufferLength* com o número real de bytes disponíveis, que é gravado em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: o identificador indicado por *HandleType* e *identificador* não era um identificador válido.  
  
-   SQL_ERROR: uma das seguintes ocorrências:  
  
    -   *O argumento DiagIdentifier* não era um dos valores válidos.  
  
    -   *O argumento DiagIdentifier* foi SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE ou SQL_DIAG_ROW_COUNT, mas o *identificador* não era um identificador de instrução. (O Gerenciador de driver retorna esse diagnóstico.)  
  
    -   *O argumento RecNumber* era negativo ou 0 quando *DiagIdentifier* indicou um campo de um registro de diagnóstico. *RecNumber* é ignorado para campos de cabeçalho.  
  
    -   O valor solicitado foi uma cadeia de caracteres e *BufferLength* era menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona no identificador não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* foi maior que o número de registros de diagnóstico que existia para o identificador especificado no *identificador.* A função também retorna SQL_NO_DATA para qualquer *RecNumber* positivo se não houver nenhum registro de diagnóstico para o *identificador*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLGetDiagField** para realizar uma das três metas:  
  
1.  Para obter informações específicas de erro ou aviso quando uma chamada de função tiver retornado SQL_ERROR ou SQL_SUCCESS_WITH_INFO (ou SQL_NEED_DATA para a função **SQLBrowseConnect** ).  
  
2.  Para determinar o número de linhas na fonte de dados que foram afetadas quando as operações de inserção, exclusão ou atualização foram executadas com uma chamada para **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** (do campo de cabeçalho SQL_DIAG_ROW_COUNT) ou para determinar o número de linhas que existem no cursor aberto atual, se o driver puder fornecer essas informações (a partir do campo de cabeçalho SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Para determinar qual função foi executada por uma chamada para **SQLExecDirect** ou **SQLExecute** (dos campos de cabeçalho SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Qualquer função ODBC pode postar zero ou mais registros de diagnóstico toda vez que for chamada, de modo que um aplicativo possa chamar **SQLGetDiagField** após qualquer chamada de função ODBC. Não há nenhum limite para o número de registros de diagnóstico que podem ser armazenados a qualquer momento. **SQLGetDiagField** recupera apenas as informações de diagnóstico mais recentemente associadas à estrutura de dados de diagnóstico especificada no argumento *Handle* . Se o aplicativo chamar uma função ODBC diferente de **SQLGetDiagField** ou **SQLGetDiagRec**, todas as informações de diagnóstico de uma chamada anterior com o mesmo identificador serão perdidas.  
  
 Um aplicativo pode verificar todos os registros de diagnóstico incrementando *RecNumber*, desde que **SQLGetDiagField** retorne SQL_SUCCESS. O número de registros de status é indicado no campo de cabeçalho SQL_DIAG_NUMBER. As chamadas para **SQLGetDiagField** não são destrutivas para os campos de cabeçalho e registro. O aplicativo pode chamar **SQLGetDiagField** novamente mais tarde para recuperar um campo de um registro, desde que uma função diferente das funções de diagnóstico não tenha sido chamada no interim, o que pode postar registros no mesmo identificador.  
  
 Um aplicativo pode chamar **SQLGetDiagField** para retornar qualquer campo de diagnóstico a qualquer momento, exceto para SQL_DIAG_CURSOR_ROW_COUNT ou SQL_DIAG_ROW_COUNT, que retornará SQL_ERROR se o *identificador* não for um identificador de instrução. Se qualquer outro campo de diagnóstico for indefinido, a chamada para **SQLGetDiagField** retornará SQL_SUCCESS (desde que nenhum outro diagnóstico seja encontrado) e um valor indefinido será retornado para o campo.  
  
 Para obter mais informações, consulte [usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente daquela que está sendo executada de forma assíncrona gerará HY010 "erro de sequência de função". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona seja concluída.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador pode ter informações de diagnóstico associadas a ele. O argumento *HandleType* indica o tipo de manipulador do *identificador*.  
  
 Alguns campos de cabeçalho e de registro não podem ser retornados para identificadores de ambiente, conexão, instrução e descritor. Os identificadores para os quais um campo não é aplicável são indicados nas seções "campos de cabeçalho" e "campos de registro" a seguir.  
  
 Se *HandleType* for SQL_HANDLE_ENV, o *identificador* poderá ser um identificador de ambiente compartilhado ou não compartilhado.  
  
 Nenhum campo de diagnóstico de cabeçalho específico do driver deve ser associado a um identificador de ambiente.  
  
 Os únicos campos de cabeçalho de diagnóstico que são definidos para um identificador de descritor são SQL_DIAG_NUMBER e SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argumento DiagIdentifier  
 Esse argumento indica o identificador do campo necessário na estrutura de dados de diagnóstico. Se *RecNumber* for maior ou igual a 1, os dados no campo descreverão as informações de diagnóstico retornadas por uma função. Se *RecNumber* for 0, o campo estará no cabeçalho da estrutura de dados de diagnóstico e, portanto, conterá dados pertencentes à chamada de função que retornaram as informações de diagnóstico, e não às informações específicas.  
  
 Os drivers podem definir campos de cabeçalho e registro específicos do driver na estrutura de dados de diagnóstico.  
  
 Um aplicativo ODBC 3 *. x* trabalhando com um driver ODBC 2 *. x* poderá chamar **SQLGetDiagField** somente com um argumento *DiagIdentifier* de SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME ou SQL_DIAG_SQLSTATE. Todos os outros campos de diagnóstico retornarão SQL_ERROR.  
  
## <a name="header-fields"></a>Campos de cabeçalho  
 Os campos de cabeçalho listados na tabela a seguir podem ser incluídos no argumento *DiagIdentifier* .  
  
|DiagIdentifier|Tipo de retorno|Retornos|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Este campo contém a contagem de linhas no cursor. Sua semântica depende dos tipos de informações do **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 e SQL_STATIC_CURSOR_ATTRIBUTES2, que indicam quais contagens de linhas estão disponíveis para cada tipo de cursor (nos bits SQL_CA2_CRC_EXACT e SQL_CA2_CRC_APPROXIMATE).<br /><br /> O conteúdo deste campo é definido somente para identificadores de instrução e somente após **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado. Chamar **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_CURSOR_ROW_COUNT em vez de um identificador de instrução retornará SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR|Esta é uma cadeia de caracteres que descreve a instrução SQL executada pela função subjacente. (Consulte "valores dos campos de função dinâmica", posteriormente nesta seção, para obter valores específicos.) O conteúdo deste campo é definido somente para identificadores de instrução e somente após uma chamada para **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults**. Chamar **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION em vez de um identificador de instrução retornará SQL_ERROR. O valor desse campo é indefinido antes de uma chamada para **SQLExecute** ou **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Este é um código numérico que descreve a instrução SQL que foi executada pela função subjacente. (Consulte "valores dos campos de função dinâmica", posteriormente nesta seção, para obter um valor específico.) O conteúdo deste campo é definido somente para identificadores de instrução e somente após uma chamada para **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults**. Chamar **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION_CODE em vez de um identificador de instrução retornará SQL_ERROR. O valor desse campo é indefinido antes de uma chamada para **SQLExecute** ou **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|O número de registros de status que estão disponíveis para o identificador especificado.|  
|SQL_DIAG_RETURNCODE|SqlReturn|Código de retorno retornado pela função. Para obter uma lista de códigos de retorno, consulte [códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md). O driver não precisa implementar SQL_DIAG_RETURNCODE; Ele é sempre implementado pelo Gerenciador de driver. Se nenhuma função ainda tiver sido chamada no *identificador*, SQL_SUCCESS será retornado para SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|O número de linhas afetadas por uma inserção, exclusão ou atualização executada por **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos**. Ele é definido por driver após a execução de uma *especificação de cursor* . O conteúdo deste campo é definido somente para identificadores de instrução. Chamar **SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_ROW_COUNT em vez de um identificador de instrução retornará SQL_ERROR. Os dados nesse campo também são retornados no argumento *RowCountPtr* de **SQLRowCount**. Os dados nesse campo são redefinidos após cada chamada de função não de diagnóstico, enquanto que a contagem de linhas retornada por **SQLRowCount** permanece a mesma até que a instrução seja configurada de volta para o estado preparado ou alocado.|  
  
## <a name="record-fields"></a>Campos de registro  
 Os campos de registro listados na tabela a seguir podem ser incluídos no argumento *DiagIdentifier* .  
  
|DiagIdentifier|Tipo de retorno|Retornos|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR|Uma cadeia de caracteres que indica o documento que define a parte da classe do valor SQLSTATE neste registro. Seu valor é "ISO 9075" para todos os sqlstates definidos pelo grupo aberto e pela interface de nível de chamada ISO. Para sqlstates específicos do ODBC (todos aqueles cuja classe SQLSTATE é "IM"), seu valor é "ODBC 3,0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Se o campo de SQL_DIAG_ROW_NUMBER for um número de linha válido em um conjunto de linhas ou um grupo de parâmetros, esse campo conterá o valor que representa o número da coluna no conjunto de resultados ou o número do parâmetro no conjunto de parâmetros. Os números de coluna do conjunto de resultados sempre começam em 1; Se esse registro de status pertencer a uma coluna de indicador, o campo poderá ser zero. Os números de parâmetros começam em 1. Ele tem o valor SQL_NO_COLUMN_NUMBER se o registro de status não estiver associado com um número de coluna ou número de parâmetro. Se o driver não puder determinar o número da coluna ou o número do parâmetro ao qual esse registro está associado, esse campo terá o valor SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> O conteúdo deste campo é definido somente para identificadores de instrução.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR|Uma cadeia de caracteres que indica o nome da conexão à qual o registro de diagnóstico está relacionado. Este campo é definido pelo driver. Para estruturas de dados de diagnóstico associadas ao identificador de ambiente e para diagnósticos que não estão relacionados a nenhuma conexão, esse campo é uma cadeia de caracteres de comprimento zero.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR|Uma mensagem informativa sobre o erro ou aviso. Esse campo é formatado conforme descrito em [mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md). Não há comprimento máximo para o texto da mensagem de diagnóstico.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Um código de erro nativo específico da fonte de dados/driver. Se não houver nenhum código de erro nativo, o driver retornará 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Este campo contém o número da linha no conjunto de linhas ou o número do parâmetro no conjunto de parâmetros, com o qual o registro de status está associado. Números de linha e números de parâmetros começam com 1. Esse campo tem o valor SQL_NO_ROW_NUMBER se esse registro de status não estiver associado a um número de linha ou número de parâmetro. Se o driver não puder determinar o número de linha ou o número de parâmetro ao qual esse registro está associado, esse campo terá o valor SQL_ROW_NUMBER_UNKNOWN.<br /><br /> O conteúdo deste campo é definido somente para identificadores de instrução.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR|Uma cadeia de caracteres que indica o nome do servidor ao qual o registro de diagnóstico está relacionado. É o mesmo que o valor retornado para uma chamada para **SQLGetInfo** com a opção SQL_DATA_SOURCE_NAME. Para estruturas de dados de diagnóstico associadas ao identificador de ambiente e para diagnósticos que não estão relacionados a nenhum servidor, esse campo é uma cadeia de caracteres de comprimento zero.|  
|SQL_DIAG_SQLSTATE|SQLCHAR|Um código de diagnóstico SQLSTATE de cinco caracteres. Para obter mais informações, consulte [SQLstates](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR|Uma cadeia de caracteres com o mesmo formato e valores válidos que SQL_DIAG_CLASS_ORIGIN, que identifica a parte de definição da parte da subclasse do código SQLSTATE. Os sqlstates específicos do ODBC para os quais "ODBC 3,0" é retornado incluem o seguinte:<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011,.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valores dos campos de função dinâmica  
 A tabela a seguir descreve os valores de SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE que se aplicam a cada tipo de instrução SQL executada por uma chamada para **SQLExecute** ou **SQLExecDirect**. O driver pode adicionar valores definidos pelo driver àqueles listados.  
  
|Instrução SQL<br /><br /> executo|Valor de <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valor de <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*instrução ALTER-Domain-*|"ALTERAR DOMÍNIO"|SQL_DIAG_ALTER_DOMAIN|  
|*instrução ALTER-TABLE-*|"ALTERAR TABELA"|SQL_DIAG_ALTER_TABLE|  
|*definição de asserção*|"CRIAR ASSERÇÃO"|SQL_DIAG_CREATE_ASSERTION|  
|*definição de conjunto de caracteres*|"CRIAR CONJUNTO DE CARACTERES"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*definição de agrupamento*|"CRIAR AGRUPAMENTO"|SQL_DIAG_CREATE_COLLATION|  
|*domainn-definição*|"CRIAR DOMÍNIO"|SQL_DIAG_CREATE_DOMAIN|
|*instrução CREATE-INDEX-*|"CRIAR ÍNDICE"|SQL_DIAG_CREATE_INDEX|  
|*instrução CREATE-TABLE-*|"CREATE TABLE"|SQL_DIAG_CREATE_TABLE|  
|*instrução CREATE-View-*|"CRIAR MODO DE EXIBIÇÃO"|SQL_DIAG_CREATE_VIEW|  
|*especificação de cursor*|"SELECIONAR CURSOR"|SQL_DIAG_SELECT_CURSOR|  
|*Delete-instruções posicionadas*|"CURSOR DE EXCLUSÃO DINÂMICA"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*excluir instrução-pesquisada*|"EXCLUIR ONDE"|SQL_DIAG_DELETE_WHERE|  
|*instrução DROP-Assertion-*|"DESCARTAR ASSERÇÃO"|SQL_DIAG_DROP_ASSERTION|  
|*Drop-character-set-stmt*|"REMOVER CONJUNTO DE CARACTERES"|SQL_DIAG_DROP_CHARACTER_SET|  
|*instrução DROP-agrupamento-*|"REMOVER AGRUPAMENTO"|SQL_DIAG_DROP_COLLATION|  
|*instrução DROP-Domain-*|"REMOVER DOMÍNIO"|SQL_DIAG_DROP_DOMAIN|  
|*instrução DROP-INDEX-*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*instrução DROP-Schema-*|"DESCARTAR ESQUEMA"|SQL_DIAG_DROP_SCHEMA|  
|*instrução DROP-TABLE-*|"REMOVER TABELA"|SQL_DIAG_DROP_TABLE|  
|*instrução DROP-translation-*|"REMOVER TRANSLAÇÃO"|SQL_DIAG_DROP_TRANSLATION|  
|*instrução DROP-View-*|"DESCARTAR EXIBIÇÃO"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|CONCEDER|SQL_DIAG_GRANT|
|*instrução INSERT*|INSERIDO|SQL_DIAG_INSERT|  
|*ODBC – procedimento-extensão*|LIGAÇÃO|CHAMADA DE SQL_DIAG_|  
|*instrução REVOKE*|CANCELAR|SQL_DIAG_REVOKE|  
|*definição de esquema*|"CRIAR ESQUEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*conversão-definição*|"CRIAR TRADUÇÃO"|SQL_DIAG_CREATE_TRANSLATION|  
|*atualização – posicionada na instrução*|"CURSOR DE ATUALIZAÇÃO DINÂMICA"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*Update-Statement-pesquised*|"ATUALIZAR ONDE"|SQL_DIAG_UPDATE_WHERE|  
|Unknown (desconhecido)|*cadeia de caracteres vazia*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>Sequência de registros de status

 Os registros de status são posicionados em uma sequência com base no número da linha e no tipo de diagnóstico. O Gerenciador de driver determina a ordem final para retornar os registros de status que ele gera. O driver determina a ordem final para retornar os registros de status que ele gera.  
  
 Se os registros de diagnóstico forem postados pelo Gerenciador de driver e pelo driver, o Gerenciador de driver será responsável por ordená-los.  
  
 Se houver dois ou mais registros de status, a sequência dos registros será determinada primeiro por número de linha. As regras a seguir se aplicam para determinar a sequência de registros de diagnóstico por linha:  
  
-   Os registros que não correspondem a nenhuma linha aparecem na frente dos registros que correspondem a uma linha específica, porque SQL_NO_ROW_NUMBER é definido como-1.  
  
-   Os registros para os quais o número de linha é desconhecido aparecem na frente de todos os outros registros, porque SQL_ROW_NUMBER_UNKNOWN é definido como-2.  
  
-   Para todos os registros que pertencem a linhas específicas, os registros são classificados pelo valor no campo SQL_DIAG_ROW_NUMBER. Todos os erros e avisos da primeira linha afetada são listados e, em seguida, todos os erros e avisos da próxima linha afetadas e assim por diante.  
  
> [!NOTE]
>  O Gerenciador de driver ODBC 3 *. x* não ordena registros de status na fila de diagnóstico se SQLSTATE 01S01 (erro na linha) for retornado por um driver ODBC 2 *. x* ou se SQLSTATE 01S01 (erro na linha) for RETORNADO por um driver ODBC 3 *. x* quando **SQLExtendedFetch** for chamado ou **SQLSetPos** for chamado em um cursor que tenha sido posicionado com **SQLExtendedFetch**.  
  
 Dentro de cada linha, ou para todos os registros que não correspondem a uma linha ou para o qual o número de linha é desconhecido, ou para todos os registros com um número de linha igual a SQL_NO_ROW_NUMBER, o primeiro registro listado é determinado usando um conjunto de regras de classificação. Após o primeiro registro, a ordem dos outros registros que afetam uma linha é indefinida. Um aplicativo não pode supor que os erros precedem avisos após o primeiro registro. Os aplicativos devem examinar a estrutura de dados de diagnóstico completa para obter informações completas sobre uma chamada malsucedida para uma função.  
  
 As regras a seguir são usadas para determinar o primeiro registro dentro de uma linha. O registro com a classificação mais alta é o primeiro registro. A origem de um registro (Gerenciador de driver, Driver, gateway e assim por diante) não é considerada durante a classificação de registros.  
  
-   **Erros** do Os registros de status que descrevem erros têm a classificação mais alta. As regras a seguir são aplicadas a erros de classificação:  
  
    -   Registros que indicam uma falha de transação ou possível falha de transação outrank todos os outros registros.  
  
    -   Se dois ou mais registros descreverem a mesma condição de erro, sqlstates definidos pela especificação CLI do grupo aberto (classes 03 a HZ) outrank ODBC-e sqlstates definidos pelo driver.  
  
-   **Implementação-nenhum valor de dados definido** Os registros de status que descrevem os valores de dados definidos pelo driver (classe 02) têm a segunda classificação mais alta.  
  
-   **Avisos** Os registros de status que descrevem avisos (classe 01) têm a classificação mais baixa. Se dois ou mais registros descreverem a mesma condição de aviso, em seguida, avisará que o estado definido pela especificação da CLI do grupo aberto outrank o definido pelo ODBC e os hiperestados definidos pelo driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo vários campos de uma estrutura de dados de diagnóstico|[Função SQLGetDiagRec](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
