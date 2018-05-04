---
title: Usando buffer adaptável | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32360b15802e9c06f25ec1f4227130705cf4e2bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-adaptive-buffering"></a>Usando buffer adaptável
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O buffer adaptável é criado para recuperar qualquer tipo de dados de valor grande sem a sobrecarga de cursores de servidor. Aplicativos podem usar o recurso de buffer adaptável com todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que são suportados pelo driver.  
  
 Normalmente, quando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] executa uma consulta, o driver recupera todos os resultados do servidor na memória do aplicativo. Embora esta abordagem minimize o consumo de recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ela pode lançar um OutOfMemoryError no aplicativo de JDBC para as consultas que geram resultados muito grandes.  
  
 Para permitir que aplicativos administrem resultados muito grandes, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece um buffer adaptável. Com buffer adaptável, o driver recupera os resultados de execução de instrução da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como o aplicativo precisa deles, e não tudo de uma vez. O driver também descarta os resultados assim que o aplicativo já não os pode acessar. Veja a seguir alguns exemplos em que o buffer adaptável pode ser útil:  
  
-   **A consulta produz um conjunto de resultados muito grande:** o aplicativo pode executar uma instrução SELECT que produz mais linhas do que o aplicativo pode armazenar na memória. Em versões anteriores, o aplicativo tinha que usar um cursor de servidor para evitar um OutOfMemoryError. O buffer adaptável permite fazer uma passagem somente avanço somente leitura de um conjunto de resultados arbitrariamente grande sem exigir um cursor de servidor.  
  
-   **A consulta gera colunas muito grandes**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**colunas ou**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**valores de parâmetro OUT:** O aplicativo pode recuperar um único valor (coluna ou parâmetro OUT) que é muito grande para caber inteiramente na memória do aplicativo. O buffer adaptável permite que o aplicativo cliente recupere esse valor como um fluxo usando o getAsciiStream, o getBinaryStream ou os métodos getCharacterStream. O aplicativo recupera o valor da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como ele lê o fluxo.  
  
> [!NOTE]  
>  Com buffer adaptável, o JDBC Driver armazena em buffer somente a quantidade de dados que precisa. O driver não fornece nenhum método público para controlar ou limitar o tamanho do buffer.  
  
## <a name="setting-adaptive-buffering"></a>Definindo buffer adaptável  
 Começando com o driver JDBC versão 2.0, o comportamento padrão do driver é "**adaptável**". Em outras palavras, para obter o comportamento de buffer adaptável, o aplicativo não precisa solicitar o comportamento adaptável explicitamente. Na versão 1.2, no entanto, o modo de buffer era "**completo**" por padrão e o aplicativo precisava solicitar o modo de buffer adaptável explicitamente.  
  
 Há três maneiras de um aplicativo solicitar que a execução de instrução use buffer adaptável:  
  
