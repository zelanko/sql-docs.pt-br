---
title: Usos de parâmetros valorizados em tabela da ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e88092c6566d9e5838f8a2cb59cd7c23564af9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297727"
---
# <a name="uses-of-odbc-table-valued-parameters"></a>Usos de parâmetros ODBC com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico discute os principais cenários de usuário para o uso de parâmetros com valor de tabela com ODBC:  
  
-   Parâmetro com valor de tabela com buffers de várias linhas totalmente associados (Enviar dados como um RVP com todos os valores na memória)  
  
-   Parâmetro com valor de tabela com streaming de linhas (Enviar dados como TVP usando dados em execução)  
  
-   Recuperando metadados do parâmetro com valor de tabela do catálogo do sistema  
  
-   Recuperando metadados do parâmetro com valor de tabela para uma instrução preparada  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>Parâmetro com valor de tabela com buffers de várias linhas totalmente associados (Enviar dados como um RVP com todos os valores na memória)  
 Quando usados com buffers de várias linhas totalmente associados, todos os valores de parâmetro ficam disponíveis na memória. Por exemplo, isto é típico de uma transação de OLTP na qual os parâmetros com valor de tabela podem ser empacotados em um único procedimento armazenado. Sem parâmetros com valor de tabela, isso envolveria gerar um lote de várias instruções complexas dinamicamente ou fazer várias chamadas para o servidor.  
  
 O parâmetro avaliado em tabela em si está vinculado usando [o SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328) juntamente com os outros parâmetros. Depois que todos os parâmetros foram vinculados, o aplicativo define o atributo de foco do parâmetro, SQL_SOPT_SS_PARAM_FOCUS, em cada parâmetro avaliado em tabela e chama SQLBindParameter para as colunas do parâmetro avaliado em tabela.  
  
 O tipo de servidor para um parâmetro com valor de tabela é um novo tipo específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SQL_SS_TABLE. O tipo de C que associa para SQL_SS_TABLE sempre deve ser SQL_C_DEFAULT. Nenhum dado é transferido para o parâmetro associado ao parâmetro com valor de tabela. Ele é usado para transmitir metadados de tabela e controlar a maneira de transmitir dados nas colunas constituintes do parâmetro com valor de tabela.  
  
 O comprimento do parâmetro com valor tabela é definido como o número de linhas que são enviadas ao servidor. O parâmetro *ColumnSize* do SQLBindParameter para um parâmetro de valor de tabela especifica o número máximo de linhas que podem ser enviadas; este é o tamanho da matriz dos buffers de coluna. *ParâmetroValuePtr* é o buffer de parâmetros para um parâmetro de valor de tabela no SQLBindParameter. *ParâmetroValuePtr* e seu *BufferLength* associado são usados para passar o nome do tipo do parâmetro avaliado pela tabela quando necessário. O nome de tipo não é necessário para chamadas de procedimento armazenado, mas é necessário para instruções SQL.  
  
 Quando um nome de tipo de parâmetro de valor de tabela é especificado em uma chamada para SQLBindParameter, ele deve sempre ser especificado como um valor Unicode, mesmo em aplicativos que são construídos como aplicativos ANSI. Quando você especifica um nome de tipo de parâmetro de valor de tabela usando SQLSetDescField, você pode usar um literal que esteja em conformidade com a forma como o aplicativo é construído. O Gerenciador do Driver ODBC executará todas as conversões de Unicode necessárias.  
  
 Metadados para parâmetros de valor de tabela e colunas de parâmetros de valor de tabela podem ser manipulados individual e explicitamente usando SQLGetDescRec, SQLSetDescRec, SQLGetDescField e SQLSetDescField. No entanto, a sobrecarga do SQLBindParameter geralmente é mais conveniente e não requer acesso explícito ao descritor na maioria dos casos. Esta abordagem é consistente com a definição de SQLBindParameter para outros tipos de dados, exceto que para um parâmetro de valor de tabela os campos descritores afetados são ligeiramente diferentes.  
  
 Às vezes, um aplicativo usa um parâmetro com valor de tabela com SQL dinâmico e é necessário fornecer o nome do tipo do parâmetro com valor de tabela. Se este for o caso e o parâmetro de valor de tabela não for definido no esquema padrão atual para a conexão, SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME devem ser definidos usando SQLSetDescField. Como as definições de tipo de tabela e parâmetros com valor de tabela devem ocorrer no mesmo banco de dados, SQL_CA_SS_TYPE_CATALOG_NAME não deve ser definido se o aplicativo usar parâmetros com valor de tabela. Caso contrário, SQLSetDescField reportará um erro.  
  
 O código amostral para `demo_fixed_TVP_binding` este cenário está no procedimento em [Use Table-Valued Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>Parâmetro com valor de tabela com streaming de linhas (Enviar dados como TVP usando dados em execução)  
 Neste cenário, o aplicativo fornece linhas ao driver conforme ele precisa e elas são transmitidas ao servidor. Isto evita ter a necessidade de armazenar em buffer todas as linhas na memória. Isto representa os cenários de inserção/atualização em massa. Parâmetros com valor de tabela fornecem um ponto de desempenho em algum local entre as matrizes do parâmetro e a cópia em massa. Isto é, parâmetros com valor de tabela são quase tão simples de programar quanto matrizes de parâmetros, mas eles fornecem mais flexibilidade no servidor.  
  
 O parâmetro com valor de tabela e suas colunas são associados conforme discutido na seção anterior, Parâmetro com valor de tabela com buffers de várias linhas totalmente associados, mas o indicador de comprimento do parâmetro com valor de tabela é definido como SQL_DATA_AT_EXEC. O driver responde ao SQLExecute ou ao SQLExecuteDirect da maneira usual para parâmetros de data-at-execution - ou seja, retornando SQL_NEED_DATA. Quando o driver estiver pronto para aceitar dados para um parâmetro avaliado em tabela, o SQLParamData retorna o valor de *ParameterValuePtr* no SQLBindParameter.  
  
 Um aplicativo usa SQLPutData para um parâmetro de valor de tabela para indicar a disponibilidade de dados para colunas constituintes de parâmetros de valor de tabela. Quando o SQLPutData é chamado para um parâmetro de valor de tabela, *o DataPtr* deve ser sempre nulo e *StrLen_or_Ind* deve ser 0 ou um número menor ou igual ao tamanho da matriz especificado para buffers de parâmetros de valor de tabela (o parâmetro *ColumnSize* do SQLBindParameter). 0 significa que não há mais linhas para o parâmetro com valor de tabela e que o driver continuará a processar o próximo parâmetro de procedimento real. Quando *StrLen_or_Ind* não for 0, o driver processará as colunas constituintes de parâmetros de parâmetro sumido da tabela da mesma forma que parâmetros vinculados a parâmetros de parâmetros não valorizados pela tabela: Cada coluna de parâmetro sí00, avaliada em tabela, pode especificar seu comprimento real de dados, SQL_NULL_DATA ou pode especificar dados em execução através de seu buffer de comprimento/indicador. Os valores da coluna de parâmetros avaliados em tabela podem ser passados por chamadas repetidas para SQLPutData, como de costume, quando um caractere ou valor binário deve ser passado em pedaços.  
  
 Quando todas as colunas de parâmetro com valor de tabela tiverem sido processadas, o driver retornará ao parâmetro com valor de tabela para processar outras linhas dos dados. Portanto, para parâmetros com valor de tabela de dados em execução, o driver não segue a verificação sequencial habitual de parâmetros associados. Um parâmetro de tabela vinculada será pesquisado até que o SQLPutData seja chamado com *StrLen_Or_IndPtr* igual a 0, momento em que o driver pula colunas de parâmetros de tabela e se move para o próximo parâmetro de procedimento armazenado real.  Quando o SQLPutData passa um valor indicador maior ou igual a 1, o driver processa colunas e linhas de parâmetros avaliadas em tabela sequencialmente até que tenha valores para todas as linhas e colunas vinculadas. Então o driver retornará o parâmetro com valor de tabela. Entre receber o token para o parâmetro de valor de tabela do SQLParamData e ligar para SQLPutData (hstmt, NULL, n) para um parâmetro de valor de tabela, o aplicativo deve definir dados da coluna constituinte do parâmetro de tabela e o conteúdo do buffer indicador para que a próxima linha ou linhas sejam passadas para o servidor.  
  
 O código amostral para `demo_variable_TVP_binding` este cenário está na rotina em [Use Table-Valued Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>Recuperando metadados do parâmetro com valor de tabela do catálogo do sistema  
 Quando um aplicativo chama SQLProcedureColumns para um procedimento que tem parâmetros de parâmetros de valor de tabela, DATA_TYPE é devolvido como SQL_SS_TABLE e TYPE_NAME é o nome do tipo de tabela para o parâmetro avaliado em tabela. Duas colunas adicionais são adicionadas ao conjunto de resultados retornado por SQLProcedureColumns: SS_TYPE_CATALOG_NAME retorna o nome do catálogo onde o tipo de tabela do parâmetro de valor de tabela é definido e SS_TYPE_SCHEMA_NAME retorna o nome do esquema onde o tipo de tabela do parâmetro de valor de tabela é definido. Em conformidade com a especificação ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem diante de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]todas as colunas específicas do driver que foram adicionadas em versões anteriores de , e depois de todas as colunas exigidas pela própria ODBC.  
  
 As colunas novas serão populadas não apenas para parâmetros com valor de tabela, mas também para parâmetros de tipo definido pelo usuário de CLR. As colunas existentes do esquema e do catálogo de parâmetros UDT ainda serão populadas, mas ter colunas de esquema e catálogo para tipos de dados que precisem delas simplificará o desenvolvimento do aplicativo no futuro. (Observe que as coleções de esquema XML são ligeiramente diferentes e não estão incluídas nessa alteração.)  
  
 Um aplicativo usa SQLTables para determinar os nomes dos tipos de tabela da mesma forma que faz para tabelas, tabelas de sistema e exibições persistentes. Um tipo de tabela novo, TABLE TYPE, é introduzido para permitir que um aplicativo para identifique tipos de tabela associados com parâmetros com valor de tabela. Tipos de tabela e tabelas regulares usam namespaces diferentes. Isto significa que você pode usar o mesmo nome para um tipo de tabela e uma tabela real. Para tratar isto, um novo atributo de instrução, SQL_SOPT_SS_NAME_SCOPE, foi introduzido. Este atributo especifica se sqltables e outras funções de catálogo que tomam um nome de tabela como parâmetro devem interpretar o nome da tabela como o nome de uma tabela real ou o nome de um tipo de tabela.  
  
 Um aplicativo usa SQLColumns para determinar as colunas para um tipo de tabela da mesma forma que faz para tabelas persistentes, mas deve primeiro definir SQL_SOPT_SS_NAME_SCOPE para indicar que está trabalhando com tipos de tabela em vez de tabelas reais. SQLPrimaryKeys também pode ser usado com tipos de tabela, novamente usando SQL_SOPT_SS_NAME_SCOPE.  
  
 O código amostral para `demo_metadata_from_catalog_APIs` este cenário está na rotina em [Use Table-Valued Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>Recuperando metadados do parâmetro com valor de tabela para uma instrução preparada  
 Neste cenário, um aplicativo usa SQLNumParameters e SQLDescribeParam para recuperar metadados para parâmetros de valor de tabela.  
  
 O campo de IPD SQL_CA_SS_TYPE_NAME é usado para recuperar o nome de tipo para parâmetros com valor de tabela. Os campos de IPD SQL_CA_SS_TYPE_SCHEMA_NAME e SQL_CA_SS_TYPE_CATALOG_NAME são usados para recuperar seu catálogo e seu esquema, respectivamente.  
  
 As definições de tipo de tabela e parâmetros com valor de tabela devem ocorrer no mesmo banco de dados. O SQLSetDescField reportará um erro se um aplicativo definir SQL_CA_SS_TYPE_CATALOG_NAME ao usar parâmetros avaliados em tabela.  
  
 Também é possível usar SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME para recuperar o catálogo e o esquema associados com parâmetros de tipo definido pelo usuário CLR. SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME são alternativas aos atributos de esquema de catálogo específico de tipos UDT da CLR.  
  
 Um aplicativo usa SQLColumns para recuperar metadados de coluna para um parâmetro de valor de tabela neste cenário, também, porque o SQLDescribeParam não retorna metadados para as colunas de uma coluna de parâmetros valorizadas em tabela.  
  
 O código amostral para este `demo_metadata_from_prepared_statement` caso de uso está na rotina em [Use Table-Valued Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros avaliados em tabela &#40;&#41;o ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
