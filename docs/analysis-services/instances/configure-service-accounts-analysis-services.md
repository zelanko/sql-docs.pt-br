---
title: Configurar contas de serviço (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc968281f9aec0cc86f7b5f8f92fb035d9854af9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209538"
---
# <a name="configure-service-accounts-analysis-services"></a>Configurar contas de serviço (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O provisionamento de conta de todo o produto é documentado em [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md), um tópico que fornece informações abrangentes da conta de serviço para todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluindo o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Consulte-o para obter informações sobre tipos de contas válidos, privilégios do Windows atribuídos por configuração, permissões do sistema de arquivo, permissões de registro e muito mais.  
  
 Este tópico fornece informações complementares para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluindo as permissões adicionais necessárias para instalações em tabela e em cluster. Abrange também as permissões necessárias para oferecer suporte às operações do servidor. Por exemplo, você pode configurar operações de processamento e de consulta para serem executadas na conta d serviço, caso no qual você terá de conceder permissões adicionais para funcionar.  
  
-   [Privilégios do Windows atribuídos ao Analysis Services](#bkmk_winpriv)  
  
-   [Permissões do sistema de arquivos atribuídos ao Analysis Services](#bkmk_FilePermissions)  
  
-   [Concedendo permissões adicionais para operações de servidor específico](#bkmk_tasks)  
  
 Uma etapa de configuração adicional, e não documentada aqui, é registrar um SPN (nome da entidade de serviço) para a instância e a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Essa etapa habilita a autenticação de passagem de aplicativos cliente a fontes de dados back-end em cenários de salto duplo. Essa etapa somente se aplica aos serviços configurados para delegação restrita de Kerberos. Consulte [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) para obter mais instruções.  
  
## <a name="logon-account-recommendations"></a>Recomendações de conta de logon  
 Em um cluster de failover, todas as instâncias do Analysis Services devem ser configuradas para usar uma conta de usuário de domínio do Windows. Atribua a mesma conta para todas as instâncias. Consulte [Como realizar cluster no Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) para obter detalhes.  
  
 Instâncias autônomas devem usar a conta virtual padrão, **NT Service\MSSQLServerOLAPService** para a instância padrão, ou **NT Service\MSOLAP$** _nome de instância_ para uma instância nomeada. Essa recomendação se aplica a instâncias do Analysis Services em todos os modos de servidor, considerando o Windows Server 2008 R2 e posterior para o sistema operacional e o SQL Server 2012 e posterior para o Analysis Services.  
  
## <a name="granting-permissions-to-analysis-services"></a>Concedendo permissões ao Analysis Services  
 Esta seção explica as permissões exigidas para operações internas e locais do Analysis Services, tais como iniciar o executável, ler o arquivo de configuração e carregar os bancos de dados do diretório de dados. Se você estiver procurando orientação sobre definição de permissões para acesso a dados externos e interoperabilidade com outros serviços e aplicativos, consulte [Concedendo permissões adicionais para operações de servidor específicas](#bkmk_tasks) mais adiante neste tópico.  
  
 Para operações internas, o detentor da permissão no Analysis Services não é a conta de logon, mas um grupo de segurança local do Windows criado pelo programa de instalação que contém o SID por serviço. A atribuição de permissões ao grupo de segurança é consistente com as versões anteriores do Analysis Services. Além disso, as contas de logon podem mudar com o tempo, mas o SID por serviço e o grupo de segurança local são constantes durante o ciclo de vida da instalação do servidor. Para o Analysis Services, isso torna o grupo de segurança, em vez da conta de logon, uma opção melhor para manter permissões. Sempre que você conceder direitos para a instância de serviço manualmente, sejam permissões ou privilégios do Windows, conceda permissões ao grupo de segurança local criado para a instância do servidor.  
  
 O nome do grupo de segurança segue um padrão. O prefixo é sempre **SQLServerMSASUser$** , seguido pelo nome do computador e terminando com o nome da instância. A instância padrão é **MSSQLSERVER**. Uma instância nomeada é o nome fornecido durante a instalação.  
  
 Você pode ver esse grupo de segurança nas configurações de segurança local:  
  
-   Execute compmgmt. msc | **Usuários e grupos locais** | **grupos** | **SQLServerMSASUser$** \<nome do servidor > **$MSSQLSERVER**  (para uma instância padrão).  
  
-   Clique duas vezes no grupo de segurança para exibir seus membros.  
  
 O único membro do grupo é o SID por serviço. Ao lado dele fica a conta de logon. O nome da conta de logon é apenas uma ilustração, a fim de fornecer contexto para o SID por serviço. Se você alterar posteriormente a conta de logon e retornar a esta página, observará que o grupo de segurança e o SID por serviço não serão alterados, mas o rótulo da conta de logon será diferente.  
  
##  <a name="bkmk_winpriv"></a> Privilégios do Windows atribuídos à conta de serviço do Analysis Services  
 O Analysis Services precisa de permissões do sistema operacional para iniciar o serviço e para solicitar recursos do sistema. Os requisitos variam de acordo com o modo do servidor e se a instância está agrupada. Se não estiver familiarizado com os privilégios do Windows, consulte [Privilégios](http://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) e [Constantes de privilégio (Windows)](/windows/desktop/SecAuthZ/privilege-constants) para obter detalhes.  
  
 Todas as instâncias do Analysis Services exigem o privilégio **Fazer logon como um serviço** (SeServiceLogonRight). A Instalação do SQL Server atribui o privilégio a você na conta de serviço especificada durante a instalação. Para servidores executados nos modos multidimensional e mineração de dados, esse é o único privilégio do Windows exigido pela conta de serviço do Analysis Services para instalações autônomas de servidores, bem como é o único privilégio que a Instalação configura para o Analysis Services. Para instâncias em cluster e de tabela, privilégios adicionais do Windows devem ser adicionados manualmente.  
  
 Instâncias de cluster de failover, tanto no modo de tabela quanto no multidimensional, devem ter o privilégio **Aumentar a prioridade de agendamento** (SeIncreaseBasePriorityPrivilege).  
  
 As instâncias de tabela usam os três seguintes privilégios adicionais, os quais devem ser concedidos manualmente após a instância ser instalada.  
  
|||  
|-|-|  
|**Aumentar conjunto de trabalho de processo** (SeIncreaseWorkingSetPrivilege)|Este privilégio está disponível para todos os usuários por padrão por meio do grupo de segurança **Usuários** . Se você bloquear um servidor ao remover um privilégio desse grupo, o Analysis Services pode falhar ao iniciar, registro em log o erro: "Um privilégio obrigatório não é mantido pelo cliente." Quando esse erro ocorre, restaure o privilégio ao Analysis Services, concedendo-o ao grupo de segurança do Analysis Services apropriado.|  
|**Ajustar quotas de memória para um processo** (SeIncreaseQuotaPrivilege)|Este privilégio é usado para solicitar mais memória se um processo tiver recursos insuficientes para concluir a sua execução, sujeito aos limites estabelecidos de memória para a instância.|  
|**Bloquear páginas na memória** (SeLockMemoryPrivilege)|Este privilégio somente é necessário quando a paginação está totalmente desativada. Por padrão, uma instância de servidor de tabela usa o arquivo de paginação do Windows, mas é possível configurá-lo para não usar a paginação do Windows ao definir **VertiPaqPagingPolicy** como 0.<br /><br /> **VertiPaqPagingPolicy** como 1 (padrão) instrui a instância do servidor de tabela a usar o arquivo de paginação do Windows. Alocações não são bloqueadas, permitindo que o Windows realize a paginação conforme necessário. Como a paginação está em uso, não é necessário bloquear páginas na memória. Assim, para a configuração padrão (em que **VertiPaqPagingPolicy** = 1), você não precisa conceder o privilégio **Bloquear páginas na memória** a uma instância de tabela.<br /><br /> **VertiPaqPagingPolicy** como 0. Se você desligar a paginação para o Analysis Services, as alocações são bloqueadas, assumindo que o privilégio **Bloquear páginas na memória** seja concedido à instância de tabela. Com essa configuração e o privilégio **Bloquear páginas na memória** , o Windows não pode realizar a paginação das alocações de memória feitas no Analysis Services quando o sistema está sob pressão de memória. O Analysis Services depende da permissão **Bloquear páginas na memória** como a imposição atrás de **VertiPaqPagingPolicy** = 0. Observe que não recomendamos desativar a paginação do Windows. Ela aumentará a taxa de erros de falta de memória para operações que poderiam ser bem-sucedidas se a paginação fosse permitida. Consulte [Memory Properties](../../analysis-services/server-properties/memory-properties.md) para obter mais informações sobre **VertiPaqPagingPolicy**.|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>Para exibir ou adicionar privilégios do Windows na conta de serviço  
  
1.  Execute GPEDIT.msc | Política de Computador Local | Configuração do Computador | Configurações do Windows | Configurações de Segurança | Políticas Locais | Atribuições de Direitos do Usuário.  
  
2.  Analise as políticas existentes que incluem o **SQLServerMSASUser$** . Esse é um grupo de segurança local encontrado em computadores que possuem uma instalação do Analysis Services. Tanto os privilégios do Windows quanto as permissões de pastas de arquivo são concedidos a esse grupo de segurança. Clique duas vezes na política **Fazer logon como um serviço** para ver como o grupo de segurança está especificado em seu sistema. O nome completo do grupo de segurança poderá variar, dependendo se você instalou o Analysis Services como uma instância nomeada ou não. Use este grupo de segurança, em vez da conta de serviço real, ao adicionar privilégios de conta.  
  
3.  Para adicionar privilégios de conta no GPEDIT, clique com o botão direito do mouse em **Aumentar conjunto de trabalho de processo** e selecione **Propriedades**.  
  
4.  Clique em **Adicionar Usuário ou Grupo**.  
  
5.  Digite o grupo de usuário para a instância do Analysis Services. Lembre-se que a conta de serviço é um membro de um grupo de segurança local, exigindo que você fixe previamente o nome do computador local como o domínio da conta.  
  
     A lista a seguir mostra dois exemplos para uma instância padrão e uma instância nomeada, chamada "Tubular" em uma máquina chamada "SQL01-WIN12", onde o nome da máquina é o domínio local.  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  Repita para **Ajustar cotas de memória para um processo**e, como opção, para **Bloquear páginas na memória** ou **Aumentar a prioridade de agendamento**.  
  
> [!NOTE]  
>  Versões anteriores da Instalação adicionaram inadvertidamente a conta de serviço do Analysis Services ao grupo **Usuários de Log de Desempenho** . Embora essa falha tenha sido corrigida, talvez instalações existentes tenham essa associação de grupo desnecessária. Como a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não requer associação no grupo **Usuários de Log de Desempenho** , você pode removê-la do grupo.  
  
##  <a name="bkmk_FilePermissions"></a> Permissões do sistema de arquivos atribuídas à conta de serviço do Analysis Services  
  
> [!NOTE]  
>  Consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) para obter uma lista de permissões associadas a cada pasta de programa.  
>   
>  Consulte [Configurar o acesso HTTP ao Analysis Services no Serviços de Informações da Internet &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) para obter informações de permissão de arquivo relacionadas à configuração do IIS e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Todas as permissões do sistema de arquivos necessárias para as operações do servidor ─ incluindo permissões necessárias para carga e descarga de bancos de dados a partir de uma pasta de dados designada ─ são atribuídas pela Instalação do SQL Server durante a instalação.  
  
 O detentor da permissão sobre arquivos de dados, executáveis de arquivo de programa, arquivos de configuração, arquivos de log e arquivos temporários é um grupo de segurança local criado pela Instalação do SQL Server.  
  
 Há um grupo de segurança criado para cada instância que você instalar. O grupo de segurança é chamado após a instância ─ tanto **SQLServerMSASUser$ MSSQLSERVER** para a instância padrão, ou **SQLServerMSASUser$** \<servername >$\< InstanceName > para uma instância nomeada. A instalação provisiona esse grupo de segurança com as permissões de arquivo necessárias para executar operações de servidor. Se você verificar as permissões de segurança no diretório \MSAS13.MSSQLSERVER\OLAP\BIN, notará que o grupo de segurança (não a conta de serviço ou seu SID por serviço) é o detentor da permissão nesse diretório.  
  
 O grupo de segurança contém apenas um membro: o SID (Identificador de Segurança) por serviço da conta de inicialização da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . A instalação adiciona o SID por serviço ao grupo de segurança local. O uso de um grupo de segurança local, com associação de SID, é uma diferença sutil, mas perceptível, de como a instalação do SQL Server provisiona o Analysis Services, em comparação com o Mecanismo de Banco de Dados.  
  
 Se acreditar que as permissões de arquivos estão corrompidas, siga estas etapas para verificar se o serviço ainda está provisionado corretamente:  
  
1.  Use a ferramenta de linha de comando de Controle de Serviço (sc.exe) para obter o SID de uma instância de serviço padrão.  
  
     `SC showsid MSSqlServerOlapService`  
  
     Para uma instância nomeada (onde o nome da instância é Tabular), use a seguinte sintaxe:  
  
     `SC showsid MSOlap$Tabular`  
  
2.  Use **Gerenciador de computador** | **usuários e grupos locais** | **grupos** para inspecionar a associação de SQLServerMSASUser$\<servername >$\<instancename > grupo de segurança.  
  
     O SID do membro deve corresponder ao SID por serviço a partir da etapa 1.  
  
3.  Use **Windows Explorer** | **Arquivos de Programas** | **Microsoft SQL Server** | MSASxx.MSSQLServer | **OLAP** | **bin** para verificar se as propriedades de segurança de pasta são concedidas ao grupo de segurança na etapa 2.  
  
> [!NOTE]  
>  Nunca remova nem modifique um SID. Para restaurar um SID por serviço excluído acidentalmente, consulte [ http://support.microsoft.com/kb/2620201 ](http://support.microsoft.com/kb/2620201).  
  
 **Mais informações sobre os SIDs por serviço**  
  
 Toda conta do Windows tem um [SID](http://en.wikipedia.org/wiki/Security_Identifier)associado, mas os serviços também podem ter SIDs, que serão chamados daqui em diante de SIDs por serviço. Um SID por serviço é criado quando a instância do serviço é instalada, como um acessório exclusivo e permanente do serviço. O SID por serviço é um local, o SID de computador gerado por meio do nome do serviço. Em uma instância padrão, seu nome de usuário amigável é NT SERVICE\MSSQLServerOLAPService.  
  
 O benefício de um SID por serviço é que ele permite que uma conta de logon mais amplamente visível seja alterada arbitrariamente, sem afetar as permissões do arquivo. Por exemplo, digamos que você instalou duas instâncias do Analysis Services, uma instância padrão e uma instância nomeada, ambas executadas na mesma conta de usuário do Windows. Embora a conta de logon seja compartilhada, cada instância de serviço terá um SID por serviço exclusivo. Esse SID é diferente do SID da conta de logon. O SID por serviço é usado para permissões de arquivo e privilégios do Windows. Por outro lado, o SID da conta de logon é usado para cenários de autenticação e autorização, e SIDS diferentes são usados para finalidades diferentes.  
  
 Como o SID é imutável, as ACLs do sistema de arquivos criadas durante a instalação do serviço podem ser usadas por tempo indeterminado, independente de quantas vezes você alterar a conta de serviço. Como medida adicional de segurança, as ACLs que especificam permissões via um SID garantem que os executáveis do programa e as pastas de dados sejam acessados somente por uma única instância de um serviço, mesmo que outros serviços sejam executados na mesma conta.  
  
##  <a name="bkmk_tasks"></a> Concedendo permissões adicionais do Analysis Services para operações de servidor específicas  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa algumas tarefas no contexto de segurança da conta de serviço (ou conta de logon) que é usada para iniciar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e executa outras tarefas no contexto de segurança do usuário que está solicitando a tarefa.  
  
 A tabela a seguir descreve as permissões adicionais necessárias para oferecer suporte a tarefas executadas como a conta de serviço.  
  
|Operação de servidor|Item de Trabalho|Justificação|  
|----------------------|---------------|-------------------|  
|Acesso remoto a fontes de dados relacionais externas|Crie um logon de banco de dados para a conta de serviço|O processamento se refere à recuperação de dados de uma fonte de dados externa (em geral, um banco de dados relacional), que é subsequentemente carregada em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Uma das opções de credencial para recuperar dados externos é usar a conta de serviço. Esta opção de credencial só funcionará se você criar um logon de banco de dados para a conta de serviço e conceder permissões de leitura no banco de dados de origem. Consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md) Para obter mais informações sobre como a opção de conta de serviço é usada para esta tarefa. Da mesma forma, se ROLAP for usado como o modo de armazenamento, as mesmas opções de representação estarão disponíveis. Nesse caso, a conta também deve ter acesso de gravação nos dados de origem para processar as partições ROLAP (isto é, para armazenar agregações).|  
|DirectQuery|Crie um logon de banco de dados para a conta de serviço|O DirectQuery é um recurso de tabela usado para consultar conjuntos de dados externos que são grandes demais para caber no modelo de tabela ou têm outras características que tornam o DirectQuery mais adequado do que a opção padrão de armazenamento na memória. Uma das opções de conexão disponíveis no modo DirectQuery é usar a conta de serviço. Novamente, esta opção só funciona quando a conta de serviço tem um logon de banco de dados e permissões de leitura na fonte de dados de destino. Consulte [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md) Para obter mais informações sobre como a opção de conta de serviço é usada para esta tarefa. Como alternativa, as credenciais do usuário atual podem ser usadas para recuperar dados. Na maioria dos casos, esta opção engloba uma conexão de salto duplo; portanto, configure a conta de serviço para delegação restrita de Kerberos para que a conta de serviço possa delegar identidades para um servidor downstream. Para obter mais informações, consulte [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).|  
|Acesso remoto a outras instâncias do SSAS|Adicione a conta de serviço a funções de banco de dados do Analysis Services definidos no servidor remoto|Partições remotas e a referência a objetos vinculados em outras instâncias remotas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são ambos recursos do sistema que exigem permissões em um computador ou dispositivo remoto. Quando alguém cria e popula partições remotas, ou configura um objeto vinculado, essa operação é executada no contexto de segurança do usuário atual. Se você subsequentemente automatizar essas operações, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] acessará instâncias remotas no contexto de segurança de sua conta de serviço. Para acessar os objetos vinculados em uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a conta de logon deve ter a permissão adequada para ler os objetos apropriados na instância remota, como o acesso de leitura em algumas dimensões. Da mesma forma, o uso de partições remotas exige que a conta de serviço tenha direitos administrativos na instância remota. Essas permissões são concedidas na instância remota do Analysis Services, usando funções que associam operações permitidas com um objeto específico. Consulte [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obter instruções sobre como conceder permissões de Controle Total que permitem operações de processamento e consulta. Consulte [Criar e gerenciar uma partição remota &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md) para obter mais informações sobre partições remotas.|  
|Write-back|Adicione a conta de serviço a funções de banco de dados do Analysis Services definidos no servidor remoto|Quando habilitado em aplicativos cliente, o write-back é um recurso de modelos multidimensionais que permite a criação de novos valores de dados durante a análise de dados. Se o write-back estiver habilitado em alguma dimensão ou cubo, a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deverá ter permissões de gravação na tabela de write-back do banco de dados relacional de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se essa tabela ainda não existir e for necessário criá-la, a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também deverá ter permissões de criação de tabelas no banco de dados designado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|Grave em uma tabela de log de consultas em um banco de dados relacional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Crie um logon de banco de dados para a conta de serviço e atribua permissões de gravação na tabela de log de consultas|Você pode habilitar o log de consultas para coletar dados de uso em uma tabela de banco de dados para a análise subsequente. A conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve ter permissões de gravação na tabela de log de consultas no banco de dados designado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se essa tabela ainda não existir e for necessário criá-la, a conta de logon do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também deve ter permissões de criação de tabelas no banco de dados designado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Melhorar o desempenho do SQL Server Analysis Services com o Assistente de Otimização Baseado no Uso (Blog)](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) e [Log de consultas no Analysis Services (Blog)](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx).|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Conta de Serviço do SQL Server e o SID por serviço (Blog)](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [O SQL Server usa um SID de serviço para fornecer isolamento de serviço (artigo do KB)](http://support.microsoft.com/kb/2620201)   
 [Token de Acesso (MSDN)](/windows/desktop/SecAuthZ/access-tokens)   
 [Identificadores de Segurança (MSDN)](/windows/desktop/SecAuthZ/security-identifiers)   
 [Token de Acesso (Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [Listas de Controle de Acesso (Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
