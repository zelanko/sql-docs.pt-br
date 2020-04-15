---
title: Buscar dados de resultados | Microsoft Docs
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
ms.openlocfilehash: e1d9fdfcd7bcc4f86afacc75dff5b40b77bb7b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304594"
---
# <a name="fetching-result-data"></a>Buscando dados de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um aplicativo ODBC tem três opções para buscar dados de resultados.  
  
 A primeira opção é baseada no [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Antes de buscar o conjunto de resultados, o aplicativo usa **SQLBindCol** para vincular cada coluna no resultado definido a uma variável de programa. Depois que as colunas foram vinculadas, o driver transfere os dados da linha atual para as variáveis vinculadas às colunas definidas de resultado cada vez que o aplicativo chama **SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). O driver manipulará as conversões de dados se a coluna do conjunto de resultados e a variável de programa tiverem tipos de dados diferentes. Se o aplicativo tiver SQL_ATTR_ROW_ARRAY_SIZE conjunto maior que 1, ele pode vincular colunas de resultado a matrizes de variáveis, que serão todas preenchidas em cada chamada para **SQLFetchScroll**.  
  
 A segunda opção é baseada no [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). O aplicativo não usa **SQLBindCol** para vincular colunas de conjunto de resultados a variáveis do programa. Após cada chamada para **SQLFetch,** o aplicativo chama **SQLGetData** uma vez para cada coluna no conjunto de resultados. **O SQLGetData** instrui o driver a transferir dados de uma coluna definida de resultados específico para uma variável de programa específica e especifica os tipos de dados da coluna e da variável. Isso permitirá que o driver converta os dados se a coluna de resultados e a variável de programa tiverem tipos de dados diferentes. As colunas **de texto,** **ntext**e **imagem** são tipicamente grandes demais para se encaixar em uma variável de programa, mas ainda podem ser recuperadas usando **SQLGetData**. Se o **texto,** **ntext**ou dados **de imagem** na coluna de resultado for maior que a variável de programa, **o SQLGetData** retorna SQL_SUCCESS_WITH_INFO e sQLSTATE 01004 (dados de seqüência, truncados à direita). Chamadas sucessivas para **SQLGetData** retornam recortes sucessivos dos dados de **texto** ou **imagem.** Quando o fim dos dados é alcançado, o **SQLGetData** retorna SQL_SUCCESS. Cada busca retornará um conjunto de linhas se SQL_ATTR_ROW_ARRAY_SIZE for maior do que 1. Antes de usar **SQLGetData,** você deve primeiro usar **SQLSetPos** para especificar uma linha específica dentro do conjunto de linhas como a linha atual.  
  
 A terceira opção é usar uma mistura de **SQLBindCol** e **SQLGetData**. Um aplicativo poderia, por exemplo, vincular as dez primeiras colunas de um conjunto de resultados e, em seguida, em cada busca, chamar **SQLGetData** três vezes para recuperar os dados de três colunas não vinculadas. Isso normalmente seria usado quando um conjunto de resultados contiver uma ou mais colunas **de texto** ou **imagem.**  
  
 Dependendo das opções de cursor definidas para o conjunto de resultados, um aplicativo também pode usar as opções de rolagem do **SQLFetchScroll** para rolar ao redor do conjunto de resultados.  
  
 O uso excessivo do **SQLBindCol** para vincular uma coluna de conjunto de resultados a uma variável de programa é caro porque **o SQLBindCol** faz com que um driver ODBC aloque a memória. Quando você vincula uma coluna de resultado a uma variável, essa vinculação permanece em vigor até que você ligue para [o SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar o cabo de declaração ou ligue para [o SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com *fOption* definido para SQL_UNBIND. As associações não são desfeitas automaticamente quando a instrução é concluída.  
  
 Essa lógica permite lidar efetivamente com a execução da mesma instrução SELECT várias vezes com parâmetros diferentes. Como o conjunto de resultados mantém a mesma estrutura, você pode vincular o conjunto de resultados uma vez, processar todas as instruções SELECT e, em seguida, chamar **SQLFreeStmt** com *fOption* definido para SQL_UNBIND após a última execução. Você não deve chamar **sqlBindCol** para vincular as colunas em um conjunto de resultados sem antes chamar **SQLFreeStmt** com *fOption* definido para SQL_UNBIND para liberar quaisquer vinculações anteriores.  
  
 Ao usar **o SQLBindCol,** você pode fazer a vinculação em termos de linha ou de coluna. A associação por linha é um pouco mais rápida do que a associação por coluna.  
  
 Você pode usar **o SQLGetData** para recuperar dados em uma base de coluna por coluna, em vez de colunas de conjunto de resultados vinculativos usando **SQLBindCol**. Se um conjunto de resultados contiver apenas algumas linhas, o uso **do SQLGetData** em vez do **SQLBindCol** é mais rápido; caso contrário, **SQLBindCol** dá o melhor desempenho. Se você nem sempre colocar os dados no mesmo conjunto de variáveis, você deve usar **SQLGetData** em vez de revincular constantemente. Você só pode usar **SQLGetData** em colunas que estão na lista de seleção depois que todas as colunas estiverem vinculadas ao **SQLBindCol**. A coluna também deve aparecer após quaisquer colunas nas quais você já tenha usado **SQLGetData**.  
  
 As funções ODBC que lidam com a movimentação de dados dentro ou fora das variáveis do programa, como **SQLGetData,** **SQLBindCol**e [SQLBindParameter,](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)suportam a conversão implícita do tipo de dados. Por exemplo, se um aplicativo associar uma coluna inteira a uma variável de programa de cadeia de caracteres, o driver converterá automaticamente os dados de inteiro em caractere antes de colocá-lo na variável de programa.  
  
 A conversão de dados em aplicativos deve ser minimizada. A menos que a conversão de dados seja necessária ao processamento executado pelo aplicativo, os aplicativos devem associar colunas e parâmetros a variáveis de programa do mesmo tipo de dados. Se for necessário converter os dados entre um tipo e outro, entretanto, será mais eficiente fazer com que o driver execute a conversão do que fazê-lo no aplicativo. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente só transfere dados diretamente dos buffers de rede para as variáveis do aplicativo. A solicitação do driver para fazer a conversão dos dados obriga o driver a armazenar em buffer os dados e os ciclos de CPU de uso para convertê-los.  
  
 As variáveis do programa devem ser grandes o suficiente para conter dados transferidos de uma coluna, exceto **texto,** **ntext**e dados **de imagem.** Se um aplicativo tentar recuperar os dados do conjunto de resultados e colocá-los em uma variável pequena demais para retê-los, o driver gerará um aviso. Isso obriga o driver a alocar memória para a mensagem, e o driver e o aplicativo têm de gastar ciclos de CPU processando a mensagem e manipulando o erro. O aplicativo deve alocar uma variável grande o suficiente para reter os dados que estão sendo recuperados ou usar a função SUBSTRING na lista de seleção para reduzir o tamanho da coluna no conjunto de resultados.  
  
 É necessário ter cuidado ao usar SQL_C_DEFAULT para especificar o tipo da variável C. SQL_C_DEFAULT especifica que o tipo da variável C corresponde ao tipo de dados SQL da coluna ou parâmetro. Se SQL_C_DEFAULT for especificado para uma coluna **ntext**, **nchar**ou **nvarchar,** os dados unicode serão devolvidos ao aplicativo. Isso poderá causar vários problemas se o aplicativo não foi codificado para manipular dados Unicode. Os mesmos tipos de problemas podem ocorrer com o tipo de dados **uniqueidentifier** (SQL_GUID).  
  
 **texto,** **ntext**e dados **de imagem** são tipicamente muito grandes para se encaixar em uma única variável de programa, e geralmente são processados com **SQLGetData** em vez de **SQLBindCol**. Ao usar cursores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de servidor, o driver ODBC do Cliente Nativo é otimizado para não transmitir os dados para **texto**sem vínculo, **ntext**ou colunas **de imagem** no momento em que a linha é buscada. Os dados **de texto,** **ntext**ou **imagem** não são realmente recuperados do servidor até que o aplicativo emita **SQLGetData** para a coluna.  
  
 Essa otimização pode ser aplicada aos aplicativos para que nenhum **texto,** **ntext**ou dados **de imagem** sejam exibidos enquanto um usuário está rolando para cima e para baixo em um cursor. Depois que o usuário seleciona uma linha, o aplicativo pode chamar **SQLGetData** para recuperar os dados **de texto,** **ntext**ou **imagem.** Isso salva a transmissão de **dados de texto,** **ntext**ou **imagem** para qualquer uma das linhas que o usuário não seleciona e pode salvar a transmissão de quantidades muito grandes de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Resultados de processamento &#40;&#41;Da ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
