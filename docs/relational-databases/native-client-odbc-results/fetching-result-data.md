---
title: Buscando dados de resultado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-results
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f1c828f3e63e3167a0685f450e318055a9b71fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-result-data"></a>Buscando dados de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um aplicativo ODBC tem três opções para buscar dados de resultados.  
  
 A primeira opção é baseada no [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md). Antes de buscar o resultado definido, o aplicativo usa **SQLBindCol** para associar cada coluna no conjunto de resultados para uma variável de programa. Depois que as colunas de associação, o driver transfere os dados da linha atual em variáveis associados ao resultado colunas de conjunto de cada vez que o aplicativo chama **SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). O driver manipulará as conversões de dados se a coluna do conjunto de resultados e a variável de programa tiverem tipos de dados diferentes. Se o aplicativo tiver SQL_ATTR_ROW_ARRAY_SIZE definido maior que 1, ele pode associar colunas de resultados a matrizes de variáveis, que serão preenchidas em cada chamada para **SQLFetchScroll**.  
  
 A segunda opção é baseada no [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). O aplicativo não usar **SQLBindCol** vincular resultado colunas do conjunto de variáveis de programa. Após cada chamada para **SQLFetch**, o aplicativo chama **SQLGetData** uma vez para cada coluna no resultado definido. **SQLGetData** instrui o driver a transferir dados de uma coluna do conjunto de resultados específicos para uma variável de programa específico e especifica os tipos de dados da coluna e variável. Isso permitirá que o driver converta os dados se a coluna de resultados e a variável de programa tiverem tipos de dados diferentes. **Texto**, **ntext**, e **imagem** colunas normalmente são grandes demais para caber em uma variável de programa, mas ainda podem ser recuperadas usando **SQLGetData**. Se o **texto**, **ntext**, ou **imagem** dados da coluna de resultados são maiores do que a variável de programa, **SQLGetData** retorna SQL_SUCCESS_ WITH_INFO e SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita). As chamadas sucessivas para **SQLGetData** retornarão partes sucessivas do **texto** ou **imagem** dados. Quando é atingido o fim dos dados, **SQLGetData** retorna SQL_SUCCESS. Cada busca retornará um conjunto de linhas se SQL_ATTR_ROW_ARRAY_SIZE for maior do que 1. Antes de usar **SQLGetData**, primeiro você deve usar **SQLSetPos** para especificar uma linha específica no conjunto de linhas como a linha atual.  
  
 A terceira opção é usar uma combinação de **SQLBindCol** e **SQLGetData**. Um aplicativo poderia, por exemplo, associe as dez primeiras colunas de um conjunto de resultados e, em seguida, em cada busca, chamar **SQLGetData** três vezes para recuperar os dados de três colunas não associadas. Isso normalmente seria usado quando um conjunto de resultados contém um ou mais **texto** ou **imagem** colunas.  
  
 Dependendo das opções de cursor para o conjunto de resultados, um aplicativo também pode usar as opções de rolagem de **SQLFetchScroll** para rolar o conjunto de resultados.  
  
 O uso excessivo de **SQLBindCol** para associar um resultado de conjunto de colunas para uma variável de programa é caro porque **SQLBindCol** faz com que um driver ODBC alocar memória. Quando você associa uma coluna de resultado a uma variável, essa associação permanece em vigor até que você chamar [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar o identificador de instrução ou chamada [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com *fOption* definido como SQL_UNBIND. As associações não são desfeitas automaticamente quando a instrução é concluída.  
  
 Essa lógica permite lidar efetivamente com a execução da mesma instrução SELECT várias vezes com parâmetros diferentes. Como o conjunto de resultados mantém a mesma estrutura, você pode associar o conjunto de resultados de uma vez, processar todas as instruções SELECT, em seguida, chame **SQLFreeStmt** com *fOption* definido como SQL_UNBIND após a última execução. Você não deve chamar **SQLBindCol** para associar as colunas em um conjunto de resultados sem primeiro chamar **SQLFreeStmt** com *fOption* definido como SQL_UNBIND para liberar quaisquer associações anteriores.  
  
 Ao usar **SQLBindCol**, você pode fazer a associação por linha ou. A associação por linha é um pouco mais rápida do que a associação por coluna.  
  
 Você pode usar **SQLGetData** para recuperar dados em uma base por coluna em vez de associação de resultado conjunto de colunas usando **SQLBindCol**. Se um conjunto de resultados contém apenas algumas linhas, usando **SQLGetData** em vez de **SQLBindCol** mais rápido; caso contrário, **SQLBindCol** oferece o melhor desempenho. Se você não colocar sempre os dados no mesmo conjunto de variáveis, você deve usar **SQLGetData** em vez de reassociar constantemente. Você só pode usar **SQLGetData** em colunas que estão na lista de seleção após todas as colunas são associadas com **SQLBindCol**. A coluna também deve aparecer após todas as colunas em que você já usou **SQLGetData**.  
  
 As funções ODBC que lidam com a movimentação de dados para ou de variáveis de programa, como **SQLGetData**, **SQLBindCol**, e [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), oferece suporte ao tipo de dados implícitas conversão. Por exemplo, se um aplicativo associar uma coluna inteira a uma variável de programa de cadeia de caracteres, o driver converterá automaticamente os dados de inteiro em caractere antes de colocá-lo na variável de programa.  
  
 A conversão de dados em aplicativos deve ser minimizada. A menos que a conversão de dados seja necessária ao processamento executado pelo aplicativo, os aplicativos devem associar colunas e parâmetros a variáveis de programa do mesmo tipo de dados. Se for necessário converter os dados entre um tipo e outro, entretanto, será mais eficiente fazer com que o driver execute a conversão do que fazê-lo no aplicativo. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente só transfere dados diretamente dos buffers de rede para as variáveis do aplicativo. A solicitação do driver para fazer a conversão dos dados obriga o driver a armazenar em buffer os dados e os ciclos de CPU de uso para convertê-los.  
  
 Variáveis do programa devem ser grandes o suficiente para reter os dados transferidos de uma coluna, exceto para **texto**, **ntext**, e **imagem** dados. Se um aplicativo tentar recuperar os dados do conjunto de resultados e colocá-los em uma variável pequena demais para retê-los, o driver gerará um aviso. Isso obriga o driver a alocar memória para a mensagem, e o driver e o aplicativo têm de gastar ciclos de CPU processando a mensagem e manipulando o erro. O aplicativo deve alocar uma variável grande o suficiente para reter os dados que estão sendo recuperados ou usar a função SUBSTRING na lista de seleção para reduzir o tamanho da coluna no conjunto de resultados.  
  
 É necessário ter cuidado ao usar SQL_C_DEFAULT para especificar o tipo da variável C. SQL_C_DEFAULT especifica que o tipo da variável C corresponde ao tipo de dados SQL da coluna ou parâmetro. Se SQL_C_DEFAULT for especificado para um **ntext**, **nchar**, ou **nvarchar** coluna, dados Unicode são retornados ao aplicativo. Isso poderá causar vários problemas se o aplicativo não foi codificado para manipular dados Unicode. Os mesmos tipos de problemas podem ocorrer com o **uniqueidentifier** tipo de dados (SQL_GUID).  
  
 **texto**, **ntext**, e **imagem** dados geralmente é muito grandes para caber em uma única variável de programa e normalmente são processados com **SQLGetData** em vez de **SQLBindCol**. Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client é otimizado para não transmitir os dados para desassociada **texto**, **ntext**, ou **imagem** colunas do hora em que a linha é buscada. O **texto**, **ntext**, ou **imagem** dados não são realmente recuperados do servidor até que o aplicativo não emite **SQLGetData** para a coluna.  
  
 Essa otimização pode ser aplicada a aplicativos para que nenhum **texto**, **ntext**, ou **imagem** dados são exibidos enquanto um usuário está rolando um cursor para cima e. Depois que o usuário seleciona uma linha, o aplicativo pode chamar **SQLGetData** para recuperar o **texto**, **ntext**, ou **imagem** dados. Isso economiza transmitir o **texto**, **ntext**, ou **imagem** dados para qualquer uma das linhas, o usuário não seleciona e pode salvar a transmissão de quantidades muito grandes de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Processando resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
