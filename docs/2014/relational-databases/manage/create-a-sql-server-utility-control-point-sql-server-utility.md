---
title: Criar um ponto de controle do Utilitário do SQL Server (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.create.ucp.progress.F1
- SQL12.SWB.create.ucp.welcome.F1
- SQL12.SWB.create.ucp.Summary.F1
- SQL12.SWB.create.ucp.validation.F1
- SQL12.SWB.create.ucp.instancename.F1
- SQL12.SWB.create.ucp.agentconfiguration.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: eefa464ae8cb694001d40c5ad9090f7f4efbd8e6
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175875"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>Criar um ponto de controle do Utilitário do SQL Server (Utilitário do SQL Server)
  Uma empresa pode ter vários Utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , e cada Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode gerenciar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos da camada de dados. Cada Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem apenas um UCP (ponto de controle do utilitário). Você deve criar um novo UCP para cada Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e cada aplicativo da camada de dados é membro somente de um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , e é gerenciada por um único UCP.

 O UCP coleta informações de configuração e de desempenho de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cada 15 minutos. Estas informações são armazenadas no UMDW (data warehouse de gerenciamento do utilitário) no UCP; o nome de arquivo UMDW é sysutility_mdw. Dados de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são comparados a políticas para ajudar a identificar gargalos no uso de recursos e oportunidades de consolidação.

## <a name="before-you-begin"></a>Antes de começar
 Antes de criar um UCP, revise os seguintes requisitos e recomendações:

 Nesta versão, o UCP e todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem atender aos seguintes requisitos:

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar na versão 10.50 ou superior.

-   O tipo da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser [!INCLUDE[ssDE](../../includes/ssde-md.md)].

-   O Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve operar dentro de um único domínio do Windows ou em domínios com relações de confiança bidirecionais.

-   As contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no UCP e todas as instâncias gerenciadas do SQL Server devem ter permissão de leitura para Usuários no Active Directory.

 Nesta versão, o UCP deve atender aos seguintes requisitos:

-   A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser uma edição com suporte. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).

-   É recomendável que o UCP seja hospedado por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que diferencie maiúsculas de minúsculas.

 Leve em consideração as seguintes recomendações para o planejamento da capacidade no computador do UCP:

-   Em um cenário típico, o espaço em disco usado pelo banco de dados UMDW (sysutility_mdw) no UCP é de aproximadamente 2 GB por instância gerenciada do SQL Server por ano. Essa estimativa pode variar dependendo do número de objetos do bancos de dados e do sistema coletados pela instância gerenciada. A taxa de crescimento do espaço em disco de UMDW (sysutility_mdw) é mais alta durante os primeiros dois dias.

-   Em um cenário típico, o espaço em disco usado pelo msdb no UCP é de aproximadamente 20 MB por instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Observe que essa estimativa pode variar dependendo das políticas de utilização de recursos e do número de objetos do banco de dados e do sistema coletados pela instância gerenciada. Em geral, o uso do espaço em disco aumenta conforme aumentam o número de violações das políticas e a duração da janela de tempo da movimentação de recursos voláteis.

-   Observe que a remoção de uma instância gerenciada do UCP não reduzirá o espaço em disco usado por bancos de dados do UCP até a expiração dos períodos de retenção dos dados da instância gerenciada.

 Nesta versão, todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem atender aos seguintes requisitos:

-   Recomendamos que, se o UCP for hospedado por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que não diferencia maiúsculas e minúsculas, as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também não deverão diferenciar maiúsculas de minúsculas.

-   Não há suporte para dados FILESTREAM para monitoramento do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

 Para obter mais informações, consulte [especificações de capacidade máxima para SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) e [recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).

### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>Remover pontos de controle do utilitário anteriores antes de instalar um novo
 Se estiver instalando um ponto de controle do utilitário (UCP) em uma instância do SQL Server que nunca foi configurada como um UCP, antes você deverá remover todas as instâncias gerenciadas do SQL Server e remover o UCP. Faça isso executando o procedimento armazenado **sp_sysutility_ucp_remove** .

 Antes de executar o procedimento, observe os seguintes requisitos:

-   Esse procedimento deve ser executado em um computador que seja um UCP.

-   Esse procedimento deve ser executado por um usuário com permissões de sysadmin, as mesmas permissões necessárias para criar um UCP.

