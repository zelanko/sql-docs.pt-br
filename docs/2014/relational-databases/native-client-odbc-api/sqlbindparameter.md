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
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364688"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter` pode eliminar o peso da conversão de dados quando usado para fornecer dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client, resultando em ganhos significativos de desempenho para componentes de cliente e no servidor de aplicativos. Entre os outros benefícios está a menor perda de precisão ao inserir ou atualizar tipos de dados numéricos aproximados.  
  
> [!NOTE]  
>  Ao inserir dados de tipos `char` e `wchar` em uma coluna de imagem, é usado o tamanho dos dados sendo passados, e não o tamanho dos dados após a conversão em formato binário.  
  
 Se o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encontrar um erro em um único elemento de uma matriz de parâmetros, o driver continuará executando a instrução para os elementos restantes. Se o aplicativo tiver associado uma matriz de elementos de status de parâmetro para a instrução, as linhas dos parâmetros que geram erros poderão ser determinadas a partir da matriz.  
  
 Ao usar o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, especifique SQL_PARAM_INPUT ao associar parâmetros de entrada. Só especifique SQL_PARAM_OUTPUT ou SQL_PARAM_INPUT_OUTPUT ao associar parâmetros de procedimento armazenado definidos com a palavra-chave OUTPUT.  
  
 [SQLRowCount](sqlrowcount.md) não será confiável com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se um elemento de uma matriz de parâmetro associado causar erro na execução da instrução. O atributo da instrução ODBC – SQL_ATTR_PARAMS_PROCESSED_PTR – informa o número de linhas processadas antes da ocorrência do erro. O aplicativo pode atravessar sua matriz de status de parâmetro para descobrir o número de instruções executadas com êxito, se necessário.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Associando parâmetros para tipos de caractere SQL  
 Se o tipo de dados SQL passado for um tipo de caractere, *ColumnSize* será o tamanho em caracteres (não em bytes). Se o comprimento da cadeia de caracteres de dados em bytes for maior que 8000, *ColumnSize* deve ser definido como `SQL_SS_LENGTH_UNLIMITED`, indicando que não há nenhum limite para o tamanho do tipo SQL.  
  
 Por exemplo, se for o tipo de dados SQL `SQL_WVARCHAR`, *ColumnSize* não deve ser maior que 4000. Se o comprimento de dados real for maior que 4000, então *ColumnSize* deve ser definido como `SQL_SS_LENGTH_UNLIMITED` , de modo que `nvarchar(max)` será usada pelo driver.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter e parâmetros com valor de tabela  
 Como outros tipos de parâmetro, os parâmetros com valor de tabela são associados por SQLBindParameter.  
  
 Depois que um parâmetro com valor de tabela é associado, suas colunas também são associadas. Para associar as colunas, chame [SQLSetStmtAttr](sqlsetstmtattr.md) para definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal do parâmetro com valor de tabela. Em seguida, chame SQLBindParameter para cada coluna no parâmetro com valor de tabela. Para voltar às associações de parâmetro de nível superior, defina SQL_SOPT_SS_PARAM_FOCUS como 0.  
  
 Para obter informações sobre como mapear parâmetros para campos de descritor para parâmetros com valor de tabela, consulte [associação e Data Transfer of Table-Valued parâmetros e valores de coluna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>Suporte de SQLBindParameter a recursos aprimorados de data e hora  
 Valores de parâmetros dos tipos de data/hora são convertidos conforme descrito em [conversões do C para SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Observe que os parâmetros do tipo `time` e `datetimeoffset` deve ter *ValueType* especificado como `SQL_C_DEFAULT` ou `SQL_C_BINARY` se suas estruturas correspondentes (`SQL_SS_TIME2_STRUCT` e `SQL_SS_TIMESTAMPOFFSET_STRUCT`) são usados.  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Suporte de SQLBindParameter a UDTs CLR grandes  
 `SQLBindParameter` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes de implementação de API do ODBC](odbc-api-implementation-details.md)   
 [Função SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
