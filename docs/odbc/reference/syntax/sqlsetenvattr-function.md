---
title: Função SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299536"
---
# <a name="sqlsetenvattr-function"></a>Função SQLSetEnvAttr
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLSetEnvAttr** define atributos que regem aspectos dos ambientes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Alça do meio ambiente.  
  
 *Atributo*  
 [Entrada] Atributo ao conjunto, listado em "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado com *Atributo*. Dependendo do valor de *Atributo,* *ValuePtr* será um valor inteiro de 32 bits ou apontará para uma seqüência de caracteres com término nulo.  
  
 *Stringlength*  
 [Entrada] Se *ValuePtr* aponta para uma seqüência de caracteres ou um buffer binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de seqüência de caracteres, este argumento deve conter o número de bytes na seqüência de caracteres.  
  
 Se *ValuePtr* for um inteiro, *StringLength* será ignorado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetEnvAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_ENV e uma *alça* de *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetEnvAttr** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário. Se um driver não suportar um atributo de ambiente, o erro só poderá ser retornado durante o tempo de conexão.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não suportava o valor especificado no *ValuePtr* e substituiu um valor semelhante. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY009|Uso inválido do ponteiro nulo|O argumento Atributo identificou um atributo de ambiente que exigia um valor de seqüência de strings, e o argumento *ValuePtr* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma alça de conexão foi alocada no *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** não foi definido com **SQLSetEnvAttr** e *Atributo* não é igual a **SQL_ATTR_ODBC_VERSION**. Você não precisa definir **SQL_ATTR_ODBC_VERSION** explicitamente se estiver usando **SQLAllocHandleStd**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY024|Valor do atributo inválido|Dado o valor *atributo* especificado, um valor inválido foi especificado no *ValuePtr*.|  
|HY090|Comprimento de seqüência ou buffer inválido|O argumento *StringLength* era menor que 0, mas não foi SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) O valor especificado para o *atributo argumental* não era válido para a versão do ODBC suportada pelo driver.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o *atributo argumental* era um atributo de ambiente ODBC válido para a versão do ODBC suportado pelo driver, mas não foi suportado pelo driver.<br /><br /> (DM) O argumento *do Atributo* foi SQL_ATTR_OUTPUT_NTS, e *o ValuePtr* foi SQL_FALSE.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo só pode chamar **SQLSetEnvAttr** se nenhuma alça de conexão for alocada no ambiente. Todos os atributos do ambiente definidos com sucesso pelo aplicativo para o ambiente persistem até **que o SQLFreeHandle** seja chamado ao ambiente. Mais de uma alça de ambiente pode ser alocada simultaneamente em ODBC *3.x*.  
  
 O formato das informações definidas através *do ValuePtr* depende do *Atributo*especificado . **O SQLSetEnvAttr** aceitará informações de atributos em um dos dois formatos diferentes: uma seqüência de caracteres com término nulo ou um valor inteiro de 32 bits. O formato de cada um é anotado na descrição do atributo.  
  
 Não há atributos de ambiente específicos para o motorista.  
  
 Os atributos de conexão não podem ser definidos por uma chamada para **SQLSetEnvAttr**. Tentar fazer isso retornará SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
