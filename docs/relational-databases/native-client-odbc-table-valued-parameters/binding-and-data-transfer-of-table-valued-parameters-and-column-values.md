---
title: Associação e os dados transferidos de valor de tabela parâmetros e valores de coluna | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7a5d0aac8e3d45f67ca83950ee139e3cb7377a96
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32947691"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>Associação e transferência de dados de parâmetros com valor de tabela e valores de coluna
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Parâmetros com valor de tabela, como outros parâmetros, devem ser associados antes de serem passados para o servidor. O aplicativo associa parâmetros com valor de tabela da mesma maneira que associa outros parâmetros: usando SQLBindParameter ou chamadas equivalentes para SQLSetDescField ou SQLSetDescRec. O tipo de dados do servidor para um parâmetro com valor de tabela é SQL_SS_TABLE. O tipo C pode ser especificado como SQL_C_DEFAULT ou SQL_C_BINARY.  
  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior, só existe suporte para parâmetros com valor de tabela de entrada. Portanto, qualquer tentativa de definir SQL_DESC_PARAMETER_TYPE como um valor diferente de SQL_PARAM_INPUT retornará SQL_ERROR com SQLSTATE = HY105 e a mensagem "Tipo de parâmetro inválido".  
  
 Valores padrão podem ser atribuídos a colunas inteiras de parâmetros com valor de tabela usando o atributo SQL_CA_SS_COL_HAS_DEFAULT_VALUE. Valores de coluna de parâmetro com valor de tabela individual, no entanto, não podem ser atribuídos valores padrão usando SQL_DEFAULT_PARAM em *StrLen_or_IndPtr* com SQLBindParameter. Parâmetros com valor de tabela como um todo não podem ser definidos como um valor padrão usando SQL_DEFAULT_PARAM em *StrLen_or_IndPtr* com SQLBindParameter. Se essas regras não forem seguidas, SQLExecute ou SQLExecDirect retornará SQL_ERROR. Um registro de diagnóstico será gerado com SQLSTATE = 07S01 e a mensagem "uso inválido de parâmetro padrão para o parâmetro \<p >", onde \<p > é o ordinal de TVP na instrução de consulta.  
  
 Depois de associar o parâmetro com valor de tabela, o aplicativo deverá, então, associar cada coluna de parâmetros com valor de tabela. Para fazer isso, o aplicativo primeiro chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal de um parâmetro com valor de tabela. Em seguida, o aplicativo associa as colunas do parâmetro com valor de tabela por chamadas para as seguintes rotinas: SQLBindParameter, SQLSetDescRec e SQLSetDescField. A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o efeito habitual de SQLBindParameter, SQLSetDescRec e SQLSetDescField em operação em parâmetros normais de nível superior.
 
 Observação: para os Linux e Mac drivers de ODBC com unixODBC 2.3.1 para 2.3.4, ao definir o nome TVP por meio de SQLSetDescField com o campo do descritor SQL_CA_SS_TYPE_NAME, unixODBC não converte automaticamente entre ANSI e Unicode cadeias de caracteres dependendo exato função de chamada (SQLSetDescFieldA / SQLSetDescFieldW). É necessário sempre usar SQLBindParameter ou SQLSetDescFieldW com uma cadeia de caracteres Unicode (UTF-16) para definir o nome TVP.
  
 Nenhum dado real é enviado ou recebido para o próprio parâmetro com valor de tabela, mas dados são enviados e recebidos para cada uma de suas colunas constituintes. Como o parâmetro com valor de tabela é uma pseudocoluna, os parâmetros para SQLBindParameter são usados para fazer referência aos atributos diferentes que outros tipos de dados, da seguinte maneira:  
  