-   Todas as instâncias gerenciadas do SQL Server devem ser removidas do UCP. Observe que o UCP é uma instância gerenciada do SQL Server. Para obter mais informações, confira [Como remover uma instância do SQL Server do Utilitário do SQL Server](https://go.microsoft.com/fwlink/?LinkId=169392).

 Use este procedimento para remover um SQL Server UCP do Utilitário do SQL Server. Após a conclusão da operação, um UCP pode ser novamente criado na instância do SQL Server.

 Use o SQL Server Management Studio para conectar-se ao UCP e, em seguida, execute este script:

```sql
EXEC msdb.dbo.sp_sysutility_ucp_remove;
```

> [!NOTE]
>  Se a instância do SQL Server em que o UCP foi removido tiver um conjunto de coleta de dados que não seja do Utilitário, o banco de dados sysutility_mdw não será removido pelo procedimento. Neste caso, o banco de dados sysutility_mdw deverá ser removido manualmente antes de o UCP ser criado novamente.

 Cada instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e cada aplicativo da camada de dados é membro somente de um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , e é gerenciada por um único UCP. Para obter mais informações sobre os conceitos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Recursos e tarefas do Utilitário do SQL Server](sql-server-utility-features-and-tasks.md).

 Um UCP é o ponto de raciocínio central do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Com o UCP, é possível exibir informações de configuração e desempenho coletadas de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de aplicativos da camada de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executar atividades gerais de planejamento da capacidade. O UCP é o ponto de inicialização para inscrição e remoção de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.

 Após a inscrição de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, é possível monitorar a integridade dos recursos para instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de aplicativos de associação de dados para identificar oportunidades de consolidação e isolar gargalos de recursos. Para obter mais informações, consulte [Monitorar instâncias do SQL Server no Utilitário do SQL Server](monitor-instances-of-sql-server-in-the-sql-server-utility.md).

> [!IMPORTANT]
>  O conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility tem suporte lado a lado com conjuntos de coleta não Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ou seja, uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser monitorada por outros conjuntos de coleta enquanto ainda é membro de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Observe, no entanto, que todos os conjuntos de coleta na instância gerenciada carregarão seus dados no data warehouse de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Considerações sobre a execução de Conjuntos de Coleta do Utilitário e não Utilitário na mesma instância do SQL Server](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) e [Configurar o data warehouse do ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md).

