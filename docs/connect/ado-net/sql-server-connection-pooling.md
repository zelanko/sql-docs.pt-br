---
title: Pool de conexões do SQL Server
description: Saiba como o Provedor de Dados Microsoft SqlClient para SQL Server minimiza o custo da abertura de conexões usando o pool de conexões do SQL Server, o que reduz a sobrecarga para novas conexões.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 7e51d44e-7c4e-4040-9332-f0190fe36f07
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: ef687114ff2ceceabc1ed87d67a4585a5846029d
ms.sourcegitcommit: 7a3fdd3f282f634f7382790841d2c2a06c917011
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96563072"
---
# <a name="sql-server-connection-pooling-adonet"></a>Pool de conexões do SQL Server (ADO.NET)

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Para se conectar a um servidor de banco de dados, existem, normalmente, várias etapas demoradas. Um canal físico, como um soquete ou um pipe nomeado, deve ser estabelecido, o handshake inicial com o servidor deve ocorrer, informações de cadeia de conexão devem ser analisadas, a conexão deve ser autenticada pelo servidor, verificações devem ser realizadas para a inscrição na transação atual e assim por diante.

Na prática, a maioria dos aplicativos usa apenas uma ou algumas configurações diferentes para conexões. Isso significa que, durante a execução do aplicativo, muitas conexões idênticas serão abertas e fechadas repetidamente. Para minimizar o custo de abertura de conexões, o Provedor de Dados Microsoft SqlClient para SQL Server usa uma técnica de otimização chamada *pool de conexões*.

O pool de conexões reduz o número de vezes que as novas conexões devem ser abertas. O *pooler* mantém a propriedade da conexão física. Para gerenciar as conexões, ele mantém um conjunto de conexões ativas para cada configuração de conexão específica. Sempre que um usuário chama `Open` em uma conexão, o pooler procura uma conexão disponível no pool. Se houver uma conexão agrupada disponível, ele retornará essa conexão para o chamador, em vez de abrir uma nova conexão. Quando o aplicativo chama `Close` na conexão, o pooler retorna essa chamada para o conjunto de conexões ativas agrupadas, em vez de fechar a conexão. Depois de retornada ao pool, a conexão está pronta para ser reutilizada na próxima chamada `Open`.

Somente conexões com a mesma configuração podem ser agrupadas. O Provedor de Dados Microsoft SqlClient para SQL Server mantém vários pools ao mesmo tempo, um para cada configuração. As conexões são separadas em pools pela cadeia de conexão e, quando o modo de segurança integrada é usado, pela identidade do Windows. As conexões também são agrupadas conforme estejam ou não inscritas em uma transação. Ao usar o <xref:Microsoft.Data.SqlClient.SqlConnection.ChangePassword%2A>, a instância <xref:Microsoft.Data.SqlClient.SqlCredential> afeta o pool de conexões. As instâncias diferentes de <xref:Microsoft.Data.SqlClient.SqlCredential> usarão pools de conexões diferentes, mesmo se a identificação do usuário e a senha forem iguais.

O pooling de conexões pode melhorar significativamente o desempenho e a escalabilidade do aplicativo. Por padrão, o pool de conexões é habilitado no Provedor de Dados Microsoft SqlClient para SQL Server. A menos que você explicitamente o desabilite, o pooler otimiza as conexões quando elas são abertas e fechadas no aplicativo. Você também pode fornecer vários modificadores de cadeias de conexão para controlar o comportamento do pool de conexões. Para obter mais informações, confira "**Controlar o pool de conexões com palavras-chave da cadeia de conexão**", mais adiante neste tópico.

> [!IMPORTANT]
> Quando o pool de conexões estiver habilitado e se ocorrer um erro de tempo limite ou outro erro de logon, uma exceção será lançada, e as tentativas de conexão subsequentes falharão nos próximos **cinco** segundos, o "`blocking period`". Se o aplicativo tentar se conectar dentro do período de bloqueio, a primeira exceção será gerada novamente. Falhas subsequentes após o término do período de bloqueio resultarão em novos períodos de bloqueio, duas vezes maiores que o anterior, até um *máximo de **um** minuto*.

> [!NOTE]
> O mecanismo "`blocking period`" não se aplica ao SQL Server do Azure por padrão. Esse comportamento pode ser alterado modificando a propriedade <xref:Microsoft.Data.SqlClient.PoolBlockingPeriod> em <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString>, exceto para *.NET Standard*.

## <a name="pool-creation-and-assignment"></a>Criação e atribuição de pools

Quando uma conexão é aberta pela primeira vez, um pool de conexões é criado com base em um algoritmo compatível exato que associa o pool à cadeia de conexão na conexão. Cada pool de conexões é associado a uma cadeia de conexão distinta. Se a cadeia de conexão não for uma correspondência exata de um pool existente, quando uma nova conexão for aberta, um novo pool será criado.

> [!NOTE]
> As conexões são separadas em pool por _processo_, _domínio do aplicativo_, _cadeia de conexão_ e, quando a segurança integrada é usada, por _identidade do Windows_. As cadeias de conexão também devem ser uma correspondência exata; as palavras-chave fornecidas em uma ordem diferente para a mesma conexão serão agrupadas separadamente.