-   O aplicativo pode definir a propriedade de conexão **responseBuffering** como "adaptável". Para obter mais informações sobre como definir as propriedades de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
-   O aplicativo pode usar o [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) método o [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto para definir a modo para todas as conexões criadas por aquele de buffer de resposta [ SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.  
  
-   O aplicativo pode usar o [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe para definir o modo de buffer de um objeto de instrução específico de resposta.  
  
 Ao usar o JDBC Driver versão 1.2, os aplicativos precisaram converter o objeto de instrução para um [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe para usar o [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método. Exemplos de código a [lendo amostras de dados grandes](../../connect/jdbc/reading-large-data-sample.md) e [leitura de dados grandes com exemplo de procedimentos armazenados](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) demonstram este uso antigo.  
  
 No entanto, o driver JDBC versão 2.0, aplicativos podem usar o [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) método e o [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) método para acessar a funcionalidade específica do fornecedor sem qualquer pressuposição sobre a hierarquia de classe de implementação. Por exemplo de código, consulte o [amostra de dados grande atualização](../../connect/jdbc/updating-large-data-sample.md) tópico.  
  
## <a name="retrieving-large-data-with-adaptive-buffering"></a>Recuperando dados grandes com buffer adaptável  
 Quando valores grandes são lidos uma vez usando get\<tipo > métodos de fluxo e as colunas ResultSet e os parâmetros CallableStatement OUT são acessados na ordem retornada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o buffer adaptável minimiza o aplicativo uso de memória ao processar os resultados. Ao usar buffer adaptável:  
  
-   Get\<tipo > fluxo métodos definidos no [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes retornam fluxos somente leitura por padrão, embora os fluxos possam ser reiniciados se marcado pelo aplicativo. Se o aplicativo deseja `reset` o fluxo, ele tem que chamar o `mark` método naquele fluxo pela primeira vez.  
  
-   Get\<tipo > fluxo métodos definidos no [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) e [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) classes retornam fluxos que sempre podem ser reposicionados para a posição de início do fluxo sem chamar o `mark` método.  
  
 Quando o aplicativo usar buffer adaptável, os valores recuperados pelos get\<tipo > métodos fluxo só podem ser recuperados uma vez. Se você tentar chamar qualquer get\<tipo > método na mesma coluna ou parâmetro depois de chamar get\<tipo > método Stream do mesmo objeto, uma exceção será lançado com a mensagem, "os dados foram acessados e não estão disponíveis para este coluna ou parâmetro".  
  
> [!NOTE]
> Uma chamada para ResultSet.close() no meio de um conjunto de resultados de processamento requer o Microsoft JDBC Driver para SQL Server ler e descartar todos os pacotes restantes. Isso pode levar tempo substancial se a consulta retornou um grande conjunto de dados e, especialmente se a conexão de rede estiver lenta.     
  
## <a name="guidelines-for-using-adaptive-buffering"></a>Diretrizes para usar buffer adaptável  
 Os desenvolvedores devem seguir estas diretrizes importantes para minimizar o uso de memória pelo aplicativo:  
  
-   Evite usar a propriedade de cadeia de caracteres de conexão **selectMethod = cursor** permitir que o aplicativo processe um resultado muito grande definido. O recurso de buffer adaptável permite que os aplicativos processem conjuntos de resultados somente encaminhamento e somente leitura muito grandes sem usar um cursor de servidor. Observe que, quando você definir **selectMethod = cursor**, todos os somente encaminhamento, conjuntos de resultados somente leitura produzidos por essa conexão são afetados. Em outras palavras, se seu aplicativo habitualmente conjuntos de resultados curtos com algumas linhas, criar, ler e fechar um cursor de servidor para cada conjunto de resultados usará mais recursos do lado do cliente e do lado do servidor que é o caso em que o  **selectMethod** não está definido como **cursor**.  
  
-   Leia texto grande ou valores binários como fluxos usando o getAsciiStream, o getBinaryStream ou os métodos getCharacterStream em vez da getBlob ou os métodos getClob. A partir da versão 1.2, o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe fornece novos get\<tipo > fluxo métodos para essa finalidade.  
  
-   Certifique-se de que colunas com valores potencialmente grandes são colocadas por último na lista de colunas em uma instrução SELECT e que get\<tipo > fluxo métodos do [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) são usadas para acessar as colunas a ordem em que eles são selecionados.  
  
-   Certifique-se de que os parâmetros OUT com valores potencialmente grandes são declarados por último na lista de parâmetros no SQL usada para criar o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Além disso, certifique-se de que o get\<tipo > métodos de fluxo de [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) são usadas para acessar os parâmetros OUT na ordem em que eles são declarados.  
  
-   Evite executar mais de uma instrução na mesma conexão simultaneamente. Executar outra instrução antes de processar os resultados da instrução anterior pode fazer os resultados não processados serem armazenados em buffer na memória do aplicativo.  
  
-   Há alguns casos em que usar **selectMethod = cursor** em vez de **responseBuffering = adaptive** seria mais benéfico, por exemplo:  
  
    -   Se seu aplicativo processa um somente avanço, somente leitura conjunto de resultados lentamente, como ler cada linha depois de alguma entrada do usuário, usando **selectMethod = cursor** em vez de **responseBuffering = adaptive** pode ajudar a reduzir o uso de recursos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Se seu aplicativo processar dois ou conjuntos de resultados mais somente avanço, somente leitura ao mesmo tempo em que a mesma conexão, usando **selectMethod = cursor** em vez de **responseBuffering = adaptive** pode ajudar Reduza a memória exigida pelo driver para processar estes conjuntos de resultados.  
  
     Em ambos os casos, você precisa considerar a sobrecarga de criar, ler e fechar os cursores de servidor.  
  
 Além disso, a lista a seguir fornece algumas recomendações para conjuntos de resultados roláveis e atualizáveis somente avanço:  
  
-   Para conjuntos de resultados roláveis, ao buscar um bloco de linhas o driver sempre lê na memória o número de linhas indicado pelo [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto, mesmo quando o buffer adaptável está habilitado. Se rolar causar um OutOfMemoryError, você pode reduzir o número de linhas buscadas chamando o [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto para definir o tamanho da busca como um número menor de linhas até mesmo 1 linha, se necessário. Se isso não impede que um OutOfMemoryError, evite incluir colunas muito grandes em conjuntos de resultados roláveis.  
  
-   Para conjuntos de resultados atualizáveis de somente avanço, ao buscar um bloco de linhas o driver geralmente lê na memória o número de linhas indicado pelo [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto mesmo quando o buffer adaptável está habilitado na conexão. Se chamar o [próximo](../../connect/jdbc/reference/next-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) resultados de objeto em um OutOfMemoryError, você pode reduzir o número de linhas buscadas chamando o [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método de [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto para definir o tamanho da busca como um número menor de linhas, até mesmo 1 linha, se necessário. Você também pode forçar o driver não armazenar em buffer nenhuma linha chamando o [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) do objeto com "**adaptável**" parâmetro antes de execução da instrução. Como o conjunto de resultados não é rolável, se o aplicativo acessa um valor de coluna grande usando um get\<tipo > métodos de fluxo, o driver descartará o valor assim que o aplicativo lê-lo, assim como faz para o somente de avanço somente leitura conjuntos de resultados.  
  
## <a name="see-also"></a>Consulte também  
 [Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
