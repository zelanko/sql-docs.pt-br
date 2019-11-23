---
title: Implantar um banco de dados do SQL Server em uma máquina virtual do Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploymentwizard.deploymentsettings.f1
- sql12.swb.deploymentwizard.progress.f1
- sql11.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.f1
- sql12.swb.deploymentwizard.azuresignin.f1
- sql11.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.azuresignin.f1
- sql12.swb.deploymentwizard.f1
- sql12.swb.sqlvmdialog.f1
- sql11.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.results.f1
- sql11.swb.deploymentwizard.progress.f1
- sql12.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.sourcesettings.f1
- sql12.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.sourcesettings.f1
- sql11.swb.deploymentwizard.results.f1
- sql12.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.deploymentsettings.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7d84fbe56d36bd91f2b7f8b49a3df73fb383c6e
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175732"
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Implantar um banco de dados do SQL Server em uma máquina virtual do Microsoft Azure
  Use o assistente **para implantar um banco de dados SQL Server em uma VM do Azure** para implantar um banco de dados de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma VM (máquina virtual) do Azure. O assistente utiliza uma operação de backup completo de banco de dados, de modo que sempre copia o esquema de banco de dados completo e os dados de um banco de dados de usuário do SQL Server. O assistente também faz toda a configuração da VM do Azure para você, de modo que nenhuma configuração prévia de VM é necessária.  
  
 Você não pode usar o assistente para backups diferenciais porque o assistente não substituirá um banco de dados existente que tenha o mesmo nome. Para substituir um banco de dados existente na VM, você deverá primeiro remover o banco de dados existente ou alterar o nome dele. Se houver um conflito de nomeação entre o nome do banco de dados de uma operação de implantação em curso e um banco de dados existente na VM, o assistente sugerirá um nome de banco de dados anexado para que o banco de dados em curso permita que você conclua a operação.  
  
##  <a name="before_you_begin"></a> Antes de começar  
 Para concluir esse assistente, você deve poder fornecer as informações a seguir e definir as configurações:  
  
-   Os detalhes de conta Microsoft associados à sua assinatura do Azure.  
  
-   Seu perfil de publicação do Azure.  
  
    > [!CAUTION]  
    >  No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
  
-   O certificado de gerenciamento carregado em sua assinatura do Azure.  
  
-   O certificado de gerenciamento salvo no repositório de certificados pessoais no computador em que o assistente sendo executado.  
  
-   Você deve ter um local de armazenamento temporário que esteja disponível para o computador onde o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está hospedado. O local de armazenamento temporário também deve estar disponível para o computador onde o assistente está sendo executado.  
  
-   Se você estiver implantando o banco de dados em uma VM existente, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser configurada para escutar em uma porta TCP/IP.  
  
-   Uma imagem da galeria ou VM do Azure que você planeja usar para a criação da VM deve ter a SQL Server Adaptador de Nuvem configurada e em execução.  
  
-   Você deve configurar um ponto de extremidade aberto para seu SQL Server Adaptador de Nuvem no gateway do Azure com a porta privada 11435.  
  
 Além disso, se você planeja implantar seu banco de dados em uma VM do Azure existente, você também deve ser capaz de fornecer:  
  
-   O nome DNS do serviço de nuvem que hospeda a VM.  
  
-   As credenciais do administrador para a VM.  
  
-   Credenciais com privilégios de Operador de backup no banco de dados que pretende implantar, da instância de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como executar SQL Server em máquinas virtuais do Azure, consulte [preparando-se para migrar para SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/dn133142.aspx).  
  
 Em computadores que executam sistemas operacionais do Windows Server, você deverá usar os seguintes parâmetros de configuração para executar esse assistente:  
  
-   Desative a Configuração de Segurança Avançada: use o Gerenciador do Servidor > Servidor Local para definir a ESC (Configuração de Segurança Avançada) do Internet Explorer como **OFF**.  
  
-   Habilite o JavaScript: Internet Explorer > Opções da Internet > Segurança > Nível do Cliente > Scripts > Scripts Ativos: **Habilitar**.  
  
