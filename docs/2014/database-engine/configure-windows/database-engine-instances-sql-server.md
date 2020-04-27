---
title: Instâncias do Mecanismo de Banco de Dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2e38b572535011737f33ba1e4c438540ecdd6849
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62811227"
---
# <a name="database-engine-instances-sql-server"></a>Instâncias do mecanismo de banco de dados (SQL Server)
  Uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é uma cópia do executável `sqlservr.exe` que é executada como um serviço do sistema operacional. Cada instância gerencia vários bancos de dados do sistema e um ou mais bancos de dados de usuários. Cada computador pode executar várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Aplicativos conectam à instância para executar trabalhos em um banco de dados gerenciado pela instância.  
  
## <a name="instances"></a>Instâncias  
 Uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] opera como um serviço que trata toda as solicitações do aplicativo pede trabalhar com os dados em quaisquer bancos de dados gerenciados por essa instância. É o destino das solicitações de conexão (logons) de aplicativos. A conexão será executada em uma conexão de rede se o aplicativo e a instância estiverem em computadores separados. Se o aplicativo e a instância estiverem no mesmo computador, a conexão de SQL Server poderá executar como uma conexão de rede ou uma conexão de memória. Quando uma conexão for concluída, um aplicativo enviará instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] pela conexão para a instância. A instância resolve as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em operações nos dados e objetos nos bancos de dados e, se as permissões exigidas tiverem sido concedidas às credenciais de logon, executará o trabalho. Quaisquer dados recuperados são retornados ao aplicativo, junto com mensagens como erros.  
  
 Você pode executar várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em um computador. Uma instância pode ser a instância padrão. A instância padrão não tem nome. Se a solicitação de conexão especificar apenas o nome do computador, a conexão será feita para a instância padrão. Uma instância nomeada é um onde você especifica um nome de instância ao instalar a instância. Uma solicitação de conexão deve especificar o nome do computador e o nome da instância para a conexão à instância. Não há requisitos para instalar uma instância padrão; todas as instâncias executadas em um computador podem ser instâncias nomeadas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como configurar as propriedades de uma instância. Configure padrões como locais de arquivo e formatos de data, ou como a instância usa recursos de sistema operacional, como memória ou threads.|[Configurar instâncias do mecanismo de banco de dados &#40;SQL Server&#41;](database-engine-instances-sql-server.md)|  
|Descreve como gerenciar a ordenação de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. As ordenações definem os padrões de bit usados para representar caracteres, comportamentos associados como classificação, e diferenciação entre maiúsculas e minúsculas ou a diferenciação de acentos em operações de comparação.|[Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)|  
|Descreve como configurar definições de servidor vinculado, que permitem a execução de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma instância para trabalhar com dados armazenados em fontes de dados OLE DB separadas.|[Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|Descreve como criar um gatilho de logon, que especifica ações a serem adotadas depois que uma tentativa de logon é validada, mas antes do início do trabalho com recursos na instância. O logon dispara ações de suporte como registrar em log as atividades de conexão ou restringir logons com base em lógica além da autenticação de credencial executada pelo Windows e pelo SQL Server.|[Gatilhos de logon](../../relational-databases/triggers/logon-triggers.md)|  
|Descreve como gerenciar o serviço associado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Isso inclui ações como iniciar e parar o serviço ou configurando opções de inicialização.|[Gerenciar os serviços do Mecanismo de Banco de Dados](manage-the-database-engine-services.md)|  
|Descreva como realizar tarefas de configuração de rede de servidor, como habilitação de protocolos, modificação de porta ou pipe usado por um protocolo, configuração de criptografia, configuração do serviço SQL Server Browser, exposição ou ocultação do Mecanismo de Banco de Dados do SQL Server na rede e registro do Nome da Entidade de Segurança do Servidor.|[Configuração de rede do servidor](server-network-configuration.md)|  
|Descreve como executar tarefas de configuração de rede de cliente como configurar protocolos de cliente e criar ou excluir um Alias de Servidor.|[Configuração de rede de cliente](client-network-configuration.md)|  
|Descreve os editores [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] que podem ser usados para criar, depurar e executar scripts tais como scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] . Também descreve como codificar scripts do Windows PowerShell para trabalhar com componentes do SQL Server.|[Geração de scripts do mecanismo de banco de dados](../../relational-databases/scripting/database-engine-scripting.md)|  
|Descreve como usar planos de manutenção para especificar um fluxo de trabalho de tarefas de administração comum para uma instância. Fluxos de trabalho incluem tarefas como backup de bancos de dados e atualização de estatísticas para melhorar o desempenho.|[Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|Descreve como usar o administrador de recursos para gerenciar o consumo de recursos e cargas de trabalho, especificando limites para a quantidade de CPU e memória que solicitações de aplicativo podem usar.|[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)|  
|Descreve como aplicativos de banco de dados podem usar o email do banco de dados para enviar mensagens de email do [!INCLUDE[ssDE](../../includes/ssde-md.md)].|[Database Mail](../../relational-databases/database-mail/database-mail.md)|  
|Descreve como usar eventos estendidos para capturar dados de desempenho para criar linhas de base de desempenho ou diagnosticar problemas de desempenho. Eventos estendidos são um sistema leve e altamente escalonável de coleta de dados de desempenho.|[Eventos estendidos](../../relational-databases/extended-events/extended-events.md)|  
|Descreve como usar o Rastreamento do SQL para criar um sistema personalizado para capturar e registrar eventos no [!INCLUDE[ssDE](../../includes/ssde-md.md)].|[Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)|  
|Descreve como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler para capturar rastreamentos de solicitações de aplicativo recebidas por uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Estes rastreamentos podem ser reproduzidos posteriormente para atividades como teste de desempenho ou diagnóstico de problemas.|[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|Descreve os recursos CDC (Change Data Capture) e Controle de Alterações e descreve como usá-los para controlar as alterações de dados em um banco de dados.|[Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|Descreve como usar o visualizador de Arquivo de Log para localizar e exibir erros e mensagens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em vários logs, como o histórico de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , logs do SQL Server e logs de evento do Windows.|[Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer.md)|  
|Descreve como usar o Orientador de Otimização [!INCLUDE[ssDE](../../includes/ssde-md.md)] para analisar bancos de dados e fazer recomendações para tratar de problemas de desempenho em potencial.|[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|Descreve como os administradores de banco de dados de produção podem fazer uma conexão de diagnóstico com instâncias quando conexões padrão não estão sendo aceitas.|[Conexão de diagnóstico para administradores de banco de dados](diagnostic-connection-for-database-administrators.md)|  
|Descreve como usar o recurso de servidores remotos substituídos para habilitar o acesso de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para outra. O mecanismo preferido para esta funcionalidade é um servidor vinculado.|[Servidores remotos](remote-servers.md)|  
|Descreve os recursos do Service Broker para mensagens e enfileiramento de aplicativos e fornece ponteiros à documentação do Service Broker.|[Service Broker](sql-server-service-broker.md)|  
|Descreve como a extensão do pool de buffers pode ser usada para fornecer integração consistente de armazenamento de acesso aleatório (unidades de estado sólido) não volátil com o pool de buffers do Mecanismo de Banco de Dados para melhor significativamente a taxa de transferência de E/S.|[Arquivo de extensão do pool de buffers](buffer-pool-extension.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativo sqlservr](../../tools/sqlservr-application.md)   
 [Recursos de banco de dados](../../relational-databases/database-features.md)   
 [Recursos entre instâncias do Mecanismo de Banco de Dados](../database-engine-cross-instance-features.md)  
  
  
