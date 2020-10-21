---
description: Trabalhos do SQL Server Agent para pacotes
title: Trabalhos do SQL Server Agent para pacotes | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 04007ee3165838669fd1b0faefdcb20d09940af7
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192464"
---
# <a name="sql-server-agent-jobs-for-packages"></a>Trabalhos do SQL Server Agent para pacotes

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Você pode automatizar e agendar a execução de pacotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Você pode agendar pacotes que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e está armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o Armazenamento de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] e o sistema de arquivos.  
 
> [!NOTE]
> Este artigo descreve como agendar pacotes do SSIS em geral e como agendar pacotes localmente. Também é possível executar e agendar pacotes do SSIS nas seguintes plataformas:
> - **A nuvem do Microsoft Azure**. Para obter mais informações, consulte [Migrar cargas de trabalho do SQL Server Integration Services por lift-and-shift para a nuvem](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md) e [Agendar a execução de um pacote SSIS no Azure](../lift-shift/ssis-azure-schedule-packages.md).
> - **Linux**. Para obter mais informações, consulte [Extrair, transformar e carregar dados em Linux com o SSIS](../../linux/sql-server-linux-migrate-ssis.md) e [Schedule SQL Server Integration Services package execution on Linux with cron](../../linux/sql-server-linux-schedule-ssis-packages.md) (Agendar a execução do pacote do SQL Server Integration Services no Linux com cron).

## <a name="sections-in-this-topic"></a>Seções neste tópico  
 Este tópico contém as seguintes seções:  
  
