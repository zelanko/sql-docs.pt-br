---
title: "Planejar e testar o plano de atualiza&#231;&#227;o do mecanismo de banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19c5b725-7400-4881-af8f-fd232ca28234
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# Planejar e testar o plano de atualiza&#231;&#227;o do mecanismo de banco de dados
  Para executar uma atualização bem-sucedida do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , independentemente da abordagem, o planejamento apropriado é obrigatório.  
  
## Notas de Versão e problemas de atualização conhecidos  
 Antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], examine as [Notas de Versão do SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md) e o tópico [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md).  
  
## Lista de verificação de planejamento da pré-atualização  
 Antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], examine a seguinte lista de verificação e os tópicos associados. Estes tópicos se aplicam a todas as atualizações, independentemente do método, e ajudam a determinar o método de atualização mais apropriado: atualização sem interrupção, atualização de nova instalação ou atualização in-loco. Por exemplo, talvez você não possa executar uma atualização in-loco ou uma atualização sem interrupção se estiver atualizando o sistema operacional, atualizando do SQL Server 2005 ou atualizando de uma versão de 32 bits do SQL Server. Para ver uma árvore de decisão, confira [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
-   **Requisitos de hardware e software:** analise os requisitos de hardware e software para instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esses requisitos podem ser encontrados em: [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md). Uma parte de qualquer ciclo de planejamento de atualização é considerar a atualização do hardware (um hardware mais novo é mais rápido e pode reduzir o licenciamento, seja devido ao menor número de processadores, seja devido à consolidação de banco de dados e servidor) e a atualização do sistema operacional. Esses tipos de alteração de hardware e software afetarão o tipo de método de atualização que você escolhe.  
  
-   **Ambiente atual:** pesquise seu ambiente atual para entender os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão sendo usados e os clientes que se conectam ao seu ambiente.  
  
    -   **Provedores de cliente:** embora a atualização não exija que você atualize o provedor de cada um de seus clientes, você pode optar por fazer isso. Os recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a seguir exigirão um provedor atualizado para cada cliente ou o provedor atualizado fornecerá funcionalidade adicional:  
  
        -   [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
        -   [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
        -   [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md)  
  
        -   Atualização de segurança do SSL  
  
    -   **Componentes de terceiros:** determine a compatibilidade de componentes de terceiros, como backup integrado.  
  
-   **Ambiente de destino:** verifique se seu ambiente de destino atende aos requisitos de hardware e software e se pode lidar com os requisitos do sistema original. Por exemplo, a atualização pode envolver a consolidação de várias instâncias do SQL Server em um instância única e nova do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou a virtualização do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma nuvem privada ou pública.  
  
-   **Edição:** determine a edição apropriada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , bem como os caminhos válidos para a atualização. Para obter informações detalhadas, consulte [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Antes de atualizar de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra, verifique se há suporte à funcionalidade usada atualmente na edição para a qual está atualizando.  
  
    > [!NOTE]  
    >  Quando você atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de uma versão anterior da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise, escolha entre Enterprise Edition: Licenciamento baseado em núcleo e Enterprise Edition. Estas edições Enterprise só diferem com relação aos modos de licenciamento. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
-   **Compatibilidade com versões anteriores:** leia o tópico sobre compatibilidade com versões anteriores do mecanismo de banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para examinar as alterações no comportamento entre o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da qual você está atualizando. Consulte [SQL Server Database Engine Backward Compatibility](../../database-engine/sql-server-database-engine-backward-compatibility.md).  
  
-   **Supervisor de atualização:**  execute o Supervisor de Atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para auxiliar no diagnóstico de problemas que podem bloquear o processo de atualização ou exigem modificação em scripts ou aplicativos existentes devido a uma alteração significativa. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] contém uma nova versão do Supervisor de Atualização para ajudar os clientes a se prepararem para atualizar um sistema existente.  Essa ferramenta também tem a capacidade de verificar os bancos de dados existentes a fim de verificar se eles podem aproveitar novos recursos, como Ampliar Tabelas, depois que a atualização estiver concluída.   
    Você pode baixar o Supervisor de Atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=48119).  
  
-   **Verificador de configuração do sistema:** execute o SCC (Verificador de Configuração do Sistema) do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para determinar se o programa de instalação do SQL Server detecta todos os problemas de bloqueio antes de você agendar de fato a atualização. Para obter mais informações, consulte [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).  
  
-   **Atualização de tabelas com otimização de memória:** ao atualizar uma instância de banco de dados do SQL Server 2014 contendo tabelas com otimização de memória para o SQL Server 2016, o processo de atualização exigirá tempo adicional para converter as tabelas com otimização de memória no novo formato em disco (e o banco de dados estará offline enquanto essas etapas estiverem ocorrendo).   A quantidade de tempo depende do tamanho das tabelas com otimização de memória e da velocidade do subsistema de E/S. A atualização exige três tamanhos de operações de dados para atualizações de instalação nova e in-loco (a etapa 1 não é necessária para atualizações sem interrupção, mas as etapas 2 e 3 são obrigatórias):  
  
    1.  Execute a recuperação de banco de dados usando o formato em disco antigo (isso inclui carregar todos os dados em tabelas com otimização de memória do disco na memória)  
  
    2.  Serialize os dados no disco no novo formato em disco  
  
    3.  Execute a recuperação de banco de dados usando o novo formato (isso inclui carregar todos os dados em tabelas com otimização de memória do disco na memória)  
  
     Além disso, espaço insuficiente em disco durante esse processo causará a falha da recuperação. Verifique se há espaço suficiente no disco para armazenar o banco de dados existente e se o armazenamento adicional é igual ao tamanho atual dos contêineres no grupo de arquivos MEMORY_OPTIMIZED_DATA no banco de dados para executar uma atualização in-loco ou ao anexar um banco de dados do SQL Server 2014 a uma instância do SQL Server 2016. Use a consulta a seguir para determinar o espaço em disco atualmente necessário para o grupo de arquivos MEMORY_OPTIMIZED_DATA e, consequentemente, a quantidade de espaço livre em disco exigida para que a atualização seja bem-sucedida:  
  
    ```  
    select cast(sum(size) as float)*8/1024/1024 'size in GB'   
    from sys.database_files  
    where data_space_id in (select data_space_id from sys.filegroups where type=N'FX')  
    ```  
  
## Desenvolver e testar o plano de atualização  
 A melhor abordagem é tratar a atualização como trataria qualquer projeto de TI. Você deve organizar uma equipe de atualização que tenha a administração, a rede, ETL (extração, transformação e carregamento) e outras habilidades necessárias de banco de dados para a atualização. A equipe precisa:  
  
-   **Escolher o método de atualização:** consulte [Escolher um Método de Atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
-   **Desenvolver um plano de reversão:**. executar esse plano permitirá que você restaure o ambiente original se precisar fazer uma reversão.  
  
-   **Determinar os critérios de aceitação:** você precisa saber se a atualização foi bem-sucedida antes de direcionar os usuários para o ambiente atualizado.  
  
-   **Testar o plano de atualização:** para testar o desempenho usando a carga de trabalho real, use o utilitário Microsoft SQL Server Distributed Replay. Esse utilitário pode usar vários computadores para reproduzir dados de rastreamento, simulando uma carga de trabalho crítica à missão. Ao executar uma reprodução em um servidor de teste antes e depois de uma atualização do SQL Server, você pode medir diferenças de desempenho e procurar alguma incompatibilidade que seu aplicativo possa ter com a atualização. Para obter mais informações, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md) e [Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md).  
  
## Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Plan%20and%20Test%20the%20Database%20Engine%20Upgrade%20Plan%20page)  
  
## Consulte também  
 [Atualizar o Mecanismo de Banco de Dados](../../database-engine/install-windows/upgrade-database-engine.md)  
  
  