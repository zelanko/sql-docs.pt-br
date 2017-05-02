---
title: "Implantar um banco de dados do SQL Server em uma máquina virtual do Microsoft Azure | Microsoft Docs"
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deploymentwizard.deploymentsettings.f1
- sql13.swb.deploymentwizard.sourcesettings.f1
- sql13.swb.deploymentwizard.summary.f1
- sql13.swb.agdashboard.agp9virtualnw.issues.f1
- sql13.swb.deploymentwizard.f1
- sql13.swb.deploymentwizard.progress.f1
- sql13.swb.usevmdialog.f1
- sql13.swb.newvmdialog.f1
- sql13.swb.sqlvmdialog.f1
- sql13.swb.deploymentwizard.results.f1
- sql13.swb.deploymentwizard.azuresignin.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Windows Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2aca87c0050dd501c73bb4da8953a93bf40c0c8e
ms.lasthandoff: 04/11/2017

---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Implantar um banco de dados do SQL Server em uma máquina virtual do Microsoft Azure
  Use o assistente para **Implantar um Banco de Dados em uma VM do Microsoft Azure** para implantar um banco de dados de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma VM (Máquina Virtual) do Microsoft Azure. O assistente usa uma operação completa de backup do banco de dados para copiar sempre o esquema completo do banco de dados e os dados de um banco de dados de usuário do SQL Server. O assistente também faz toda a configuração da VM do Azure para você, de modo que nenhuma configuração prévia de VM é necessária.  
  
 Você não pode usar o assistente para backups diferenciais. O assistente não substituirá um banco de dados existente com o mesmo nome do banco de dados. Para substituir um banco de dados existente na VM, você deverá primeiro remover o banco de dados existente ou alterar o nome dele. Se houver um conflito de nomeação entre o nome do banco de dados de uma operação de implantação em curso e um banco de dados existente na VM, o assistente sugerirá um nome de banco de dados anexado para que o banco de dados em curso permita que você conclua a operação.  
  
