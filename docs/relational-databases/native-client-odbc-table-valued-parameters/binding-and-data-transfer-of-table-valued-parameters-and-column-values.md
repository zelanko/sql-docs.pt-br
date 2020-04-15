---
title: Transferência de dados de parâmetros avaliados em tabela
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b7eecfdac3d42b7a3d8d66ffe1f8ac68652230f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304490"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>Associação e transferência de dados de parâmetros com valor de tabela e valores de coluna
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Parâmetros com valor de tabela, como outros parâmetros, devem ser associados antes de serem passados para o servidor. O aplicativo vincula parâmetros de valor de tabela da mesma forma que vincula outros parâmetros: usando SQLBindParameter ou chamadas equivalentes para SQLSetDescField ou SQLSetDescRec. O tipo de dados do servidor para um parâmetro com valor de tabela é SQL_SS_TABLE. O tipo C pode ser especificado como SQL_C_DEFAULT ou SQL_C_BINARY.  
  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior, só existe suporte para parâmetros com valor de tabela de entrada. Portanto, qualquer tentativa de definir SQL_DESC_PARAMETER_TYPE como um valor diferente de SQL_PARAM_INPUT retornará SQL_ERROR com SQLSTATE = HY105 e a mensagem "Tipo de parâmetro inválido".  
  
 Valores padrão podem ser atribuídos a colunas inteiras de parâmetros com valor de tabela usando o atributo SQL_CA_SS_COL_HAS_DEFAULT_VALUE. Os valores individuais da coluna de parâmetros avaliados em tabela, no entanto, não podem ser atribuídos valores padrão usando SQL_DEFAULT_PARAM em *StrLen_or_IndPtr* com SQLBindParameter. Os parâmetros avaliados em tabela como um todo não podem ser definidos como um valor padrão usando SQL_DEFAULT_PARAM em *StrLen_or_IndPtr* com o SQLBindParameter. Se essas regras não forem seguidas, o SQLExecute ou o SQLExecDirect retornarão SQL_ERROR. Um registro de diagnóstico será gerado com SQLSTATE=07S01 e a mensagem \<"Uso \<inválido do parâmetro padrão para parâmetro p>", onde p> é a ordinal do TVP na declaração de consulta.  
  
 Depois de associar o parâmetro com valor de tabela, o aplicativo deverá, então, associar cada coluna de parâmetros com valor de tabela. Para fazer isso, o aplicativo primeiro chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS à ordinal de um parâmetro de valor de tabela. Em seguida, o aplicativo vincula as colunas do parâmetro avaliado em tabela por chamadas às seguintes rotinas: SQLBindParameter, SQLSetDescRec e SQLSetDescField. A configuração SQL_SOPT_SS_PARAM_FOCUS a 0 restaura o efeito usual do SQLBindParameter, SQLSetDescRec e SQLSetDescField em operação em parâmetros regulares de nível superior.
 
 Nota: para os drivers Linux e Mac ODBC com unixODBC 2.3.1 a 2.3.4, ao definir o nome TVP através de SQLSetDescField com o campo descritor SQL_CA_SS_TYPE_NAME, o unixODBC não converte automaticamente entre as strings ANSI e Unicode dependendo da função exata chamada (SQLSetDescFieldA / SQLSetDescFieldW). É necessário usar sempre SQLBindParameter ou SQLSetDescFieldW com uma seqüência Unicode (UTF-16) para definir o nome TVP.
  
 Nenhum dado real é enviado ou recebido para o próprio parâmetro com valor de tabela, mas dados são enviados e recebidos para cada uma de suas colunas constituintes. Como o parâmetro de valor de tabela é uma pseudo coluna, os parâmetros para SQLBindParameter são usados para se referir a atributos diferentes de outros tipos de dados, da seguinte forma:  
  
