---
title: Requisitos do aplicativo Web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 15b394c836cb24229944f4e0775dfccad847a32b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482880"
---
# <a name="web-application-requirements-master-data-services"></a>Requisitos do aplicativo Web (Master Data Service)
  
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] é um aplicativo Web hospedado pelo IIS (Serviços de Informações da Internet). O [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] funciona apenas no Internet Explorer (IE) 7 ou posterior. Não há suporte para o IE 7 e versões anteriores, o Microsoft Edge e o Chrome.  
  
 Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar e configurar o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . 
  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] configura o IIS no computador local; portanto, ele é ideal para tarefas de configuração inicial da Web. Por exemplo, configure um ambiente do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] com um único aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ou configure o primeiro aplicativo Web em uma implantação em expansão do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Use ferramentas do IIS para executar tarefas mais complexas, como, por exemplo, configurar vários servidores Web em uma implantação em expansão.  
  
> [!NOTE]  
>  Qualquer computador em que os componentes do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] deve ser licenciado. Para obter mais informações, consulte o Contrato de Licença de Usuário Final (EULA).  
  
## <a name="requirements"></a>Requisitos  
  
### <a name="operating-system"></a>Sistema operacional  
 Os sistemas operacionais Windows a seguir incluem a funcionalidade de IIS (Serviços de Informações da Internet) necessária para o aplicativo Web do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e o serviço Web.  
  