-   [Agendando trabalhos no SQL Server Agent](#jobs)  
  
-   [Agendando pacotes do Integration Services](#packages)  
  
-   [Solucionando problemas de pacotes agendados](#trouble)  
  
##  <a name="scheduling-jobs-in-sql-server-agent"></a><a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent é o serviço instalado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite automatizar e agendar tarefas executando trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar sendo executado antes que os trabalhos possam ser executados automaticamente. Para obter mais informações, consulte [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md).  
  
 O nó do **SQL Server Agent** é exibido no Pesquisador de Objetos em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando você se conecta a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para automatizar uma tarefa recorrente, crie um trabalho na caixa de diálogo **Novo Trabalho** . Para obter mais informações, consulte [Implementar trabalhos](../../ssms/agent/implement-jobs.md).  
  
 Depois de criar o trabalho, adicione pelo menos uma etapa. Um trabalho pode incluir várias etapas, e cada etapa pode executar uma tarefa diferente. Para obter mais informações, consulte [Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md).  
  
 Depois de criar o trabalho e as etapas do trabalho, crie uma agenda para executar o trabalho. Entretanto, você também pode criar um trabalho agendado para execução manual. Para obter mais informações, veja [Criar e anexar agendamentos a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 Você pode aperfeiçoar o trabalho configurando opções de notificação, como especificar um operador para enviar uma mensagem de email quando o trabalho for concluído ou adicionar alertas. Para obter mais informações, consulte [Alertas](../../ssms/agent/alerts.md).  
  
##  <a name="scheduling-integration-services-packages"></a><a name="packages"></a> Scheduling Integration Services Packages  
 Quando você cria um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , é necessário adicionar pelo menos uma etapa e definir o tipo da etapa para o **Pacote do SQL Server Integration**. Um trabalho pode incluir várias etapas, e cada etapa pode executar um pacote diferente.  
  
 A execução de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de uma etapa de trabalho é semelhante à execução de um pacote com os utilitários **dtexec** (dtexec.exe) e **DTExecUI** (dtexecui.exe). Em vez de configurar as opções de tempo de execução para um pacote usando as opções de linha de comando ou a caixa de diálogo **Executar Utilitário de Pacote** , defina as opções de tempo de execução na caixa de diálogo **Nova Etapa do Trabalho** . Para obter mais informações sobre as opções para executar um pacote, consulte [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md).  
  
 Para obter mais informações, consulte [Agendar um pacote usando o SQL Server Agent](#schedule).  
  
 Assista a um vídeo que demonstra como usar o Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar um pacote na página inicial de vídeos, [Como automatizar a execução de pacotes usando o SQL Server Agent (vídeo do SQL Server)](/previous-versions/sql/sql-server-2008/dd440761(v=sql.100)), na Biblioteca MSDN.  
  
##  <a name="troubleshooting"></a><a name="trouble"></a> Solução de problemas  
 Uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não inicia um pacote, embora o pacote seja executado com êxito no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e na linha de comando. Há algumas razões comuns para esse problema e várias soluções recomendadas. Para obter mais informações, consulte os recursos a seguir.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Artigo da Base de Dados de Conhecimento, [Um pacote SSIS não é executado quando você chama o pacote SSIS a partir de uma etapa de trabalho do SQL Server Agent](https://support.microsoft.com/kb/918760)  
  
-   Vídeo, [Solução de problemas: execução de pacotes SSIS usando o SQL Server Agent (vídeo do SQL Server)](/previous-versions/sql/sql-server-2008/dd440760(v=sql.100)), na Biblioteca MSDN.  
  
 Depois que uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent iniciar um pacote, a execução do pacote poderá falhar ou o pacote poderá ser executado com êxito, mas com resultados inesperados. Você pode usar uma das ferramentas a seguir para solucionar esses problemas.  
  
-   Para pacotes armazenados no banco de dados MSDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o repositório de pacotes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , ou em uma pasta no computador local, você pode usar o **Visualizador do Arquivo de Log** , bem como todos os logs e arquivos de despejo de depuração gerados durante a execução do pacote.  
  
     **Para usar o Visualizador do Arquivo de Log, siga os procedimentos a seguir.**  
  
    1.  Clique com o botão direito do mouse no trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Pesquisador de Objetos. Em seguida, clique em **Exibir Histórico**.  
  
    2.  Localize a execução do trabalho na caixa **Resumo do arquivo de log** com a mensagem **falha no trabalho** na coluna **Mensagem** .  
  
    3.  Expanda o nó do trabalho, e clique na etapa de trabalho para exibir os detalhes da mensagem na área abaixo da caixa **Resumo do arquivo de log** .  
  
-   Para pacotes armazenados no banco de dados SSISDB, você também pode usar o **Visualizador do Arquivo de Log** , bem como todos os logs e arquivos de despejo de depuração gerados durante a execução do pacote. Além de isso, você pode usar os relatórios do servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     **Para localizar informações nos relatórios para a execução do pacote associada à execução de um trabalho, siga os procedimentos abaixo.**  
  
    1.  Siga as etapas anteriores para exibir os detalhes da mensagem para a etapa de trabalho.  
  
    2.  Localize a ID da execução listada na mensagem.  
  
    3.  Expanda o nó Catálogo do Integration Services no Pesquisador de Objetos.  
  
    4.  Clique com o botão direito do mouse em SSISDB, aponte para Relatórios, depois para Relatórios Padrão e, então, clique em Todas as Execuções.  
  
    5.  No relatório **Todas as Execuções** , localize a ID de execução na coluna **ID** . Clique em **Visão Geral**, **Todas as Mensagens**ou **Desempenho de Execução** para exibir informações sobre essa execução de pacote.  
  
    Para obter mais informações sobre os relatórios Visão Geral, Todas as Mensagens e Desempenho de Execução, consulte [Relatórios do servidor do Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  

## <a name="schedule-a-package-by-using-sql-server-agent"></a><a name="schedule"></a> Agendar um pacote usando o SQL Server Agent
  O procedimento a seguir fornece as etapas para automatizar a execução do pacote usando uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar o pacote.  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>Para automatizar a execução do pacote usando o SQL Server Agent  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você deseja criar um trabalho ou a instância que contém o trabalho ao qual deseja adicionar uma etapa.  
  
2.  Expanda o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Pesquisador de Objetos e execute uma das tarefas a seguir:  
  
    -   Para criar um trabalho novo, clique com o botão direito do mouse em **Trabalhos** e, em seguida, clique em **Novo Trabalho**.  
  
    -   Para adicionar uma etapa a um trabalho existente, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho e, em seguida, clique em **Propriedades**.  
  
3.  Na página **Geral** , se você estiver criando um novo trabalho, forneça um nome de trabalho, selecione uma categoria e um proprietário e, se desejar, forneça uma descrição do trabalho.  
  
4.  Para disponibilizar o trabalho para agendamento, selecione **Habilitado**.  
  
5.  Para criar uma etapa de trabalho do pacote que deseja agendar, clique em **Etapas**e, em seguida, em **Nova**.  
  
6.  Selecione **Pacote do Integration Services** para o tipo de etapa do trabalho.  
  
7.  Na lista **Executar como** , selecione **Conta de Serviço do SQL Server Agent** ou selecione uma conta proxy com as credenciais que a etapa de trabalho usará. Para obter informações sobre como criar uma conta proxy, consulte [Create a SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md).  

    Usar uma conta proxy em vez de uma **Conta de Serviço do SQL Server Agent** pode resolver problemas comuns que podem ocorrer ao executar um pacote usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações sobre esses problemas, consulte o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Artigo da Base de Dados de Conhecimento, [Um pacote SSIS não é executado quando você chama o pacote do SSIS a partir de uma etapa de trabalho do SQL Server Agent](https://support.microsoft.com/kb/918760). 
     
    - Ao executar o trabalho com um Proxy, é preciso ter os itens de segurança a seguir em vigor para que o trabalho seja executado com sucesso.

        As credenciais de logon usadas pelo Proxy, a conta que executa o SQL Server Agent e a conta que executa o serviço do SQL Server exigem as seguintes permissões:

        - Atributo da Política de Segurança Local: Substituir um token de nível de processo
        - Controle total sobre %SYSTEMROOT%\Temp 

        A falha em incluir os itens de segurança resultará na falha do trabalho e em uma mensagem de erro semelhante a esta: Houve falha no trabalho. O cliente não possui o privilégio exigido.

        > **OBSERVAÇÃO:** Se a senha for alterada para as credenciais usadas pela conta proxy, será necessário atualizar a senha da credencial. Caso contrário, a etapa do trabalho falhará.  

        Para obter informações sobre como configurar a conta de serviço do SQL Server Agent, consulte [Definir a conta de inicialização do serviço para o SQL Server Agent &#40;SQL Server Configuration Manager&#41;](../../ssms/agent/set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md).  

8.  Na caixa de listagem **Origem do Pacote** , clique na origem do pacote e configure as opções para a etapa do trabalho.  
  
    **A seguinte tabela descreve as possíveis origens do pacote.**  
  
    |Origem do Pacote|Descrição|  
    |--------------------|-----------------|  
    |**Catálogo do SSIS**|Os pacotes armazenados no banco de dados SSISDB. Os pacotes são contidos em projetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que são implantados no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
    |**SQL Server**|Os pacotes armazenados no banco de dados MSDB. Use o serviço de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para gerenciar esses pacotes.|  
    |**Armazenamento de Pacotes SSIS**|Pacotes que estão armazenados na pasta padrão no computador. A pasta padrão é *\<drive>* :\Arquivos de Programas\Microsoft SQL Server\110\DTS\Pacotes. Use o serviço de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para gerenciar esses pacotes.<br /><br /> Observação: Você pode especificar uma pasta diferente ou pastas adicionais no sistema de arquivos a ser gerenciado pelo serviço de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] modificando o arquivo de configuração para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obter mais informações, veja [Serviço Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).|  
    |**Sistema de Arquivos**|Pacotes que estão armazenados em qualquer pasta em sua máquina local.|  
    |||
  
    **As tabelas seguintes descrevem as opções de configuração que estão disponíveis para a etapa de trabalho segundo a origem do pacote que você selecionou.**  
  
    > **IMPORTANTE:** Se o pacote estiver protegido por senha, quando você clicar em qualquer uma das guias na página **Geral** da caixa de diálogo **Nova Etapa do Trabalho** , com exceção da guia **Pacote** , precisará digitar a senha na caixa de diálogo **Senha do Pacote** que aparecer. Caso contrário, o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não poderá executar o pacote.  
  
    **Origem do pacote**: Catálogo do SSIS  
  
    |Tab|Opções|  
    |---------|-------------|  
    |**Pacote**|**Servidor**<br /><br /> Digite ou selecione o nome da instância de servidor de banco de dados que hospeda o catálogo de SSISDB.<br /><br /> Quando o **Catálogo do SSIS** é a origem do pacote, você pode fazer logon no servidor que usa somente uma conta de usuário do Microsoft Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não disponível.|  
    ||**Pacote**<br /><br /> Clique no botão de reticências e selecione um pacote.<br /><br /> Você está selecionando um pacote em uma pasta sob o nó de **Catálogos do Integration Services** no **Pesquisador de Objetos**.|  
    |**Parâmetros**<br /><br /> Localizado na guia **Configuração** .|O **Assistente de Conversão de Projetos do Integration Services** permite substituir configurações de pacote por parâmetros.<br /><br /> A guia **Parâmetros** exibe os parâmetros que você adicionou quando criou o pacote, por exemplo, usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A guia também exibe os parâmetros que foram adicionados ao pacote quando você converteu o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do modelo de implantação de pacote para o modelo de implantação de projeto. Insira novos valores de parâmetros que estão contidos no pacote. Você pode inserir um valor literal ou usar o valor contido em uma variável de ambiente de servidor que já mapeou para o parâmetro.<br /><br /> Para digitar o valor literal, clique no botão de reticências ao lado de um parâmetro. A caixa de diálogo **Editar Valor Literal para Execução** é exibida.<br /><br /> Para usar uma variável de ambiente, clique em **Ambiente** e selecione o ambiente que contém a variável que você deseja usar.<br /><br /> **\*\* Important \*\*** Se você tiver mapeado vários parâmetros e/ou propriedades do gerenciador de conexões para variáveis contidas em vários ambientes, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent exibirá uma mensagem de erro. Para uma execução específica, um pacote pode ser executado somente com os valores contidos em um único ambiente de servidor.<br /><br /> Para obter informações sobre como criar um ambiente de servidor e mapear uma variável para um parâmetro, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).|  
    |**Gerenciadores de conexões**<br /><br /> Localizado na guia **Configuração** .|Altere os valores das propriedades do gerenciador de conexões. Por exemplo, você pode alterar o nome do servidor. Os parâmetros são gerados automaticamente no servidor do SSIS para as propriedades do gerenciador de conexões. Para alterar um valor de propriedade, você pode inserir um valor literal ou usar o valor contido em uma variável de ambiente de servidor que já mapeou para a propriedade do gerenciador de conexões.<br /><br /> Para digitar o valor literal, clique no botão de reticências ao lado de um parâmetro. A caixa de diálogo **Editar Valor Literal para Execução** é exibida.<br /><br /> Para usar uma variável de ambiente, clique em **Ambiente** e selecione o ambiente que contém a variável que você deseja usar.<br /><br /> **\*\* Important \*\*** Se você tiver mapeado vários parâmetros e/ou propriedades do gerenciador de conexões para variáveis contidas em vários ambientes, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent exibirá uma mensagem de erro. Para uma execução específica, um pacote pode ser executado somente com os valores contidos em um único ambiente de servidor.<br /><br /> Para obter informações sobre como criar um ambiente de servidor e mapear uma variável para uma propriedade do gerenciador de conexões, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).|  
    |**Avançado**<br /><br /> Localizado na guia **Configuração** .|Defina as seguintes configurações adicionais para a execução do pacote:|  
    ||**Substituições de propriedades**:<br /><br /> Clique em **Adicionar** para digitar um novo valor para uma propriedade de pacote, especificar o caminho da propriedade e indicar se o valor da propriedade é confidencial. O servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criptografa dados confidenciais. Para editar ou remover as configurações de uma propriedade, clique em uma linha na caixa das substituições **Propriedade** e clique em **Editar** ou em **Remover**. Você pode encontrar o caminho da propriedade seguindo um destes procedimentos:<br /><br /> -Copie o caminho da propriedade do arquivo de configuração XML (\*.dtsconfig). O caminho é listado na seção Configuração do arquivo como um valor do atributo Caminho. Veja a seguir um exemplo de caminho para a propriedade MaximumErrorCount: \Package.Properties[MaximumErrorCount]<br /><br /> Execute o **Assistente de Configuração de Pacotes** e copie os caminhos da propriedade da página final **Conclusão do Assistente** . Então, você pode cancelar o assistente.<br /><br /> <br /><br /> Observação: A opção de **Substituições de Propriedades** é destinada a pacotes com configurações atualizadas de uma versão anterior de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Pacotes que você cria usando [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] e implanta para o servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usam parâmetros em vez de configurações.|  
    ||**Nível de log**<br /><br /> Selecione um dos seguintes níveis de log para a execução do pacote. Observe que a seleção do nível de log **Desempenho** ou **Detalhado** pode afetar o desempenho da execução do pacote.<br /><br /> **Nenhum**:<br />                          O log está desativado. Apenas o status da execução do pacote é registrado em log.<br /><br /> **Básico**:<br />                          Todos os eventos são registrados em log, menos personalizados e de diagnóstico. Este é o valor padrão do nível de log.<br /><br /> **Desempenho**:<br />                          Apenas estatísticas de desempenho e eventos OnError e OnWarning são registrados em log.<br /><br /> **Detalhado**:<br />                          Todos os eventos são registrados em log, inclusive eventos personalizados e de diagnóstico.<br /><br /> O nível de log selecionado determina quais informações são exibidas em exibições SSISDB e nos relatórios do servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Log do SSIS (Integration Services)](../../integration-services/performance/integration-services-ssis-logging.md).|  
    ||**Despejar quando ocorrerem erros**<br /><br /> Especifique se os arquivos de despejo de depuração são gerados quando ocorre um erro durante a execução do pacote. O arquivo contém informações sobre a execução do pacote que pode ajudar a solucionar problemas de execução. Quando você seleciona essa opção e ocorre um erro durante a execução, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um arquivo .mdmp (arquivo binário) e um arquivo .tmp (arquivo de texto). Por padrão, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazena os arquivos na pasta *\<drive>:* \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps.|  
    ||**runtime de 32 bits**<br /><br /> Indique se o pacote será executado usando a versão de 32 bits do utilitário dtexec em um computador de 64 bits que tenha a versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent instalada.<br /><br /> Você pode precisar executar o pacote usando uma versão de 32 bits do dtexec, por exemplo, se o pacote usar um provedor OLE DB nativo que não esteja disponível em uma versão de 64 bits. Para obter mais informações, consulte [Considerações do Integration Services sobre versões de 64 bits](https://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx).<br /><br /> Por padrão, quando você seleciona o tipo de etapa de trabalho **Pacote do SQL Server Integration Services** , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa o pacote usando a versão do utilitário dtexec invocada automaticamente pelo sistema. O sistema invoca a versão de 32 bits ou de 64 bits do utilitário, dependendo do processador do computador, e a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que está sendo executada no computador.|  
  
     **Origem do pacote**:  SQL Server, Repositório de Pacotes SSIS ou Sistema de Arquivos  
  
     Muitas das opções que você pode definir para pacotes armazenados no SQL Server, no Repositório de Pacotes SSIS ou no sistema de arquivos correspondem às opções de linha de comando para o utilitário de prompt de comando **dtexec** . Para obter mais informações sobre as opções de linha de comando e utilitário, consulte [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md).  
  
    |Tab|Opções|  
    |---------|-------------|  
    |**Pacote**<br /><br /> Estas são as opções da guia para pacotes que estão armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no Armazenamento de pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] .|**Servidor**<br /><br /> Digite ou selecione o nome da instância do servidor do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
    ||**Usar Autenticação do Windows**<br /><br /> Selecione esta opção para fazer logon no servidor usando uma conta de usuário do Microsoft Windows.|  
    ||**Usar Autenticação do SQL Server**<br /><br /> Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua a autenticação verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha registrada previamente. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não localizar a conta de login, ocorrerá uma falha na autenticação e o usuário receberá uma mensagem de erro.|  
    ||**Nome de usuário**|  
    ||**Senha**|  
    ||**Pacote**<br /><br /> Clique no botão de reticências e selecione o pacote.<br /><br /> Você está selecionando um pacote em uma pasta sob o nó de **Pacotes Armazenados** no **Pesquisador de Objetos**.|  
    |**Pacote**<br /><br /> Estas são as opções da guia para pacotes que estão armazenados no sistema de arquivos.|**Pacote**<br /><br /> Digite o caminho completo do arquivo do pacote ou clique no botão de reticências para selecionar o pacote.|  
    |**Configurações**|Adicione um arquivo de configuração XML para executar o pacote com uma configuração específica. Use uma configuração de pacote para atualizar os valores das propriedades do pacote no runtime.<br /><br /> Essa opção corresponde à opção de **/ConfigFile** para **dtexec**.<br /><br /> Para compreender como são aplicadas as configurações de pacote, consulte [Package Configurations](./legacy-package-deployment-ssis.md). Para obter informações sobre como criar uma configuração de pacote, consulte [Create Package Configurations](./legacy-package-deployment-ssis.md).|  
    |**Arquivos de comando**|Especifique opções adicionais que deseja executar com **dtexec**em um arquivo separado.<br /><br /> Por exemplo, você pode incluir um arquivo que contém a opção de /Dump *errorcode* para gerar arquivos de despejo de depuração quando um ou mais eventos especificados ocorrerem durante a execução do pacote.<br /><br /> Você pode executar um pacote com conjuntos diferentes de opções criando vários arquivos e especificando o arquivo apropriado usando a opção **Arquivos de Comando** .<br /><br /> A opção **Arquivos de comando** corresponde à opção **/CommandFile** para **dtexec**.|  
    |**Fontes de dados**|Exiba os gerenciadores de conexões contidos no pacote. Para modificar uma cadeia de caracteres de conexão, clique no gerenciador de conexões e depois na cadeia de conexões.<br /><br /> Essa opção corresponde à opção de **/Connection** para **dtexec**.|  
    |**Opções de Execução**|**Reprovar o pacote nos avisos de validação**<br /> Indica se uma mensagem de aviso é considerada um erro. Se você selecionar essa opção e ocorrer um aviso durante a validação, o pacote falhará durante a validação. Essa opção corresponde à opção de **/WarnAsError** para **dtexec**.<br /><br /> **Validar pacote sem executar**<br /> Indica se a execução do pacote é interrompida depois da fase de validação, sem executar realmente o pacote. Essa opção corresponde à opção de **/Validate** para **dtexec**.<br /><br /> **Substituir a propriedade MacConcurrentExecutables**<br /> Especifica o número de arquivos executáveis que o pacote pode executar simultaneamente. O valor de -1 significa que o pacote pode executar um número máximo de arquivos executáveis igual ao número total de processadores no computador que executa o pacote mais dois. Essa opção corresponde à opção de **/MaxConcurrent** para **dtexec**.<br /><br /> **Ativar pontos de verificação do pacote**<br /> Indica se o pacote usará pontos de verificação durante sua execução. Para saber mais, confira [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).<br /><br /> Essa opção corresponde à opção de **/CheckPointing** para **dtexec**.<br /><br /> **Substituir opções de reinicialização**<br /> Indica se um novo valor está definido para a propriedade **CheckpointUsage** no pacote. Selecione um valor na caixa de listagem **Opção de Reinicialização** .<br /><br /> Essa opção corresponde à opção de **/Restart** para **dtexec**.<br /><br /> **Use o runtime de 32 bits**<br /> Indique se o pacote será executado usando a versão de 32 bits do utilitário dtexec em um computador de 64 bits que tenha a versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent instalada.<br /><br /> Você pode precisar executar o pacote usando uma versão de 32 bits do dtexec, por exemplo, se o pacote usar um provedor OLE DB nativo que não esteja disponível em uma versão de 64 bits. Para obter mais informações, consulte [Considerações do Integration Services sobre versões de 64 bits](https://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx).<br /><br /> Por padrão, quando você seleciona o tipo de etapa de trabalho **Pacote do SQL Server Integration Services** , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa o pacote usando a versão do utilitário dtexec invocada automaticamente pelo sistema. O sistema invoca a versão de 32 bits ou de 64 bits do utilitário, dependendo do processador do computador, e a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que está sendo executada no computador.|  
    |**Logging**|Associe um provedor de logs à execução do pacote.<br /><br /> **Provedor de log SSIS log para arquivos de Texto**<br /> Grava entradas de log em arquivos de texto ASCII<br /><br /> **Provedor de log SSIS log para o SQL Server**<br /> Escreve entradas de log na tabela sysssislog do banco de dados MSDB.<br /><br /> **Provedor de log SSIS para o SQL Server Profiler**<br /> Grava rastreamentos que você pode exibir usando o SQL Server Profiler.<br /><br /> **Provedor de log SSIS para o Log de Eventos do Windows**<br /> Grava entradas de log no log de aplicativos do log de eventos do Windows Event.<br /><br /> **Provedor de log SSIS log para arquivos XML**<br /> Grava arquivos de log em um arquivo XML.<br /><br /> Para o arquivo de texto, arquivo XML e os provedores de log do Profiler [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você está selecionando os gerenciadores de conexões de arquivos que estão contidos no pacote. Para o provedor de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você está selecionando um gerenciador de conexões OLE DB que está contido no pacote.<br /><br /> Essa opção corresponde à opção de **/Logger** para **dtexec**.|  
    |**Valores definidos**|Substitua uma configuração de propriedade do pacote. Na caixa **Propriedades** , digite os valores nas colunas **Caminho da Propriedade** e **Valor** . Depois que você inserir valores para uma propriedade, uma linha vazia será exibida na caixa **Propriedades** para permitir que você insira valores para outra propriedade.<br /><br /> Para remover uma propriedade da caixa Propriedades, clique na linha e depois em **Remover**.<br /><br /> Você pode encontrar o caminho da propriedade seguindo um destes procedimentos:<br /><br /> -Copie o caminho da propriedade do arquivo de configuração XML (\*.dtsconfig). O caminho é listado na seção Configuração do arquivo como um valor do atributo Caminho. Veja a seguir um exemplo de caminho para a propriedade MaximumErrorCount: \Package.Properties[MaximumErrorCount]<br /><br /> Execute o **Assistente de Configuração de Pacotes** e copie os caminhos da propriedade da página final **Conclusão do Assistente** . Então, você pode cancelar o assistente.|  
    |**Verificação**|**Executar apenas pacotes assinados**<br /> Indica se a assinatura do pacote foi verificada. Se o pacote não for assinado ou a assinatura não for válida, o pacote falhará. Essa opção corresponde à opção de **/VerifySigned** para **dtexec**.<br /><br /> **Verificar a compilação do pacote**<br /> Indica se o número da compilação do pacote será verificado no número da compilação inserido na caixa **Compilar** ao lado dessa opção. Se uma ocorrer um erro de correspondência, o pacote não será executado. Essa opção corresponde à opção de **/VerifyBuild** para **dtexec**.<br /><br /> **Verificar ID do pacote**<br /> Indica se o GUID do pacote será verificado comparando-o ao ID do pacote inserido na caixa **ID do Pacote** ao lado dessa opção. Essa opção corresponde à opção de **/VerifyPackageID** para **dtexec**.<br /><br /> **Verificar ID da versão**<br /> Indica se o GUID da versão do pacote será verificada comparando o ID da versão inserido na caixa **ID da Versão** ao lado dessa opção. Essa opção corresponde à opção de **/VerifyVersionID** para **dtexec**.|  
    |**Linha de comando**|Modifique as opções de linha de comando para dtexec. Para obter mais informações sobre as opções, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).<br /><br /> **Restaurar as opções originais**<br /> Use as opções de linha de comando que você definiu nas guias **Pacote**, **Configurações**, **Arquivos de comando**, **Fontes de dados**, **Opções de execução**, **Logging**, **Definir valores**e **Verificação** da caixa de diálogo **Propriedades do Trabalho** .<br /><br /> **Editar o comando manualmente**<br /> Digite opções adicionais de linha de comando na caixa **Linha de Comando** .<br /><br /> Antes de clicar em **OK** para salvar suas alterações na etapa de trabalho, você pode remover todas as opções adicionais que digitou na caixa **Linha de Comando** clicando em **Restaurar as Opções Originais**.<br /><br /> **\*\* Dica \*\*** Você pode copiar a linha de comando para uma janela de prompt de comando, adicionar `dtexec`e executar o pacote na linha de comando. Essa é uma maneira fácil de gerar o texto da linha de comando.|  
  
9. Clique em **OK** para salvar as configurações e feche a caixa de diálogo **Nova Etapa de Trabalho** .  
  
    > [!NOTE]
    > Para pacotes armazenados no **Catálogo do SSIS**, o botão **OK** é desativado quando há um parâmetro não resolvido ou uma configuração de propriedade do gerenciador de conexões. Uma configuração não resolvida ocorre quando você está usando um valor contido em uma variável de ambiente de servidor para definir o parâmetro ou a propriedade e uma das seguintes condições é atendida:  
    >   
    >  A caixa de seleção **Ambiente** na guia **Configuração** não está marcada.  
    >   
    >  O ambiente de servidor que contém a variável não está selecionado na caixa de listagem na guia **Configuração** .  
  
10. Para criar uma agenda para uma etapa de trabalho, clique em **Agendas** no painel **Selecionar uma Página** . Para obter informações sobre como configurar uma agenda, consulte [Schedule a Job](../../ssms/agent/schedule-a-job.md).  
  
    > [!TIP]  
    >  Ao nomear a agenda, use um nome que seja exclusivo e descritivo para que você possa distinguir mais facilmente a agenda de outras agendas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  

## <a name="see-also"></a>Consulte Também  
 [Execução de projetos e pacotes](deploy-integration-services-ssis-projects-and-packages.md)  

## <a name="external-resources"></a>Recursos externos  
  
-   Artigo da Base de Dados de Conhecimento [Um pacote do SSIS não é executado quando você chama o pacote do SSIS a partir de uma etapa de trabalho do SQL Server Agent](https://support.microsoft.com/kb/918760), no site do [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Vídeo, [Solução de problemas: execução de pacotes SSIS usando o SQL Server Agent (vídeo do SQL Server)](/previous-versions/sql/sql-server-2008/dd440760(v=sql.100)), na Biblioteca MSDN  
  
-   Vídeo, [Como automatizar a execução de pacotes usando o SQL Server Agent (vídeo do SQL Server)](/previous-versions/sql/sql-server-2008/dd440761(v=sql.100)), na Biblioteca MSDN  
  
-   Artigo técnico [Checking SQL Server Agent jobs using Windows PowerShell](https://go.microsoft.com/fwlink/?LinkId=165675)(Verificando trabalhos do SQL Server Agent usando o Windows PowerShell), em mssqltips.com  
  
-   Artigo técnico [Auto alert for SQL Agent jobs when they are enabled or disabled](https://go.microsoft.com/fwlink/?LinkId=165676)(Alerta automático para trabalhos do SQL Agent quando estão habilitados ou desabilitados), em mssqltips.com  
  
-   Entrada de blog, [Configuring SQL Agent Jobs to Write to Windows Event Log](https://go.microsoft.com/fwlink/?LinkId=220745)(Configurando trabalhos do SQL Agent para gravação Log de Eventos do Windows), em mssqltips.com.  
  
