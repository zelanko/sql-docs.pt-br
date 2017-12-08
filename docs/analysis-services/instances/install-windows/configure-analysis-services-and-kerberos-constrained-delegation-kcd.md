---
title: "Configurar o Analysis Services e delegação restrita Kerberos (KCD) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0006e143-d3ba-4d10-a415-e42c45e2bb0a
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 95a002a015a94f0b6ad69bc2331403604717d778
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>Configurar o Analysis Services e a KCD (Delegação restrita de Kerberos)
  A KCD (delegação restrita de Kerberos) é um protocolo de autenticação que você pode configurar com a autenticação do Windows a fim de delegar credenciais de cliente, de serviço para serviço, em todo o seu ambiente. A KCD exige infraestrutura adicional, por exemplo, um Controlador de Domínio, e a configuração adicional de seu ambiente. A KCD é um requisito em alguns cenários que envolvem dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] com o SharePoint 2016. No SharePoint 2016, os Serviços do Excel foram movidos para fora do farm do SharePoint para um servidor novo e separado, o **Servidor do Office Online**. Como o Servidor do Office Online é separado, há uma necessidade crescente por uma forma de delegar credenciais de cliente em cenários típicos de dois saltos.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
## <a name="overview"></a>Visão geral  
 A KCD permite que uma conta represente outra conta com a finalidade de fornecer acesso aos recursos. A conta de representação pode ser uma conta de serviço atribuída a um aplicativo Web, ou a conta de computador do servidor Web. Enquanto a conta representada seria uma conta de usuário que exige acesso aos recursos. A KCD funciona no nível de serviço, para que os serviços selecionados em um servidor possam receber acesso da conta de representação, enquanto outros serviços no mesmo servidor, ou serviços em outros servidores, não recebem o acesso.  
  
 As seções neste tópico analisam cenários comuns com [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , nos quais a KCD é necessária, assim como um exemplo de implantação de servidor com um resumo de alto nível do que você precisa instalar e configurar. Confira a seção [Mais informações e conteúdo da comunidade](#bkmk_moreinfo) para obter links para informações mais detalhadas sobre as tecnologias envolvidas, como Controladores de domínio e KCD.  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>Cenário 1: Pasta de trabalho como fonte de dados (WDS).  
 ![Consulte 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "consulte 1") servidor do Office Online abre uma pasta de trabalho do Excel e ![consulte 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "consulte 2") detecta uma conexão de dados para outra pasta de trabalho. Servidor do Office Online envia uma solicitação para o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] serviço do redirecionador ![consulte 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "consulte 3") para abrir a segunda pasta de trabalho e os dados ![consulte 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "consulte 4 ").  
  
 Nesse cenário, as credenciais do usuário precisam ser delegadas do Servidor do Office Online para o Serviço do Redirecionador [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] do SharePoint no SharePoint.  
  
 ![pasta de trabalho como uma fonte de dados](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "pasta de trabalho como uma fonte de dados")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>Cenário 2: Um modelo de Tabela do Analysis Services é vinculado a uma pasta de trabalho do Excel  
 Um modelo de tabela do Analysis Services ![consulte 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "consulte 1") links para uma pasta de trabalho do Excel que contém um modelo do PowerPivot. Nesse cenário, quando o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carrega o modelo de Tabela, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] detecta o link para a pasta de trabalho. Ao processar o modelo, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] envia uma solicitação de consulta para o SharePoint para carregar a pasta de trabalho. Nesse cenário, as credenciais do cliente **não** precisam ser delegadas do Analysis Services para o SharePoint. No entanto, um aplicativo cliente pode substituir as informações da fonte de dados em uma associação fora de linha. Se a solicitação de associação fora de linha especificar a representação do usuário atual, as credenciais do usuário deverão ser delegadas, o que exige a configuração da KCD entre o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e o SharePoint.  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>Exemplo de implantação do KCD com o Servidor do Office Online e o Analysis Services  
 Esta seção descreve um exemplo de implantação que usa quatro computadores. As seções a seguir resumem as principais etapas de instalação e configuração de cada computador. Antes de começar a implantação, recomendamos que os computadores estejam atualizados com patches do sistema operacional, e que você saiba os nomes de computador, pois eles serão necessários em algumas das etapas de configuração.  
  
-   Controlador de domínio  
  
-   Mecanismo de banco de dados do SQL Server e Analysis Services no modo Power Pivot. A instância do mecanismo de banco de dados será usada para os bancos de dados de conteúdo do SharePoint.  
  
-   SharePoint Server 2016  
  
-   Servidor do Office Online  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>Controlador de domínio  
 Veja a seguir um resumo do que instalar para o DC (controlador de domínio).  
  
-   **Função:** Serviços de Domínio do Active Directory. Para obter uma visão geral, consulte [Configuring Active Directory (AD DS) in Windows Server 2012](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)(Configuração do AD DS (Active Directory) no Windows Server 2012).  
  
