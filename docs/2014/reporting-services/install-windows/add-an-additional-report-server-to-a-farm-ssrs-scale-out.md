---
title: Adicionar um servidor de relatório a um farm (expansão do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 13e4dfa2d6fe01908d6144dc0ca6af07216af0fb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276122"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>Adicionar um servidor de relatório a um farm (expansão SSRS)
  Adicionar um segundo ou mais servidores de relatório de modo do SharePoint ao seu farm do SharePoint pode melhorar o desempenho e o tempo de resposta do processamento do servidor de relatório. Se você perceber que o desempenho está mais lento à medida que você adiciona mais usuários, relatórios e outros aplicativos ao servidor de relatório, então a adição de servidores de relatório pode melhorar o desempenho. Isto também é recomendado para adicionar um segundo servidor de relatório para aumentar a disponibilidade de servidores de relatório quando houver problemas com hardware ou você estiver realizando manutenção geral em servidores individuais em seu ambiente. A partir da versão do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as etapas para expansão de um ambiente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo do SharePoint seguem a implantação padrão de farm do SharePoint e aproveita os recursos de balanceamento de carga do SharePoint.  
  
> [!IMPORTANT]  
>  Não há suporte expansão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] seção de [recursos compatíveis com as edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!TIP]  
>  A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , você não usa o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para adicionar servidores e expandir servidores de relatório. Os produtos do SharePoint gerenciam a expansão dos serviços de relatório à medida que os servidores do SharePoint com o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são adicionados ao farm.  
  
 Para obter informações sobre como expandir os servidores de relatório do modo nativo, veja [Configurar uma implantação em expansão do servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
-   [O balanceamento de carga](#bkmk_loadbalancing)  
  
-   [Pré-requisitos](#bkmk_prerequisites)  
  
-   [Etapas](#bkmk_steps)  
  
-   [Configuração adicional](#bkmk_additional)  
  
##  <a name="bkmk_loadbalancing"></a> Balanceamento de carga  
 O balanceamento de carga de aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será gerenciado automaticamente pelo SharePoint a menos que seu ambiente tenha uma solução de balanceamento de carga personalizada ou de terceiros. O comportamento padrão de balanceamento de carga do SharePoint é que cada Aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será balanceado em todos os servidores de aplicativos onde você iniciou o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para verificar se o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado e iniciado, clique em **Gerenciar serviços no servidor** na Administração Central do SharePoint.  
  
##  <a name="bkmk_prerequisites"></a> Pré-requisitos  
  
-   Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
-   O computador deve ser unido a um domínio.  
  
-   Você precisa saber o nome do servidor de banco de dados existente que está hospedando a configuração do SharePoint e os bancos de dados de conteúdo.  
  
-   O servidor de banco de dados deve ser configurado para permitir conexões de bancos de dados remotos.  Se não, você não poderá unir o novo servidor ao farm porque o novo servidor não poderá fazer uma conexão com os bancos de dados de configuração do SharePoint.  
  
-   O novo servidor precisará ter a mesma versão de SharePoint instalado que os servidores de farm atuais estão executando. Por exemplo, se o farm já tiver o SharePoint 2010 Service Pack 1 (SP1) instalado, você também precisará instalar o SP1 no novo servidor antes de unir o farm.  
  
-   Analise os tópicos adicionais a seguir para entender os requisitos de sistema e de versão:  
  
     [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="bkmk_steps"></a> Etapas  
 As etapas neste tópico pressupõem que um administrador de farm do SharePoint esteja instalando e configurando o servidor. O diagrama mostra um ambiente típico de três camadas e os itens numerados no diagrama são descritos na lista a seguir:  
  
-   (1) Vários servidores de front-end da Web (WFE). Os servidores WFE exigem o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010.  
  
-   (2) Um único servidor de aplicativos que executa o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sites, por exemplo a Administração Central. As etapas a seguir adicionam um segundo servidor de aplicativos a esta camada.  
  
-   (3) Dois servidores de banco de dados do SQL Server.  
  
-   (4) Representa uma solução de software ou hardware de NLB (balanceamento de carga de rede)  
  
 ![Adicionando um servidor de aplicativos do Reporting Services](../../../2014/sql-server/install/media/rs-sharepointscale.gif "Adicionando um servidor de aplicativos do Reporting Services")  
  
 As etapas a seguir pressupõem que um administrador esteja instalando e configurando o servidor. O servidor será instalado como um novo servidor de aplicativos no farm e não usado como um WFE (front-end da Web).  
  
|Etapa|Descrição e link|  
|----------|--------------------------|  
|Execute a ferramenta de preparação dos produtos do SharePoint 2010.|Você deve ter a mídia de instalação do SharePoint 2010. A ferramenta de preparação é o **PrerequisiteInstaller.exe** na mídia de instalação.|  
|Instale um produto do SharePoint 2010.|1) selecione a **Farm de servidores** tipo de instalação.<br /><br /> 2) selecione **concluir** para o tipo de servidor.<br /><br /> 3) Quando a instalação for concluída, não execute o assistente de Configuração de Produtos do SharePoint se seu farm do SharePoint existente tiver o SharePoint 2010 SP1 instalado. Você deve instalar o SharePoint SP1 antes de executar o assistente de configuração de produtos do SharePoint.|  
|Instale o SharePoint Server 2010 SP1.|Se seu farm do SharePoint existente tiver o SharePoint 2010 SP1 instalado baixar e instalar o SharePoint 2010 SP1 de:[http://support.microsoft.com/kb/2460045](http://go.microsoft.com/fwlink/p/?linkID=219697).<br /><br /> Para obter mais informações sobre o SharePoint 2010 SP1, consulte [Problemas conhecidos quando você instala o Office 2010 SP1 e o SharePoint 2010 SP1](http://support.microsoft.com/kb/2532126):|  
|Execute o Assistente de Configuração de Produtos do SharePoint para adicionar o servidor ao farm.|1) na **produtos do Microsoft SharePoint 2010** grupo de programas, clique em **Assistente de configuração de produtos do Microsoft SharePoint 2010**.<br /><br /> 2) na **conectar-se a um Farm de servidores** página, selecione **conectar-se a um Farm existente** e clique em **próxima**.<br /><br /> 3) na **especificar definições do banco de dados de configuração** página, digite o nome do servidor de banco de dados usado para o farm existente e o nome do banco de dados de configuração. Clique em **Avançar**.<br />**\*\* Importante \* \* ** se você vir uma mensagem de erro semelhante à seguinte e você tiver verificado que tem permissões, em seguida, verificar quais protocolos estão habilitados para a configuração de rede do SQL Server no **do Sql Server Configuration Manager**: "Falha ao conectar ao servidor de banco de dados. Verifique se o banco de dados existe, é um Sql Server e que você tenha as permissões apropriadas para acessar o servidor."<br />**\*\* Importante \* \* ** se você vir a página **produto de Farm de servidor e o Status do Patch**, você precisará analisar as informações na página e atualizar o servidor com os arquivos necessários antes de prosseguir a unir o servidor ao farm.<br /><br /> 4) na **especificar configurações de segurança do Farm** página digitar sua frase secreta de farm e clique em **próxima**. Clique em **Avançar** na página de confirmação para executar o assistente.<br /><br /> 5) clique em **próxima** para executar o **Assistente de configuração de Farm**.|  
|Verifique se o servidor foi adicionado ao farm do SharePoint.|1) Na Administração Central do SharePoint, clique em **Gerenciar servidores neste farm** no grupo **Configurações do Sistema** .<br /><br /> 2) Verifique se o novo servidor foi adicionado e se o status está correto.<br /><br /> 3) Observe você não vir o serviço **serviço do SQL Server Reporting Services** em execução. O serviço será instalado na Próxima etapa.<br /><br /> 4) para remover este servidor da função WFE, clique em **gerenciar serviços no servidor** e interrompa o serviço **aplicativo Web do Microsoft SharePoint Foundation**.|  
|Instalar e configurar o modo do SharePoint do Reporting Services.|Executar a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obter mais informações sobre a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint, consulte [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) se o servidor só será usado como um servidor de aplicativos e o servidor não serão usados como um WFE, você não precisa selecionar **suplemento Reporting Services para produtos do SharePoint** em:<br /><br /> o **função de instalação** página, selecione **instalação de recurso do SQL Server**<br /><br /> o **seleção de recursos** página, selecione **Reporting Services - SharePoint**<br /><br /> -ou-<br /><br /> o **configuração do Reporting Services** verificação de página a **instalar somente** opção estiver selecionada para **Reporting Services SharePoint Mode**.|  
|Verifique se o Reporting Services está funcionando.|1) Na Administração Central do SharePoint, clique em **Gerenciar servidores neste farm** no grupo **Configurações do Sistema** .<br /><br /> 2) Verifique o serviço **SQL Server Reporting Services Service**.<br /><br /> Para obter mais informações, consulte [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).|  
  
