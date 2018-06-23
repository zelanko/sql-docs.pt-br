---
title: SQL Server recursos descontinuados no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b842b9a3a98dd69d04f76ce26ccc84d6ec008822
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008976"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>Recursos do SQL Server descontinuados no SQL Server 2014
  Este tópico descreve os recursos que não estão mais disponíveis após a atualização para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>Recursos descontinuados no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Sem recursos descontinuados no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>Recursos descontinuados no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="discontinued-active-directory-helper-service"></a>Serviço auxiliar do Active Directory descontinuado  
 O serviço auxiliar do Active Directory e os componentes relacionados foram removidos. A tabela a seguir lista os componentes associados que são removidos como consequência:  
  
|Categoria|Recurso descontinuado|Substituição|  
|--------------|--------------------------|-----------------|  
|Procedimentos armazenados do sistema|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|Não há substituição disponível.|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>Recursos descontinuados no SQL Server 2008 R2  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Suporte à plataforma de 64 bits no Reporting Services  
 A partir do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] componente não oferece suporte a servidores baseados em Itanium que executam o Windows Server 2003 ou Windows Server 2003 R2. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua dar suporte a outros sistemas operacionais de 64 bits. incluindo o Windows Server°2008 for Itanium-Based Systems e o Windows Server°2008°R2 for Itanium-Based Systems. Para atualizar o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de uma instalação do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em uma edição Itanium-Based System do Windows Server 2003 ou do Windows Server 2003 R2, você deve atualizar o sistema operacional primeiro.  
  
## <a name="discontinued-features-in-sql-server-2008"></a>Recursos descontinuados no SQL Server 2008  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>SQL-DMO descontinuado da instalação do SQL Server Express  
 O SQL-DMO para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] foi removido do [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)]. É recomendável que você modifique os aplicativos que usam atualmente esse recurso o mais rápido possível. Se você deve dar suporte a SQL-DMO para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express, instale os componentes de compatibilidade com versões anteriores do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] feature pack a partir de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=51230). Use o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects (SMO) para novos trabalhos de desenvolvimento.  
  
### <a name="discontinued-option-for-web-assistant"></a>Opção descontinuada para Assistente da Web  
 A opção `sp_configure` para habilitar o Assistente da Web foi removida do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Em vez dessa função, recomendamos usar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
### <a name="surface-area-configuration-tool"></a>Ferramenta Configuração da Área da Superfície  
 A ferramenta Configuração da Área de Superfície foi substituída no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. A tabela a seguir mostra o que você pode usar para definir as configurações, as opções e os recursos do componente nesta versão.  
  
|Configurações de substituição e recursos de componente|Como configurar|  
|-------------------------------------------------|----------------------|  
|Opções de protocolos, conexão e inicialização|Use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do Configuration Manager.|  
|Recursos do [!INCLUDE[ssDE](../includes/ssde-md.md)]|Use o Gerenciamento Baseado em Política, as configurações de propriedade no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou sp_Configure.|  
|Recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Use as configurações de propriedade do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Propriedade EnableIntegrated Security|Use as configurações de propriedade do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -"Agendar eventos e entrega de relatórios" e "Serviço Web e acesso HTTP"|Edite o arquivo de configuração RSReportServer.config.|  
|Opções de linha de comando|Sem suporte nesta versão.|  
|SOAP e pontos de extremidade do [!INCLUDE[ssSB](../includes/sssb-md.md)]|Use [CREATE ENDPOINT](/sql/t-sql/statements/create-endpoint-transact-sql)e [ALTER ENDPOINT](/sql/t-sql/statements/alter-endpoint-transact-sql).|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>Parâmetros de prompt de comando descontinuados para a Instalação do SQL Server  
 A tabela a seguir mostra os parâmetros do prompt de comando Instalação das versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que não são suportados no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
|Parâmetro descontinuado|Parâmetro de substituição|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Desinstalar e /FEATURES|  
|DISABLENETWORKPROTOCOLS|/TCPENABLED para TCP/IP<sup>1</sup>|  
|DISABLENETWORKPROTOCOLS|/NPENABLED para Pipes nomeados<sup>1</sup>|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|Nenhum equivalente nesta versão.|  
|REINSTALLMODE|Nenhum equivalente nesta versão.|  
|REMOVE|/ACTION=Desinstalar e /FEATURES|  
|SAMPLEDATABASE|Nenhum equivalente nesta versão.|  
|SAVESYSDB|Nenhum equivalente nesta versão.|  
|SKUUPGRADE<sup>2</sup>|Nenhum equivalente nesta versão.|  
|UPGRADE|/ACTION=Atualizar e /FEATURES|  
|USESYSDB|Nenhum equivalente nesta versão.|  
  
 <sup>1</sup>esses parâmetros são válidos somente para a instalação.  
  
 <sup>2</sup>iniciando [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], especifique /Action = EditionUpgrade para atualizar uma edição existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para uma edição diferente qualquer momento sem usar a mídia de instalação original. Para obter mais informações sobre a versão e as atualizações de edição com suporte, consulte [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Para obter mais informações, consulte [Install SQL Server 2014 from the Command Prompt](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) (Instalar o SQL Server 2014 do Prompt de Comando).  
  
  
