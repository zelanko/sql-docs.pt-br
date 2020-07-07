---
title: Transferência de Dados de parâmetros com valor de tabela
description: Descrever Transferência de Dados de parâmetros com valor de tabela
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: native-client
ms.topic: reference
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 07/01/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0be2ffbfb7160d5be8f5ebb2a2ed688103a54b4d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004618"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>Associação e transferência de dados de parâmetros com valor de tabela e valores de coluna

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Os parâmetros com valor de tabela (TVP), como outros parâmetros, devem ser associados antes de serem passados para o servidor. O aplicativo associa parâmetros com valor de tabela da mesma forma que associa outros parâmetros: usando SQLBindParameter ou chamadas equivalentes a SQLSetDescField ou SQLSetDescRec. O tipo de dados do servidor para um parâmetro com valor de tabela é SQL_SS_TABLE. O tipo C pode ser especificado como SQL_C_DEFAULT ou SQL_C_BINARY.  

No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior, só existe suporte para parâmetros com valor de tabela de entrada. Portanto, qualquer tentativa de definir SQL_DESC_PARAMETER_TYPE com um valor diferente de SQL_PARAM_INPUT retorna SQL_ERROR com SQLSTATE = HY105 e a mensagem "tipo de parâmetro inválido".  

Valores padrão podem ser atribuídos a colunas inteiras de parâmetros com valor de tabela usando o atributo SQL_CA_SS_COL_HAS_DEFAULT_VALUE. Os valores de coluna de parâmetro com valor de tabela individual, no entanto, não podem ser atribuídos a valores padrão usando SQL_DEFAULT_PARAM em *StrLen_or_IndPtr* com SQLBindParameter. Os parâmetros com valor de tabela como um todo não podem ser definidos como um valor padrão usando SQL_DEFAULT_PARAM em *StrLen_or_IndPtr* com SQLBindParameter. Se essas regras não forem seguidas, SQLExecute ou SQLExecDirect retornarão SQL_ERROR. Um registro de diagnóstico é gerado com SQLSTATE = 07S01 e a mensagem "uso inválido do parâmetro padrão para \<p> o parâmetro", em que \<p> é o ORDINAL do TVP na instrução de consulta.  

> [!Note]
> Os parâmetros com valor de tabela não têm um valor padrão que possa ser definido, pois SQL_DEFAULT_PARAM indica que não há linhas. Portanto, se não houver linhas, não haverá nenhuma coluna a ser associada.

Depois de associar o parâmetro com valor de tabela, o aplicativo deverá, então, associar cada coluna de parâmetros com valor de tabela. Para fazer isso, o aplicativo primeiro chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS para o ordinal de um parâmetro com valor de tabela. O aplicativo associa as colunas do parâmetro com valor de tabela por meio de chamadas para as seguintes rotinas: SQLBindParameter, SQLSetDescRec e SQLSetDescField. A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o efeito usual de SQLBindParameter, SQLSetDescRec e SQLSetDescField em operando em parâmetros de nível superior regulares.

> [!Note]
> Para os drivers ODBC do Linux e do Mac com unixODBC 2.3.1 para 2.3.4, ao definir o nome do TVP por meio de SQLSetDescField com o campo descritor de SQL_CA_SS_TYPE_NAME, unixODBC não converte automaticamente entre cadeias de caracteres ANSI e Unicode, dependendo da função exata chamada (SQLSetDescFieldA/SQLSetDescFieldW). É necessário sempre usar SQLBindParameter ou SQLSetDescFieldW com uma cadeia de caracteres Unicode (UTF-16) para definir o nome do TVP.

Nenhum dado real é enviado ou recebido para o próprio parâmetro com valor de tabela, mas dados são enviados e recebidos para cada uma de suas colunas constituintes. Como o parâmetro com valor de tabela é uma pseudo coluna, os parâmetros de SQLBindParameter referem-se a diferentes atributos do que outros tipos de dados, da seguinte maneira:  