-   **Função:** servidor DNS  
  
-   **Recurso:** recursos do .NET Framework 3.5 / .NET Framework 3.5  
  
-   **Recurso:** Ferramentas de Administração de Servidor Remoto / Ferramentas de Administração de Funções  
  
-   Configure o Active Directory para criar uma nova Floresta e para ingressar os computadores ao domínio. Antes de tentar adicionar outros computadores ao domínio particular, você precisará configurar o DNS dos computadores cliente para o endereço IP do controlador de domínio. No computador do controlador de domínio, execute `ipconfig /all` para obter os endereços IPv4 e IPv6 para a próxima etapa.  
  
-   Recomendamos a configuração de endereços IPv4 e IPv6. Faça isso no painel de controle do Windows:  
  
    1.  Clique em **Central de Rede e Compartilhamento**  
  
    2.  Clique em sua conexão Ethernet  
  
    3.  Clique em **Propriedades**  
  
    4.  Clique em **Protocolo IP versão 6 (TCP/IPv6)**  
  
    5.  Clique em **Propriedades**  
  
    6.  Clique em **Usar os seguintes endereços de servidor DNS**  
  
    7.  Digite o endereço IP do comando ipconfig.  
  
    8.  Clique no botão **Avançado** , clique na guia **DNS** e verifique se os sufixos DNS estão corretos.  
  
    9. Clique em **Acrescentar estes sufixos DNS.**  
  
    10. Repita as etapas para IPv4.  
  
-   **Observação:** você pode ingressar computadores no domínio por meio do Painel de Controle do Windows, nas Configurações do sistema. Para obter mais informações, consulte [How To Join Windows Server 2012 to a Domain](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)(Como ingressar o Windows Server 2012 em um domínio).  
  
 ![servidor de SSAS no modo powerpivot](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "servidor ssas no modo do powerpivot")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>Mecanismo de banco de dados do SQL Server 2016 e o Analysis Services no modo Power Pivot  
 A seguir está um resumo do que instalar no computador com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 ![Observação](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Observação") no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Assistente de instalação, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no Power Pivot modo é instalado como parte do fluxo de trabalho de seleção de recurso.  
  
1.  Execute o assistente de instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e, na página de seleção do recurso, clique no mecanismo de banco de dados, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], e nas Ferramentas de gerenciamento. Em uma instalação posterior do assistente de instalação, você pode especificar o modo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
2.  Para a configuração da instância, defina uma instância nomeada do "POWERPIVOT".  
  
