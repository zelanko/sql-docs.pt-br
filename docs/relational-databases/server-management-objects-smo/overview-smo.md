---
title: Visão geral (SMO) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
caps.latest.revision: 69
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 21d71757b4f8520e2ec2b3b7c2d1cb3c1407b420
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34708004"
---
# <a name="overview-smo"></a>Visão geral (SMO)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) são objetos criados para o gerenciamento programático do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar os SMO para compilar aplicativos de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizados. Embora o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] seja um aplicativo extenso e abrangente para o gerenciamento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pode haver vezes em que um aplicativo SMO funcione melhor.  
  
 Por exemplo, pode ser necessário simplificar os aplicativos de usuário que controlam as tarefas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atender as necessidades dos novos usuários e reduzir custos de treinamento. Pode ser necessário criar bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizados ou criar um aplicativo para criar e monitorar a eficiência de índices. Um aplicativo de SMO também pode ser usado para incluir hardware ou software de terceiros de modo homogêneo no aplicativo de gerenciamento de banco de dados.  
  
 Como o SMO é compatível com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e com versões posteriores, você pode gerenciar facilmente um ambiente de várias versões.  
  
 Recursos do SMO incluem o seguinte:  
  
-   Modelo de objeto armazenado em cache e criação de instância de objeto otimizada. Os objetos são carregados somente quando especificamente referenciados. As propriedades do objeto são parcialmente carregadas apenas quando o objeto é criado. Os objetos e propriedades restantes são carregados quando referenciados diretamente.  
  
-   Execução processada em lotes de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. As instruções são processadas em lote para melhorar o desempenho de rede.  
  
-   Captura de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Permite capturar qualquer operação em um script. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] usa esse recurso para executar uma operação em script, em vez de executá-la imediatamente.  
  
-   Gerenciamento de serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o Provedor de WMI. Os serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser iniciados, interrompidos e pausados de modo programático.  
  
