---
title: Reporting Services (SSRS) opções de configuração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.reportserverinstoptions.f1
helpviewer_keywords:
- Report Server Installation Options page [SQL Server Installation Wizard]
- report servers [Reporting Services], installing
- SQL Server Installation Wizard, Report Server Installation Options page
ms.assetid: e4561f6c-bc7f-467e-821a-cde8e5cd7391
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 67c1cf99f536b7cc6de0cef3633af19ae88014a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092585"
---
# <a name="reporting-services-configuration-options-ssrs"></a>Opções de configuração do Reporting Services (SSRS)
  Use a página **Configuração do Reporting Services** do Assistente de Instalação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar como um servidor de relatório é instalado e configurado. A disponibilidade de uma opção de instalação depende das opções escolhidas anteriormente na página **Seleção de Recursos** e se você também está instalando uma instância local do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] enquanto está instalando o servidor de relatório.  
  
 Em alguns casos, se um certificado SSL estiver instalado no computador e estiver associado a um caractere curinga forte, a Instalação criará as URLs do Reporting Services usando o prefixo HTTPS. Para obter mais informações sobre como os certificados são mapeados para URLs do Reporting Services, consulte [Configurando um servidor de relatório para conexões do Secure Sockets Layer (SSL)](https://go.microsoft.com/fwlink/?LinkId=199089) (https://go.microsoft.com/fwlink/?LinkId=199089) nos Manuais Online do SQL Server.  
  
 Para obter mais informações sobre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a instalação e configuração dessa versão, consulte [informações de instalação adicionais](https://go.microsoft.com/fwlink/?LinkId=207425) (https://go.microsoft.com/fwlink/?LinkId=207425).  
  
## <a name="options"></a>Opções  
  
### <a name="reporting-services-native-mode"></a>Modo nativo do Reporting Services  
 Se a Instalação não puder executar uma configuração padrão do servidor de relatório porque um ou mais requisitos não foram atendidos, o Assistente de Instalação permitirá somente a opção de instalação mínima, copiando os arquivos que você precisa, mas exigindo que você use o Gerenciador de Configuração do Reporting Services para configurar o servidor de relatório de modo nativo depois que a instalação for concluída.  
  
> [!NOTE]  
>  Um arquivo de banco de dados do servidor de relatório existente pode causar falha na instalação se você escolher uma das opções de instalação padrão. Ao escolher uma opção de instalação padrão, a instalação tentará criar um banco de dados do servidor de relatório usando o nome padrão. Se já houver um banco de dados com esse nome, ocorrerá falha na instalação e você deverá reverter a instalação. Para evitar esse problema, renomeie o banco de dados existente antes de executar a instalação ou escolher a opção **Instalar somente** para que você possa especificar configurações de banco de dados personalizadas depois que a instalação for concluída.  
  
#### <a name="install-and-configure"></a>Instalar e configurar  
 Instala uma instância do servidor de relatório no Modo Nativo usando os valores padrão dos bancos de dados do servidor de relatório, a conta de serviço e as reservas de URL. Ao escolher essa opção, a instância do servidor de relatório estará pronta para uso quando a Instalação for concluída. A Instalação cria o banco de dados do servidor de relatório usando uma instância local do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e configura um servidor de relatório para usar valores padrão.  
  
 Essa opção estará disponível apenas se os valores padrão usados em uma instalação do servidor de relatório forem válidos para o seu sistema. Essa opção é recomendada para desenvolvedores que desejam instalar todos os componentes localmente e para os usuários que estejam avaliando o software.  
  
 Para exibir informações sobre as Configurações padrão que a Instalação usa ou para descobrir por que a configuração padrão não pode ser instalada, clique em **Detalhes**. Para obter mais informações sobre a configuração padrão para um servidor de relatório do modo nativo, consulte [a configuração padrão para instalação no modo nativo (Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199091) (https://go.microsoft.com/fwlink/?LinkId=199091).  
  
#### <a name="install-only"></a>Instalar somente  
 Instala os arquivos de programas do servidor de relatório, cria a conta do serviço Servidor de Relatório e registra o provedor WMI (Instrumentação de Gerenciamento do Windows) do servidor de relatório. Essa opção de instalação é chamada de instalação "somente arquivos". Selecione-a se você não quiser usar a configuração padrão. Se não for possível instalar a configuração padrão ou se você estiver instalando um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que inclua o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], essa será a única opção disponível. Para obter mais informações sobre uma instalação somente arquivos, consulte [instalação somente de arquivos (Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199093) (https://go.microsoft.com/fwlink/?LinkId=199093).  
  
 Depois que a Instalação for concluída, você deverá criar o banco de dados do servidor de relatório e configurar o servidor de relatório antes que ele possa ser usado. Para configurar um servidor de relatório e criar o banco de dados, use a ferramenta Gerenciador de Configurações do Reporting Services. Para obter mais informações, confira [Como Criar um banco de dados do servidor de relatório (configuração do Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199094) (https://go.microsoft.com/fwlink/?LinkId=199094) e [Configurando uma Conexão de banco de dados do servidor de relatório](https://go.microsoft.com/fwlink/?LinkId=199095) (https://go.microsoft.com/fwlink/?LinkId=199095).  
  
### <a name="reporting-services-sharepoint-mode"></a>Modo do SharePoint do Reporting Services  
  
#### <a name="install-only"></a>Instalar somente  
 Instala os arquivos de programa do servidor de relatório e os cmdlets do PowerShell. Depois que a instalação for concluída, você precisará iniciar os serviços do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e criar um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte o seguinte:  
  
-   [Instalando o Reporting Services servidor de relatório do modo do SharePoint para Power View e alerta de dados](https://go.microsoft.com/fwlink/?LinkId=207543) (https://go.microsoft.com/fwlink/?LinkId=207543).  
  
-   [Instalar o Reporting Services modo do SharePoint como um único Farm de servidores](https://go.microsoft.com/fwlink/?LinkId=207544) (https://go.microsoft.com/fwlink/?LinkId=207544).  
  
-   [Reporting Services Report Server (SSRS)](https://go.microsoft.com/fwlink/?LinkID=207244) (https://go.microsoft.com/fwlink/?LinkID=207244).  
  
## <a name="installing-the-reporting-services-add-in-for-sharepoint-technologies"></a>Instalando o Suplemento Reporting Services para Tecnologias SharePoint  
 A partir da versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o suplemento pode ser instalado como parte da instalação do SQL Server na página de seleção de recursos do assistente de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 No entanto, você pode instalar o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010 usando um dos métodos a seguir:  
  
-   Execute a ferramenta de Preparação de Produtos do SharePoint 2010 **PreRequisiteInstaller.exe**.  
  
-   Execute a instalação a partir da mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Clique no arquivo **rsSharePoint.msi** na pasta de Instalação da mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depois que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for concluída.  
  
-   Baixar e instalar o suplemento. Para obter mais informações, consulte [onde encontrar o suplemento Reporting Services para produtos do SharePoint](https://go.microsoft.com/fwlink/?LinkID=208634) (https://go.microsoft.com/fwlink/?LinkID=208634).  
  
## <a name="see-also"></a>Consulte também  
 [Inicie o Reporting Services Configuration Manager](https://go.microsoft.com/fwlink/?LinkId=199096)   
 [Criar um banco de dados do servidor de relatório (configuração do Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199094)   
 [Atualizar e migrar o Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)   
 [Instalação de prompt de comando de modo do SharePoint do Reporting Services e modo nativo](https://go.microsoft.com/fwlink/?LinkId=217620)  
  
  
