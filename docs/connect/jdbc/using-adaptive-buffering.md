---
title: Usando buffer adaptável | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16ac54c78839df4c5ce911a1258dfa052ac1666c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624995"
---
# <a name="using-adaptive-buffering"></a>Usando buffer adaptável

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O buffer adaptável é criado para recuperar qualquer tipo de dados de valor grande sem a sobrecarga de cursores de servidor. Aplicativos podem usar o recurso de utilização de buffer adaptável com todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compatíveis com o driver.

Normalmente, quando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] executa uma consulta, o driver recupera todos os resultados do servidor na memória do aplicativo. Embora esta abordagem minimize o consumo de recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ela pode lançar um OutOfMemoryError no aplicativo de JDBC para as consultas que geram resultados muito grandes.

Para permitir que aplicativos administrem resultados muito grandes, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece um buffer adaptável. Com buffer adaptável, o driver recupera os resultados da execução da instrução do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à medida que o aplicativo precisa deles, em vez de todos de uma vez. O driver também descarta os resultados assim que o aplicativo já não os pode acessar. Veja a seguir alguns exemplos em que o buffer adaptável pode ser útil:

- **A consulta produz um conjunto de resultados muito grande:** o aplicativo pode executar uma instrução SELECT que produz mais linhas do que o aplicativo pode armazenar na memória. Em versões anteriores, o aplicativo precisava usar um cursor de servidor para evitar um OutOfMemoryError. O buffer adaptável permite fazer uma passagem somente avanço somente leitura de um conjunto de resultados arbitrariamente grande sem exigir um cursor de servidor.

- **A consulta gera colunas muito grandes** [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) **colunas ou** [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) **os valores de parâmetro:** O aplicativo pode recuperar um valor único (coluna ou parâmetro OUT) que é muito grande para caber inteiramente na memória do aplicativo. Buffer adaptável permite que o aplicativo cliente recupere esse valor como um fluxo, usando o getAsciiStream, o getBinaryStream ou os métodos getCharacterStream. O aplicativo recupera o valor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à medida que o lê o fluxo.

> [!NOTE]  
> Com buffer adaptável, o JDBC Driver armazena em buffer somente a quantidade de dados que precisa. O driver não fornece nenhum método público para controlar ou limitar o tamanho do buffer.

## <a name="setting-adaptive-buffering"></a>Definindo buffer adaptável

Do driver JDBC versão 2.0 em diante, o comportamento padrão do driver é "**adaptável**". Em outras palavras, para obter o comportamento de buffer adaptável, o aplicativo não precisa solicitar o comportamento adaptável explicitamente. No entanto, na versão 1.2 o modo padrão de buffer era "**full**" e o aplicativo precisava solicitar explicitamente o modo de buffer adaptável.

Há três maneiras de um aplicativo solicitar que a execução de instrução use buffer adaptável:

- O aplicativo pode definir a propriedade de conexão **responseBuffering** como "adaptável". Para obter mais informações sobre como definir as propriedades de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).

- O aplicativo pode usar o método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) do objeto [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) para definir o modo de buffer de resposta para todas as conexões criadas por aquele objeto [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).

- O aplicativo pode usar o método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para definir o modo de buffer de resposta para um objeto de instrução específico.

Ao usar o JDBC Driver versão 1.2, os aplicativos precisaram converter o objeto de instrução para uma classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para usar o método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md). Exemplos de código a [lendo amostras de dados grandes](../../connect/jdbc/reading-large-data-sample.md) e [leitura de dados grandes com exemplo de procedimentos armazenados](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) demonstram este uso antigo.