> [!NOTE]
> Se `MinPoolSize` não for especificado na cadeia de conexão, nem estiver especificado como zero, as conexões no pool serão fechadas após um período de inatividade. Entretanto, se o `MinPoolSize` especificado for maior que zero, o pool de conexões não será destruído até que o `AppDomain` seja descarregado e o processo concluído. A manutenção de pools inativos ou vazios envolve sobrecarga mínima do sistema.

> [!NOTE]
> O pool é limpo automaticamente quando ocorre um erro fatal, como um failover.

No exemplo de C# a seguir, três novos objetos <xref:Microsoft.Data.SqlClient.SqlConnection> são criados, mas apenas dois pools de conexões são necessários para gerenciá-los. Observe que a primeira e a segunda cadeias de conexão diferem pelo valor atribuído para `Initial Catalog`.  


[!code-csharp[SqlConnection_Pooling#1](~/../sqlclient/doc/samples/SqlConnection_Pooling.cs#1)]

## <a name="adding-connections"></a>Adicionando conexões

Um pool de conexões é criado para cada cadeia de conexão exclusiva. Quando um pool é criado, vários objetos de conexão são criados e adicionados ao pool para que o requisito de tamanho mínimo de pool seja atendido. As conexões são adicionadas ao pool conforme necessário, até o tamanho máximo de pool especificado (**100 é o padrão**). As conexões são retornadas para o pool quando fechadas ou descartadas.

Quando um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> é solicitado, ele é obtido do pool caso haja uma conexão útil disponível. Para ser útil, uma conexão não deve estar em uso, deve ter um contexto de transação correspondente (ou não deve estar associada a nenhum contexto de transação) e deve ter um vínculo válido com o servidor.

O pool de conexões atende às solicitações de conexões realocando-as à medida que são retornadas ao pool. Se o tamanho máximo de pool for atingido e nenhuma conexão útil estiver disponível, a solicitação será colocada na fila. Então, o pooler tenta recuperar todas as conexões até que o tempo limite seja atingido (**o padrão é 15 segundos**). Se o pooler não puder atender à solicitação antes que se esgote o tempo limite de conexão, uma exceção será gerada.

> [!CAUTION]
> É altamente recomendável sempre fechar a conexão quando você terminar de usá-la para que a conexão seja retornada ao pool. Você pode fazer isso usando os métodos `Close` ou `Dispose` do objeto `Connection` ou abrindo todas as conexões em uma instrução `using` no C# ou uma instrução `Using` no Visual Basic. As conexões que não são fechadas explicitamente não podem ser adicionadas nem retornadas ao pool. Para obter mais informações, confira [Instrução using](/dotnet/csharp/language-reference/keywords/using-statement) ou [Como descartar um recurso de sistema](/dotnet/visual-basic/programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource) para Visual Basic.

> [!NOTE]
> Não chame `Close` nem `Dispose` em um objeto `Connection`, em um `DataReader` nem em nenhum outro objeto gerenciado no método `Finalize` de sua classe. Em um finalizador, libere somente recursos não gerenciados que sua classe possui diretamente. Se a classe não tiver nenhum recurso não gerenciado, não inclua um método `Finalize` em sua definição de classe. Para obter mais informações, confira [Coleta de lixo](/dotnet/standard/garbage-collection/index).

Para obter mais informações sobre os eventos associados à abertura e ao fechamento de conexões, confira [Classe de Evento Audit Login](/sql/relational-databases/event-classes/audit-login-event-class) e [Classe de Evento Audit Logout](/sql/relational-databases/event-classes/audit-logout-event-class) na documentação do SQL Server.

## <a name="removing-connections"></a>Removendo conexões

O pooler de conexões remove uma conexão do pool após ela estar ociosa por aproximadamente **oito** minutos ou caso detecte que a conexão com o servidor foi interrompida.

> [!NOTE]
> Uma conexão interrompida pode ser detectada somente após a tentativa de comunicação com o servidor. Se for encontrada uma conexão que não esteja mais conectada ao servidor, ela será marcada como inválida. As conexões inválidas são removidas de pool de conexões somente quando são fechadas ou recuperadas.

Se uma conexão com um servidor desapareceu, ela pode ser removida do pool mesmo se o pooler de conexões não tiver detectado a conexão interrompida e a marcado como inválida. Este é o caso porque a sobrecarga de verificar se a conexão ainda é válida eliminaria os benefícios de se ter um pooler, provocando outra viagem de ida e volta ao servidor. Quando isso ocorrer, a primeira tentativa de usar a conexão detectará que a conexão foi interrompida e uma exceção será gerada.

## <a name="clearing-the-pool"></a>Limpando o pool

O Provedor de Dados Microsoft SqlClient para SQL Server introduziu dois novos métodos para limpar o pool: <xref:Microsoft.Data.SqlClient.SqlConnection.ClearAllPools%2A> e <xref:Microsoft.Data.SqlClient.SqlConnection.ClearPool%2A>. `ClearAllPools` limpa os pools de conexões de um provedor específico e `ClearPool` limpa o pool de conexões associado a uma conexão específica.

> [!NOTE]
> Se houver conexões em uso no momento da chamada, elas serão devidamente marcadas. Quando fechadas, serão descartadas, em vez de retornadas ao pool.

## <a name="transaction-support"></a>Suporte a transações

As conexões são removidas do pool e atribuídas com base no contexto de transação. A menos que `Enlist=false` seja especificado na cadeia de conexão, o pool de conexões verifica se a conexão está inscrita no contexto de <xref:System.Transactions.Transaction.Current%2A>. Quando uma conexão é fechada e retornada ao pool com uma transação `System.Transactions` inscrita, ela é reservada para que a próxima solicitação desse pool de conexões com a mesma transação `System.Transactions` seja retornada à mesma conexão, se disponível. Se uma solicitação desse tipo for emitida, e não houver conexões agrupadas disponíveis, uma conexão será removida da parte não transacionada do pool e depois inscrita. Se não houver conexões disponíveis em nenhuma área do pool, uma nova conexão será criada e inscrita.

Quando uma conexão for fechada, ela será retornada ao pool e à subdivisão apropriada com base no contexto de transação. Portanto, é possível fechar a conexão sem gerar erros, mesmo que uma transação distribuída ainda esteja pendente. Isso permite confirmar ou anular a transação distribuída posteriormente.

## <a name="controlling-connection-pooling-with-connection-string-keywords"></a>Controlando o pool de conexões com palavras-chave de cadeias de conexão

A propriedade `ConnectionString` do objeto <xref:Microsoft.Data.SqlClient.SqlConnection> dá suporte a pares chave-valor de cadeias de conexão que podem ser usados para ajustar o comportamento da lógica do pool de conexões. Para obter mais informações, consulte <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.

## <a name="pool-fragmentation"></a>Fragmentação de pool

A fragmentação de pool é um problema comum em muitos aplicativos da Web nos quais o aplicativo pode criar um grande número de pools que não são liberados até que o processo seja encerrado. Isso deixa um grande número de conexões abertas e consumindo memória, o que resulta em baixo desempenho.

### <a name="pool-fragmentation-due-to-integrated-security"></a>Fragmentação de pool devido à segurança integrada

As conexões são agrupadas de acordo com a cadeia de conexão e a identidade do usuário. Portanto, se você usa autenticação Básica ou autenticação do Windows no site, bem como um logon de segurança integrada, pode obter um pool por usuário. Embora isso melhore o desempenho de solicitações de bancos de dados subsequentes feitas por um único usuário, esse usuário não pode aproveitar as vantagens das conexões feitas por outros usuários. Isso também resulta em, pelo menos, uma conexão por usuário com o servidor de banco de dados. Trata-se de um efeito colateral de uma arquitetura de aplicativo Web específico que os desenvolvedores devem ponderar em relação aos requisitos de segurança e auditoria.

### <a name="pool-fragmentation-due-to-many-databases"></a>Fragmentação de pool devido a vários bancos de dados

Vários provedores de serviços de Internet hospedam vários sites em um único servidor. Eles podem usar um único banco de dados para confirmar um logon de autenticação de formulários e para abrir uma conexão com um banco de dados específico desse usuário ou grupo de usuários. A conexão com o banco de dados de autenticação é agrupada e usada por todos. Entretanto, há um pool de conexões separado para cada banco de dados, que aumenta o número de conexões com o servidor.

Trata-se também de um efeito colateral de projeto do aplicativo. Existe uma forma relativamente simples de evitar esse efeito colateral sem comprometer a segurança quando você se conectar ao SQL Server. Em vez de se conectar a um banco de dados separado para cada usuário ou grupo, conecte-se ao mesmo banco de dados no servidor e execute a instrução Transact-SQL USE para alternar para o banco de dados desejado.
 
O fragmento de código a seguir demonstra como criar uma conexão inicial com o banco de dados `master` e depois alternar para o banco de dados desejado especificado na variável da cadeia de caracteres `databaseName`.

[!code-csharp[SqlConnection_Pooling_Use_Statement#1](~/../sqlclient/doc/samples/SqlConnection_Pooling_Use_Statement.cs#1)]

## <a name="application-roles-and-connection-pooling"></a>Funções de aplicativo e pool de conexões

Depois de ativada uma função de aplicativo do SQL Server ao chamar o procedimento armazenado do sistema `sp_setapprole`, o contexto de segurança dessa conexão não pode ser redefinido. Entretanto, se o pool estiver habilitado, a conexão será retornada a ele e ocorrerá um erro quando a conexão agrupada for reutilizada.

### <a name="application-role-alternatives"></a>Alternativas a funções de aplicativo

Recomendamos que você aproveite todas as vantagens dos mecanismos de segurança que podem ser usados no lugar de funções de aplicativo.

## <a name="see-also"></a>Confira também

- [Pool de conexões](connection-pooling.md)
- [SQL Server e ADO.NET](./sql/index.md)