|Parâmetro|Atributo relacionado para tipos de parâmetros não avaliados em tabela, incluindo colunas|Atributo relacionado para parâmetros com valor de tabela|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|SQL_DESC_PARAMETER_TYPE em IPD.<br /><br /> Para colunas de parâmetros com valor de tabela, isso deve ser igual à configuração do próprio parâmetro com valor de tabela.|SQL_DESC_PARAMETER_TYPE em IPD.<br /><br /> Isso deve ser SQL_PARAM_INPUT.|  
|*Valuetype*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em APD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em APD.<br /><br /> Isso deve ser SQL_C_DEFAULT ou SQL_C_BINARY.|  
|*Parametertype*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em IPD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em IPD.<br /><br /> Isso deve ser SQL_SS_TABLE.|  
|*ColumnSize*|SQL_DESC_LENGTH ou SQL_DESC_PRECISION em IPD.<br /><br /> Isso depende do valor de *ParameterType*.|SQL_DESC_ARRAY_SIZE<br /><br /> Também poderá ser definido usando SQL_ATTR_PARAM_SET_SIZE quando o foco do parâmetro for definido como o parâmetro com valor de tabela.<br /><br /> Para um parâmetro com valor de tabela, esse é o número de linhas nos buffers de colunas de parâmetros com valor de tabela.|  
|*DecimalDigits*|SQL_DESC_PRECISION ou SQL_DESC_SCALE em IPD.|Não utilizado. Isso deve ser 0.<br /><br /> Se este parâmetro não for 0, o SQLBindParameter retornará SQL_ERROR e um registro de diagnóstico será gerado com SQLSTATE= HY104 e a mensagem "Precisão ou escala inválida".|  
|*ParâmetroValuePtr*|SQL_DESC_DATA_PTR em APD.|SQL_CA_SS_TYPE_NAME.<br /><br /> Isso é opcional para chamadas de procedimento armazenado e NULL poderá ser especificado se ele não for necessário. Deve ser especificado para instruções SQL que não são chamadas de procedimento.<br /><br /> Esse parâmetro também funciona como um valor exclusivo que o aplicativo poderá usar para identificar esse parâmetro com valor de tabela quando a associação de linha variável for usada. Para obter mais informações, consulte a seção "Associação de linha variável de parâmetros com valor de tabela", mais adiante neste tópico.<br /><br /> Quando um nome de tipo de parâmetro de valor de tabela é especificado em uma chamada para SQLBindParameter, ele deve ser especificado como um valor Unicode, mesmo em aplicativos que são construídos como aplicativos ANSI. O valor utilizado para o parâmetro *StrLen_or_IndPtr* deve ser SQL_NTS ou o comprimento da seqüência do nome multiplicado pelo tamanho (WCHAR).|  
|*BufferLength*|SQL_DESC_OCTET_LENGTH em APD.|O comprimento do nome do tipo de parâmetro com valor de tabela em bytes.<br /><br /> Isso poderá ser SQL_NTS se o nome do tipo terminar com caractere nulo ou 0 se o nome do tipo de parâmetro com valor de tabela não for necessário.|  
|*Strlen_or_indptr*|SQL_DESC_OCTET_LENGTH_PTR em APD.|SQL_DESC_OCTET_LENGTH_PTR em APD.<br /><br /> Para parâmetros com valor de tabela, essa é uma contagem de linhas e não um comprimento de dados.|  
||||

 Existe suporte para dois modos de transferência de dados para parâmetros com valor de tabela: associação de linha fixa e associação de linha variável.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>Associação de linha fixa de parâmetros com valor de tabela  
 Para associação de linha fixa, um aplicativo aloca buffers (ou matrizes de buffers) grandes o bastante para todos os possíveis valores de coluna de entrada. O aplicativo faz o seguinte:  
  
1.  Vincula todos os parâmetros usando chamadas SQLBindParameter, SQLSetDescRec ou SQLSetDescField.  
  
    1.  Define SQL_DESC_ARRAY_SIZE como o número máximo de linhas que podem ser transferidas para cada parâmetro com valor de tabela. Isso pode ser feito na chamada SQLBindParameter.  
  
2.  Chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS à ordinal de cada parâmetro avaliado em tabela.  
  
    1.  Para cada parâmetro avaliado em tabela, vincula colunas de parâmetros valorizadas em tabela usando chamadas SQLBindParameter, SQLSetDescRec ou SQLSetDescField.  
  
    2.  Para cada coluna de parâmetros avaliada em tabela que deve ter valores padrão, chama SQLSetDescField para definir SQL_CA_SS_COL_HAS_DEFAULT_VALUE para 1.  
  
3.  Chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS a 0. Isso deve ser feito antes que SQLExecute ou SQLExecDirect sejam chamados. Caso contrário, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY024 e a mensagem "Valor de atributo inválido, SQL_SOPT_SS_PARAM_FOCUS (deve ser zero em tempo de execução)".  
  
4.  Define *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR para SQL_DEFAULT_PARAM para um parâmetro avaliado em tabela sem linhas ou o número de linhas a serem transferidas na próxima chamada de SQLExecute ou SQLExecDirect se o parâmetro avaliado em tabela tiver linhas. *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR não podem ser definidos para SQL_NULL_DATA para um parâmetro avaliado em tabela, pois os parâmetros avaliados em tabela não são anulados (embora as colunas constituintes de parâmetros de valor de tabela possam ser anuladas). Se isso for definido como um valor inválido, SQLExecute ou SQLExecDirect retornarSQL_ERROR e um registro de diagnóstico for gerado com SQLSTATE=HY090 e a mensagem "Comprimento inválido de seqüência ou buffer para parâmetro \<p>", onde p é o número do parâmetro.  
  