Porém, com o driver JDBC versão 2.0, os aplicativos podem usar o método [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e o método [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) para acessar a funcionalidade específica do fornecedor sem qualquer pressuposição sobre a hierarquia de classe de implementação. Por exemplo de código, consulte o [atualizando exemplo de dados grandes](../../connect/jdbc/updating-large-data-sample.md) tópico.

## <a name="retrieving-large-data-with-adaptive-buffering"></a>Recuperando dados grandes com buffer adaptável

Quando valores grandes são lidos uma vez usando os métodos get\<Type>Stream e as colunas ResultSet e os parâmetros CallableStatement OUT são acessados na ordem retornada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o buffer adaptável minimiza o uso de memória do aplicativo ao processar os resultados. Ao usar buffer adaptável:

- Os métodos get\<Type>Stream definidos nas classes [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) retornam fluxos somente leitura por padrão, embora os fluxos possam ser reiniciados se estiver marcado pelo aplicativo. Se o aplicativo desejar `reset` o fluxo, primeiro precisará chamar o método `mark` naquele fluxo.

- Os métodos get\<Type>Stream definidos nas classes [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) e [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) retornam fluxos que sempre podem ser reposicionados para a posição de início do fluxo sem chamar o método `mark`.

Quando o aplicativo usar buffer adaptável, os valores recuperados pelos métodos get\<Type>Stream somente poderão ser recuperados uma vez. Se você tentar chamar qualquer método get\<Type> na mesma coluna ou parâmetro depois de chamar o método get\<Type>Stream do mesmo objeto, uma exceção será lançada com a mensagem "Os dados foram acessados e não estão disponíveis para esta coluna ou parâmetro".

> [!NOTE]
> Uma chamada para ResultSet.close() no meio de um conjunto de resultados de processamento exige que o Microsoft JDBC Driver para SQL Server ler e descartar todos os pacotes restantes. Se a consulta retornou um grande conjunto de dados e, especialmente se a conexão de rede estiver lenta, isso pode levar um tempo considerável.

## <a name="guidelines-for-using-adaptive-buffering"></a>Diretrizes para usar buffer adaptável

Os desenvolvedores devem seguir estas diretrizes importantes para minimizar o uso de memória pelo aplicativo:

- Evite usar a propriedade da cadeia de conexão **selectMethod=cursor** para permitir que o aplicativo processe um conjunto de resultados muito grande. O recurso de buffer adaptável permite que os aplicativos processem conjuntos de resultados somente encaminhamento e somente leitura muito grandes sem usar um cursor de servidor. Observe que, quando você define **selectMethod=cursor**, todos os conjuntos de resultados somente avanço e somente leitura gerados por aquela conexão são afetados. Em outras palavras, se o aplicativo processar conjuntos de resultados curtos habitualmente com alguns linhas, criar, ler e fechar um cursor de servidor para cada conjunto de resultados usará mais recursos nos lados do cliente e do servidor do que seria o caso quando **selectMethod** não está definido como **cursor**.

- Leia texto grande ou valores binários como fluxos usando o getAsciiStream, o getBinaryStream ou os métodos getCharacterStream em vez da getBlob ou os métodos getClob. Da versão 1.2 em diante, a classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) oferece novos métodos get\<Type>Stream para este propósito.

- Verifique se as colunas com valores potencialmente grandes são colocadas por último na lista de colunas em uma instrução SELECT e se os métodos get\<Type>Stream do [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) são usados para acessar as colunas na ordem em que são selecionadas.

- Verifique se os parâmetros OUT com valores potencialmente grandes são declarados por último na lista de parâmetros no SQL usada para criar [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Além disso, verifique se os métodos get\<Type>Stream do [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) são usados para acessar os parâmetros OUT na ordem em que eles são declarados.

- Evite executar mais de uma instrução na mesma conexão simultaneamente. Executar outra instrução antes de processar os resultados da instrução anterior pode fazer os resultados não processados serem armazenados em buffer na memória do aplicativo.

- Há alguns casos em que usar **selectMethod = cursor** em vez de **responseBuffering = adaptive** seria mais benéfico, por exemplo:

  - Se seu aplicativo processa um somente de avanço, somente leitura conjunto de resultados lentamente, como ler cada linha depois de alguma entrada do usuário, usando **selectMethod = cursor** em vez de **responseBuffering = adaptive** talvez ajudar a reduzir o uso de recursos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

  - Se o aplicativo processar dois ou mais conjuntos de resultados somente avanço e somente leitura ao mesmo tempo na mesma conexão, usar **selectMethod=cursor** em vez de **responseBuffering=adaptive** poderá ajudar a reduzir a memória exigida pelo driver para processar esses conjuntos de resultados.

  Em ambos os casos, você precisa considerar a sobrecarga de criar, ler e fechar os cursores de servidor.

Além disso, a lista a seguir fornece algumas recomendações para conjuntos de resultados roláveis e atualizáveis somente avanço:

- Para conjuntos de resultados roláveis, ao buscar um bloco de linhas, o driver sempre lê na memória o número de linhas indicado pelo método [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), até mesmo quando o buffer adaptável está habilitado. Se rolar causar um OutOfMemoryError, você poderá reduzir o número de linhas buscadas chamando o método [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) para definir o tamanho da busca como um número menor de linhas, até mesmo 1 linha, se necessário. Se isto não impedir um OutOfMemoryError, evite incluir colunas muito grandes em conjuntos de resultados roláveis.

- Para conjuntos de resultados roláveis, ao buscar um bloco de linhas, o driver geralmente lê na memória o número de linhas indicado pelo método [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), até mesmo quando o buffer adaptável está habilitado na conexão. Se chamar o método [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) resultar em um OutOfMemoryError, você poderá reduzir o número de linhas buscadas chamando o método [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) para definir o tamanho da busca como um número menor de linhas, até mesmo 1 linha, se necessário. Você também pode forçar o driver a não armazenar em buffer nenhuma linha chamando o método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) do objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) com o parâmetro "**adaptive**" antes de executar a instrução. Como o conjunto de resultados não é rolável, se o aplicativo acessar um valor de coluna grande usando um dos métodos get\<Type>Stream, o driver descartará o valor assim que ele for lido pelo aplicativo, da mesma maneira que faz para os conjuntos de resultados somente leitura somente avanço.

## <a name="see-also"></a>Consulte Também

[Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
