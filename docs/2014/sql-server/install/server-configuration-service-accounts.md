---
title: Configuração do servidor-contas de serviço | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a894475f9dbdc95396f27b32f25f56bc409f0348
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036718"
---
# <a name="server-configuration---service-accounts"></a>Configuração do servidor - Contas de serviço
  Use a página Configuração do Servidor do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atribuir contas de logon aos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os serviços reais configurados nessa página dependem dos recursos que você selecionou para instalação.  
  
As contas de inicialização usadas para iniciar e executar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser contas de usuário de domínio, contas de usuário locais, contas de serviço gerenciado, contas virtuais ou contas de sistema internas.  
  
## <a name="options"></a>Opções  
 Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. Você também pode especificar se os serviços serão iniciados automaticamente ou manualmente, ou se eles serão desabilitados. A conta padrão é recomendada para a maioria das instalações.  
  
 No Windows 7 e no [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2, a maioria das contas assume como padrão uma conta virtual.  
  
 Se você configurar serviços para usar contas de domínio, a [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você configure as contas de serviço individualmente para fornecer privilégios mínimos a cada serviço, nos quais os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebem as permissões mínimas necessárias para concluir suas tarefas. Para obter mais informações que incluem descrições dos tipos de contas, consulte [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
 **Configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contas de serviço individualmente (recomendado)**  
 Use a grade para provisionar cada serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um nome de usuário e senha de logon, e para definir o tipo de inicialização para o serviço. Você pode usar contas de sistema internas, uma conta local, um grupo local, um grupo de domínio ou contas de usuário do domínio para os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Selecione quaisquer dos serviços a seguir para personalizar suas configurações.  
  
|Selecione este serviço|Para configurar os parâmetros de autenticação para|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|O serviço que executa trabalhos, monitores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e permite a automação de tarefas administrativas.<br /><br /> Não há conta de logon padrão para esse serviço.<br /><br /> O tipo de inicialização padrão é Manual.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|O tipo de inicialização padrão é Automático.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|O tipo de inicialização padrão é Automático.<br /><br /> Para o modo Integrado do SharePoint, você deve especificar uma conta de usuário do domínio Windows. A conta que você especifica é usada para o serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . A conta que você especifica para a instância atual também deve ser usada para as outras instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que você adicionar ao mesmo farm subsequentemente.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|As contas de serviço são usadas para configurar uma conexão de banco de dados do servidor de relatório. Escolha o serviço de rede interno se quiser usar configurações de autenticação padrão. Se você especificar uma conta de usuário de domínio, verifique se o SPN (Nome da Entidade de Serviço) está registrado para a conta, caso esteja usando a Autenticação do Windows no servidor de relatórios. Para obter mais informações, consulte [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).<br /><br /> O tipo de inicialização padrão é Automático.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um conjunto de ferramentas gráficas e objetos programáveis para mover, copiar e transformar dados.<br /><br /> O tipo de inicialização padrão é Automático.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Distributed Replay|A conta de serviço usada para o serviço do Distributed Replay Client.<br /><br /> Forneça uma conta na qual executará o serviço do Distributed Replay Client. Essa conta deve ser diferente da conta usada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> O tipo de inicialização padrão é Manual.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador Distributed Replay|A conta de serviço usada para o serviço do Distributed Replay Controller.<br /><br /> Forneça uma conta na qual executará o serviço do Distributed Replay Controller. Essa conta deve ser diferente da conta usada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> O tipo de inicialização padrão é Manual.|  
|Iniciador do Daemon de Filtro de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|O serviço que cria os processos de fdhost.exe. Ele é necessário para hospedar os separadores de palavras e os filtros que processam dados textuais para indexação de texto completo.<br /><br /> Se você fornecer uma conta de domínio na qual executará o serviço do Iniciador FDHOST, é altamente recomendável que você use uma conta de baixo privilégio. Essa conta deve ser diferente da conta usada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|O Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o serviço de resolução de nomes que fornece informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para computadores cliente. Esse serviço é compartilhado por várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A conta de logon padrão é NT Authority\Local service e não pode ser alterada durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode alterar a conta depois que a instalação for concluída. Se o tipo inicial não for especificado durante a instalação, isso será determinado da seguinte maneira:<br /><br /> O Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está definido como Automático e é executado nos cenários de instalação descritos a seguir:<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instância de cluster de failover<br />-<br />                            Instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que TCP ou NP está habilitado<br />-<br />                            Instância nomeada do Analysis Server e não está clusterizada<br /><br /> Se nenhum dos cenários anteriores se aplicar, e o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já estiver instalado, o estado atual do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será mantido.<br /><br /> O tipo de inicialização está definido como Desabilitado e não há uma instância existente de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior à instalação.|  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações sobre segurança para uma instalação do SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
