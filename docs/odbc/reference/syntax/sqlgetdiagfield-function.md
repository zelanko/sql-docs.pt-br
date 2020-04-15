---
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
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285426"
---
# <a name="sqlgetdiagfield-function"></a>Função SQLGetDiagField

**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLGetDiagField** retorna o valor atual de um campo de um registro da estrutura de dados diagnósticos (associado a uma alça especificada) que contém informações de erro, aviso e status.  
  
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
 *Handletype*  
 [Entrada] Um identificador de tipo de alça que descreve o tipo de alça para a qual os diagnósticos são necessários. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN alça é usada apenas pelo Driver Manager e pelo motorista. Os aplicativos não devem usar este tipo de alça. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [Developing Connection-Pool Awareness em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Uma alça para a estrutura de dados diagnósticos, do tipo indicado pelo *HandleType*. Se *o HandleType* estiver SQL_HANDLE_ENV, *o Handle* pode ser um cabo de ambiente compartilhado ou não compartilhado.  
  
 *RecNumber*  
 [Entrada] Indica o registro de status a partir do qual o aplicativo busca informações. Os registros de status são numerados a partir de 1. Se o argumento *DiagIdentifier* indicar qualquer campo do cabeçalho de diagnóstico, *O RecNumber* será ignorado. Se não, deve ser mais de 0.  
  
 *DiagIdentifier*  
 [Entrada] Indica o campo do diagnóstico cujo valor deve ser devolvido. Para obter mais informações, consulte a seção *"Argumento do DiagIdentifier"* em "Comentários".  
  
 *DiagInfoPtr*  
 [Saída] Ponteiro para um buffer no qual para retornar as informações de diagnóstico. O tipo de dados depende do valor do *DiagIdentifier*. Se *o DiagInfoPtr* for um tipo inteiro, os aplicativos devem usar um buffer de SQLULEN e inicializar o valor para 0 antes de chamar essa função, pois alguns drivers só podem gravar o buffer de 32 bits ou 16 bits inferiores e deixar o bit de ordem superior inalterado.  
  
 Se *o DiagInfoPtr* for NULL, *stringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *DiagInfoPtr*.  
  
 *BufferLength*  
 [Entrada] Se *o DiagIdentifier* é um diagnóstico definido pelo ODBC e *o DiagInfoPtr* aponta para \*uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento do *DiagInfoPtr*. Se *diagIdentifier* é um campo definido \*pelo ODBC e *DiagInfoPtr* é um inteiro, *BufferLength* é ignorado. Se o valor no * \*DiagInfoPtr* for uma seqüência unicode (ao chamar **SQLGetDiagFieldW),** o argumento *BufferLength* deve ser um número uniforme.  
  
 Se *o DiagIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength.* *BufferLength* pode ter os seguintes valores:  
  
-   Se *DiagInfoPtr* for um ponteiro para uma seqüência de caracteres, *BufferLength* será o comprimento da seqüência ou SQL_NTS.  
  
-   Se *DiagInfoPtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *DiagInfoPtr* for um ponteiro para um valor diferente de uma seqüência de caracteres ou cadeia binária, *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se * \*o DiagInfoPtr* contiver um tipo de dados de comprimento fixo, *o BufferLength* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o número de bytes necessários para o caractere de rescisão nula) disponível para retornar no \* *DiagInfoPtr*, para dados de caracteres. Se o número de bytes disponíveis para retornar for maior \*ou igual a *BufferLength,* o texto no *DiagInfoPtr* será truncado para *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLGetDiagField** não posta registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retorno para relatar o resultado de sua própria execução:  
  
-   SQL_SUCCESS: A função retornou com sucesso as informações de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* era muito pequeno para manter o campo de diagnóstico solicitado. Portanto, os dados no campo de diagnóstico foram truncados. Para determinar que ocorreu uma truncamento, o aplicativo deve comparar *BufferLength* com o número real de bytes disponíveis, que está escrito em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: A alça indicada por *HandleType* e *Handle* não era uma alça válida.  
  
-   SQL_ERROR: Ocorreu um dos seguintes:  
  
    -   *O argumento DiagIdentifier* não era um dos valores válidos.  
  
    -   O argumento *DiagIdentifier* foi SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE ou SQL_DIAG_ROW_COUNT, mas *Handle* não era um manipulador de declaração. (O Driver Manager retorna este diagnóstico.)  
  
    -   O argumento *RecNumber* foi negativo ou 0 quando *o DiagIdentifier* indicou um campo a partir de um registro de diagnóstico. *RecNumber* é ignorado para campos de cabeçalho.  
  
    -   O valor solicitado foi uma seqüência de caracteres e *BufferLength* foi menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona na alça não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* foi maior do que o número de registros de diagnóstico que existiam para a alça especificada no *Handle.* A função também retorna SQL_NO_DATA para qualquer *RecNumber* positivo se não houver registros de diagnóstico para *Handle*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **o SQLGetDiagField** para alcançar um dos três objetivos:  
  
