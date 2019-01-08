---
title: Adicionar um front-end da Web do Reporting Services a um farm | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 40641f0a6c16c697fb328b6ae4a87eb511a22aef
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367858"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>Adicionar um front-end da Web do Reporting Services a um farm
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo SharePoint inclui componentes necessários para servidores de aplicativos e WFE (servidores de front-end da Web). Este tópico aborda a instalação de componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] necessárias para um servidor de WFE, inclusive as páginas de aplicativo usadas por recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como assinaturas, alertas de dados e [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. A instalação primária do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] necessária para um WFE é instalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint 2010.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve ser um administrador local para executar a Instalação do SQL Server.  
  
-   O computador deve ser unido a um domínio.  
  
-   Você precisa saber o nome do servidor de banco de dados existente que está hospedando a configuração do SharePoint e os bancos de dados de conteúdo.  
  
-   O servidor de banco de dados deve ser configurado para permitir conexões de bancos de dados remotos.  Se não, você não poderá unir o novo servidor ao farm porque o novo servidor não poderá fazer uma conexão com os bancos de dados de configuração do SharePoint.  
  
-   O novo servidor precisará ter a mesma versão de SharePoint instalado que os servidores de farm atuais estão executando. Por exemplo, se o farm já tiver o SharePoint 2010 Service Pack 1 (SP1) instalado, você também precisará instalar o SP1 no novo servidor antes de unir o farm.  
  
-   Analise os tópicos adicionais a seguir para entender os requisitos de sistema e de versão:  
  
     [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>Etapas  
 As etapas neste tópico pressupõem que um administrador de farm do SharePoint esteja instalando e configurando o servidor. O diagrama mostra um ambiente típico de três camadas e os itens numerados no diagrama são descritos na lista a seguir:  
  
-   (1) Vários servidores de front-end da Web (WFE). Os servidores WFE exigem o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010. As etapas a seguir adicionam um segundo servidor de aplicativos a esta camada.  
  
-   (2) Dois servidores de aplicativos que executam o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sites, por exemplo a Administração Central.  
  
-   (3) Dois servidores de banco de dados do SQL Server.  
  
-   (4) Representa uma solução de software ou hardware de NLB (balanceamento de carga de rede)  
  
 ![Adicionar o SSRS a um novo WFE do SharePoint](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "Add SSRS to a new SharePoint WFE")  
  
 As etapas a seguir pressupõem que um administrador esteja instalando e configurando o servidor.  
  
|Etapa|Descrição e link|  
|----------|--------------------------|  
|Execute a ferramenta de preparação dos produtos do SharePoint 2010.|Você deve ter a mídia de instalação do SharePoint 2010. A ferramenta de preparação é o **PrerequisiteInstaller.exe** na mídia de instalação.|  
|Instale um produto do SharePoint 2010.|1) selecione a **Farm de servidores** tipo de instalação.<br /><br /> 2) selecione **concluir** para o tipo de servidor.<br /><br /> 3) Quando a instalação for concluída, não execute o assistente de Configuração de Produtos do SharePoint se seu farm do SharePoint existente tiver o SharePoint 2010 SP1 instalado. Você deve instalar o SharePoint SP1 antes de executar o assistente de configuração de produtos do SharePoint.|  
|Instale o SharePoint Server 2010 SP1.|Se seu farm do SharePoint existente tiver o SharePoint 2010 SP1 instalado baixar e instalar o SharePoint 2010 SP1 de:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697).<br /><br /> Para obter mais informações sobre o SharePoint 2010 SP1, consulte [Problemas conhecidos quando você instala o Office 2010 SP1 e o SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126):|  
|Execute o Assistente de Configuração de Produtos do SharePoint para adicionar o servidor ao farm.|1) na **produtos do Microsoft SharePoint 2010** grupo de programas, clique em **Assistente de configuração de produtos do Microsoft SharePoint 2010**.<br /><br /> 2) na **conectar-se a um Farm de servidores** página, selecione **conectar-se a um Farm existente** e clique em **próxima**.<br /><br /> 3) na **especificar definições do banco de dados de configuração** página, digite o nome do servidor de banco de dados usado para o farm existente e o nome do banco de dados de configuração. Clique em **Avançar**.<br />**&#42;&#42;Importante &#42; &#42;**  se você vir uma mensagem de erro semelhante à seguinte e você tiver verificado que tem permissões, em seguida, verificar quais protocolos estão habilitados para a configuração de rede do SQL Server no **Sql Server Configuration Manager**. "Falha ao conectar ao servidor de banco de dados. Verifique se o banco de dados existe, é um Sql Server e que você tenha as permissões apropriadas para acessar o servidor."<br />**&#42;&#42;Importante &#42; &#42;**  se você vir a página **produto de Farm de servidor e o Status do Patch**, você precisará analisar as informações na página e atualizar o servidor com os arquivos necessários antes de continuar a unir o servidor ao farm.<br /><br /> 4) na **especificar configurações de segurança do Farm** página digitar sua frase secreta de farm e clique em **próxima**. Clique em **Avançar** na página de confirmação para executar o assistente.<br /><br /> 5) clique em **próxima** para executar o **Assistente de configuração de Farm**.|  
|Verifique se o servidor foi adicionado ao farm do SharePoint.|1) Na Administração Central do SharePoint, clique em **Gerenciar servidores neste farm** no grupo **Configurações do Sistema** .<br /><br /> 2) Verifique se o novo servidor foi adicionado e se o status está correto.<br /><br /> 3) para remover este servidor da função WFE, clique em **gerenciar serviços no servidor** e interrompa o serviço **aplicativo Web do Microsoft SharePoint Foundation**.|  
|Instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] suplemento para produtos do SharePoint 2010.|Há vários métodos para instalar o suplemento. As seguintes etapas usam o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obter mais informações sobre como instalar o suplemento, consulte [instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;do SharePoint 2010 e SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Executar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalação:<br /><br /> 1) Na página **Função de instalação** , selecione **Instalação de recurso do SQL Server**<br /><br /> 2) na **seleção de recursos** página, selecione **suplemento do Reporting Services para produtos do SharePoint**<br /><br /> 3) clique em **próxima** nas próximas várias páginas para concluir as opções de instalação.<br /><br /> Para obter mais informações sobre como instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [instalar o Reporting Services SharePoint Mode para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Verifique se o novo servidor está operacional.|1) Na Administração Central do SharePoint, clique em **Gerenciar servidores neste farm** no grupo **Configurações do Sistema** .<br /><br /> 2) Verifique se o novo servidor está na lista.|  
|Atualize sua solução de NLB.|Se apropriado, atualize seu ambiente de hardware ou software NLB para incluir o novo servidor.|  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar uma Web ou servidor de aplicativos ao farm (SharePoint Server 2010)](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\))   
 [Configurar serviços (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
