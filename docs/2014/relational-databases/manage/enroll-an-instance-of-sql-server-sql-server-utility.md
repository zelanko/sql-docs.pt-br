---
title: Inscrever uma instância do SQL Server (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.makemanaged.agentaccount.F1
- SQL12.SWB.makemanaged.Summary.F1
- SQL12.SWB.makemanaged.enrolling.F1
- SQL12.SWB.makemanaged.progress.F1
- SQL12.SWB.makemanaged.instancename.F1
- SQL12.SWB.makemanaged.welcome.F1
- SQL12.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1cebb8ef23c5c1c7a12bdc17bc721e51d542a3d6
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810922"
---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>Inscrever uma instância do SQL Server (Utilitário do SQL Server)
  Inscreva uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente para monitorar o desempenho e a configuração como uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O UCP (ponto de controle de utilitário) coleta informações de configuração e de desempenho de instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cada 15 minutos. Estas informações são armazenadas no UMDW (data warehouse de gerenciamento do utilitário) no UCP; o nome de arquivo UMDW é sysutility_mdw. Dados de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são comparados a políticas para ajudar a identificar gargalos no uso de recursos e oportunidades de consolidação.  
  
 Nesta versão, o UCP e todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem atender aos seguintes requisitos:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar na versão 10.50 ou superior.  
  
-   O tipo da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   O Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve operar dentro de um único domínio do Windows ou de domínios com relações de confiança bidirecionais.  
  
-   As contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no UCP e todas as instâncias gerenciadas do SQL Server devem ter permissão de leitura para Usuários no Active Directory.  
  
-   A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser inscrita não pode ser o SQL Azure.  
  
 Nesta versão, o UCP deve atender aos seguintes requisitos:  
  
-   A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser uma edição com suporte. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   É recomendável que o UCP seja hospedado por uma instância do SQL Server que diferencie maiúsculas de minúsculas.  
  
-   Leve em consideração as seguintes recomendações para o planejamento da capacidade no computador do UCP:  
  
    -   Em um cenário típico, o espaço em disco usado pelo banco de dados UMDW (sysutility_mdw) no UCP é de aproximadamente 2 GB por instância gerenciada do SQL Server por ano. Essa estimativa pode variar dependendo do número de objetos do bancos de dados e do sistema coletados pela instância gerenciada. A taxa de crescimento do espaço em disco de UMDW (sysutility_mdw) é mais alta durante os primeiros dois dias.  
  
    -   Em um cenário típico, o espaço em disco usado pelo msdb no UCP é de aproximadamente 20 MB por instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Observe que essa estimativa pode variar dependendo das políticas de utilização de recursos e do número de objetos do banco de dados e do sistema coletados pela instância gerenciada. Em geral, o uso do espaço em disco aumenta conforme aumentam o número de violações das políticas e a duração da janela de tempo da movimentação de recursos voláteis.  
  
    -   Observe que a remoção de uma instância gerenciada do UCP não reduzirá o espaço em disco usado por bancos de dados do UCP até a expiração dos períodos de retenção dos dados da instância gerenciada.  
  
 Nesta versão, todas as instâncias gerenciadas do SQL Server devem atender aos seguintes requisitos:  
  
-   É recomendável que, se o UCP for hospedado por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sem diferenciação de maiúsculas e minúsculas, as instâncias gerenciadas do SQL Server também não diferenciarão maiúsculas de minúsculas.  
  
-   Não há suporte para dados FILESTREAM para monitoramento do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações, consulte [especificações de capacidade máxima para o SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md) e [recursos compatíveis com as edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Para obter mais informações sobre os conceitos do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Recursos e tarefas do Utilitário do SQL Server](sql-server-utility-features-and-tasks.md).  
  
> [!IMPORTANT]  
>  O conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility tem suporte lado a lado com conjuntos de coleta não Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ou seja, uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser monitorada por outros conjuntos de coleta enquanto ainda é membro de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Observe, no entanto, que todos os conjuntos de coleta na instância gerenciada carregam seus dados no data warehouse de gerenciamento do utilitário. Para obter mais informações, veja [Considerações sobre a execução de Conjuntos de Coleta do Utilitário e não Utilitário na mesma instância do SQL Server](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) e [Configurar o data warehouse do ponto de controle do utilitário &#40;Utilitário do SQL Server&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md).  
  
## <a name="wizard-steps"></a>Etapas do Assistente  
 As seções a seguir fornecem informações detalhadas sobre cada página no fluxo de trabalho do Assistente. Clique no link para buscar os detalhes em uma página do Assistente. Para obter mais informações sobre um script do PowerShell desta operação, veja o [exemplo](#PowerShell_enroll)do PowerShell.  
  
-   [Introdução ao Assistente para Inscrever Instância](#Welcome)  
  
-   [Especificar a instância do SQL Server](#Instance_name)  
  
-   [Caixa de diálogo de conexão](#Connection_dialog)  
  
-   [Conta do conjunto de coleta do utilitário](#Proxy_configuration)  
  
-   [Validação de instância do SQL Server](#Validation_rules)  
  
-   [Resumo da inscrição da instância](#Summary)  
  
-   [Inscrevendo a instância do SQL Server](#Enrolling)  
  
##  <a name="Welcome"></a> Introdução ao Assistente para Inscrever Instância  
 Para iniciar o Assistente, expanda a árvore do Gerenciador do Utilitário em um ponto de controle do utilitário, clique com o botão direito do mouse em **Instâncias Gerenciadas**e selecione **Adicionar Instância Gerenciada...**.  
  
 Para continuar, clique em **Avançar**.  
  
##  <a name="Instance_name"></a> Especificar a instância do SQL Server  
 Para selecionar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na caixa de diálogo de conexão, clique em **Conectar…**. Forneça o nome do computador e o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no formato ComputerName\InstanceName. Para obter mais informações, veja [Conectar-se ao servidor &#40;Mecanismo de Banco de Dados&#41;](../../ssms/f1-help/connect-to-server-database-engine.md).  
  
 Para continuar, clique em **Avançar**.  
  
##  <a name="Connection_dialog"></a> Caixa de diálogo de conexão  
 Na caixa de diálogo Conectar ao Servidor, verifique as informações de tipo de servidor, nome do computador e nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Conectar-se ao servidor &#40;Mecanismo de Banco de Dados&#41;](../../ssms/f1-help/connect-to-server-database-engine.md).  
  
> [!NOTE]  
>  Se a conexão for criptografada, ela será usada. Se a conexão não for criptografada, o Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectará novamente usando uma conexão criptografada.  
  
 Para continuar, clique em **Conectar...**.  
  
##  <a name="Proxy_configuration"></a> Conta do conjunto de coleta do utilitário  
 Especifique uma conta de domínio do Windows para executar o conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa conta é usada como a conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o conjunto de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Alternativamente, você pode usar a conta de Serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent existente. Para passar nos requisitos de validação, use as diretrizes a seguir para especificar a conta.  
  
 Se você especificar a opção de conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
-   A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser uma conta de domínio do Windows que não seja uma conta interna como LocalSystem, NetworkService ou LocalService.  
  
 Para continuar, clique em **Avançar**.  
  
##  <a name="Validation_rules"></a> Validação de instância do SQL Server  
 Nesta versão, as seguintes condições devem ser verdadeiras na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para serem inscritas no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Condição|Ação corretiva|  
|---------------|-----------------------|  
|É necessário ter privilégios de administrador na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no UCP.|Faça logon com uma conta que tenha privilégios de administrador na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no UCP.|  
|A edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve oferecer suporte à inscrição de instância.|Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).|  
|A instância especificada do UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar com o TCP/IP habilitado.|Habilite o TCP/IP no UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode já estar inscrita com nenhum outro UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você especifica já for gerenciada como parte de um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente, você não poderá inscrevê-la com um UCP diferente.|  
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode já ser um UCP.|Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada já for um UCP diferente do UCP ao qual você está conectado, você não poderá inscrevê-la neste UCP.|  
|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter conjuntos de coleta do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados.|Reinstale a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|É necessário parar os conjuntos de coleta na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Pare os conjuntos de coleta pré-existentes na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o coletor de dados estiver desabilitado, habilite-o, pare os conjuntos de coleta em execução e execute novamente as regras de validação para a operação Criar UCP.<br /><br /> Para habilitar o coletor de dados:<br /><br /> No Pesquisador de Objetos, expanda o nó **Gerenciamento** .<br /><br /> Clique com o botão direito do mouse em **Coleta de Dados**e clique em **Habilitar Coleta de Dados**.<br /><br /> Para parar um conjunto de coleta:<br /><br /> No Pesquisador de Objetos, expanda o nó Gerenciamento, expanda **Coleta de Dados**e, em seguida, expanda **Conjuntos de Coleta de Dados do Sistema**.<br /><br /> Clique com o botão direito do mouse no conjunto de coleta a ser interrompido e clique em **Parar Conjunto de Coleta de Dados**.<br /><br /> Uma caixa de mensagem exibirá o resultado dessa ação, e um círculo vermelho no ícone do conjunto de coleta indicará que este foi interrompido.|  
|O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser iniciado na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Inicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar manualmente. Caso contrário, configure o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar automaticamente.|  
|O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser iniciado no UCP.|Inicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no UCP. Se a instância especificada do UCP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar manualmente. Caso contrário, configure o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar automaticamente.|  
|O WMI deve ser configurado corretamente.|Para solucionar problemas de configuração do WMI, veja [Solucionar problemas do Utilitário do SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md).|  
|A conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser uma conta de domínio do Windows válida no UCP.|Especifique uma conta de domínio do Windows válida. Para assegurar que a conta seja válida, faça logon na instância especificada do UCP usando a conta de domínio do Windows.|  
|Se você selecionar a opção de conta proxy, a conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser uma conta de domínio do Windows válida na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Especifique uma conta de domínio do Windows válida. Para assegurar que a conta seja válida, faça logon na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a conta de domínio do Windows.|  
|A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não pode ser uma conta interna, como Serviço de Rede.|Reatribua a conta a uma conta de domínio do Windows. Para assegurar que a conta seja válida, faça logon na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a conta de domínio do Windows.|  
|A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser uma conta de domínio do Windows válida no UCP.|Especifique uma conta de domínio do Windows válida. Para assegurar que a conta seja válida, faça logon na instância especificada do UCP usando a conta de domínio do Windows.|  
|Se você selecionar a opção de conta de serviço, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá ser uma conta de domínio do Windows válida na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Especifique uma conta de domínio do Windows válida. Para assegurar que a conta seja válida, faça logon na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a conta de domínio do Windows.|  
  
 Se houver condições de falha nos resultados da validação, corrija os problemas de bloqueio e clique em **Executar Validação Novamente** para verificar a configuração do computador.  
  
 Para salvar o relatório de validação, clique em **Salvar Relatório** e especifique um local para o arquivo.  
  
 Para continuar, clique em **Avançar**.  
  
##  <a name="Summary"></a> Resumo da inscrição da instância  
 A página de resumo lista as informações sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a serem adicionadas ao Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Configurações de instâncias gerenciadas:  
  
-   Nome da Instância do SQL Server: NomedoComputador\NomedaInstância  
  
-   Conta de Conjunto de Coleta do Utilitário: NomedoDomínio\NomedoUsuário  
  
 Para continuar, clique em **Avançar**.  
  
##  <a name="Enrolling"></a> Inscrevendo a instância do SQL Server  
 A página de inscrição fornece o status da operação:  
  
-   Preparando a instância para inscrição.  
  
-   Criando o diretório de cache para os dados coletados.  
  
-   Configurando o conjunto de coleta do utilitário.  
  
 Para salvar um relatório sobre a operação de inscrição, clique em **Salvar Relatório** e especifique um local para o arquivo.  
  
 Para concluir o Assistente, clique em **Concluir**.  
  
> [!NOTE]  
>  Se você usar a Autenticação do SQL Server para conectar-se à instância do SQL Server para inscrição, e especificar uma conta proxy pertencente a um domínio do Active Directory diferente do domínio onde o UCP está localizado, a validação de instância terá êxito, mas a operação de inscrição falhará apresentando a seguinte mensagem de erro:  
>   
>  Ocorreu uma exceção ao executar uma instrução ou um lote Transact-SQL. (Microsoft.SqlServer.ConnectionInfo)  
>   
>  Informações adicionais: não foi possível obter informações sobre o grupo/usuário '\<DomainName\AccountName>' do Windows NT, código de erro 0x5. (Microsoft SQL Server, Erro: 15404)  
>   
>  Para obter mais informações sobre como solucionar essa falha, veja [Solucionar problemas do Utilitário do SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md).  
  
> [!IMPORTANT]  
>  Não altere nenhuma propriedade do conjunto de coleta “Informações sobre o Utilitário” em uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e não ative/desative a coleta de dados manualmente, pois ela é controlada por um trabalho de agente do utilitário.  
  
 Depois de concluir as etapas do Assistente para Inscrever Instância, clique no nó **Instâncias Gerenciadas** no painel **Navegação do Gerenciador do Utilitário** do SSMS. As instâncias inscritas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas na exibição de lista no painel **conteúdo do Gerenciador do Utilitário** .  
  
 O processo de coleta de dados é iniciado imediatamente, mas pode demorar até 30 minutos para os dados aparecerem pela primeira vez no painel e nos pontos de vista do painel de conteúdo do Gerenciador do Utilitário. A coleta de dados continua uma vez a cada 15 minutos. Para atualizar os dados, clique com o botão direito do mouse no nó **Instâncias Gerenciadas** , no painel de navegação do **Gerenciador do Utilitário** , e selecione **Atualizar**, ou clique com o botão direito do mouse no nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na exibição de lista e selecione **Atualizar**.  
  
 Para remover instâncias gerenciadas do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Instâncias Gerenciadas** no painel de **Navegação do Gerenciador do Utilitário** para popular a exibição de lista de instâncias gerenciadas, clique com o botão direito do mouse no nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na exibição de lista do **Conteúdo do Gerenciador do Utilitário** e selecione **Tornar Instância Não Gerenciada**.  
  
##  <a name="PowerShell_enroll"></a> Inscrever uma instância do SQL Server usando o PowerShell  
 Use o seguinte exemplo para inscrever uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente:  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas do Utilitário do SQL Server](sql-server-utility-features-and-tasks.md)   
 [Monitorar instâncias do SQL Server no Utilitário do SQL Server](monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Solucionar problemas do Utilitário do SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
