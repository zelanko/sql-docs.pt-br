---
title: Usar o espelhamento de banco de dados | Microsoft Docs
description: Usando o espelhamento de banco de dados com o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- OLE DB Driver for SQL Server, database mirroring
- data access [OLE DB Driver for SQL Server], database mirroring
- database mirroring [SQL Server], connecting clients to
- MSOLEDBSQL, database mirroring
- OLE DB Driver for SQL Server, database mirroring
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3abdb1363cf147d493b38d2fcbc657632e9d764b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-database-mirroring"></a>Usando o espelhamento de banco de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]Use [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em vez disso.  
  
 O espelhamento de banco de dados, apresentado no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], é uma solução que visa aumentar a disponibilidade do banco de dados e a redundância de dados. OLE DB Driver para SQL Server fornece suporte implícito ao espelhamento de banco de dados, para que o desenvolvedor não precisa escrever nenhum código nem executar qualquer outra ação depois que ele foi configurado para o banco de dados.  
  
 Banco de dados de espelhamento, que é implementado em uma base por banco de dados, mantém uma cópia de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados de produção em um servidor em espera. Esse servidor é um servidor em espera ativa ou passiva, dependendo da configuração e do estado da sessão de espelhamento de banco de dados. Um servidor em espera ativa dá suporte ao failover rápido sem perda de transações confirmadas, e um servidor em espera passiva dá suporte ao serviço de imposição (com possível perda de dados).  
  
 O banco de dados de produção é chamado de *banco de dados principal*, e a cópia em espera é chamada de *banco de dados espelho*. O banco de dados principal e o banco de dados espelho devem residir em instâncias separadas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (instâncias de servidor), e eles devem residir em computadores separados se possível.  
  
 A instância de servidor de produção, chamada de *servidor principal*, se comunica com a instância de servidor em espera, chamada de *servidor espelho*. Os servidores principal e espelho atuam como parceiros dentro de um espelhamento de banco de dados *sessão*. Se o servidor principal falhar, o servidor espelho poderá transformar seu banco de dados no banco de dados principal por meio de um processo chamado *failover*. Por exemplo, Parceiro_A e Parceiro_B são dois servidores parceiros, com o banco de dados principal inicialmente no Parceiro_A como servidor principal e o banco de dados espelho residindo no Parceiro_B como o servidor espelho. Se o Parceiro_A ficar offline, o banco de dados no Parceiro_B pode fazer failover para se tornar o banco de dados principal atual. Quando o Parceiro_A ingressar novamente na sessão de espelhamento, ele se tornará o servidor espelho e seu banco de dados se tornará o banco de dados espelho.  
  
 Configurações alternativas de espelhamento de banco de dados oferecem diferentes níveis de desempenho e segurança de dados, e dão suporte a diversas formas de failover. Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 É possível usar um alias ao especificar o nome de banco de dados espelho.  
  
> [!NOTE]  
>  Para obter informações sobre tentativas de conexão inicial e tentativas de reconexão com um banco de dados espelho, consulte [conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>Considerações sobre programação  
 Quando o servidor do banco de dados principal falhar, o aplicativo cliente receberá erros em resposta a chamadas API, o que indica que a conexão com o banco de dados foi interrompida. Quando isto acontece, todas as alterações não confirmadas do banco de dados são perdidas e a transação atual é revertida. Se isso ocorrer, o aplicativo deve fechar a conexão (ou liberar o objeto da fonte de dados) e abri-la novamente. A conexão é redirecionada de forma transparente para o banco de dados espelho, que agora atua como servidor principal.  
  
 Quando uma conexão é estabelecida, o servidor principal envia a identidade de seu parceiro de failover ao cliente a ser usado quando ocorrer failover. No caso de um aplicativo tentar estabelecer uma conexão depois que o servidor principal falhou, o cliente não sabe a identidade do parceiro de failover. Para que os clientes possam lidar com este cenário, uma propriedade de inicialização e uma palavra-chave de cadeia de conexão associada permitem que o próprio cliente especifique a identidade do parceiro de failover. O atributo do cliente é usado apenas nesse cenário; se o servidor principal estiver disponível, ele não será usado. Se o servidor do parceiro de failover fornecido pelo cliente não se referir a um servidor que está atuando como um parceiro de failover, a conexão será recusada pelo servidor. Para que os aplicativos possam se adaptar a alterações de configuração, a identidade do parceiro de failover real pode ser determinada inspecionando o atributo depois que a conexão for estabelecida. Considere o armazenamento em cache das informações do parceiro para atualizar a cadeia de conexão ou criar uma estratégia de repetição no caso de falha da primeira tentativa de estabelecer uma conexão.  
  
> [!NOTE]  
>  Especifique explicitamente o banco de dados a ser usado por uma conexão, se desejar usar esse recurso em um DSN, uma cadeia de conexão ou uma propriedade/atributo da conexão. OLE DB Driver para SQL Server não tentará fazer failover para o banco de dados do parceiro, se isso não for feito.  
>   
>  O espelhamento é um recurso do banco de dados. Talvez os aplicativos que usam vários bancos de dados não consigam explorar esse recurso.  
>   
>  Além disso, os nomes de servidor não diferenciam maiúsculas de minúsculas, mas os nomes de banco de dados o fazem. Portanto, certifique-se de usar as mesmas maiúsculas e minúsculas em DSNs e cadeias de conexões.  
  
## <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server  
 O Driver OLE DB para SQL Server dá suporte a atributos de cadeia de caracteres de espelhamento por meio de conexão e conexão de banco de dados. A propriedade SSPROP_INIT_FAILOVERPARTNER foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT e o **FailoverPartner** palavra-chave é um novo atributo de cadeia de caracteres de conexão para DBPROP_INIT_PROVIDERSTRING. Para obter mais informações, consulte [usando Conexão String Keywords com OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 O cache de failover é mantido como o provedor estiver carregado, ou seja, até **CoUninitialize** é chamado ou desde que o aplicativo tem uma referência para algum objeto gerenciado pelo Driver OLE DB para SQL Server como um objeto de fonte de dados .  
  
 Para obter detalhes sobre o Driver do OLE DB para o suporte para espelhamento de banco de dados do SQL Server, consulte [propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  
 
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para recursos do SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
