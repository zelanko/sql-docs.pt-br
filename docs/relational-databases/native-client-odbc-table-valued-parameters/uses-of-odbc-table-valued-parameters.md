---
title: Usos de parâmetros com valor de tabela ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
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
  
 O parâmetro com valor de tabela é associado usando [SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328) junto com os outros parâmetros. Depois que todos os parâmetros tiverem sido associados, o aplicativo definirá o atributo Focus do parâmetro, SQL_SOPT_SS_PARAM_FOCUS, em cada parâmetro com valor de tabela e chamará SQLBindParameter para as colunas do parâmetro com valor de tabela.  
  
 O tipo de servidor para um parâmetro com valor de tabela é um novo tipo específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SQL_SS_TABLE. O tipo de C que associa para SQL_SS_TABLE sempre deve ser SQL_C_DEFAULT. Nenhum dado é transferido para o parâmetro associado ao parâmetro com valor de tabela. Ele é usado para transmitir metadados de tabela e controlar a maneira de transmitir dados nas colunas constituintes do parâmetro com valor de tabela.  
  
 O comprimento do parâmetro com valor tabela é definido como o número de linhas que são enviadas ao servidor. O parâmetro *ColumnSize* de SQLBindParameter para um parâmetro com valor de tabela especifica o número máximo de linhas que podem ser enviadas; Esse é o tamanho da matriz dos buffers de coluna. *ParameterValuePtr* é o buffer de parâmetro para um parâmetro com valor de tabela em SQLBindParameter. *ParameterValuePtr* e seus *BufferLength* associados são usados para passar o nome de tipo do parâmetro com valor de tabela quando necessário. O nome de tipo não é necessário para chamadas de procedimento armazenado, mas é necessário para instruções SQL.  
  
 Quando um nome de tipo de parâmetro com valor de tabela é especificado em uma chamada para SQLBindParameter, ele sempre deve ser especificado como um valor Unicode, mesmo em aplicativos criados como aplicativos ANSI. Quando você especifica um nome de tipo de parâmetro com valor de tabela usando SQLSetDescField, você pode usar um literal que está de acordo com a maneira como o aplicativo é compilado. O Gerenciador do Driver ODBC executará todas as conversões de Unicode necessárias.  
  
 Os metadados para parâmetros com valor de tabela e colunas de parâmetro com valor de tabela podem ser manipulados individualmente e explicitamente usando SQLGetDescRec, SQLSetDescRec, SQLGetDescField e SQLSetDescField. No entanto, o sobrecarregamento de SQLBindParameter é geralmente mais conveniente e não requer acesso de descritor explícito na maioria dos casos. Essa abordagem é consistente com a definição de SQLBindParameter para outros tipos de dados, exceto pelo fato de que, para um parâmetro com valor de tabela, os campos de descritor afetados são ligeiramente diferentes.  
  
 Às vezes, um aplicativo usa um parâmetro com valor de tabela com SQL dinâmico e é necessário fornecer o nome do tipo do parâmetro com valor de tabela. Se esse for o caso e o parâmetro com valor de tabela não estiver definido no esquema padrão atual para a conexão, SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME deverão ser definidos usando SQLSetDescField. Como as definições de tipo de tabela e parâmetros com valor de tabela devem ocorrer no mesmo banco de dados, SQL_CA_SS_TYPE_CATALOG_NAME não deve ser definido se o aplicativo usar parâmetros com valor de tabela. Caso contrário, o SQLSetDescField relatará um erro.  
  
 O código de exemplo para esse cenário está no `demo_fixed_TVP_binding` procedimento em [usar parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>Parâmetro com valor de tabela com streaming de linhas (Enviar dados como TVP usando dados em execução)  
 Neste cenário, o aplicativo fornece linhas ao driver conforme ele precisa e elas são transmitidas ao servidor. Isto evita ter a necessidade de armazenar em buffer todas as linhas na memória. Isto representa os cenários de inserção/atualização em massa. Parâmetros com valor de tabela fornecem um ponto de desempenho em algum local entre as matrizes do parâmetro e a cópia em massa. Isto é, parâmetros com valor de tabela são quase tão simples de programar quanto matrizes de parâmetros, mas eles fornecem mais flexibilidade no servidor.  
  
 O parâmetro com valor de tabela e suas colunas são associados conforme discutido na seção anterior, Parâmetro com valor de tabela com buffers de várias linhas totalmente associados, mas o indicador de comprimento do parâmetro com valor de tabela é definido como SQL_DATA_AT_EXEC. O driver responde a SQLExecute ou SQLExecuteDirect da maneira usual para parâmetros de dados em execução, ou seja, retornando SQL_NEED_DATA. Quando o driver estiver pronto para aceitar dados para um parâmetro com valor de tabela, SQLParamData retornará o valor de *ParameterValuePtr* em SQLBindParameter.  
  
 Um aplicativo usa SQLPutData para um parâmetro com valor de tabela para indicar a disponibilidade de dados para colunas constituintes de parâmetro com valor de tabela. Quando SQLPutData é chamado para um parâmetro com valor de tabela, *DataPtr* sempre deve ser nulo e *StrLen_or_Ind* deve ser 0 ou um número menor ou igual ao tamanho da matriz especificado para os buffers de parâmetro com valor de tabela (o parâmetro *colunasize* de SQLBindParameter). 0 significa que não há mais linhas para o parâmetro com valor de tabela e que o driver continuará a processar o próximo parâmetro de procedimento real. Quando *StrLen_or_Ind* não for 0, o driver processará as colunas constituintes do parâmetro com valor de tabela da mesma maneira que os parâmetros vinculados a parâmetros que não têm valor de tabela: cada coluna de parâmetro com valor de tabela pode especificar seu comprimento de dados real, SQL_NULL_DATA ou pode especificar dados na execução por meio de seu buffer de comprimento/indicador. Os valores de coluna de parâmetro com valor de tabela podem ser passados por chamadas repetidas para SQLPutData como de costume quando um valor de caractere ou binário é passado em partes.  
  
 Quando todas as colunas de parâmetro com valor de tabela tiverem sido processadas, o driver retornará ao parâmetro com valor de tabela para processar outras linhas dos dados. Portanto, para parâmetros com valor de tabela de dados em execução, o driver não segue a verificação sequencial habitual de parâmetros associados. Um parâmetro de valor de tabela associado será sondado até que SQLPutData seja chamado com *StrLen_or_IndPtr* igual a 0, quando o driver ignorar colunas de parâmetro com valor de tabela e passar para o próximo parâmetro de procedimento armazenado real.  Quando SQLPutData passa um valor de indicador maior ou igual a 1, o driver processa colunas de parâmetro com valor de tabela e linhas sequencialmente até que tenha valores para todas as linhas e colunas associadas. Então o driver retornará o parâmetro com valor de tabela. Entre o recebimento do token para o parâmetro com valor de tabela de SQLParamData e a chamada de SQLPutData (HSTMT, NULL, n) para um parâmetro com valor de tabela, o aplicativo deve definir dados de coluna constituintes de parâmetro com valor de tabela e o conteúdo do buffer de indicador para a próxima linha ou linhas a serem passadas para o servidor.  
  
 O código de exemplo para esse cenário está na `demo_variable_TVP_binding` rotina em [usar parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>Recuperando metadados do parâmetro com valor de tabela do catálogo do sistema  
 Quando um aplicativo chama SQLProcedureColumns para um procedimento que tem parâmetros de parâmetro com valor de tabela, DATA_TYPE é retornado como SQL_SS_TABLE e TYPE_NAME é o nome do tipo de tabela para o parâmetro com valor de tabela. Duas colunas adicionais são adicionadas ao conjunto de resultados retornado por SQLProcedureColumns: SS_TYPE_CATALOG_NAME retorna o nome do catálogo em que o tipo de tabela do parâmetro de valor de tabela é definido e SS_TYPE_SCHEMA_NAME retorna o nome do esquema onde o tipo de tabela do parâmetro de tabela-valor é definido. Em conformidade com a especificação ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem antes de todas as colunas específicas do driver que foram adicionadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]em versões anteriores do e depois de todas as colunas exigidas pelo próprio ODBC.  
  
 As colunas novas serão populadas não apenas para parâmetros com valor de tabela, mas também para parâmetros de tipo definido pelo usuário de CLR. As colunas existentes do esquema e do catálogo de parâmetros UDT ainda serão populadas, mas ter colunas de esquema e catálogo para tipos de dados que precisem delas simplificará o desenvolvimento do aplicativo no futuro. (Observe que as coleções de esquema XML são ligeiramente diferentes e não estão incluídas nessa alteração.)  
  
 Um aplicativo usa SQLTables para determinar os nomes dos tipos de tabela da mesma maneira que faz para tabelas persistentes, tabelas do sistema e exibições. Um tipo de tabela novo, TABLE TYPE, é introduzido para permitir que um aplicativo para identifique tipos de tabela associados com parâmetros com valor de tabela. Tipos de tabela e tabelas regulares usam namespaces diferentes. Isto significa que você pode usar o mesmo nome para um tipo de tabela e uma tabela real. Para tratar isto, um novo atributo de instrução, SQL_SOPT_SS_NAME_SCOPE, foi introduzido. Esse atributo especifica se SQLTables e outras funções de catálogo que usam um nome de tabela como parâmetro devem interpretar o nome da tabela como o nome de uma tabela real ou o nome de um tipo de tabela.  
  
 Um aplicativo usa SQLColumns para determinar as colunas para um tipo de tabela da mesma maneira que faz para tabelas persistentes, mas deve primeiro definir SQL_SOPT_SS_NAME_SCOPE para indicar que ele está funcionando com tipos de tabela em vez de tabelas reais. SQLPrimaryKeys também pode ser usado com tipos de tabela, novamente usando SQL_SOPT_SS_NAME_SCOPE.  
  
 O código de exemplo para esse cenário está na `demo_metadata_from_catalog_APIs` rotina em [usar parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>Recuperando metadados do parâmetro com valor de tabela para uma instrução preparada  
 Nesse cenário, um aplicativo usa SQLNumParameters e SQLDescribeParam para recuperar metadados para parâmetros com valor de tabela.  
  
 O campo de IPD SQL_CA_SS_TYPE_NAME é usado para recuperar o nome de tipo para parâmetros com valor de tabela. Os campos de IPD SQL_CA_SS_TYPE_SCHEMA_NAME e SQL_CA_SS_TYPE_CATALOG_NAME são usados para recuperar seu catálogo e seu esquema, respectivamente.  
  
 As definições de tipo de tabela e parâmetros com valor de tabela devem ocorrer no mesmo banco de dados. O SQLSetDescField relatará um erro se um aplicativo definir SQL_CA_SS_TYPE_CATALOG_NAME ao usar parâmetros com valor de tabela.  
  
 Também é possível usar SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME para recuperar o catálogo e o esquema associados com parâmetros de tipo definido pelo usuário CLR. SQL_CA_SS_TYPE_CATALOG_NAME e SQL_CA_SS_TYPE_SCHEMA_NAME são alternativas aos atributos de esquema de catálogo específico de tipos UDT da CLR.  
  
 Um aplicativo usa SQLColumns para recuperar metadados de coluna para um parâmetro com valor de tabela nesse cenário também, porque SQLDescribeParam não retorna metadados para as colunas de uma coluna de parâmetro com valor de tabela.  
  
 O código de exemplo para esse caso de uso está `demo_metadata_from_prepared_statement` na rotina em [usar parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