###  <a name="limitations"></a> Limitações e restrições  
 A limitação de tamanho do banco de dados para essa operação é de 1 TB.  
  
 Esse recurso de implantação está disponível no SQL Server Management Studio para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Esse recurso de implantação é para uso apenas com bancos de dados de usuário; implantar bancos de dados de sistema não tem suporte.  
  
 O recurso de implantação não oferece suporte aos serviços hospedados associados a um grupo de afinidade. Por exemplo, as contas de armazenamento associadas a um grupo de afinidade não podem ser selecionadas para uso na página **Configurações de Implantação** desse assistente.  
  
 A versão do SQL Server na VM deve ser o mesmo ou posterior que a versão do SQL Server de origem. SQL Server versões de banco de dados que podem ser implantadas em uma VM do Azure usando este assistente:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 SQL Server versões de banco de dados executadas em um banco de dados de VM do Azure podem ser implantadas em:  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Se houver um conflito de nomeação entre o nome do banco de dados de uma operação de implantação em curso e um banco de dados existente na VM, o assistente sugerirá um nome de banco de dados anexado para que o banco de dados em curso permita que você conclua a operação.  
  
###  <a name="filestream"></a> Considerações para implantar um banco de dados habilitado para FILESTREAM em uma VM do Azure  
 Observe as seguintes diretrizes e restrições ao implantar bancos de dados com BLOBS armazenados em objetos FILESTREAM:  
  