| Parâmetro | Atributo relacionado para tipos de parâmetro não com valor de tabela, incluindo colunas | Atributo relacionado para parâmetros com valor de tabela |
|-----------|---------------------------------------------------------------------------|-----------------------------------------------|
|*InputOutputType*|SQL_DESC_PARAMETER_TYPE em IPD.<br /><br /> Para colunas de parâmetros com valor de tabela, isso deve ser igual à configuração do próprio parâmetro com valor de tabela.|SQL_DESC_PARAMETER_TYPE em IPD.<br /><br /> Isso deve ser SQL_PARAM_INPUT.|  
|*ValueType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em APD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em APD.<br /><br /> Isso deve ser SQL_C_DEFAULT ou SQL_C_BINARY.|  
|*ParameterType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em IPD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em IPD.<br /><br /> Isso deve ser SQL_SS_TABLE.|  
|*ColumnSize*|SQL_DESC_LENGTH ou SQL_DESC_PRECISION em IPD.<br /><br /> Isso depende do valor de *ParameterType*.|SQL_DESC_ARRAY_SIZE<br /><br /> Também poderá ser definido usando SQL_ATTR_PARAM_SET_SIZE quando o foco do parâmetro for definido como o parâmetro com valor de tabela.<br /><br /> Para um parâmetro com valor de tabela, esse é o número de linhas nos buffers de colunas de parâmetros com valor de tabela.|  
|*DecimalDigits*|SQL_DESC_PRECISION ou SQL_DESC_SCALE em IPD.|Não utilizado. Isso deve ser 0.<br /><br /> Se esse parâmetro não for 0, SQLBindParameter retornará SQL_ERROR e um registro de diagnóstico será gerado com SQLSTATE = HY104 e a mensagem "precisão ou escala inválida".|  
|*ParameterValuePtr*|SQL_DESC_DATA_PTR em APD.|SQL_CA_SS_TYPE_NAME.<br /><br /> Isso é opcional para chamadas de procedimento armazenado e NULL pode ser especificado se não for necessário. Ele deve ser especificado para instruções SQL que não são chamadas de procedimento.<br /><br /> Esse parâmetro também funciona como um valor exclusivo que o aplicativo poderá usar para identificar esse parâmetro com valor de tabela quando a associação de linha variável for usada. Para obter mais informações, consulte a seção "Associação de linha variável de parâmetros com valor de tabela", mais adiante neste tópico.<br /><br /> Quando um nome de tipo de parâmetro com valor de tabela é especificado em uma chamada para SQLBindParameter, ele deve ser especificado como um valor Unicode, mesmo em aplicativos criados como aplicativos ANSI. O valor usado para o parâmetro *StrLen_or_IndPtr* deve ser SQL_NTS ou o comprimento da cadeia de caracteres do nome multiplicado pelo tamanho (WCHAR).|  
|*BufferLength*|SQL_DESC_OCTET_LENGTH em APD.|O comprimento do nome do tipo de parâmetro com valor de tabela em bytes.<br /><br /> Isso pode ser SQL_NTS se o nome do tipo for terminada em nulo ou 0 se o nome do tipo de parâmetro com valor de tabela não for necessário.|  
|*StrLen_or_IndPtr*|SQL_DESC_OCTET_LENGTH_PTR em APD.|SQL_DESC_OCTET_LENGTH_PTR em APD.<br /><br /> Para parâmetros com valor de tabela, essa é uma contagem de linhas e não um comprimento de dados.|  
||||

Existe suporte para dois modos de transferência de dados para parâmetros com valor de tabela: associação de linha fixa e associação de linha variável.  

## <a name="fixed-table-valued-parameter-row-binding"></a>Associação de linha fixa de parâmetros com valor de tabela

Para associação de linha fixa, um aplicativo aloca buffers (ou matrizes de buffers) grandes o bastante para todos os possíveis valores de coluna de entrada. O aplicativo faz o seguinte:  

1. Associa todos os parâmetros usando chamadas SQLBindParameter, SQLSetDescRec ou SQLSetDescField.  

    1. Define SQL_DESC_ARRAY_SIZE como o número máximo de linhas que podem ser transferidas para cada parâmetro com valor de tabela. Isso pode ser feito na chamada SQLBindParameter.  

2. Chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS para o ordinal de cada parâmetro com valor de tabela.  

    1. Para cada parâmetro com valor de tabela, o associa colunas de parâmetro com valor de tabela usando chamadas SQLBindParameter, SQLSetDescRec ou SQLSetDescField.  

    2. Para cada coluna de parâmetro com valor de tabela que deve ter valores padrão, chama SQLSetDescField para definir SQL_CA_SS_COL_HAS_DEFAULT_VALUE como 1.  

3. Chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS como 0. Isso deve ser feito antes de SQLExecute ou SQLExecDirect ser chamado. Caso contrário, SQL_ERROR é retornado e um registro de diagnóstico é gerado com SQLSTATE = HY024 e a mensagem "valor de atributo inválido, SQL_SOPT_SS_PARAM_FOCUS (deve ser zero em tempo de execução)."  

4. Define *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR como SQL_DEFAULT_PARAM para um parâmetro com valor de tabela sem linhas ou o número de linhas a serem transferidas na próxima chamada de SQLExecute ou SQLExecDirect se o parâmetro com valor de tabela tiver linhas. Não é possível definir *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR como SQL_NULL_DATA para um parâmetro com valor de tabela, pois os parâmetros com valor de tabela não permitem valor nulo (embora colunas constituintes de parâmetro com valor de tabela possam ser anuláveis). Se isso for definido como um valor inválido, SQLExecute ou SQLExecDirect retornará SQL_ERROR, e um registro de diagnóstico será gerado com SQLSTATE = HY090 e a mensagem "cadeia de caracteres ou comprimento de buffer inválido para o parâmetro \<p> ", em que p é o número do parâmetro.