## <a name="wizard-steps"></a>Etapas do Assistente
 ![](../../database-engine/media/create-ucp.gif "Create_UCP")

 As seções a seguir fornecem informações sobre cada página no fluxo de trabalho do assistente para criar um novo UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para iniciar o assistente para criar um UCP, abra o painel do Gerenciador do Utilitário no menu Exibir do SSMS e, em seguida, clique no botão ![](../../database-engine/media/create-ucp.gif "Create_UCP") **Criar UCP** na parte superior do painel do Gerenciador do Utilitário.

 Clique em um link na lista abaixo para navegar para os detalhes de uma página do assistente:

 Para obter mais informações sobre um script do PowerShell desta operação, consulte o [exemplo](#PowerShell_create_UCP).

-   [Introdução ao Assistente para Criar UCP](#Welcome)

-   [Especificar Instância](#Instance_name)

-   [Caixa de diálogo de conexão](#Connection_dialog)

-   [Conta do conjunto de coleta do utilitário](#Agent_configuration)

-   [Regras de validação](#Validation_rules)

-   [Resumo](#Summary)

-   [Criando o ponto de controle do utilitário](#Creating_UCP)

##  <a name="Welcome"></a> Introdução ao Assistente para Criar UCP
 Se você abrir o Gerenciador do Utilitário e não houver nenhum ponto de controle de utilitário conectado, deverá se conectar a um ou criar um novo.

 **Conectar ao UCP existente**: se já houver um ponto de controle do utilitário na implantação, você poderá se conectar a ele clicando no botão ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**Conectar ao Utilitário** na parte superior do painel do Gerenciador do Utilitário. Para se conectar a um UCP existente, você deve ter credenciais de administrador ou ser membro da função Leitor do Utilitário. Observe que pode haver somente um UCP por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility e você pode ser conectado a um UCP somente de uma instância de SSMS.

 **Criar um UCP**: para criar um ponto de controle do utilitário, clique no botão ![](../../database-engine/media/create-ucp.gif "Create_UCP")**Criar UCP** na parte superior do painel do Gerenciador do Utilitário. Para criar um novo UCP, especifique o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e forneça credenciais de administrador na caixa de diálogo de conexão. Observe que pode haver somente um UCP por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.

##  <a name="Instance_name"></a> Especificar Instância
 Especifique as seguintes informações sobre o UCP que você está criando:

-   **Nome da Instância** – para selecionar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na caixa de diálogo de conexão, clique em **Conectar...** . Forneça o nome do computador e o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no formato ComputerName\InstanceName.

-   **Nome do Utilitário** – Especifique um nome que será usado para identificar o Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na rede.

 Para continuar, clique em **Avançar**.

##  <a name="Connection_dialog"></a> Caixa de diálogo Conexão
 Na caixa de diálogo Conectar ao Servidor, verifique as informações de tipo de servidor, nome do computador e nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Conectar-se ao servidor &#40;Mecanismo de Banco de Dados&#41;](../../ssms/f1-help/connect-to-server-database-engine.md).

> [!NOTE]
>  Se a conexão for criptografada, ela será usada. Se a conexão não for criptografada, o Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectará novamente usando uma conexão criptografada.

 Para continuar, clique em **Conectar...** .

##  <a name="Agent_configuration"></a> Conta do conjunto de coleta do utilitário
 Especifique uma conta de domínio do Windows para executar o conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa conta é usada como a conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Alternativamente, você pode usar a conta de Serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent existente. Para passar nos requisitos de validação, use as diretrizes a seguir para especificar a conta.

 Se você especificar a opção de conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:

-   A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser uma conta de domínio do Windows que não seja uma conta interna como LocalSystem, NetworkService ou LocalService.

 Para continuar, clique em **Avançar**.

##  <a name="Validation_rules"></a> Regras de validação
 Nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as seguintes condições devem ser verdadeiras na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o UCP será criado:

|Regra de validação|Ação Corretiva|
|---------------------|-----------------------|
|Você deve ter privilégios de administrador na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o ponto de controle de utilitário será criado.|Faça logon com uma conta que tenha privilégios de administrador na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|
|A versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser 10.50 ou superior.|Especifique uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o UCP.|
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser uma edição com suporte. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).|Especifique uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o UCP.|
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não deve ser uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inscrita em nenhum outro UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Especifique uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o UCP ou cancele a inscrição da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do UCP onde é atualmente uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode já ser o host de um ponto de controle de utilitário.|Especifique uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o UCP.|
|A instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar com o TCP/IP habilitado.|Habilite o TCP/IP da instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ter um banco de dados chamado “sysutility_mdw”.|A operação de criação de UCP criará um data warehouse de gerenciamento de utilitário chamado (UMDW) "sysutility_mdw". A operação exige que o nome não exista no computador no momento em que as regras de validação são executadas. Para continuar, você deve remover ou renomear qualquer banco de dados chamado "sysutility_mdw". Para obter mais informações sobre as operações de renomeação, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).|
|É necessário parar os conjuntos de coleta na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Interrompa os conjuntos de coleta preexistentes enquanto o UCP é criado na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o coletor de dados estiver desabilitado, habilite-o, pare os conjuntos de coleta em execução e execute novamente as regras de validação para a operação Criar UCP.<br /><br /> Para habilitar o coletor de dados:<br /><br /> No Pesquisador de Objetos, expanda o nó **Gerenciamento** .<br /><br /> Clique com o botão direito do mouse em **Coleta de Dados**e clique em **Habilitar Coleta de Dados**.<br /><br /> Para parar um conjunto de coleta:<br /><br /> No Pesquisador de Objetos, expanda o nó Gerenciamento, expanda **Coleta de Dados**e, em seguida, expanda **Conjuntos de Coleta de Dados do Sistema**.<br /><br /> Clique com o botão direito do mouse no conjunto de coleta a ser interrompido e clique em **Parar Conjunto de Coleta de Dados**.<br /><br /> Uma caixa de mensagem exibirá o resultado dessa ação, e um círculo vermelho no ícone do conjunto de coleta indicará que este foi interrompido.|
|O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser iniciado na instância especificada. Se a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser configurado para iniciar manualmente. Caso contrário, o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser configurado para iniciar automaticamente.|Inicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar manualmente. Caso contrário, configure o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar automaticamente.|
|O WMI deve ser configurado corretamente.|Para solucionar problemas de configuração do WMI, veja [Solucionar problemas do Utilitário do SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md).|
|A conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não pode ser uma conta interna, como Serviço de Rede.|Se a conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for uma conta interna, como Serviço de Rede, reatribua a conta a uma conta de domínio do Windows que seja sysadmin.|
|Se você selecionar a opção de conta proxy, a conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser uma conta de domínio do Windows válida.|Especifique uma conta de domínio do Windows válida. Para assegurar que a conta seja válida, faça logon na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a conta de domínio do Windows.|
|Se você selecionar a opção de conta de serviço, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não poderá ser uma conta interna, como Serviço de Rede.|Se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for uma conta interna, como Serviço de Rede, reatribua a conta a uma conta de domínio do Windows.|
|Se você selecionar a opção de conta de serviço, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser uma conta de domínio do Windows válida.|Especifique uma conta de domínio do Windows válida. Para assegurar que a conta seja válida, faça logon na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a conta de domínio do Windows.|

 Se houver condições de falha nos resultados da validação, corrija os problemas de bloqueio e clique em **Executar Validação Novamente** para verificar a configuração do computador.

 Para salvar o relatório de validação, clique em **Salvar Relatório** e especifique um local para o arquivo.

 Para continuar, clique em **Avançar**.

##  <a name="Summary"></a> Resumo
 A página de resumo exibe as informações que você forneceu sobre o UCP:

-   O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o UCP.

-   O nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.

-   O nome da conta que será usada para execução de trabalhos para a coleta de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.

 Para alterar os parâmetros de configuração do UCP, clique em **Anterior**. Para continuar, clique em **Avançar**.

##  <a name="Creating_UCP"></a> Criando o ponto de controle do utilitário
 Durante a operação para criar o UCP, o assistente exibirá as etapas e fornecerá o status:

-   Preparando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para criação do UCP.

-   Criando o UMDW (data warehouse de gerenciamento do utilitário).

-   Inicializando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UMDW; o nome de arquivo UMDW é sysutility_mdw.

-   Configurando o UCP.

-   Configurando o conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

 Para salvar um relatório sobre a operação de criação de UCP, clique em **Salvar Relatório** e especifique um local para o arquivo.

 Para concluir o assistente, clique em **Concluir**.

 Após a conclusão do Assistente para Criar UCP, o painel de navegação Gerenciador do Utilitário no SSMS exibirá um nó para o UCP com nós sob ele para Aplicativos da Camada de Dados Implantados, Instâncias Gerenciadas e Administração do Utilitário. O UCP se torna automaticamente uma instância gerenciada.

 O processo de coleta de dados é iniciado imediatamente, mas pode demorar até 30 minutos para os dados aparecerem pela primeira vez no painel e nos pontos de vista do painel de conteúdo do Gerenciador do Utilitário. A coleta de dados continua uma vez a cada 15 minutos. Os dados iniciais serão do próprio UCP. Ou seja, o UCP é a primeira instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.

 Para exibir o painel, clique em **Exibir** e selecione **Conteúdo do Gerenciador do Utilitário** no menu SSMS. Para atualizar os dados, clique com o botão direito do mouse no nome do utilitário no painel Gerenciador do Utilitário e selecione **Atualizar**.

 Para obter mais informações sobre como inscrever instâncias adicionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md). Para remover o UCP como uma instância gerenciada do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Instâncias Gerenciadas** no painel **Gerenciador do Utilitário** para popular a exibição de lista das instâncias gerenciadas, clique com o botão direito do mouse no nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na exibição de lista **Conteúdo do Gerenciador do Utilitário** e selecione **Tornar Instância Não Gerenciada**.

##  <a name="PowerShell_create_UCP"></a> Criar um novo ponto de controle de utilitário usando o PowerShell
 Use o seguinte exemplo para criar um novo ponto de controle de utilitário:

```powershell
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";
$SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");
```

## <a name="see-also"></a>Consulte Também
 [Utilitário do SQL Server recursos e tarefas](sql-server-utility-features-and-tasks.md) [solucionar problemas de utilitário do SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)
