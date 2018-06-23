---
title: Configuração do servidor — contas de serviço | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e390c18563b092fd0460da5b9aed90828921d10b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120940"
---
# <a name="server-configuration---service-accounts"></a>Configuração do servidor - Contas de serviço
  Use a página Configuração do Servidor do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atribuir contas de logon aos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os serviços reais configurados nessa página dependem dos recursos que você selecionou para instalação.  
  
 Contas de inicialização usadas para iniciar e executar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser contas de usuário de domínio do HYPERLINK "ms-help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm" \l "Domain_User", contas de usuário locais, contas de serviço gerenciado contas virtuais ou contas de sistema internas.  
  
## <a name="options"></a>Opções  
 Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. A conta padrão é recomendada para a maioria das instalações.  
  
 No Windows 7 e [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2, a maioria das contas padrão para uma conta virtual.  
  
 Se você configurar serviços para usar contas de domínio, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para fornecer privilégios mínimos para cada serviço, onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviços recebem o mínimo permissões necessárias para concluir suas tarefas. Para mais informações, inclusive descrições dos tipos de contas, consulte [configurar contas de serviço do Windows e permissões](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
 **Configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contas de serviço individualmente (recomendado)**  
 Use a grade para provisionar cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço com um nome de logon do usuário e senha e para definir o tipo de inicialização para o serviço. Você pode usar contas de sistema internas, uma conta local, grupo, grupo de domínio ou contas de usuário de domínio para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviços.  
  
 Selecione quaisquer dos serviços a seguir para personalizar suas configurações.  
  
|Selecione este serviço|Para configurar os parâmetros de autenticação para|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|O serviço que executa trabalhos, monitores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e permite a automação de tarefas administrativas.<br /><br /> Não há conta de logon padrão para esse serviço.<br /><br /> O tipo de inicialização padrão é Manual.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|O tipo de inicialização padrão é Automático.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|O tipo de inicialização padrão é Automático.<br /><br /> Para o modo Integrado do SharePoint, você deve especificar uma conta de usuário do domínio Windows. A conta especificada é usada para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] service. A conta que você especifica para a instância atual também deve ser usada para as outras instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que você adicionar ao mesmo farm subsequentemente.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|As contas de serviço são usadas para configurar uma conexão de banco de dados do servidor de relatório. Escolha o serviço de rede interno se quiser usar configurações de autenticação padrão. Se você especificar uma conta de usuário de domínio, verifique se o SPN (Nome da Entidade de Serviço) está registrado para a conta, caso esteja usando a Autenticação do Windows no servidor de relatórios. Para obter mais informações, consulte [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).<br /><br /> O tipo de inicialização padrão é Automático.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um conjunto de ferramentas gráficas e objetos programáveis para mover, copiar e transformar dados.<br /><br /> O tipo de inicialização padrão é Automático.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Distributed Replay|A conta de serviço usada para o serviço do Distributed Replay Client.<br /><br /> Forneça uma conta na qual executará o serviço do Distributed Replay Client. Essa conta deve ser diferente da conta que você usa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service.<br /><br /> O tipo de inicialização padrão é Manual.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador Distributed Replay|A conta de serviço usada para o serviço do Distributed Replay Controller.<br /><br /> Forneça uma conta na qual executará o serviço do Distributed Replay Controller. Essa conta deve ser diferente da conta que você usa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service.<br /><br /> O tipo de inicialização padrão é Manual.|  
|Iniciador do Daemon de Filtro de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|O serviço que cria os processos de fdhost.exe. Ele é necessário para hospedar os separadores de palavras e os filtros que processam dados textuais para indexação de texto completo.<br /><br /> Se você fornecer uma conta de domínio na qual executará o serviço do Iniciador FDHOST, é altamente recomendável que você use uma conta de baixo privilégio. Essa conta deve ser diferente da conta que você usa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] É o serviço de resolução de nome fornece [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de conexão para computadores cliente. Esse serviço é compartilhado por várias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instâncias. A conta de logon padrão é NT Authority\Local service e não pode ser alterada durante a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação. Você pode alterar a conta depois que a instalação for concluída. Se o tipo inicial não for especificado durante a instalação, isso será determinado da seguinte maneira:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Está definido como automático e é executado nos cenários de instalação descritos abaixo:<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instância de cluster de failover<br />-<br />                            Instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que TCP ou NP está habilitado<br />-<br />                            Instância nomeada do Analysis Server e não está clusterizada<br /><br /> Se nenhum dos cenários anteriores se aplicar, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] navegador já estiver instalado, o estado atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] navegador será mantido.<br /><br /> O tipo de inicialização está definido como Desabilitado e não há uma instância existente de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior à instalação.|  
  
## <a name="see-also"></a>Consulte também  
 [Considerações sobre segurança para uma instalação do SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  