5.  Chamadas SQLExecute ou SQLExecDirect.  
  
 Os valores da coluna de parâmetros de entrada avaliados na tabela podem ser passados em peças se *StrLen_or_IndPtr* for definido como*SQL_LEN_DATA_AT_EXEC(comprimento)* ou SQL_DATA_AT_EXEC para a coluna. Isso é semelhante a passar valores em partes quando são usadas matrizes de parâmetros. Como em todos os parâmetros de dados em execução, o SQLParamData não indica para qual linha do array o driver está solicitando dados; a aplicação deve cuidar disso. O aplicativo não pode fazer nenhuma pressuposição sobre a ordem na qual o driver solicitará valores.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>Associação de linha variável de parâmetros com valor de tabela  
 Para associação de linha variável, as linhas são transferidas em lotes em tempo de execução e o aplicativo passa linhas para o driver sob demanda. Isso é semelhante a dados em execução para valores de parâmetros individuais. Para associação de linha variável, o aplicativo faz o seguinte:  
  
1.  Associa parâmetros e colunas de parâmetros com valor de tabela como descrito nas etapas de 1 a 3 da seção anterior, "Associação de linha fixa de parâmetros com valor de tabela".  
  
2.  Define *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR para quaisquer parâmetros de valor de tabela que devem ser passados no momento da execução para SQL_DATA_AT_EXEC. Se nenhum dos dois for definido, o parâmetro será processado como descrito na seção anterior.  
  
3.  Chamadas SQLExecute ou SQLExecDirect. Isso retornará SQL_NEED_DATA se houver qualquer parâmetro SQL_PARAM_INPUT ou SQL_PARAM_INPUT_OUTPUT para ser tratado como parâmetro de dados em execução. Nesse caso, o aplicativo faz o seguinte:  
  
    -   Chama SQLParamData. Isso retorna o valor *ParameterValuePtr* para um parâmetro de data-at-execution e um código de retorno de SQL_NEED_DATA. Quando todos os dados de parâmetros forem passados para o driver, o SQLParamData retorna SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Para parâmetros de data-at-execution, *o ParameterValuePtr*, que é o mesmo que o campo descritor SQL_DESC_DATA_PTR, pode ser considerado como um token para identificar exclusivamente um parâmetro para o qual um valor é necessário. Esse "token" é passado do aplicativo para o driver em tempo de associação e, depois, devolvido ao aplicativo em tempo de execução.  
  
4.  Para enviar dados de linha de parâmetros de valor de tabela para parâmetros de valor de tabela nulos, se o parâmetro avaliado em tabela não tiver linhas, um aplicativo chama SQLPutData com *StrLen_or_Ind* definido como SQL_DEFAULT_PARAM.  
  
     Para TVPs não nulos, um aplicativo:  
  
    -   Define *Str_Len_or_Ind* para todas as colunas de parâmetros avaliadas em tabela para valores apropriados e preenche buffers de dados para colunas de parâmetros de valor de tabela que não devem ser parâmetros de dados em execução. Você pode usar dados em execução para colunas de parâmetros com valor de tabela de forma semelhante ao modo como parâmetros comuns podem ser passados para o driver em partes.  
  
    -   Chama SQLPutData com *Str_Len_or_Ind* definido para o número de linhas a serem enviadas para o servidor. Qualquer valor fora do intervalo de 0 a SQL_DESC_ARRAY_SIZE ou SQL_DEFAULT_PARAM é um erro e retornará SQLSTATE HY090, com a mensagem "Comprimento inválido de buffer ou cadeia de caracteres". 0 indica que todas as linhas foram enviadas e não há mais dados para um parâmetro com valor de tabela (como observado no segundo item de marcador desta lista). SQL_DEFAULT_PARAM poderá ser usado apenas na primeira vez em que o driver solicitar dados para um parâmetro com valor de tabela (como descrito no primeiro item de marcador desta lista).  
  
5.  Quando todas as linhas forem enviadas, chama SQLPutData para o parâmetro avaliado em tabela com um valor *de Str_Len_or_Ind* de 0 e, em seguida, prossegue para a etapa 3a acima.  
  
6.  Chama novamente o SQLParamData. Se houver parâmetros de execução de dados entre as colunas de parâmetros de valor de tabela, estes serão identificados pelo valor *ValuePtrPtr* retornado pelo SQLParamData. Quando todos os valores da coluna estiverem disponíveis, o SQLParamData retornará novamente o valor *de ParameterValuePtr* para o parâmetro avaliado na tabela, e o aplicativo recomeça.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros avaliados em tabela &#40;&#41;o ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