|*Atributo*|*Conteúdo ValuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Um valor SQLUINTEGER de 32 bits que permite ou desativa o pool de conexões no nível do ambiente. Os seguintes valores são utilizados:<br /><br /> SQL_CP_OFF = O pooling de conexão está desligado. Esse é o padrão.<br /><br /> SQL_CP_ONE_PER_DRIVER = Um único pool de conexão é suportado para cada driver. Cada conexão em uma piscina está associada a um driver.<br /><br /> SQL_CP_ONE_PER_HENV = Um único pool de conexão é suportado para cada ambiente. Cada conexão em uma piscina está associada a um ambiente.<br /><br /> SQL_CP_DRIVER_AWARE = Use o recurso de conscientização do driver, se estiver disponível. Se o driver não suportar a conscientização do pool de conexões, SQL_CP_DRIVER_AWARE é ignorada e SQL_CP_ONE_PER_HENV é usada. Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). Em um ambiente onde alguns motoristas apoiam e alguns drivers não suportam a conscientização do pool de conexões, SQL_CP_DRIVER_AWARE podem habilitar o recurso de conscientização do pool de conexões nos drivers de suporte, mas é equivalente à configuração para SQL_CP_ONE_PER_HENV sobre os drivers que não suportam o recurso de conscientização do pool de conexão.<br /><br /> O pool de conexões é habilitado ligando para **SQLSetEnvAttr** para definir o atributo SQL_ATTR_CONNECTION_POOLING para SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. Essa chamada deve ser feita antes que o aplicativo aloque o ambiente compartilhado para o qual o pool de conexões deve ser ativado. O cabo de ambiente na chamada para **SQLSetEnvAttr** está definido como nulo, o que torna SQL_ATTR_CONNECTION_POOLING um atributo de nível de processo. Depois que o pool de conexões é ativado, o aplicativo então aloca um ambiente compartilhado implícito ligando para **SQLAllocHandle** com o argumento *InputHandle* definido para SQL_HANDLE_ENV.<br /><br /> Depois que o pool de conexões foi ativado e um ambiente compartilhado foi selecionado para um aplicativo, SQL_ATTR_CONNECTION_POOLING não pode ser redefinido para esse ambiente, porque **o SQLSetEnvAttr** é chamado com uma alça de ambiente nulo ao definir esse atributo. Se esse atributo for definido enquanto o pool de conexões já estiver ativado em um ambiente compartilhado, o atributo afetará apenas ambientes compartilhados que são alocados posteriormente.<br /><br /> Também é possível habilitar o pool de conexões em um ambiente. Observe o seguinte sobre o pool de conexões do ambiente:<br /><br /> - Ativar o agrupamento de conexões em uma alça NULL é um atributo de nível de processo. Posteriormente, os ambientes alocados serão um ambiente compartilhado e herdarão a configuração de pooling de conexão em nível de processo.<br />- Depois que um ambiente é alocado, um aplicativo ainda pode alterar a configuração do pool de conexões.<br />- Se o pool de conexão do ambiente estiver ativado e o motorista usar o pool de drivering, o pool de ambientes tem preferência.<br /><br /> SQL_ATTR_CONNECTION_POOLING é implementado dentro do Driver Manager. Um motorista não precisa implementar SQL_ATTR_CONNECTION_POOLING. Os aplicativos ODBC 2.0 e 3.0 podem definir esse atributo de ambiente.<br /><br /> Para obter mais informações, consulte [ODBC Connection Pooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Um valor SQLUINTEGER de 32 bits que determina como uma conexão é escolhida a partir de um pool de conexões. Quando **o SQLConnect** ou **o SQLDriverConnect** são chamados, o Gerenciador de driver determina qual conexão é reutilizada a partir do pool. O Gerenciador de drivertenta tentativas de igualar as opções de conexão na chamada e os atributos de conexão definidos pelo aplicativo com as palavras-chave e atributos de conexão das conexões no pool. O valor deste atributo determina o nível de precisão dos critérios de correspondência.<br /><br /> Os seguintes valores são usados para definir o valor deste atributo:<br /><br /> SQL_CP_STRICT_MATCH = Somente as conexões que correspondem exatamente às opções de conexão na chamada e os atributos de conexão definidos pelo aplicativo são reutilizados. Esse é o padrão.<br /><br /> SQL_CP_RELAXED_MATCH = Podem ser usadas conexões com palavras-chave de cadeia de conexão correspondentes. As palavras-chave devem coincidir, mas nem todos os atributos de conexão devem coincidir.<br /><br /> Para obter mais informações sobre como o Driver Manager executa a partida ao conectar-se a uma conexão em pool, consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Para obter mais informações sobre pooling de conexões, consulte [Pooling de conexão ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Um inteiro de 32 bits que determina se determinada funcionalidade exibe o comportamento oDBC *2.x* ou o comportamento ODBC *3.x.* Os seguintes valores são usados para definir o valor deste atributo:<br /><br /> SQL_OV_ODBC3_80 = O Driver Manager e o driver apresentam o seguinte comportamento ODBC 3.8:<br /><br /> - O motorista retorna e espera códigos ODBC *3.x* para data, hora e carimbo de data.<br />- O driver retorna códigos ODBC *3.x* SQLSTATE quando **SQLError,** **SQLGetDiagField**ou **SQLGetDiagRec** são chamados.<br />- O argumento *CatalogName* em uma chamada para **SQLTables** aceita um padrão de pesquisa.<br />- O Driver Manager suporta extensibilidade do tipo de dados C. Para obter mais informações sobre extensibilidade do tipo de dados C, consulte [C Data Types in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Para obter mais informações, consulte [o que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3 = O Driver Manager e o driver exibem o seguinte comportamento ODBC *3.x:*<br /><br /> - O motorista retorna e espera códigos ODBC *3.x* para data, hora e carimbo de data.<br />- O driver retorna códigos ODBC *3.x* SQLSTATE quando **SQLError,** **SQLGetDiagField**ou **SQLGetDiagRec** são chamados.<br />- O argumento *CatalogName* em uma chamada para **SQLTables** aceita um padrão de pesquisa.<br />- O Driver Manager não suporta extensibilidade do tipo de dados C.<br /><br /> SQL_OV_ODBC2 = O Driver Manager e o driver exibem o seguinte comportamento ODBC *2.x.* Isso é especialmente útil para um aplicativo ODBC *2.x* que trabalha com um driver ODBC *3.x.*<br /><br /> - O motorista retorna e espera códigos ODBC *2.x* para data, hora e carimbo de data.<br />- O driver retorna códigos ODBC *2.x* SQLSTATE quando **SQLError,** **SQLGetDiagField**ou **SQLGetDiagRec** são chamados.<br />- O argumento *CatalogName* em uma chamada para **SQLTables** não aceita um padrão de pesquisa.<br />- O Driver Manager não suporta extensibilidade do tipo de dados C.<br /><br /> Um aplicativo deve definir esse atributo de ambiente antes de chamar qualquer função que tenha um argumento SQLHENV, ou a chamada retornará SQLSTATE HY010 (erro de seqüência de função). É específico para o motorista se existe um comportamento adicional para essas bandeiras ambientais.<br /><br /> - Para obter mais informações, consulte [Declarando a versão oDBC do aplicativo](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Um inteiro de 32 bits que determina como o driver retorna os dados da seqüência. Se SQL_TRUE, o driver retorna dados de seqüência nulos. Se SQL_FALSE, o driver não retorna dados de seqüência sem nulo.<br /><br /> Esse atributo é padrão para SQL_TRUE. Uma chamada para **SQLSetEnvAttr** para defini-lo para SQL_TRUE retorna SQL_SUCCESS. Uma chamada para **SQLSetEnvAttr** para defini-lo para SQL_FALSE retorna SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado).|  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando uma alça|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de ambiente|[Função SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