|Parâmetro|Atributo relacionado para tipos de parâmetros sem-valor de tabela, incluindo colunas|Atributo relacionado para parâmetros com valor de tabela|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|SQL_DESC_PARAMETER_TYPE em IPD.<br /><br /> Para colunas de parâmetros com valor de tabela, isso deve ser igual à configuração do próprio parâmetro com valor de tabela.|SQL_DESC_PARAMETER_TYPE em IPD.<br /><br /> Isso deve ser SQL_PARAM_INPUT.|  
|*ValueType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em APD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em APD.<br /><br /> Isso deve ser SQL_C_DEFAULT ou SQL_C_BINARY.|  
|*ParameterType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em IPD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE em IPD.<br /><br /> Isso deve ser SQL_SS_TABLE.|  
|*ColumnSize*|SQL_DESC_LENGTH ou SQL_DESC_PRECISION em IPD.<br /><br /> Isso depende do valor de *ParameterType*.|SQL_DESC_ARRAY_SIZE<br /><br /> Também poderá ser definido usando SQL_ATTR_PARAM_SET_SIZE quando o foco do parâmetro for definido como o parâmetro com valor de tabela.<br /><br /> Para um parâmetro com valor de tabela, esse é o número de linhas nos buffers de colunas de parâmetros com valor de tabela.|  
|*DecimalDigits*|SQL_DESC_PRECISION ou SQL_DESC_SCALE em IPD.|Não utilizado. Isso deve ser 0.<br /><br /> Se esse parâmetro será não 0, SQLBindParameter retorno SQL_ERROR e um registro de diagnóstico serão gerado com SQLSTATE = HY104 e a mensagem "escala ou precisão inválida".|  
|*ParameterValuePtr*|SQL_DESC_DATA_PTR em APD.|SQL_CA_SS_TYPE_NAME.<br /><br /> Isso é opcional para chamadas de procedimento armazenado e NULL poderá ser especificado se ele não for necessário. Deve ser especificado para instruções SQL que não são chamadas de procedimento.<br /><br /> Esse parâmetro também funciona como um valor exclusivo que o aplicativo poderá usar para identificar esse parâmetro com valor de tabela quando a associação de linha variável for usada. Para obter mais informações, consulte a seção "Associação de linha variável de parâmetros com valor de tabela", mais adiante neste tópico.<br /><br /> Quando um nome de tipo de parâmetro com valor de tabela é especificado em uma chamada para SQLBindParameter, ele deve ser especificado como um valor Unicode, mesmo em aplicativos que são criados como aplicativos ANSI. O valor usado para o parâmetro *StrLen_or_IndPtr* deve ser SQL_NTS ou o comprimento da cadeia de caracteres do nome multiplicado por sizeof (WCHAR).|  
|*BufferLength*|SQL_DESC_OCTET_LENGTH em APD.|O comprimento do nome do tipo de parâmetro com valor de tabela em bytes.<br /><br /> Isso poderá ser SQL_NTS se o nome do tipo terminar com caractere nulo ou 0 se o nome do tipo de parâmetro com valor de tabela não for necessário.|  
|*StrLen_or_IndPtr*|SQL_DESC_OCTET_LENGTH_PTR em APD.|SQL_DESC_OCTET_LENGTH_PTR em APD.<br /><br /> Para parâmetros com valor de tabela, essa é uma contagem de linhas e não um comprimento de dados.|  
  
 Existe suporte para dois modos de transferência de dados para parâmetros com valor de tabela: associação de linha fixa e associação de linha variável.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>Associação de linha fixa de parâmetros com valor de tabela  
 Para associação de linha fixa, um aplicativo aloca buffers (ou matrizes de buffers) grandes o bastante para todos os possíveis valores de coluna de entrada. O aplicativo faz o seguinte:  
  
1.  Associa todos os parâmetros usando chamadas SQLBindParameter, SQLSetDescRec ou SQLSetDescField.  
  
    1.  Define SQL_DESC_ARRAY_SIZE como o número máximo de linhas que podem ser transferidas para cada parâmetro com valor de tabela. Isso pode ser feito na chamada SQLBindParameter.  
  
2.  Chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal de cada parâmetro com valor de tabela.  
  
    1.  Para cada parâmetro com valor de tabela, associa as colunas de parâmetro com valor de tabela por meio de chamadas SQLBindParameter, SQLSetDescRec ou SQLSetDescField.  
  
    2.  Para cada coluna de parâmetro com valor de tabela que deve ter valores padrão, chama SQLSetDescField para definir SQL_CA_SS_COL_HAS_DEFAULT_VALUE como 1.  
  
3.  Chama SQLSetStmtAttr para definir SQL_SOPT_SS_PARAM_FOCUS como 0. Isso deve ser feito antes de SQLExecute ou SQLExecDirect é chamado. Caso contrário, SQL_ERROR será retornado e um registro de diagnóstico será gerado com SQLSTATE=HY024 e a mensagem "Valor de atributo inválido, SQL_SOPT_SS_PARAM_FOCUS (deve ser zero em tempo de execução)".  
  
4.  Conjuntos de *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR como SQL_DEFAULT_PARAM para um parâmetro com valor de tabela com nenhuma linha, ou o número de linhas a serem transferidas na próxima chamada de SQLExecute ou SQLExecDirect se o valor de tabela o parâmetro tem linhas. *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR não pode ser definida como SQL_NULL_DATA para um parâmetro com valor de tabela como parâmetros com valor de tabela não permite valor nulos (embora colunas constituintes do parâmetro com valor de tabela podem ser anuláveis). Se isso é definido como um valor inválido, SQLExecute ou SQLExecDirect retornará SQL_ERROR e um registro de diagnóstico será gerado com SQLSTATE = HY090 e a mensagem "comprimento de buffer ou cadeia de caracteres inválido para parâmetro \<p >", onde p é o número do parâmetro.  
  
