---
title: Buscando dados de resultado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 00a3245009d7f7db437a990fdf5dc814d6b19f7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724993"
---
# <a name="fetching-result-data"></a>Buscando dados de resultados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Um aplicativo ODBC tem três opções para buscar dados de resultados.  
  
 A primeira opção se baseia em [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Antes de buscar o conjunto de resultados, o aplicativo usa **SQLBindCol** para associar cada coluna no conjunto de resultados a uma variável de programa. Depois que as colunas tiverem sido associadas, o driver transferirá os dados da linha atual para as variáveis associadas às colunas do conjunto de resultados cada vez que o aplicativo chamar **SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). O driver manipulará as conversões de dados se a coluna do conjunto de resultados e a variável de programa tiverem tipos de dados diferentes. Se o aplicativo tiver SQL_ATTR_ROW_ARRAY_SIZE definido como maior que 1, ele poderá associar colunas de resultado a matrizes de variáveis, que serão todas preenchidas em cada chamada para **SQLFetchScroll**.  
  
 A segunda opção se baseia em [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). O aplicativo não usa **SQLBindCol** para associar colunas de conjunto de resultados a variáveis de programa. Após cada chamada para **SQLFetch**, o aplicativo chama **SQLGetData** uma vez para cada coluna no conjunto de resultados. O **SQLGetData** instrui o driver a transferir dados de uma coluna de conjunto de resultados específica para uma variável de programa específica e especifica os tipos de dados da coluna e da variável. Isso permitirá que o driver converta os dados se a coluna de resultados e a variável de programa tiverem tipos de dados diferentes. As colunas **Text**, **ntext**e **Image** normalmente são muito grandes para caber em uma variável de programa, mas ainda podem ser recuperadas usando **SQLGetData**. Se os dados **Text**, **ntext**ou **Image** na coluna Result forem maiores que a variável Program, **SQLGetData** retornará SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita). As chamadas sucessivas para **SQLGetData** retornam partes sucessivas dos dados de **texto** ou **imagem** . Quando o final dos dados é atingido, **SQLGetData** retorna SQL_SUCCESS. Cada busca retornará um conjunto de linhas se SQL_ATTR_ROW_ARRAY_SIZE for maior do que 1. Antes de usar **SQLGetData**, você deve primeiro usar **SQLSetPos** para especificar uma linha específica dentro do conjunto de linhas como a linha atual.  
  
 A terceira opção é usar uma combinação de **SQLBindCol** e **SQLGetData**. Um aplicativo poderia, por exemplo, associar as dez primeiras colunas de um conjunto de resultados e, em seguida, em cada busca, chamar **SQLGetData** três vezes para recuperar os dados de três colunas desassociadas. Isso normalmente seria usado quando um conjunto de resultados contiver uma ou mais colunas de **texto** ou **imagem** .  
  
 Dependendo das opções de cursor definidas para o conjunto de resultados, um aplicativo também pode usar as opções de rolagem de **SQLFetchScroll** para rolar em volta do conjunto de resultados.  
  
 O uso excessivo de **SQLBindCol** para associar uma coluna de conjunto de resultados a uma variável de programa é caro porque o **SQLBindCol** faz com que um driver ODBC aloque memória. Quando você associa uma coluna de resultado a uma variável, essa associação permanece em vigor até que você chame [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar o identificador de instrução ou chamar [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com *fOption* definido como SQL_UNBIND. As associações não são desfeitas automaticamente quando a instrução é concluída.  
  
 Essa lógica permite lidar efetivamente com a execução da mesma instrução SELECT várias vezes com parâmetros diferentes. Como o conjunto de resultados mantém a mesma estrutura, você pode associar o conjunto de resultados uma vez, processar todas as instruções SELECT e, em seguida, chamar **SQLFreeStmt** com *fOption* definido como SQL_UNBIND após a última execução. Você não deve chamar **SQLBindCol** para associar as colunas em um conjunto de resultados sem primeiro chamar **SQLFreeStmt** com *fOption* definido como SQL_UNBIND para liberar quaisquer associações anteriores.  
  
 Ao usar o **SQLBindCol**, você pode fazer uma associação de linha ou de coluna. A associação por linha é um pouco mais rápida do que a associação por coluna.  
  
 Você pode usar **SQLGetData** para recuperar dados de uma base coluna a coluna em vez de associar colunas de conjunto de resultados usando **SQLBindCol**. Se um conjunto de resultados contiver apenas algumas linhas, usar **SQLGetData** em vez de **SQLBindCol** será mais rápido; caso contrário, o **SQLBindCol** fornecerá o melhor desempenho. Se você nem sempre colocar os dados no mesmo conjunto de variáveis, deverá usar **SQLGetData** em vez de reassociar constantemente. Você só pode usar **SQLGetData** em colunas que estejam na lista de seleção depois que todas as colunas estiverem associadas a **SQLBindCol**. A coluna também deve aparecer após qualquer coluna na qual você já tenha usado **SQLGetData**.  
  
 As funções ODBC que lidam com a movimentação de dados para dentro ou fora de variáveis de programa, como **SQLGetData**, **SQLBindCol**e [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), dão suporte à conversão de tipo de dados implícito. Por exemplo, se um aplicativo associar uma coluna inteira a uma variável de programa de cadeia de caracteres, o driver converterá automaticamente os dados de inteiro em caractere antes de colocá-lo na variável de programa.  
  
 A conversão de dados em aplicativos deve ser minimizada. A menos que a conversão de dados seja necessária ao processamento executado pelo aplicativo, os aplicativos devem associar colunas e parâmetros a variáveis de programa do mesmo tipo de dados. Se for necessário converter os dados entre um tipo e outro, entretanto, será mais eficiente fazer com que o driver execute a conversão do que fazê-lo no aplicativo. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente só transfere dados diretamente dos buffers de rede para as variáveis do aplicativo. A solicitação do driver para fazer a conversão dos dados obriga o driver a armazenar em buffer os dados e os ciclos de CPU de uso para convertê-los.  
  
 As variáveis de programa devem ser grandes o suficiente para manter os dados transferidos de uma coluna, exceto os dados de **Text**, **ntext**e **Image** . Se um aplicativo tentar recuperar os dados do conjunto de resultados e colocá-los em uma variável pequena demais para retê-los, o driver gerará um aviso. Isso obriga o driver a alocar memória para a mensagem, e o driver e o aplicativo têm de gastar ciclos de CPU processando a mensagem e manipulando o erro. O aplicativo deve alocar uma variável grande o suficiente para reter os dados que estão sendo recuperados ou usar a função SUBSTRING na lista de seleção para reduzir o tamanho da coluna no conjunto de resultados.  
  
 É necessário ter cuidado ao usar SQL_C_DEFAULT para especificar o tipo da variável C. SQL_C_DEFAULT especifica que o tipo da variável C corresponde ao tipo de dados SQL da coluna ou parâmetro. Se SQL_C_DEFAULT for especificado para uma coluna **ntext**, **nchar**ou **nvarchar** , os dados Unicode serão retornados para o aplicativo. Isso poderá causar vários problemas se o aplicativo não foi codificado para manipular dados Unicode. Os mesmos tipos de problemas podem ocorrer com o tipo de dados **uniqueidentifier** (SQL_GUID).  
  
 dados de **Text**, **ntext**e **Image** normalmente são muito grandes para caber em uma única variável de programa e geralmente são processados com **SQLGetData** em vez de **SQLBindCol**. Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client é otimizado para não transmitir os dados para colunas **Text**, **ntext**ou **Image** não associadas no momento em que a linha é buscada. Os dados **Text**, **ntext**ou **Image** não são realmente recuperados do servidor até que o aplicativo emita **SQLGetData** para a coluna.  
  
 Essa otimização pode ser aplicada a aplicativos para que nenhum dado de **Text**, **ntext**ou **Image** seja exibido enquanto um usuário estiver rolando para cima e abaixando um cursor. Depois que o usuário seleciona uma linha, o aplicativo pode chamar **SQLGetData** para recuperar os dados **Text**, **ntext**ou **Image** . Isso salva a transmissão dos dados **Text**, **ntext**ou **Image** para qualquer uma das linhas que o usuário não seleciona e pode salvar a transmissão de grandes quantidades de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Processando resultados &#40;&#41;ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
