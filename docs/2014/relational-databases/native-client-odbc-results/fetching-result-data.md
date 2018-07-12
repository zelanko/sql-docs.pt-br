---
title: Buscando dados de resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2228bb8fcbc7237fabfb0239c62f512b9a223d28
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408205"
---
# <a name="fetching-result-data"></a>Buscando dados de resultados
  Um aplicativo ODBC tem três opções para buscar dados de resultados.  
  
 A primeira opção se baseia [SQLBindCol](../native-client-odbc-api/sqlbindcol.md). Antes de buscar o resultado definido, o aplicativo usa **SQLBindCol** para associar cada coluna no conjunto de resultados para uma variável de programa. Depois que as colunas de associação, o driver transfere os dados da linha atual para as variáveis associados às colunas de resultados conjunto cada vez o aplicativo chama **SQLFetch** ou [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md). O driver manipulará as conversões de dados se a coluna do conjunto de resultados e a variável de programa tiverem tipos de dados diferentes. Se o aplicativo tiver SQL_ATTR_ROW_ARRAY_SIZE definido maior que 1, ele pode associar colunas de resultados a matrizes de variáveis, que serão todas preenchidas em cada chamada para **SQLFetchScroll**.  
  
 A segunda opção se baseia [SQLGetData](../native-client-odbc-api/sqlgetdata.md). O aplicativo não usa **SQLBindCol** associar o resultado de colunas do conjunto para variáveis de programa. Após cada chamada para **SQLFetch**, o aplicativo chama **SQLGetData** uma vez para cada coluna no resultado definido. **SQLGetData** instrui o driver a transferir dados de uma coluna do conjunto de resultados específico a uma variável de programa específico e especifica os tipos de dados da coluna e variável. Isso permitirá que o driver converta os dados se a coluna de resultados e a variável de programa tiverem tipos de dados diferentes. **Texto**, **ntext**, e **imagem** colunas normalmente são grandes demais para caber em uma variável de programa, mas ainda podem ser recuperadas usando **SQLGetData**. Se o **texto**, **ntext**, ou **imagem** dados na coluna de resultado for maiores que a variável de programa **SQLGetData** retorna SQL_SUCCESS_ WITH_INFO e SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita). Chamadas sucessivas à **SQLGetData** retornarão partes sucessivas da **texto** ou **imagem** dados. Quando é atingido o final dos dados, **SQLGetData** retorna SQL_SUCCESS. Cada busca retornará um conjunto de linhas se SQL_ATTR_ROW_ARRAY_SIZE for maior do que 1. Antes de usar **SQLGetData**, primeiro você deve usar **SQLSetPos** para especificar uma linha específica dentro do conjunto de linhas como a linha atual.  
  
 A terceira opção é usar uma combinação de **SQLBindCol** e **SQLGetData**. Um aplicativo poderia, por exemplo, associar as primeiras dez colunas de um conjunto de resultados e, em cada busca, chame **SQLGetData** três vezes para recuperar os dados de três colunas não associadas. Isso normalmente seria usado quando um conjunto de resultados contém um ou mais **texto** ou **imagem** colunas.  
  
 Dependendo das opções de cursor definido para o conjunto de resultados, um aplicativo também pode usar as opções de rolagem do **SQLFetchScroll** para rolar ao redor do conjunto de resultados.  
  
 Uso excessivo de **SQLBindCol** para associar um resultado de coluna do conjunto para uma variável de programa é cara porque **SQLBindCol** faz com que um driver ODBC alocar memória. Quando você associa uma coluna de resultado a uma variável, essa associação permanece em vigor até você chamar [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) para liberar o identificador de instrução ou chamar [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) com *fOption* definido como SQL_UNBIND. As associações não são desfeitas automaticamente quando a instrução é concluída.  
  
 Essa lógica permite lidar efetivamente com a execução da mesma instrução SELECT várias vezes com parâmetros diferentes. Como o conjunto de resultados mantém a mesma estrutura, você pode associar o conjunto de resultados de uma vez, processar todas as instruções SELECT, em seguida, chame **SQLFreeStmt** com *fOption* definido como SQL_UNBIND após a última execução. Você não deve chamar **SQLBindCol** para associar as colunas em um conjunto de resultados sem primeiro chamar **SQLFreeStmt** com *fOption* definido como SQL_UNBIND para liberar quaisquer associações anteriores.  
  
 Ao usar **SQLBindCol**, você pode fazer a associação por linha ou coluna. A associação por linha é um pouco mais rápida do que a associação por coluna.  
  
 Você pode usar **SQLGetData** para recuperar dados em uma base por coluna em vez de associar um resultado conjunto de colunas usando **SQLBindCol**. Se um conjunto de resultados contém apenas algumas linhas, usando **SQLGetData** em vez de **SQLBindCol** é o mais rápido; caso contrário, **SQLBindCol** oferece o melhor desempenho. Se você nem sempre coloca os dados no mesmo conjunto de variáveis, você deve usar **SQLGetData** em vez de reassociar constantemente. Você só pode usar **SQLGetData** nas colunas que estão na lista de seleção depois que todas as colunas estão associadas **SQLBindCol**. A coluna também deve aparecer depois de quaisquer colunas em que você já usou **SQLGetData**.  
  
 As funções ODBC que lidam com a movimentação de dados para dentro ou fora de variáveis do programa, tal como **SQLGetData**, **SQLBindCol**, e [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md), suporte ao tipo de dados implícitos conversão. Por exemplo, se um aplicativo associar uma coluna inteira a uma variável de programa de cadeia de caracteres, o driver converterá automaticamente os dados de inteiro em caractere antes de colocá-lo na variável de programa.  
  
 A conversão de dados em aplicativos deve ser minimizada. A menos que a conversão de dados seja necessária ao processamento executado pelo aplicativo, os aplicativos devem associar colunas e parâmetros a variáveis de programa do mesmo tipo de dados. Se for necessário converter os dados entre um tipo e outro, entretanto, será mais eficiente fazer com que o driver execute a conversão do que fazê-lo no aplicativo. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client normalmente só transfere dados diretamente dos buffers de rede para as variáveis do aplicativo. A solicitação do driver para fazer a conversão dos dados obriga o driver a armazenar em buffer os dados e os ciclos de CPU de uso para convertê-los.  
  
 Variáveis de programa devem ser grandes o suficiente para reter os dados transferidos de uma coluna, exceto para **texto**, **ntext**, e **imagem** dados. Se um aplicativo tentar recuperar os dados do conjunto de resultados e colocá-los em uma variável pequena demais para retê-los, o driver gerará um aviso. Isso obriga o driver a alocar memória para a mensagem, e o driver e o aplicativo têm de gastar ciclos de CPU processando a mensagem e manipulando o erro. O aplicativo deve alocar uma variável grande o suficiente para reter os dados que estão sendo recuperados ou usar a função SUBSTRING na lista de seleção para reduzir o tamanho da coluna no conjunto de resultados.  
  
 É necessário ter cuidado ao usar SQL_C_DEFAULT para especificar o tipo da variável C. SQL_C_DEFAULT especifica que o tipo da variável C corresponde ao tipo de dados SQL da coluna ou parâmetro. Se SQL_C_DEFAULT for especificado para um **ntext**, **nchar**, ou **nvarchar** coluna, dados Unicode serão retornados ao aplicativo. Isso poderá causar vários problemas se o aplicativo não foi codificado para manipular dados Unicode. Os mesmos tipos de problemas podem ocorrer com o **uniqueidentifier** tipo de dados (SQL_GUID).  
  
 **texto**, **ntext**, e **imagem** dados normalmente é muito grandes para caber em uma única variável de programa e normalmente são processados com **SQLGetData** em vez de **SQLBindCol**. Ao usar cursores de servidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client é otimizado para não transmitir os dados para desassociada **texto**, **ntext**, ou **imagem** colunas no hora em que a linha é buscada. O **texto**, **ntext**, ou **imagem** dados não são realmente recuperados do servidor até que os problemas de aplicativos **SQLGetData** para o coluna.  
  
 Essa otimização pode ser aplicada a aplicativos, de modo que nenhum **texto**, **ntext**, ou **imagem** dados seja exibidos enquanto um usuário está rolando para cima e para um cursor. Depois que o usuário seleciona uma linha, o aplicativo pode chamar **SQLGetData** para recuperar o **texto**, **ntext**, ou **imagem** dados. Isso salva a transmissão de **texto**, **ntext**, ou **imagem** dados para qualquer uma das linhas, o usuário não seleciona e pode salvar a transmissão de quantidades muito grandes de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Processando resultados &#40;ODBC&#41;](processing-results-odbc.md)  
  
  