5.  Chama SQLExecute ou SQLExecDirect.  
  
 Entrada de valores de coluna de parâmetro com valor de tabela podem ser passados em partes se *StrLen_or_IndPtr* é definido como SQL_LEN_DATA_AT_EXEC (*comprimento*) ou SQL_DATA_AT_EXEC para a coluna. Isso é semelhante a passar valores em partes quando são usadas matrizes de parâmetros. Como com todos os parâmetros de dados em execução, SQLParamData não indica qual linha da matriz o driver está solicitando dados; o aplicativo deve se encarregar disso. O aplicativo não pode fazer nenhuma pressuposição sobre a ordem na qual o driver solicitará valores.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>Associação de linha variável de parâmetros com valor de tabela  
 Para associação de linha variável, as linhas são transferidas em lotes em tempo de execução e o aplicativo passa linhas para o driver sob demanda. Isso é semelhante a dados em execução para valores de parâmetros individuais. Para associação de linha variável, o aplicativo faz o seguinte:  
  
1.  Associa parâmetros e colunas de parâmetros com valor de tabela como descrito nas etapas de 1 a 3 da seção anterior, "Associação de linha fixa de parâmetros com valor de tabela".  
  
2.  Conjuntos de *StrLen_or_IndPtr* ou SQL_DESC_OCTET_LENGTH_PTR para todos os parâmetros com valor de tabela que será passado em tempo de execução para SQL_DATA_AT_EXEC. Se nenhum dos dois for definido, o parâmetro será processado como descrito na seção anterior.  
  
3.  Chama SQLExecute ou SQLExecDirect. Isso retornará SQL_NEED_DATA se houver qualquer parâmetro SQL_PARAM_INPUT ou SQL_PARAM_INPUT_OUTPUT para ser tratado como parâmetro de dados em execução. Nesse caso, o aplicativo faz o seguinte:  
  
    -   Chama SQLParamData. Isso retorna o *ParameterValuePtr* valor para um parâmetro de dados em execução e um código de retorno de SQL_NEED_DATA. Quando todos os dados de parâmetro foi passado para o driver, SQLParamData retorna SQL_SUCCESS, SQL_SUCCESS_WITH_INFO ou SQL_ERROR. Para parâmetros de dados em execução, *ParameterValuePtr*, que é o mesmo que o descritor de campo SQL_DESC_DATA_PTR, pode ser considerada como um token para identificar exclusivamente um parâmetro para o qual um valor é necessário. Esse "token" é passado do aplicativo para o driver em tempo de associação e, depois, devolvido ao aplicativo em tempo de execução.  
  
4.  Para enviar dados de linha de parâmetro com valor de tabela para parâmetros com valor de tabela nulos, se o parâmetro com valor de tabela não tem nenhuma linha, um aplicativo chama SQLPutData com *StrLen_or_Ind* definido como SQL_DEFAULT_PARAM.  
  
     Para TVPs não nulos, um aplicativo:  
  
    -   Conjuntos de *Str_Len_or_Ind* para todas as colunas de parâmetro com valor de tabela para os valores apropriados e preenche os buffers de dados para colunas de parâmetro com valor de tabela que não devem ser parâmetros de dados em execução. Você pode usar dados em execução para colunas de parâmetros com valor de tabela de forma semelhante ao modo como parâmetros comuns podem ser passados para o driver em partes.  
  
    -   Chama SQLPutData com *Str_Len_or_Ind* definido para o número de linhas a serem enviadas para o servidor. Qualquer valor fora do intervalo de 0 a SQL_DESC_ARRAY_SIZE ou SQL_DEFAULT_PARAM é um erro e retornará SQLSTATE HY090, com a mensagem "Comprimento inválido de buffer ou cadeia de caracteres". 0 indica que todas as linhas foram enviadas e não há mais dados para um parâmetro com valor de tabela (como observado no segundo item de marcador desta lista). SQL_DEFAULT_PARAM poderá ser usado apenas na primeira vez em que o driver solicitar dados para um parâmetro com valor de tabela (como descrito no primeiro item de marcador desta lista).  
  
5.  Quando todas as linhas forem enviadas, chama SQLPutData para o parâmetro com valor de tabela com um *Str_Len_or_Ind* valor de 0 e, em seguida, vai para a etapa 3a acima.  
  
6.  Chama SQLParamData novamente. Se houver quaisquer parâmetros de dados em execução entre as colunas de parâmetro com valor de tabela, esses serão identificados pelo valor *ValuePtrPtr* retornado por SQLParamData. Quando todos os valores de coluna estão disponíveis, SQLParamData retornará novamente o *ParameterValuePtr* valor para o parâmetro com valor de tabela e o aplicativo começa novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