-   Scripts avançados. Os scripts do [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser gerados para recriar objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que descrevem relações com outros objetos na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Uso de URNs (nomes de recurso exclusivos). Um URN permite criar instâncias e referências de objetos de SMO.  
  
 O SMO também representa como objetos ou propriedades novos muitos recursos e componentes que foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Esses novos recursos e componentes incluem:  
  
-   Tabela e particionamento de índice para armazenamento de dados em um esquema de partição. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
-   Pontos de extremidade de HTTP para o gerenciamento de solicitações de SOAP. Para obter mais informações, consulte [implementar pontos de extremidade](../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md).  
  
-   Isolamento de instantâneo e versão do nível de linha para aprimoramento de simultaneidade. Para obter mais informações, consulte [trabalhando com isolamento de instantâneo](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
-   A coleção do esquema XML, os índices XML e o tipo de dados XML fornecem validação e armazenamento dos dados de XML. Para obter mais informações, consulte [coleções de esquema XML &#40;SQL Server&#41; ](../../relational-databases/xml/xml-schema-collections-sql-server.md) e [Using XML Schemas](../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md).  
  
-   Bancos de dados de instantâneo para criar cópias somente leitura de bancos de dados.  
  
-   Suporte do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para comunicação baseada em mensagem. Para obter mais informações, consulte [do SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md).  
  
-   Suporte de sinônimo para vários nomes de objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [sinônimos &#40;mecanismo de banco de dados&#41;](../../relational-databases/synonyms/synonyms-database-engine.md).  
  
-   O gerenciamento de Banco de Dados de Email permite criar servidores de email, perfis de email e contas de email no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Database Mail](../../relational-databases/database-mail/database-mail.md).  
  
-   Servidores registrados dão suporte para registrar informações de conexão. Para obter mais informações, consulte [registrar servidores](../../tools/sql-server-management-studio/register-servers.md).  
  
-   Rastreamento e repetição de eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md), [rastreamento SQL](../../relational-databases/sql-trace/sql-trace.md), [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md), e [eventos estendidos](../../relational-databases/extended-events/extended-events.md).  
  
-   Suporte a certificados e chaves para controle de segurança. Para obter mais informações, consulte [hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
-   Gatilhos DDL para adicionar funcionalidade quando ocorrerem eventos de DDL. Para obter mais informações, consulte [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md).  
  
 O namespace do SMO é <xref:Microsoft.SqlServer.Management.Smo>. O SMO é implementado como um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] assembly. Isso significa que o common language runtime do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versão 2.0 deve ser instalada antes de usar os objetos do SMO. Os assemblies do SMO são instalados por padrão no GAC (cache de assembly global) com o a opção SDK do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os assemblies estão localizados em C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\. Para obter mais informações, consulte o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentação.  
  
## <a name="smo-classes"></a>Classes do SMO  
 As classes do SMO incluem duas categorias: classes de instância e classes de utilitário.  
  
 **Classes de instância**  
  
 As classes de instância representam objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como servidores, bancos de dados, tabelas, gatilhos e procedimentos armazenados. A classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> é usada para estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e controlar o modo de captura de comandos enviado a ele.  
  
 Os objetos da instância do SMO formam uma hierarquia que representa a hierarquia de um servidor de banco de dados. Na parte superior estão as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sob as quais estão os bancos de dados seguidos das tabelas, colunas, gatilhos e assim por diante. Se for lógica a existência de uma relação de um pai para vários filhos, como uma tabela tendo uma ou mais colunas, o filho é representado por uma coleção de objetos. Caso contrário, o filho apenas é representado por um objeto.  
  
 **Classes de utilitário**  
  
 Classes de utilitários são um grupo de objetos que foram criados para executar tarefas específicas explicitamente. Elas foram divididas em hierarquias de objeto diferentes baseado em função:  
  
-   Classe de transferência. Usada para transferir esquema e dados a outro banco de dados.  
  
-   Classes de backup e restauração. Usadas para fazer backup e restaurar bancos de dados.  
  
-   Classe scripter. Usada para criar arquivos de script para a regeneração de objetos e suas dependências.  
  
## <a name="smo-features"></a>Recursos do SMO  
 **Desempenho otimizado**  
  
 A arquitetura do SMO é eficiente em termos de memória porque objetos são somente parcialmente instanciados primeiro, e informações de propriedade mínimo é solicitado do servidor. A instanciação total de objetos é atrasada até que o objeto seja explicitamente referenciado. Um objeto é totalmente instanciado quando uma propriedade é solicitada e não está no conjunto de propriedades recuperadas primeiramente ou quando um método é chamado exigindo tal propriedade. A transição entre objetos parcialmente e totalmente instanciados é transparente para o usuário. Além disso, algumas propriedades que usam muitos memória nunca são recuperadas, a menos que a propriedade seja explicitamente referenciada. Um exemplo disto é a propriedade <xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> da propriedade do objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. Porém, a instanciação parcial requer mais viagens de ida e volta de rede e não é a melhor opção de desempenho para o seu aplicativo.  
  
 Você pode controlar instanciação para que fique adequada ao ambiente do sistema. A dependência na instanciação adiada minimiza a quantidade de memória exigida pelo aplicativo, embora possa ativar muitas solicitações do servidor quando as propriedades forem referenciadas.  
  
 Classes de instância – objetos que representam objetos de banco de dados reais – podem existir em três níveis de instanciação. São elas: minimamente instanciadas (somente as propriedades mínimas são lidas em um bloco), parcialmente instanciadas (todas as propriedades que usam uma quantidade relativamente grande de memória são lidas em um bloco) e totalmente instanciadas. Os estados de instanciação sem-instância e totalmente instanciadas são tradicionais. O estado parcialmente instanciadas aumenta eficiência, porque um objeto parcialmente instanciado não contém valores para o conjunto completo de propriedades de objeto. A instanciação parcial é o estado padrão para um objeto que não é referenciado diretamente. Quando um destas propriedades é referenciada, é gerada uma falha que solicita uma instanciação completa do objeto.  
  
 **Execução de captura**  
  
 A execução direta é o método habitual de execução. As instruções são enviadas diretamente a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conforme são incorridas. A execução de captura é a alternativa a isto.  
  
 A execução de captura permite capturar os lotes do [!INCLUDE[tsql](../../includes/tsql-md.md)] que seriam executados normalmente. Dessa forma, o programador de SMO pode adiar o script, armazená-lo para execução posterior ou fornecer uma visualização para o usuário final. Por exemplo, uma instrução **create database**, um **create table**e **create index** podem ser enviadas em um lote e ser executadas como três etapas sequenciais. Essa funcionalidade é controlada pelo usuário com o objeto <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>.  
  
 **Provedor WMI**  
  
 Os objetos do Provedor WMI são quebrados pelo SMO. Isso fornece ao programador de SMO um modelo de objeto simples que é muito similar a classes de SMO, sem a necessidade de compreender o modelo de programação representado pelo namespace e os detalhes do Provedor WMI do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Provedor WMI permite configurar serviços, aliases e bibliotecas de rede do servidor e do cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Script**  
  
 No SMO, a criação de scripts foi aprimorada e movida para a classe **Scripter** . A classe **Scripter** pode descobrir dependências, entender as relações entre objetos e habilitar a manipulação da hierarquia de dependência. O objeto principal da criação de scripts é o **Scripter** . Também há vários objetos que dão suporte, manipulam as dependências e respondem a eventos Error ou Progress.  
  
 O objeto **Scripter** dá suporte às seguintes opções de script avançadas:  
  
-   Criação de script de 1 fase (cria o script em uma etapa)  
  
-   Fase 3 scripts avançados (cria o script em três etapas; descoberta de dependência, geração de lista, geração de script)  
  
-   Descoberta de dependência bidirecional (permite a descoberta de dependências ou dependentes)  
  
-   Resposta para eventos Progress  
  
-   Resposta para eventos Error  
  
 **Nomes de recurso exclusivos**  
  
 Um conceito fundamental no uso da biblioteca de objetos do SMO é o URN (nome de recurso exclusivo). O URN usa uma sintaxe semelhante ao XPath. O XPath é um caminho de hierarquia usado para especificar um objeto no qual cada nível tem qualificadores e funções. No SMO, o URN tem dois elementos, o caminho e nomeação de atributo que limitaram funcionalidade. O caminho é usado para especificar o local do objeto, enquanto a nomeação do atributo permite um grau de filtragem.  
  
 Um exemplo de uma URN para um banco de dados é  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 O URN de um objeto pode ser recuperado pela referência de sua propriedade de URN. O objeto Scripter também usa URNs como parâmetros que transmitem referências de objeto ao método do objeto **Scripter** . Além disso, é possível especificar um URN para o método **GetSmoObject** do objeto **Server** . Isto é usado para criar uma instância do objeto do SMO.  
  
## <a name="sql-server-features-represented-in-smo"></a>Recursos do SQL Server representados no SMO  
 **Particionamento de tabela e índice**  
  
 O particionamento de tabela e índice permite gerenciar a expansão de dados em tabelas e índices por grupos de arquivos. Esse recurso novo é representado por objetos do SMO.  
  
 **Pontos de extremidade**  
  
 As solicitações de espelhamento de banco de dados e SOAP são manipuladas por pontos de extremidade que usam o objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint>.  
  
 **Versão do nível de linha/isolamento de instantâneo**  
  
 O Isolamento de instantâneo (controle de versão no nível de linha) é representado através de novas propriedades de objeto do <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **Namespace de esquema XML, índices XML e tipo de dados XML**  
  
 Namespaces de Esquema XML são representados no SMO por uma coleção de objetos. Os índices XML são representados no SMO por uma propriedade de objeto do **Index** .  
  
 **Aprimoramentos da pesquisa de texto completo**  
  
 São fornecidos objetos novos no SMO representando os aprimoramentos da pesquisa de texto completo.  
  
 **Verificação de Página**  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions.PageVerify%2A> representa as opções de verificação de página do banco de dados.  
  
 **Bancos de dados do instantâneo**  
  
 Um banco de dados de instantâneo é uma cópia somente leitura de um banco de dados especificado como momento determinado. Um banco de dados de instantâneo pode ser especificado usando a propriedade <xref:Microsoft.SqlServer.Management.Smo.Database.IsDatabaseSnapshot%2A> do objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **Service Broker**  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] e sua funcionalidade são representados por um grupo de objetos  
  
 **Aprimoramentos do índice**  
  
 Os aprimoramentos de índice do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são representados por propriedades novas no objeto <xref:Microsoft.SqlServer.Management.Smo.Index>.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de objetos de gerenciamento de replicação](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