-   O recurso de implantação não pode implantar um banco de dados habilitado para FILESTREAM em uma nova VM. Se FILESTREAM não estiver habilitado na VM antes da execução do assistente, a operação de restauração do banco de dados falhará e a operação do assistente não poderá ser concluída com êxito. Para implantar com êxito um banco de dados que usa FILESTREAM, habilite-o na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na VM do host antes de iniciar o assistente. Para obter mais informações, veja [FILESTREAM (SQL Server)](https://msdn.microsoft.com/library/gg471497.aspx).  
  
-   Se seu banco de dados utiliza OLTP na memória, você pode implantar o banco de dados na VM do Azure sem modificações no banco de dados. Para obter mais informações, consulte [OLTP na memória (otimização na memória)](https://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx).  
  
###  <a name="geography"></a> Considerações sobre a distribuição geográfica de recursos  
 Observe que os seguintes recursos devem estar localizados na mesma região geográfica:  
  
-   Serviço de nuvem  
  
-   Local da VM  
  
-   Serviço de armazenamento de disco de dados  
  
 Se os recursos listados acima não forem colocalizados, o assistente não poderá ser concluído com êxito.  
  
###  <a name="configuration_settings"></a> Parâmetros de configuração do assistente  
 Use os detalhes de configuração a seguir para modificar as configurações de uma implantação de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma VM do Azure.  
  
-   **Caminho padrão para o arquivo de configuração** - %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **Estrutura do arquivo de configuração**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- Logging level -->  
  
            -   BackupPath="\\\\[server name]\\[volume]\\" \<!!-- O caminho usado para o último backup. Usado como o padrão no assistente. -->  
  
            -   CleanupDisabled = false/> \<!--assistente não excluirá arquivos intermediários e objetos do Azure (VM, CS, SA). -->  
  
        -   <PublishProfile \<! -- As informações de perfil de publicação usadas pela última vez. -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- O certificado para uso no assistente. -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- A assinatura para uso no assistente. -->  
  
            -   Name="My Subscription" \<!-- O nome da assinatura. -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **Valores do arquivo de configuração**  
  
###  <a name="permissions"></a> Permissões  
 O banco de dados que está sendo implantado deve estar em um estado normal e deve ser acessível à conta de usuário que executa o assistente. A conta de usuário deve ter permissões para executar uma operação de backup.  
  
##  <a name="launch_wizard"></a>Usando o assistente para implantar banco de dados para VM do Azure  
 **Para iniciar o assistente, use as seguintes etapas:**  
  
1.  Use o SQL Server Management Studio para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o banco de dados que deseja implantar.  
  
2.  No **Pesquisador de Objetos**, expanda o nome da instância e o nó **Bancos de Dados** .  
  
3.  Clique com o botão direito do mouse no banco de dados que você deseja implantar, selecione **tarefas**e, em seguida, selecione **implantar banco de dados na VM do Azure...**  
  

  
##  <a name="Introduction"></a> Página de Introdução  
 Esta página descreve o assistente **para implantar um SQL Server banco de dados em uma VM do Azure** .  
  
 **Opções**  
  
-   **Não exibir esta página novamente.** - Clique nesta caixa de seleção para não exibir mais a página Introdução no futuro.  
  
-   **Avançar** - continua na página **Configurações de Origem** .  
  
-   **Cancelar** – cancela a operação e fecha o assistente.  
  
-   **Ajuda** -inicia o tópico da ajuda do MSDN para o assistente.  
  
##  <a name="Source_settings"></a> Configurações de origem  
 Use esta página para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados que você deseja implantar na VM do Azure. Você também especificará um local temporário para os arquivos a serem salvos no computador local antes de serem transferidos para o Azure. Pode ser um local de rede compartilhado.  
  
 **Opções**  
  
-   Clique em **conectar...** e especifique os detalhes da conexão para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados a ser implantado.  
  
-   Use a lista suspensa **Selecionar Banco de Dados** para especificar o banco de dados a ser implantado.  
  
-   No campo **outras configurações** , especifique uma pasta compartilhada que poderá ser acessada pelo serviço de VM do Azure.  
  
##  <a name="Azure_sign-in"></a>Entrada do Azure  
 Use esta página para se conectar ao Azure e fornecer o certificado de gerenciamento ou os detalhes do perfil de publicação.  
  
 **Opções**  
  
-   **Certificado de gerenciamento** -Use essa opção para especificar um certificado do repositório de certificados local que corresponde ao certificado de gerenciamento do Azure.  
  
-   **Perfil de publicação** – Use essa opção se você já tiver um perfil de publicação baixado em seu computador.  
  
-   **Entrar** -Use esta opção para entrar no Azure usando um conta Microsoft-por exemplo, uma conta do Live ID ou do hotmail-para gerar e baixar um novo certificado de gerenciamento. Observe que o número de certificados por assinatura é limitado.  
  
-   **Assinatura** – selecione, digite ou cole sua ID de assinatura do Azure que corresponda ao certificado de gerenciamento do repositório de certificados local ou de um perfil de publicação.  
  
##  <a name="Deployment_settings"></a> Página de configurações de implantação  
 Use esta página para especificar o servidor de destino e fornecer detalhes sobre seu novo banco de dados.  
  
 **Opções**  
  
-   **Máquina virtual do Azure** -especifique os detalhes da VM que hospedará o banco de dados de SQL Server:  
  
-   **Nome do serviço de nuvem** – especifique o nome do serviço que hospeda a VM. Para criar um novo Serviço em Nuvem, especifique um nome para o novo Serviço em Nuvem.  
  
-   **Nome da máquina virtual** – especifique o nome da VM que hospedará o banco de dados SQL Server. Para criar uma nova VM do Azure, especifique um nome para a nova VM.  
  
-   **Configurações** – use o botão configurações para criar uma nova VM para hospedar o banco de dados SQL Server. Se você estiver usando uma VM existente, as informações fornecidas serão usadas para autenticar suas credenciais.  
  
-   **Conta de armazenamento** – selecione a conta de armazenamento na lista suspensa. Para criar uma nova conta de armazenamento, especifique um nome para a nova conta. Observe que as contas de armazenamento associadas a um grupo de afinidade não estarão disponíveis na lista suspensa.  
  
-   **Banco de dados de destino** -especifique os detalhes do banco de dados de destino.  
  
-   **Conexão do servidor** -detalhes de conexão do servidor.  
  
-   **Banco de dados** -especifique ou confirme o nome de um novo banco de dados. Se o nome do banco de dados já existir na instância do SQL Server de destino, sugerimos especificar um nome de banco de dados modificado.  
  
##  <a name="Summary"></a> Página de Resumo  
 Use essa página para analisar as configurações especificadas da operação. Para concluir a operação de implantação usando as configurações especificadas, clique em **Concluir**. Para cancelar a operação de implantação e sair do assistente, clique em **Cancelar**.  
  
 Pode haver etapas manuais necessárias para implantar detalhes do banco de dados no banco de dados SQL Server na VM do Azure. Essas etapas serão descritas em detalhes para você.  
  
##  <a name="Results"></a> Página Resultados  
 Esta página reporta o êxito ou falha da operação de implantação, mostrando os resultados de cada ação. Todas as ações que encontrarem um erro terão uma indicação na coluna **Resultado** . Clique no link para exibir um relatório do erro para essa ação.  
  
 Clique em **Concluir** para fechar o assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Adaptador de Nuvem do SQL Server](../../database-engine/cloud-adapter-for-sql-server.md)   
 [Gerenciamento de ciclo de vida do banco de dados](../database-lifecycle-management.md)   
 [Exportar um aplicativo da camada de dados](../data-tier-applications/export-a-data-tier-application.md)   
 [Importar um arquivo BACPAC para criar um novo banco de dados de usuário](../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Backup e restauração de Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Implantação de SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/dn133141.aspx)   
 [Preparando-se para migrar para SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/dn133142.aspx)  
  
  