##  <a name="bkmk_additional"></a> Configuração adicional  
 Você pode otimizar servidores individuais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma implantação em expansão para realizar somente processamento em segundo plano, para que eles não tenham que competir por recursos com execução interativa de relatório. O processamento em segundo plano inclui agendas, assinaturas e alertas de dados.  
  
 Para alterar o comportamento de servidores de relatórios individuais, defina **\<IsWebServiceEnable>** como falso no arquivo de configuração **RSreportServer.config**.  
  
 Por padrão, os servidores de relatório são configurados com \<IsWebServiceEnable> definido como TRUE. Quando todos os servidores forem configurados para TRUE, o interativo e em segundo plano terão a carga equilibrada em todos os nós no farm.  
  
 Se você configurar todos os servidores de relatório com \<IsWebServiceEnable> definido como False, verá uma mensagem de erro semelhante à seguinte quando tentar usar os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 O Serviço Web do Reporting Services não está habilitado. Configure pelo menos uma instância do serviço Reporting Services SharePoint ter \<IsWebServiceEnable > definido como true. Para obter mais informações, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar servidores web ou aplicativo para farms do SharePoint 2013](http://technet.microsoft.com/library/cc261752.aspx)   
 [Configurar serviços (SharePoint Server 2010)](http://technet.microsoft.com/library/ee794878.aspx)  
  
  