5. Chama SQLExecute ou SQLExecDirect.

    Os valores de coluna de parâmetro com valor de tabela de entrada podem ser passados em partes se *StrLen_or_IndPtr* estiver definido como SQL_LEN_DATA_AT_EXEC (*comprimento*) ou SQL_DATA_AT_EXEC para a coluna. Isso é semelhante a passar valores em partes quando são usadas matrizes de parâmetros. Assim como ocorre com todos os parâmetros de dados em execução, SQLParamData não indica a linha da matriz para a qual o driver está solicitando dados; o aplicativo deve cuidar disso. O aplicativo não pode fazer suposições sobre a ordem em que o driver solicita valores.  

## <a name="variable-table-valued-parameter-row-binding"></a>Associação de linha variável de parâmetros com valor de tabela  

Para associação de linha variável, as linhas são transferidas em lotes em tempo de execução e o aplicativo passa linhas para o driver sob demanda. Isso é semelhante a dados em execução para valores de parâmetros individuais. Para associação de linha variável, o aplicativo faz o seguinte:  

1. Associa parâmetros e colunas de parâmetro com valor de tabela, conforme descrito nas etapas 1 a 3 da seção anterior, "Associação de linha de parâmetro com valor de tabela fixa".  

2. Define *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR para que os parâmetros com valor de tabela sejam passados no momento da execução para SQL_DATA_AT_EXEC. Se nenhum for definido, o parâmetro será processado conforme descrito na seção anterior.  

3. Chama SQLExecute ou SQLExecDirect. Isso retornará SQL_NEED_DATA se houver qualquer SQL_PARAM_INPUT ou SQL_PARAM_INPUT_OUTPUT parâmetros a serem tratados como parâmetros de dados em execução. Nesse caso, o aplicativo faz o seguinte:  

    - Chama SQLParamData. Isso retorna o valor de *ParameterValuePtr* para um parâmetro de dados em execução e um código de retorno de SQL_NEED_DATA. Quando todos os dados de parâmetro forem passados para o driver, SQLParamData retornará SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Para parâmetros de dados em execução, *ParameterValuePtr*, que é o mesmo que o campo de descritor SQL_DESC_DATA_PTR, pode ser considerado um token para identificar um parâmetro para o qual um valor é necessário exclusivamente. Esse "token" é passado do aplicativo para o driver em tempo de associação e, depois, devolvido ao aplicativo em tempo de execução.  
  
4. Para enviar dados de linha de parâmetro com valor de tabela para parâmetros nulos com valor de tabela, se o parâmetro com valor de tabela não tiver linhas, um aplicativo chamará SQLPutData com *StrLen_or_Ind* definido como SQL_DEFAULT_PARAM.  

    Para TVPs não nulos, um aplicativo:

    - Define *Str_Len_or_Ind* para todas as colunas de parâmetro com valor de tabela para valores apropriados e popula buffers de dados para colunas de parâmetro com valor de tabela que não sejam parâmetros de dados em execução. Você pode usar dados em execução para colunas de parâmetros com valor de tabela de forma semelhante ao modo como parâmetros comuns podem ser passados para o driver em partes.  

    - Chama SQLPutData com *Str_Len_or_Ind* definido como o número de linhas a serem enviadas ao servidor. Qualquer valor fora do intervalo de 0 a SQL_DESC_ARRAY_SIZE ou SQL_DEFAULT_PARAM é um erro e retorna SQLSTATE HY090, com a mensagem "comprimento de buffer ou cadeia de caracteres inválido". 0 indica que todas as linhas foram enviadas e não há mais dados para um parâmetro com valor de tabela (conforme observado no segundo item de marcador nesta lista). SQL_DEFAULT_PARAM poderá ser usado apenas na primeira vez em que o driver solicitar dados para um parâmetro com valor de tabela (como descrito no primeiro item de marcador desta lista).  

5. Quando todas as linhas forem enviadas, chama SQLPutData para o parâmetro com valor de tabela com um valor *Str_Len_or_Ind* de 0 e, em seguida, vá para a etapa 3a acima.  

6. Chama SQLParamData novamente. Se houver parâmetros de dados em execução entre as colunas de parâmetro com valor de tabela, eles serão identificados pelo valor *ValuePtrPtr* retornado por SQLParamData. Quando todos os valores de coluna estiverem disponíveis, SQLParamData retornará o valor de *ParameterValuePtr* para o parâmetro com valor de tabela e o aplicativo começará novamente.  

## <a name="next-steps"></a>Próximas etapas

[Parâmetros com valor de tabela ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)