3.  Na página Configuração do Analysis Services, configure o servidor do Analysis Services para o modo **Power Pivot** e adicione o **nome do computador** do Servidor do Office Online à lista de administradores do servidor do Analysis Services. Para saber mais, veja [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
4.  Observe que, por padrão, o tipo de objeto "Computador" não está incluído na pesquisa. Clique em ![clique em objetos para adicionar a conta de computador](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "clique em objetos para adicionar a conta de computador") para adicionar o objeto computadores.  
  
     ![Adicionar contas de computador como administradores de ssas](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "adicionar contas de computador como administradores de ssas")  
  
5.  Crie o SPN (Nome da Entidade de Serviço) da instância do Analysis Services.  
  
     Veja a seguir os comandos SPN úteis:  
  
    -   Listar o SPN de um nome de conta específico executando o serviço de interesse: `SetSPN -l <account-name>`  
  
    -   Definir um SPN para um nome de conta que está executando o serviço de interesse: `SetSPN -a <SPN> <account-name>`  
  
    -   Excluir o SPN de um nome de conta específico executando o serviço de interesse: `SetSPN -D <SPN> <account-name>`  
  
    -   Procurar por SPNs duplicados: `SetSPN -X`  
  
     O SPN para a instância do PowerPivot será na forma de:  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     Em que os FQDN e os nomes NetBIOS são o nome da máquina na qual reside a instância. Esses SPNs serão colocados na Conta de Domínio que está sendo usada para a conta de serviço.  Se você estiver usando o Serviço de Rede, o Sistema Local ou a ID do Serviço, convém colocar o SPN na conta da máquina de domínio.  Se você estiver usando uma conta de usuário de domínio, coloque o SPN nessa conta.  
  
6.  Crie o SPN para o serviço do SQL Browser no computador do Analysis Services.  
  
     [Saiba mais](https://support.microsoft.com/en-us/kb/950599)  
  
7.  **Defina as configurações de delegação restrita** na conta de serviço do Analysis Services para qualquer fonte externa por meio da qual você atualizará, por exemplo, SQL Server ou arquivos do Excel. Na conta de serviço do Analysis Services, certifique-se de que as seguintes opções estão definidas.  
  
     **Observação:** se você não vir a guia de delegação para a conta nos Usuários e Computadores do Active Directory, é porque não há SPN nessa conta.  Você pode adicionar um SPN falso para que ele seja exibido, como `my/spn`.  
  
     **Confiar neste usuário para delegação apenas aos serviços especificados** e **Usar qualquer protocolo de autenticação**.  
  
     Isso é conhecido como delegação restrita, e é necessário porque o token do Windows será proveniente de C2WTS (Declarações para os Serviços de Token do Windows), o que exige a delegação restrita com a transição de protocolos.  
  
     ![Analysis Services – a delegação restrita](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "do Analysis Services - a delegação restrita")  
  
     Você também precisará adicionar os serviços para os quais delegará. Isso pode variar com base em seu ambiente.  
  
### <a name="office-online-server"></a>Servidor do Office Online  
  
1.  Instalar o Servidor do Office Online  
  
2.  **Configure o Servidor do Office Online** para se conectar ao servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Observe que a conta de computador do Servidor do Office Online precisa ser de um administrador no servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Isso foi concluído em uma seção anterior deste tópico, pela instalação do servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
    1.  No Servidor do Office Online, abra uma janela do PowerShell com privilégios administrativos e execute o seguinte comando  
  
    2.  `New-OfficeWebAppsExcelBIServer –ServerId <AS instance name>`  
  
    3.  Exemplo: `New-OfficeWebAppsExcelBIServer –ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **Configure o Active Directory** para permitir que a conta de computador do Servidor do Office Online represente os usuários para a conta de serviço do SharePoint. Portanto, defina a propriedade de delegação na entidade executando o Pool de Aplicativos do SharePoint Web Services, no Servidor do Office Online: os comandos do PowerShell nesta seção exigem objetos do Active Directory (AD) PowerShell.  
  
    1.  Obter a identidade do Active Directory do Servidor do Office Online  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         encontre esse nome de Entidade no Gerenciador de Tarefas/Detalhes/Nome de usuário do w3wp.exe. Por exemplo, "svcSharePoint"  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  Para verificar se a propriedade foi definida corretamente  
  
    3.  ```  
        Get-ADUser svcSharePoint –Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  **Defina as configurações da delegação restrita** na conta do Servidor do Office Online para a instância do Analysis Services Power Pivot. Essa deve ser a conta do computador no qual Servidor do Office Online está em execução. Na conta da Serviço do Office Online, certifique-se de que as seguintes opções estão definidas.  
  
     **Observação:** se você não vir a guia de delegação para a conta nos Usuários e Computadores do Active Directory, é porque não há SPN nessa conta.  Você pode adicionar um SPN falso para que ele seja exibido, como `my/spn`.  
  
     **Confiar neste usuário para delegação apenas aos serviços especificados** e **Usar qualquer protocolo de autenticação**.  
  
     Isso é conhecido como delegação restrita, e é necessário porque o token do Windows será proveniente de C2WTS (Declarações para os Serviços de Token do Windows), o que exige a delegação restrita com a transição de protocolos.  Em seguida, permita a delegação para os SPNs MSOLAPSvc.3 e SPNs MSOLAPDisco.3 que criamos acima.  
  
5.  Configure o C2WTS (Declarações para serviço de token do Windows) **Isso é necessário para o cenário 1**. Para obter mais informações, consulte [Claims to Windows Token Service (C2WTS) Overview](https://msdn.microsoft.com/library/ee517278.aspx)(Visão geral do C2WTS (Declarações para serviço de token do Windows)).  
  
6.  **Defina as configurações de delegação restrita** na conta do serviço C2WTS.  As configurações devem corresponder o que você fez na etapa 4.  
  
 ![o SharePoint server](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "servidor do sharepoint")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 Veja a seguir um resumo da instalação do SharePoint Server.  
  
1.  Execute o instalador de pré-requisitos do SharePoint  
  
2.  Execute a instalação do SharePoint e selecione a função de configuração **Single Server Farm (Farm de Servidores Único)** .  
  
3.  Execute o suplemento do PowerPivot para SharePoint (spPowerPivot16.msi). Para obter mais informações, consulte [instalar ou desinstalar o PowerPivot para SharePoint Add-in (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  Execute o assistente de Configuração do PowerPivot. Consulte [Ferramentas de Configuração do Power Pivot](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
5.  Conecte o SharePoint ao Servidor Office Online.    ??Configure_xlwac_on_SPO.ps1 ??  
  
6.  Configure os provedores de autenticação do SharePoint para Kerberos. **Isso é necessário para o cenário 1**. Para obter mais informações, consulte [Plano para autenticação Kerberos no SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).  
  
##  <a name="bkmk_moreinfo"></a> Mais informações e conteúdo da comunidade  
 [Kerberos para o administrador ocupado](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [Noções básicas sobre Kerberos de salto duplo](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [ALL things .Net e SharePoint](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [Delegação restrita de Kerberos com base em recursos](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [KERBEROS PRIMER - vídeos](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft® Kerberos Configuration Manager para SQL Server®](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  