|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer (64 bits) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Enterprise (64 bits) x64|
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence (64 bits) x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|
  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 Professional, Enterprise e Ultimate<br /><br /> Windows 8.0 Professional, Enterprise e Ultimate|
  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|
  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 Para obter uma lista completa dos sistemas operacionais Windows com suporte para sua edição do, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consulte [requisitos de hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 Para trabalhar no aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , o Silverlight 5 deve estar instalado no computador cliente. Se você não tiver a versão exigida do Silverlight, será solicitado a instalá-la quando navegar até uma área do aplicativo Web que a exige. Você pode instalar o Silverlight 5 por [aqui](https://go.microsoft.com/fwlink/?LinkId=243096).  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>Função e serviços de função (sistemas operacionais Windows Server 2008 ou Windows Server 2008 R2, Windows 7)  
 No Windows Server 2008 R2, você pode usar o **Gerenciador do Servidor**, que está disponível no Microsoft Management Console (MMC), para instalar a função **Servidor Web (IIS)** e os seguintes serviços de função necessários.  
  
> [!NOTE]  
>  Nos sistemas operacionais [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] e Windows 7, use **Programas e Recursos** no Painel de Controle para habilitar essas opções na caixa de diálogo **Recursos do Windows** .  
  
||  
|-|  
|Servidor Web<br /><br /> Recursos comuns de HTTP<br /><br /> Conteúdo estático<br /><br /> Documento padrão<br /><br /> Navegação de diretório<br /><br /> Erros de HTTP<br /><br /> Desenvolvimento de Aplicativo<br /><br /> ASP.NET<br /><br /> Extensibilidade .NET<br /><br /> Extensões ISAPI<br /><br /> Filtros ISAPI<br /><br /> Integridade e diagnóstico<br /><br /> Log de HTTP<br /><br /> Monitor de solicitação<br /><br /> Segurança<br /><br /> Autenticação do Windows<br /><br /> Filtragem de solicitação<br /><br /> Desempenho<br /><br /> Compactação de conteúdo estático<br /><br /> Ferramentas de gerenciamento<br /><br /> Console de Gerenciamento IIS|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>Função e serviços de função (sistemas operacionais Windows Server 2012 ou Windows 8)  
 No Windows Server 2012, você pode usar o **Gerenciador do Servidor**, que está disponível no Microsoft Management Console (MMC), para instalar a função **Servidor Web (IIS)** e os seguintes serviços de função necessários.  
  
> [!NOTE]  
>  No sistema operacional Windows 8, use **Programas e Recursos** no Painel de Controle para habilitar essas opções na caixa de diálogo **Recursos do Windows** .  
  
||  
|-|  
|Serviços de Informação da Internet<br /><br /> Ferramentas de gerenciamento da Web<br /><br /> Console de Gerenciamento IIS<br /><br /> Serviços da World Wide Web<br /><br /> Desenvolvimento de Aplicativo<br /><br /> .NET Extensibility 3.5<br /><br /> Extensibilidade do .NET 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> Extensões ISAPI<br /><br /> Filtros ISAPI<br /><br /> Recursos comuns de HTTP<br /><br /> Documento padrão<br /><br /> Navegação de diretório<br /><br /> Erros de HTTP<br /><br /> Conteúdo estático<br /><br /> [Observação: não instale a Publicação WebDAV]<br /><br /> Integridade e diagnóstico<br /><br /> Log de HTTP<br /><br /> Monitor de solicitação<br /><br /> Desempenho<br /><br /> Compactação de conteúdo estático<br /><br /> Segurança<br /><br /> Filtragem de solicitação<br /><br /> Autenticação do Windows|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>Recursos (sistemas operacionais Windows Server 2008 ou Windows Server 2008 R2, Windows 7)  
 No [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] ou no Windows Server 2008 R2, você pode usar o **Gerenciador do Servidor** para instalar os seguintes recursos necessários.  
  
> [!NOTE]  
>  Nos sistemas operacionais [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] e Windows 7, use **Programas e Recursos** no Painel de Controle para habilitar essas opções na caixa de diálogo **Recursos do Windows** .  
  
||  
|-|  
|Recursos do .NET Framework 3.0<br /><br /> Ativação de WCF<br /><br /> Ativação de HTTP<br /><br /> Ativação não HTTP<br /><br /> Serviço de Ativação de Processos do Windows<br /><br /> Modelo de processo<br /><br /> Ambiente .NET<br /><br /> APIs de configuração|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>Recursos (sistemas operacionais Windows Server 2012 ou Windows 8)  
 No Windows Server 2012, você pode usar o **Gerenciador do Servidor** para instalar os seguintes recursos necessários:  
  
> [!NOTE]  
>  No sistema operacional Windows 8, use **Programas e Recursos** no Painel de Controle para habilitar essas opções na caixa de diálogo **Recursos do Windows** .  
  
||  
|-|  
|.NET Framework 3.5 (inclui o .NET 2.0 e 3.0)<br /><br /> Serviços avançados do .NET Framework 4.5<br /><br /> ASP.NET 4.5<br /><br /> Serviços WCF<br /><br /> Ativação de HTTP [Observação: isso é necessário.]<br /><br /> Compartilhamento de porta TCP<br /><br /> Serviço de Ativação de Processos do Windows<br /><br /> Modelo de processo<br /><br /> Ambiente .NET<br /><br /> APIs de configuração|  
  
### <a name="accounts-and-permissions"></a>Contas e permissões  
  
|Type|DESCRIÇÃO|  
|----------|-----------------|  
|Conta do Windows|Você deve fazer logon no computador do servidor Web com uma conta do Windows que tenha permissão para configurar funções, serviços de função e recursos do Windows e para criar e gerenciar pools de aplicativos, sites e aplicativos Web no IIS no computador local.|  
|Conta de serviço|Quando você criar o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] no [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], especifique uma identidade para o pool de aplicativos em que o aplicativo é executado. Esta conta pode ser diferente da conta de serviço especificada quando o banco de dados [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] foi criado.<br /><br /> Essa identidade deve ser uma conta de usuário de domínio e é acrescentada à função de banco de dados mds_exec no banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para acesso ao banco de dados. Para obter mais informações, veja [Logons, usuários e funções de banco de dados &#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md). Essa conta também é adicionada a um grupo do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no Windows, **MDS_ServiceAccounts**, que recebe permissão para o diretório temporário de compilação, **MDSTempDir**, no sistema de arquivos. Para obter mais informações, veja [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md).<br /><br /> A conta do pool de aplicativos precisa de permissão VIEW SERVER STATE, para evitar erros de servidor. Por exemplo, o comando MDS Validate Version falhará com um erro de servidor. Para obter mais informações, consulte [Falha do comando MDS Validate Version com um erro de servidor no SQL Server 2012 e no SQL Server 2014](https://go.microsoft.com/fwlink/p/?LinkId=526304)|  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar Master Data Services](install-master-data-services.md)   
 [Criar um aplicativo Web Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)   
 [&#40;Gerenciador de Configuração do Master Data Services da página de configuração da Web&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