1.  Para obter informações específicas de erro ou aviso quando uma chamada de função tiver retornado SQL_ERROR ou SQL_SUCCESS_WITH_INFO (ou SQL_NEED_DATA para a função **SQLBrowseConnect).**  
  
2.  Para determinar o número de linhas na fonte de dados que foram afetadas quando as operações de inserção, exclusão ou atualização foram realizadas com uma chamada para **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** (do campo de cabeçalho SQL_DIAG_ROW_COUNT), ou para determinar o número de linhas existentes no cursor aberto atual, se o driver pode fornecer essas informações (a partir do campo de cabeçalho SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Para determinar qual função foi executada por uma chamada para **SQLExecDirect** ou **SQLExecute** (dos campos de cabeçalho SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Qualquer função ODBC pode postar zero ou mais registros de diagnóstico toda vez que for chamada, para que um aplicativo possa chamar **SQLGetDiagField** após qualquer chamada de função ODBC. Não há limite para o número de registros diagnósticos que podem ser armazenados a qualquer momento. **O SQLGetDiagField** recupera apenas as informações de diagnóstico mais recentemente associadas à estrutura de dados diagnósticos especificada no argumento *Lidar.* Se o aplicativo chamar uma função ODBC diferente de **SQLGetDiagField** ou **SQLGetDiagRec,** qualquer informação de diagnóstico de uma chamada anterior com o mesmo cabo será perdida.  
  
 Um aplicativo pode escarná-los incrementando *o RecNumber,* desde que **o SQLGetDiagField** retorne SQL_SUCCESS. O número de registros de status é indicado no campo de cabeçalho SQL_DIAG_NUMBER. As chamadas para **SQLGetDiagField** não são destrutivas para os campos de cabeçalho e gravação. O aplicativo pode chamar **SQLGetDiagField** novamente mais tarde para recuperar um campo de um registro, desde que uma função diferente das funções de diagnóstico não tenha sido chamada nesse ínterim, o que postaria registros na mesma alça.  
  
 Um aplicativo pode ligar para **o SQLGetDiagField** para retornar qualquer campo de diagnóstico a qualquer momento, exceto para SQL_DIAG_CURSOR_ROW_COUNT ou SQL_DIAG_ROW_COUNT, que retornará SQL_ERROR se *handle* não for uma alça de declaração. Se qualquer outro campo de diagnóstico estiver indefinido, a chamada para **SQLGetDiagField** retornará SQL_SUCCESS (desde que nenhum outro diagnóstico seja encontrado) e um valor indefinido seja devolvido para o campo.  
  
 Para obter mais informações, consulte [Usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [Implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente da que está sendo executada de forma assíncrona gerará HY010 "Erro de seqüência de funções". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona seja concluída.  
  
## <a name="handletype-argument"></a>Argumento handleType  
 Cada tipo de alça pode ter informações de diagnóstico associadas a ele. O argumento *HandleType* indica o tipo de alça de *Handle*.  
  
 Alguns campos de cabeçalho e registro não podem ser retornados para alças de ambiente, conexão, declaração e descritor. As alças para as quais um campo não é aplicável são indicadas nas seções "Campos de cabeçalho" e "Campos de registro" a seguir.  
  
 Se *o HandleType* estiver SQL_HANDLE_ENV, *o Handle* pode ser um cabo de ambiente compartilhado ou não compartilhado.  
  
 Nenhum campo de diagnóstico de cabeçalho específico do driver deve ser associado a uma alça de ambiente.  
  
 Os únicos campos de cabeçalho de diagnóstico definidos para uma alça de descritor são SQL_DIAG_NUMBER e SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argumento diagidentifier  
 Este argumento indica o identificador do campo necessário a partir da estrutura de dados diagnósticos. Se *O RecNumber* for maior ou igual a 1, os dados no campo descrevem as informações de diagnóstico retornadas por uma função. Se *O RecNumber* for 0, o campo está no cabeçalho da estrutura de dados diagnósticos e, portanto, contém dados relativos à chamada de função que retornou as informações de diagnóstico, não às informações específicas.  
  
 Os drivers podem definir os campos de cabeçalho e registro específicos do driver na estrutura de dados de diagnóstico.  
  
 Um aplicativo ODBC 3 *.x* que trabalha com um driver ODBC*2.x* poderá ligar para **o SQLGetDiagField** apenas com um argumento *DiagIdentifier* de SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME ou SQL_DIAG_SQLSTATE. Todos os outros campos de diagnóstico retornarão SQL_ERROR.  
  
## <a name="header-fields"></a>Campos de cabeçalho  
 Os campos de cabeçalho listados na tabela a seguir podem ser incluídos no argumento *DiagIdentifier.*  
  
|DiagIdentifier|Tipo de retorno|Retornos|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Este campo contém a contagem de linhas no cursor. Sua semântica depende dos tipos de informações **do SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 e SQL_STATIC_CURSOR_ATTRIBUTES2, que indicam quais contagens de linha estão disponíveis para cada tipo de cursor (nos bits SQL_CA2_CRC_EXACT e SQL_CA2_CRC_APPROXIMATE).<br /><br /> O conteúdo deste campo é definido apenas para alças de declaração e somente após **sqlexecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado. Chamar **sqLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_CURSOR_ROW_COUNT em outro que não seja uma alça de declaração retornará SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Esta é uma seqüência que descreve a declaração SQL que a função subjacente executou. (Consulte "Valores dos campos de função dinâmica", mais tarde nesta seção, para valores específicos.) O conteúdo deste campo é definido apenas para alças de declaração e somente após uma chamada para **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults**. Chamar **sqLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION em que não seja uma alça de declaração retornará SQL_ERROR. O valor deste campo é indefinido antes de uma chamada para **SQLExecute** ou **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Este é um código numérico que descreve a declaração SQL que foi executada pela função subjacente. (Consulte "Valores dos Campos de Função Dinâmica", mais tarde nesta seção, para obter um valor específico.) O conteúdo deste campo é definido apenas para alças de declaração e somente após uma chamada para **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults**. Ligar para **o SQLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION_CODE em outro que não seja uma alça de declaração retornará SQL_ERROR. O valor deste campo é indefinido antes de uma chamada para **SQLExecute** ou **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|O número de registros de status disponíveis para a alça especificada.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Código de retorno retornado pela função. Para obter uma lista de códigos de retorno, consulte [Códigos](../../../odbc/reference/develop-app/return-codes-odbc.md)de retorno . O motorista não precisa implementar SQL_DIAG_RETURNCODE; é sempre implementado pelo Driver Manager. Se nenhuma função ainda tiver sido chamada no *Handle*, SQL_SUCCESS será devolvido para SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|O número de linhas afetadas por uma inserção, exclusão ou atualização realizada por **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos**. É definido pelo driver após a execução de uma *especificação do cursor.* O conteúdo deste campo é definido apenas para alças de declaração. Chamar **sqLGetDiagField** com um *DiagIdentifier* de SQL_DIAG_ROW_COUNT em outro que não seja uma alça de declaração retornará SQL_ERROR. Os dados neste campo também são retornados no argumento *RowCountPtr* do **SQLRowCount**. Os dados neste campo são redefinidos após cada chamada de função não diagnóstica, enquanto a contagem de linhas retornada pelo **SQLRowCount** permanece a mesma até que a declaração seja definida para o estado preparado ou alocado.|  
  
## <a name="record-fields"></a>Campos de Registro  
 Os campos de registro listados na tabela a seguir podem ser incluídos no argumento *DiagIdentifier.*  
  
|DiagIdentifier|Tipo de retorno|Retornos|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Uma seqüência que indica o documento que define a parte de classe do valor SQLSTATE neste registro. Seu valor é "ISO 9075" para todos os SQLSTATEs definidos pelo Open Group e pela interface de nível de chamada ISO. Para SQLSTATEs específicos da ODBC (todos aqueles cuja classe SQLSTATE é "IM"), seu valor é "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Se o campo SQL_DIAG_ROW_NUMBER for um número de linha válido em um conjunto de linhas ou um conjunto de parâmetros, este campo contém o valor que representa o número da coluna no conjunto de resultados ou o número de parâmetro no conjunto de parâmetros. Os números da coluna de conjunto de resultados sempre começam em 1; se este registro de status pertencer a uma coluna de marcadores, o campo pode ser zero. Os números dos parâmetros começam em 1. Ele tem o valor SQL_NO_COLUMN_NUMBER se o registro de status não estiver associado a um número de coluna ou número de parâmetro. Se o driver não puder determinar o número da coluna ou o número do parâmetro ao qual este registro está associado, este campo tem o valor SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> O conteúdo deste campo é definido apenas para alças de declaração.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Uma seqüência que indica o nome da conexão com a qual o registro de diagnóstico se relaciona. Este campo é definido pelo driver. Para estruturas de dados diagnósticos associadas à alça do ambiente e para diagnósticos que não se relacionam com nenhuma conexão, este campo é uma seqüência de comprimento zero.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Uma mensagem informacional sobre o erro ou aviso. Este campo é formatado conforme descrito em [Mensagens de Diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md). Não há comprimento máximo para o texto da mensagem de diagnóstico.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Um código de erro nativo específico do driver/data source. Se não houver um código de erro nativo, o driver retorna 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Este campo contém o número da linha no conjunto de linhas ou o número de parâmetro no conjunto de parâmetros, com o qual o registro de status está associado. Números de linha e números de parâmetros começam com 1. Este campo tem o valor SQL_NO_ROW_NUMBER se esse registro de status não estiver associado a um número de linha ou número de parâmetro. Se o driver não puder determinar o número da linha ou o número do parâmetro ao qual este registro está associado, este campo tem o valor SQL_ROW_NUMBER_UNKNOWN.<br /><br /> O conteúdo deste campo é definido apenas para alças de declaração.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Uma seqüência que indica o nome do servidor a que o registro de diagnóstico se relaciona. É o mesmo que o valor retornado para uma chamada para **SQLGetInfo** com a opção SQL_DATA_SOURCE_NAME. Para estruturas de dados de diagnóstico associadas à alça do ambiente e para diagnósticos que não se relacionam com nenhum servidor, este campo é uma seqüência de comprimento zero.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Um código de diagnóstico SQLSTATE de cinco caracteres. Para obter mais informações, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Uma seqüência com o mesmo formato e valores válidos SQL_DIAG_CLASS_ORIGIN, que identifica a parte definidora da parte de subclasse do código SQLSTATE. Os SQLSTATES específicos da ODBC para os quais "ODBC 3.0" é devolvido incluem o seguinte:<br /><br /> 01s00, 01S01, 01S02, 01s06, 01s07, 07S01, 08S01, 21s01, 21s02, 25s01, 25S02, 25s03, 42S01, 42s02, 42s11, 42s12, 42s21, 42s22, HY095, HY097, HY098, HY0999, HY0999, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002 iM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valores dos Campos de Função Dinâmica  
 A tabela a seguir descreve os valores de SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE que se aplicam a cada tipo de declaração SQL executada por uma chamada para **SQLExecute** ou **SQLExecDirect**. O driver pode adicionar valores definidos pelo driver aos listados.  
  
|Instrução SQL<br /><br /> Executado|Valor de <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valor de <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domínio-declaração*|"ALTER DOMAIN"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-tabela-declaração*|"TABELA ALTER"|SQL_DIAG_ALTER_TABLE|  
|*definição de afirmação*|"CRIAR AFIRMAÇÃO"|SQL_DIAG_CREATE_ASSERTION|  
|*definição de configuração de caracteres*|"CRIAR CONJUNTO DE CARACTERES"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*colagem-definição*|"CRIAR COLAGEM"|SQL_DIAG_CREATE_COLLATION|  
|*definição de domainn*|"CRIAR DOMÍNIO"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-statement*|"CRIAR ÍNDICE"|SQL_DIAG_CREATE_INDEX|  
|*criar-tabela-declaração*|"CRIAR TABELA"|SQL_DIAG_CREATE_TABLE|  
|*criação-exibição-declaração*|"CRIAR VISÃO"|SQL_DIAG_CREATE_VIEW|  
|*especificação cursor*|"SELECIONAR CURSOR"|SQL_DIAG_SELECT_CURSOR|  
|*exclusão-declaração posicionada*|"CURSOR DE EXCLUSÃO DINÂMICA"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*exclusão-declaração pesquisada*|"DELETE ONDE"|SQL_DIAG_DELETE_WHERE|  
|*drop-assertion-statement*|"DROP ASSERTION"|SQL_DIAG_DROP_ASSERTION|  
|*drop-personagem-set-stmt*|"DROP CHARACTER SET"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation-statement*|"DROP COLLATION"|SQL_DIAG_DROP_COLLATION|  
|*drop-domain-statement*|"DOMÍNIO DE QUEDA"|SQL_DIAG_DROP_DOMAIN|  
|*queda de índice-declaração*|"ÍNDICE DE QUEDA"|SQL_DIAG_DROP_INDEX|  
|*drop-schema-statement*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-statement*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop-tradução-declaração*|"DROP TRANSLATION"|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-statement*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
|*Grantstatement*|"GRANT"|SQL_DIAG_GRANT|
|*inserir-instrução*|"INSERIR"|SQL_DIAG_INSERT|  
|*ODBC-procedure-extension*|"CALL"|chamada de SQL_DIAG_|  
|*revogar-declaração*|"REVOGAR"|SQL_DIAG_REVOKE|  
|*esquema-definição*|"CRIAR ESQUEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*tradução-definição*|"CRIAR TRADUÇÃO"|SQL_DIAG_CREATE_TRANSLATION|  
|*atualização-declaração posicionada*|"CURSOR DE ATUALIZAÇÃO DINÂMICA"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*atualização-declaração pesquisada*|"ATUALIZAR ONDE"|SQL_DIAG_UPDATE_WHERE|  
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

 Os registros de status são posicionados em uma seqüência com base no número da linha e no tipo de diagnóstico. O Driver Manager determina a ordem final para retornar os registros de status que ele gera. O driver determina a ordem final para retornar os registros de status que ele gera.  
  
 Se os registros de diagnóstico forem publicados pelo Driver Manager e pelo motorista, o Driver Manager é responsável por encomendá-los.  
  
 Se houver dois ou mais registros de status, a seqüência dos registros é determinada primeiro por número de linha. As seguintes regras aplicam-se à determinação da seqüência de registros diagnósticos por linha:  
  
-   Registros que não correspondem a nenhuma linha aparecem na frente de registros que correspondem a uma linha específica, porque SQL_NO_ROW_NUMBER é definida como -1.  
  
-   Registros para os quais o número da linha é desconhecido aparecem na frente de todos os outros registros, porque SQL_ROW_NUMBER_UNKNOWN é definido como -2.  
  
-   Para todos os registros relativos a linhas específicas, os registros são classificados pelo valor no campo SQL_DIAG_ROW_NUMBER. Todos os erros e avisos da primeira linha afetada estão listados e, em seguida, todos os erros e avisos da próxima linha afetada, e assim por diante.  
  
> [!NOTE]
>  O ODBC 3 *.x* Driver Manager não solicitará registros de status na fila de diagnóstico se o SQLSTATE 01S01 (Erro em linha) for devolvido por um driver ODBC*2.x* ou se o SQLSTATE 01S01 (Erro na linha) for retornado por um driver ODBC*3.x* quando **o SQLExtendedFetch** for chamado ou **o SQLSetPos** for chamado em um cursor que tenha sido posicionado com **SQLExtendedFetch**  
  
 Dentro de cada linha, ou para todos aqueles registros que não correspondem a uma linha ou para o qual o número da linha é desconhecido, ou para todos aqueles registros com um número de linha igual a SQL_NO_ROW_NUMBER, o primeiro registro listado é determinado usando um conjunto de regras de classificação. Após o primeiro registro, a ordem dos outros registros que afetam uma linha é indefinida. Um aplicativo não pode assumir que erros precedem avisos após o primeiro registro. Os aplicativos devem escanear a estrutura completa de dados de diagnóstico para obter informações completas sobre uma chamada mal sucedida para uma função.  
  
 As seguintes regras são usadas para determinar o primeiro registro dentro de uma linha. O recorde com o posto mais alto é o primeiro recorde. A fonte de um registro (Driver Manager, driver, gateway, e assim por diante) não é considerada quando os registros de classificação.  
  
-   **Erros** Registros de status que descrevem erros têm a classificação mais alta. As seguintes regras são aplicadas aos erros de classificação:  
  
    -   Registros que indicam uma falha de transação ou possível falha de transação superam todos os outros registros.  
  
    -   Se dois ou mais registros descreverem a mesma condição de erro, os SQLSTATEs definidos pela especificação CLI do Grupo Aberto (classes 03 a HZ) superam os SQLSTATEs definidos pelo ODBC e pelo driver.  
  
-   **Sem valores de dados definidos pela implementação** Os registros de status que descrevem os valores sem dados definidos pelo driver (classe 02) têm a segunda classificação mais alta.  
  
-   **Avisos** Os registros de status que descrevem avisos (classe 01) têm a classificação mais baixa. Se dois ou mais registros descreverem a mesma condição de aviso, então o aviso SQLSTATEs definido pela especificação CLI do Grupo Aberto supera os SQLSTATEs definidos pelo ODBC e definidos pelo driver.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtenção de múltiplos campos de uma estrutura de dados diagnósticos|[Função SQLGetDiagRec](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
