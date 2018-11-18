---
title: Planejando uma instalação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: quickstart
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bad3ae2d22a1aed53cb5da61f631e48bde480d56
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701914"
---
# <a name="planning-a-sql-server-installation"></a>Planejando uma instalação do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siga estas etapas:  
  
-   Examine os requisitos de instalação, as verificações de configuração do sistema e as considerações sobre segurança da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Execute a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar ou atualizar para uma versão posterior. Antes de atualizar, leia [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md).  
  
-   Use os utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Independentemente do método de instalação, é necessário confirmar a aceitação dos termos da licença de software como indivíduo ou em nome de uma entidade, a menos que o uso do software seja governado por um contrato separado, como um contrato de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou um contrato de terceiros com um ISV ou OEM.  
  
 Os termos da licença são exibidos para exame e aceitação na interface do usuário da Instalação. As instalações autônomas (usando os parâmetros `/Q` ou `/QS`) devem incluir o parâmetro `/IAcceptSQLServerLicenseTerms`. Baixe e leia os termos de licença separadamente em [Informações e termos de licença do Microsoft SQL Server](https://www.microsoft.com/Licensing/product-licensing/sql-server.aspx). Para os termos de licenciamento por volume, consulte [Termos de licenciamento e documentação](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Para as versões anteriores do SQL Server, consulte [Termos de Licença para Software Microsoft](https://go.microsoft.com/fwlink/?LinkID=148209).  
  
> [!NOTE]  
>  Dependendo de como você recebeu o software (por exemplo, por meio de licenciamento por volume da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), o uso do software pode estar sujeito a termos e condições adicionais.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Novidades na instalação do SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)  
 Este artigo descreve os detalhes sobre os recursos novos ou aprimorados de instalação nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
 Este artigo lista os requisitos mínimos de hardware e software para a instalação e execução de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 Este artigo descreve algumas práticas recomendadas de segurança que você deve considerar antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e depois de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 Este artigo descreve a configuração padrão de serviços nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as opções de configuração de serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode definir durante e após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)  
 Este artigo descreve a configuração padrão de protocolos de rede nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bem como as opções de configuração disponíveis.  
  
 [Trabalhar com várias versões e instâncias do SQL Server](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 Este artigo descreve as considerações para a instalação de várias versões e instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Versões de idiomas locais no SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md)  
 Este artigo descreve sobre as versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Instalar o SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 Esta seção fornece uma visão geral de opções de instalação diferentes disponíveis para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Instalar os recursos do business intelligence do SQL Server](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 Esta seção da documentação de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que fazem parte da plataforma Microsoft BI.  
  
 [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 A seção fornece uma visão geral da atualização de instâncias de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Desinstalar o SQL Server](../../sql-server/install/uninstall-sql-server.md)  
 Consulte esta seção para desinstalar totalmente uma instância existente do [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] e preparar o sistema para reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar e configurar o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Soluções de alta disponibilidade &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Antes de instalar o cluster de failover](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [Fazer Upgrade do SQL Server Usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
