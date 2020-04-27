---
title: SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cba973be9b4dc2ec0da286b2d01b636f0ca4e2b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067812"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter`pode eliminar a carga da conversão de dados quando usada para fornecer dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC do Native Client, resultando em ganhos de desempenho significativos para os componentes do cliente e do servidor dos aplicativos. Entre os outros benefícios está a menor perda de precisão ao inserir ou atualizar tipos de dados numéricos aproximados.  
  
> [!NOTE]  
>  Ao inserir dados de tipos `char` e `wchar` em uma coluna de imagem, é usado o tamanho dos dados sendo passados, e não o tamanho dos dados após a conversão em formato binário.  
  
 Se o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encontrar um erro em um único elemento de uma matriz de parâmetros, o driver continuará executando a instrução para os elementos restantes. Se o aplicativo tiver associado uma matriz de elementos de status de parâmetro para a instrução, as linhas dos parâmetros que geram erros poderão ser determinadas a partir da matriz.  
  
 Ao usar o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, especifique SQL_PARAM_INPUT ao associar parâmetros de entrada. Só especifique SQL_PARAM_OUTPUT ou SQL_PARAM_INPUT_OUTPUT ao associar parâmetros de procedimento armazenado definidos com a palavra-chave OUTPUT.  
  
 [SQLRowCount](sqlrowcount.md) não será confiável com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se um elemento de uma matriz de parâmetro associado causar erro na execução da instrução. O atributo da instrução ODBC – SQL_ATTR_PARAMS_PROCESSED_PTR – informa o número de linhas processadas antes da ocorrência do erro. O aplicativo pode atravessar sua matriz de status de parâmetro para descobrir o número de instruções executadas com êxito, se necessário.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Associando parâmetros para tipos de caractere SQL  
 Se o tipo de dados SQL passado for um tipo de caractere, *ColumnSize* será o tamanho em caracteres (não em bytes). Se o comprimento da cadeia de caracteres de dados em bytes for maior que 8000, *colunasize* deverão ser `SQL_SS_LENGTH_UNLIMITED`definidas como, indicando que não há nenhum limite para o tamanho do tipo SQL.  
  
 Por exemplo, se o tipo de dados SQL `SQL_WVARCHAR`for, *ColumnSize* não deve ser maior que 4000. Se o comprimento real dos dados for maior que 4000, *colunasize* deverão ser definidas como `SQL_SS_LENGTH_UNLIMITED` para que `nvarchar(max)` serão usadas pelo driver.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter e parâmetros com valor de tabela  
 Assim como outros tipos de parâmetro, os parâmetros com valor de tabela são associados por SQLBindParameter.  
  
 Depois que um parâmetro com valor de tabela é associado, suas colunas também são associadas. Para associar as colunas, chame [SQLSetStmtAttr](sqlsetstmtattr.md) para definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal do parâmetro com valor de tabela. Em seguida, chame SQLBindParameter para cada coluna no parâmetro com valor de tabela. Para voltar às associações de parâmetro de nível superior, defina SQL_SOPT_SS_PARAM_FOCUS como 0.  
  
 Para obter informações sobre como mapear parâmetros para campos de descritor para parâmetros com valor de tabela, consulte [Binding and transferência de dados of table-valued Parameters and Column Values](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>Suporte de SQLBindParameter a recursos aprimorados de data e hora  
 Os valores de parâmetro dos tipos de data/hora são convertidos conforme descrito em [conversões de C para SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Observe que os parâmetros do `time` tipo `datetimeoffset` e devem ter *ValueType* especificado `SQL_C_DEFAULT` como `SQL_C_BINARY` ou se suas estruturas correspondentes`SQL_SS_TIME2_STRUCT` ( `SQL_SS_TIMESTAMPOFFSET_STRUCT`e) forem usadas.  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Suporte de SQLBindParameter a UDTs CLR grandes  
 `SQLBindParameter` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de implementação da API ODBC](odbc-api-implementation-details.md)   
 [Função SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
