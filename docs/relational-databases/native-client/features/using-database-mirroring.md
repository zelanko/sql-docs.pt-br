---
title: Usar espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1fc1884791b9bc2a01a5407dc09778476bdfe1d5
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009867"
---
# <a name="using-database-mirroring"></a>Usando o espelhamento de banco de dados
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
 O espelhamento de banco de dados, apresentado no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], é uma solução que visa aumentar a disponibilidade do banco de dados e a redundância de dados. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O Native Client fornece suporte implícito para espelhamento de banco de dados, de modo que o desenvolvedor não precisa escrever nenhum código ou executar qualquer outra ação depois de ter sido configurado para o banco de dados.  
  
 O espelhamento de banco de dados, que é implementado para cada banco de dados, mantém uma cópia de um banco de dados de produção do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um servidor em espera. Esse servidor é um servidor em espera ativa ou passiva, dependendo da configuração e do estado da sessão de espelhamento de banco de dados. Um servidor em espera ativa dá suporte ao failover rápido sem perda de transações confirmadas, e um servidor em espera passiva dá suporte ao serviço de imposição (com possível perda de dados).  
  
 O banco de dados de produção é chamado de *banco de dados principal*, e a cópia em espera é chamada de *banco de dados espelho*. O banco de dados principal e o banco de dados espelho precisam residir em instâncias separadas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (instâncias do servidor) e, se possível, em computadores separados.  
  
 A instância do servidor de produção, chamado *servidor principal*, se comunica com a instância do servidor em espera, chamado *servidor espelho*. Os servidores principal e espelho atuam como parceiros em uma *sessão*de espelhamento de banco de dados. Se o servidor principal falhar, o servidor espelho poderá transformar seu banco de dados no banco de dados principal por meio de um processo chamado *failover*. Por exemplo, Parceiro_A e Parceiro_B são dois servidores parceiros, com o banco de dados principal inicialmente no Parceiro_A como servidor principal e o banco de dados espelho residindo no Parceiro_B como o servidor espelho. Se o Parceiro_A ficar offline, o banco de dados no Parceiro_B pode fazer failover para se tornar o banco de dados principal atual. Quando o Parceiro_A ingressar novamente na sessão de espelhamento, ele se tornará o servidor espelho e seu banco de dados se tornará o banco de dados espelho.  
  
 Configurações alternativas de espelhamento de banco de dados oferecem diferentes níveis de desempenho e segurança de dados, e dão suporte a diversas formas de failover. Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 É possível usar um alias ao especificar o nome de banco de dados espelho.  
  
> [!NOTE]  
>  Para obter informações sobre tentativas de conexão inicial e tentativas de reconexão com um banco de dados espelho, confira [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>Considerações sobre programação  
 Quando o servidor do banco de dados principal falhar, o aplicativo cliente receberá erros em resposta a chamadas API, o que indica que a conexão com o banco de dados foi interrompida. Quando isto acontece, todas as alterações não confirmadas do banco de dados são perdidas e a transação atual é revertida. Se isso ocorrer, o aplicativo deve fechar a conexão (ou liberar o objeto da fonte de dados) e abri-la novamente. A conexão é redirecionada de forma transparente para o banco de dados espelho, que agora atua como servidor principal.  
  
 Quando uma conexão é estabelecida, o servidor principal envia a identidade de seu parceiro de failover ao cliente a ser usado quando ocorrer failover. No caso de um aplicativo tentar estabelecer uma conexão depois que o servidor principal falhou, o cliente não sabe a identidade do parceiro de failover. Para que os clientes possam lidar com este cenário, uma propriedade de inicialização e uma palavra-chave de cadeia de conexão associada permitem que o próprio cliente especifique a identidade do parceiro de failover. O atributo do cliente é usado apenas nesse cenário; se o servidor principal estiver disponível, ele não será usado. Se o servidor do parceiro de failover fornecido pelo cliente não se referir a um servidor que está atuando como um parceiro de failover, a conexão será recusada pelo servidor. Para que os aplicativos possam se adaptar a alterações de configuração, a identidade do parceiro de failover real pode ser determinada inspecionando o atributo depois que a conexão for estabelecida. Considere o armazenamento em cache das informações do parceiro para atualizar a cadeia de conexão ou criar uma estratégia de repetição no caso de falha da primeira tentativa de estabelecer uma conexão.  
  
> [!NOTE]  
>  Especifique explicitamente o banco de dados a ser usado por uma conexão, se desejar usar esse recurso em um DSN, uma cadeia de conexão ou uma propriedade/atributo da conexão. Se isso não for feito, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não tentará fazer failover para o banco de dados parceiro.  
>   
>  O espelhamento é um recurso do banco de dados. Talvez os aplicativos que usam vários bancos de dados não consigam explorar esse recurso.  
>   
>  Além disso, os nomes de servidor não diferenciam maiúsculas de minúsculas, mas os nomes de banco de dados o fazem. Portanto, certifique-se de usar as mesmas maiúsculas e minúsculas em DSNs e cadeias de conexões.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte ao espelhamento de banco de dados através de atributos de cadeia de conexão e conexão. A propriedade SSPROP_INIT_FAILOVERPARTNER foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT e a palavra-chave **FailoverPartner** é um novo atributo de cadeia de conexão para DBPROP_INIT_PROVIDERSTRING. Para obter mais informações, consulte [usando palavras-chave da cadeia de conexão com SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 O cache de failover é mantido, desde que o provedor seja carregado, o que é até que **CoUninitialize** seja chamado ou desde que o aplicativo tenha uma referência a algum objeto gerenciado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo, como um objeto de fonte de dados.  
  
 Para obter detalhes sobre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte ao provedor de OLE DB nativo do cliente para espelhamento de banco de dados, consulte [Propriedades de inicialização e autorização](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte ao espelhamento de banco de dados por meio de atributos de cadeia de conexão e conexão. Especificamente, o atributo SQL_COPT_SS_FAILOVER_PARTNER foi adicionado para uso com as funções [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) ; e a palavra-chave **Failover_Partner** foi adicionada como um novo atributo de cadeia de conexão.  
  
 O cache de failover é mantido enquanto o aplicativo tem pelo menos um identificador de ambiente alocado. Por outro lado, ele é perdido quando o último identificador de ambiente for desalocado.  
  
> [!NOTE]  
>  O Gerenciador de Driver ODBC foi aprimorado para dar suporte à especificação do nome do servidor de failover.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