-   [Antes de começar](#before_you_begin)  
  
-   [Limitações e restrições](#limitations)  
  
-   [Considerações para implantar um banco de dados habilitado para FILESTREAM](#filestream)  
  
-   [Considerações sobre a distribuição geográfica de recursos](#geography)  
  
-   [Parâmetros de configuração do assistente](#configuration_settings)  
  
-   [Permissões necessárias](#permissions)  
  
-   [Iniciando o assistente](#launch_wizard)  
  
-   [Páginas do Assistente](#wizard_pages)  
  
> [!NOTE]  
>  Para obter um passo a passo detalhado desse assistente, consulte [Migrar um banco de dados SQL Server para o SQL Server em uma VM do Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-migrate-onpremises-database/)  
  
##  <a name="before_you_begin"></a> Antes de começar  
 Para concluir esse assistente, você deve poder fornecer as informações a seguir e definir as configurações:  
  
-   Os detalhes da conta da Microsoft associada à sua assinatura do Windows Azure.  
  
-   O seu perfil de publicação do Windows Azure.  
  
    > [!CAUTION]  
    >  No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
-   O certificado de gerenciamento carregado na assinatura do Microsoft Azure.  Crie o certificado de gerenciamento com o cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/library/hh848633(v=wps.630))do PowerShell.  Em seguida, carregue o certificado de gerenciamento em sua assinatura do Microsoft Azure.  Para obter mais informações sobre como carregar um certificado de gerenciamento, consulte [Carregar um certificado de gerenciamento da API de Gerenciamento do Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-api-management-certs/).  Sintaxe de exemplo para criar um certificado de gerenciamento em [Visão geral dos certificados nos Serviços de Nuvem do Azure](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-certs-create/): 

    ```powershell  
    $cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
    $password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
    Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
    ```    

    > [!NOTE]  
    > A ferramenta MakeCert também pode ser usada para criar um certificado de gerenciamento; no entanto, MakeCert agora foi preterida.  Para obter mais informações, consulte [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968).
   
  -   O certificado de gerenciamento salvo no repositório de certificados pessoais no computador em que o assistente sendo executado.  
  
-   Você deve ter um local de armazenamento temporário que esteja disponível para o computador onde o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está hospedado. O local de armazenamento temporário também deve estar disponível para o computador onde o assistente está sendo executado.  
  
-   Se você estiver implantando o banco de dados em uma VM existente, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser configurada para escutar em uma porta TCP/IP.  
  
-   Uma imagem da Galeria ou da VM do Microsoft Azure que você planeja usar para criação da VM deve ter o [Adaptador de Nuvem do SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877) configurado e em execução.  
  
-   É necessário configurar um ponto de extremidade aberto para o [Adaptador de Nuvem do SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877) no gateway do Microsoft Azure com a porta privada 11435.  
  
 Além disso, se planeja implantar o banco de dados em uma VM existente do Windows Azure, você também deve ser capaz de fornecer:  
  
-   O nome DNS do serviço de nuvem que hospeda a VM.  
  
-   As credenciais do administrador para a VM.  
  
-   Credenciais com privilégios de Operador de backup no banco de dados que pretende implantar, da instância de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como executar o SQL Server em máquinas virtuais do Microsoft Azure, consulte [Provisionar uma máquina virtual do SQL Server no Portal do Azure](https://msdn.microsoft.com/library/dn133141.aspx) e [Migrar um banco de dados SQL Server para o SQL Server em uma VM do Azure](http://msdn.microsoft.com/library/dn133142.aspx).  
  
 Em computadores que executam sistemas operacionais do Windows Server, você deverá usar os seguintes parâmetros de configuração para executar esse assistente:  
  
-   Desative a Configuração de Segurança Avançada: use o Gerenciador do Servidor > Servidor Local para definir a ESC (Configuração de Segurança Avançada) do Internet Explorer como **OFF**.  
  
-   Habilite o JavaScript: Internet Explorer > Opções da Internet > Segurança > Nível do Cliente > Scripts > Scripts Ativos: **Habilitar**.  
  
###  <a name="limitations"></a> Limitações e restrições  
Esse recurso de implantação é para uso somente com uma Conta de Armazenamento do Azure criada por meio do modelo de implantação Gerenciamento de Serviços (Clássico). Para obter mais informações sobre os modelos de implantação do Azure, veja [Azure Resource Manager versus implantação clássica](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

 A limitação de tamanho do banco de dados para essa operação é de 1 TB.  
  
 Esse recurso de implantação está disponível no SQL Server Management Studio para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Esse recurso de implantação é para uso apenas com bancos de dados de usuário; implantar bancos de dados de sistema não tem suporte.  
  
 O recurso de implantação não oferece suporte aos serviços hospedados associados a um grupo de afinidade. Por exemplo, as contas de armazenamento associadas a um grupo de afinidade não podem ser selecionadas para uso na página **Configurações de Implantação** desse assistente.  
  
 As versões de banco de dados do SQL Server que podem ser implantadas em uma VM do Windows Azure usando esse assistente:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 As versões de banco de dados do SQL Server em execução em um banco de dados da VM do Windows Azure podem ser implantadas no:  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Se houver um conflito de nomeação entre o nome do banco de dados de uma operação de implantação em curso e um banco de dados existente na VM, o assistente sugerirá um nome de banco de dados anexado para que o banco de dados em curso permita que você conclua a operação.  
  
###  <a name="filestream"></a> Considerações para implantar um banco de dados habilitado para FILESTREAM em uma VM do Azure  
 Observe as seguintes diretrizes e restrições ao implantar bancos de dados com BLOBS armazenados em objetos FILESTREAM:  
  
-   O recurso de implantação não pode implantar um banco de dados habilitado para FILESTREAM em uma nova VM. Se FILESTREAM não estiver habilitado na VM antes da execução do assistente, a operação de restauração do banco de dados falhará e a operação do assistente não poderá ser concluída com êxito. Para implantar com êxito um banco de dados que usa FILESTREAM, habilite-o na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na VM do host antes de iniciar o assistente. Para obter mais informações, veja [FILESTREAM (SQL Server)](http://msdn.microsoft.com/library/gg471497.aspx).  
  
-   Se seu banco de dados utiliza OLTP na memória, você pode implantar o banco de dados na VM do Azure sem modificações no banco de dados. Para obter mais informações, veja [OLTP in-memory (otimização na memória)](http://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx).  
  
###  <a name="geography"></a> Considerações sobre a distribuição geográfica de recursos  
 Observe que os seguintes recursos devem estar localizados na mesma região geográfica:  
  
-   Serviço de nuvem  
  
-   Local da VM  
  
-   Serviço de armazenamento de disco de dados  
  
 Se os recursos listados acima não forem colocalizados, o assistente não poderá ser concluído com êxito.  
  
###  <a name="configuration_settings"></a> Parâmetros de configuração do assistente  
 Use os detalhes de configuração a seguir para modificar as configurações de uma implantação de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma VM do Azure.  
  
-   **Caminho padrão para o arquivo de configuração** – %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **Estrutura do arquivo de configuração**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- Logging level -->  
  
            -   BackupPath="\\\\[server name]\\[volume]\\" \<!!-- O caminho usado para o último backup. Usado como o padrão no assistente. -->  
  
            -   CleanupDisabled = False /> \<!-- O Assistente não excluirá arquivos intermediários e objetos do Microsoft Azure (VM, CS, SA). -->  
  
        -   <PublishProfile \<! -- As informações de perfil de publicação usadas pela última vez. -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- O certificado para uso no assistente. -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- A assinatura para uso no assistente. -->  
  
            -   Name="My Subscription" \<!-- O nome da assinatura. -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **Valores do arquivo de configuração**  
  
###  <a name="permissions"></a> Permissões  
 O banco de dados que está sendo implantado deve estar em um estado normal e deve ser acessível à conta de usuário que executa o assistente. A conta de usuário deve ter permissões para executar uma operação de backup.  
  
##  <a name="launch_wizard"></a> Usando o Assistente para Implantar Banco de Dados na VM do Microsoft Azure  
 **Para iniciar o assistente, use as seguintes etapas:**  
  
1.  Use o SQL Server Management Studio para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o banco de dados que deseja implantar.  
  
2.  No **Pesquisador de Objetos**, expanda o nome da instância e o nó **Bancos de Dados** .  
  
3.  Clique com o botão direito do mouse no banco de dados que você deseja implantar, selecione **Tarefas**e **Implantar Banco de Dados em uma VM do Microsoft Azure...**  
  
##  <a name="wizard_pages"></a> Páginas do Assistente  
 As seções a seguir fornecem informações adicionais sobre definições de implantação e detalhes de configuração para essa operação.  
  
-   [Introdução](#Introduction)  
  
-   [Configurações de origem](#Source_settings)  
  
-   [Entrar no Windows Azure](#Azure_sign-in)  
  
-   [Configurações de Implantação](#Deployment_settings)  
  
-   [Resumo](#Summary)  
  
-   [Resultados](#Results)  
  
##  <a name="Introduction"></a> Introdução 
 Essa página descreve o assistente para **Implantar Banco de Dados em uma VM do Microsoft Azure** .  
  
-   **Não mostrar esta página novamente.**  
  Clique nesta caixa de seleção para não exibir mais a página Introdução no futuro.  
  
-   **Próximo**  
Segue para a página **Configurações de Fonte** .  
  
-   **Cancelar**  
  Cancela a operação e fecha o assistente.  
  
-   **Ajuda**  
Inicia o tópico da Ajuda do MSDN do assistente.  
  
##  <a name="Source_settings"></a> Configurações de origem  
 Use essa página para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados que você deseja implantar na VM do Microsoft Azure. Você também especificará um local temporário para que os arquivos sejam salvos no computador local antes de serem transferidos para o Microsoft Azure. Pode ser um local de rede compartilhado.  
 
- **SQL Server**    
Clique em **Conectar** e especifique os detalhes da conexão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados a ser implantado.  
  
-   **Selecionar banco de dados**  
Use a lista suspensa para especificar o banco de dados a ser implantado.  
  
-   **Outras configurações**  
No campo, especifique uma pasta compartilhada que poderá ser acessada pelo serviço VM do Microsoft Azure.  
  
##  <a name="Azure_sign-in"></a> Entrar no Microsoft Azure  
 Entre no Microsoft Azure com sua conta da Microsoft ou conta organizacional. Sua conta da Microsoft ou organizacional está no formato de endereço de email, como patc@contoso.com. Para obter mais informações sobre as credenciais do Azure, consulte [Perguntas Frequentes sobre a Conta Institucional Microsoft](http://technet.microsoft.com/jj592903) e [Solucionando problemas](https://technet.microsoft.com/dn197220).  
  
##  <a name="Deployment_settings"></a> Configurações de Implantação
 Use esta página para especificar o servidor de destino e fornecer detalhes sobre seu novo banco de dados.  
  
 **Máquina Virtual do Microsoft Azure**  
  
-   **Nome do Serviço de Nuvem**  
Especifique o nome do serviço que hospeda a VM. Para criar um novo Serviço em Nuvem, especifique um nome para o novo Serviço em Nuvem.  
  
-   **Nome da Máquina Virtual** Especifique o nome da VM que hospedará o banco de dados SQL Server. Para criar uma nova VM do Microsoft Azure, especifique um nome para a nova VM.  
  
-   **Conta de armazenamento**  
Selecione a conta de armazenamento na lista suspensa. Para criar uma nova conta de armazenamento, especifique um nome para a nova conta. Observe que as contas de armazenamento associadas a um grupo de afinidade não estarão disponíveis na lista suspensa.  

-   **Configurações**  
Use o botão Configurações para criar uma nova VM para hospedar o banco de dados SQL Server. Se você estiver usando uma VM existente, as informações fornecidas serão usadas para autenticar suas credenciais.  
  
**Banco de Dados de Destino**
  
-   **Nome da instância SQL**  
Detalhes de conexão do servidor.  
  
-   **Nome do banco de dados**  
Especifique ou confirme o nome de um novo banco de dados. Se o nome do banco de dados já existir na instância do SQL Server de destino, sugerimos especificar um nome de banco de dados modificado.  
  
##  <a name="Summary"></a> Resumo
 Use essa página para analisar as configurações especificadas da operação. Para concluir a operação de implantação usando as configurações especificadas, clique em **Concluir**. Para cancelar a operação de implantação e sair do assistente, clique em **Cancelar**.  Se você clicar em **Concluir** , a página **Progresso da Implantação** será aberta.  Você também pode exibir o progresso no arquivo de log localizado em `"%LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM"`.
  
 Talvez haja a necessidade de etapas manuais para implantar detalhes do banco de dados no banco de dados do SQL Server na VM do Windows Azure. Essas etapas serão descritas em detalhes para você.  
  
##  <a name="Results"></a> Resultados 
 Esta página reporta o êxito ou falha da operação de implantação, mostrando os resultados de cada ação. Todas as ações que encontrarem um erro terão uma indicação na coluna **Resultado** . Clique no link para exibir um relatório do erro para essa ação.  
  
 Clique em **Concluir** para fechar o assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Adaptador de Nuvem do SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877)   
 [Gerenciamento de ciclo de vida do banco de dados](../../relational-databases/database-lifecycle-management.md)   
 [Exportar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [Importar um arquivo BACPAC para criar um novo banco de dados de usuário](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Backup e restauração de Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Implantação do SQL Server em Máquinas Virtuais do Microsoft Azure](http://msdn.microsoft.com/library/dn133141.aspx)   
 [Preparando-se para migrar para o SQL Server em Máquinas Virtuais do Microsoft Azure](http://msdn.microsoft.com/library/dn133142.aspx)  
  
  

