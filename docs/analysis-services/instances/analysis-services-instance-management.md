---
title: "Gerenciamento de instância do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7768246432f2711f7e3d99c046493e39b7e4ecf9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="analysis-services-instance-management"></a>Gerenciamento de instância do Analysis Services
  Uma instância do Analysis Services é uma cópia do executável **msmdsrv.exe** que é executada como um serviço do sistema operacional. Cada instância é completamente independente de outras instâncias no mesmo servidor, tendo seus próprios parâmetros de configuração, permissões, portas, contas de inicialização, armazenamento de arquivo e propriedades de modo de servidor.  
  
 Cada instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executada como um serviço do Windows, Msmdsrv.exe, no contexto de segurança de uma conta de logon definida.  
  
-   O nome de serviço da instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é MSSQLServerOLAPService.  
  
-   O nome de serviço de cada instância nomeada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é MSOLAP$InstanceName.  
  
> [!NOTE]  
>  Se várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] estiverem instaladas, a configuração também instalará um serviço de redirecionamento, que é integrado com o serviço do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O serviço de redirecionamento é responsável por direcionar os clientes à instância nomeada adequada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O serviço do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é executado no contexto de segurança da conta de Serviço Local, uma conta de usuário limitada usada pelo Windows para serviços que não acessam recursos fora do computador local.  
  
 A expressão várias instâncias significa que você pode aumentar a escala instalando várias instâncias de servidor no mesmo hardware. Para o Analysis Services em particular, isso também significa que você pode dar suporte a diferentes modos de servidor tendo várias instâncias no mesmo servidor, cada uma configurada para ser executada em um modo específico.  
  
 Modo de servidor é uma propriedade de servidor que determina qual armazenamento e arquitetura de memória são usados para aquela instância. Um servidor que é executado em modo Multidimensional usa a camada de gerenciamento de recurso que foi criada para bancos de dados de cubo multidimensionais e modelos de mineração de dados. Em contraste, o modo de servidor de tabela usa o mecanismo de análise in-memory VertiPaq e a compactação de dados para agregar dados conforme eles forem solicitados.  
  
 As diferenças no armazenamento e na arquitetura de memória significam que uma única instância do Analysis Services será executada em bancos de dados tabulares ou bancos de dados multidimensionais, mas não ambos. A propriedade de modo de servidor determina qual o tipo de banco de dados executado na instância.  
  
 O modo de servidor é definido durante a instalação quando você especifica o tipo de banco de dados que será executado no servidor. Para dar suporte a todos os modos disponíveis, você pode instalar várias instâncias do Analysis Services, cada uma implantada em um modo de servidor que corresponde aos projetos que você está criando.  
  
 Como regra geral, a maioria das tarefas administrativas que você deve executar não variam por modo. Como administrador de sistema do Analysis Services, você pode usar os mesmos procedimentos e scripts para gerenciar qualquer instância do Analysis Services em sua rede independentemente de como tenha sido instalado.  
  
> [!NOTE]  
>  A exceção é o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. A administração de servidor de uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sempre está dentro do contexto de um farm do SharePoint. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] difere de outros modos de servidor porque sempre é de instância única e sempre gerenciado por meio da Administração Central do SharePoint ou da Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Embora seja possível se conectar ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no SQL Server Management Studio ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], isso não é desejável. Um farm do SharePoint inclui infraestrutura que sincroniza o estado de servidor e supervisiona a disponibilidade do servidor. Usar outras ferramentas pode interferir com estas operações. Para obter mais informações sobre a administração do servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], consulte [Power Pivot para SharePoint &#40;SSAS&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Link|Descrição da tarefa|  
|----------|----------------------|  
|[Configuração de pós-instalação &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)|Descreve as tarefas necessárias e opcionais que completam ou modificam uma instalação do Analysis.|  
|[Conectar ao Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)|Descreve as propriedades de cadeia de conexão, as bibliotecas de cliente, as metodologias de autenticação, e as etapas para estabelecer ou limpar conexões.|  
|[Monitorar uma instância do Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)|Descreve ferramentas e técnicas por monitorar uma instância de servidor, inclusive como usar o Desempenho do Sistema e o SQL Server Profiler.|  
|[Alta Disponibilidade e Escalabilidade](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)|Descreve as técnicas mais usadas para fazer com que os bancos de dados do Analysis Services sejam de alta disponibilidade e escalonáveis. |  
|[Cenários de globalização para o Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)|Explica suporte a idioma e agrupamento, as etapas para alterar ambas as propriedades e dicas para definir e testar comportamentos de idioma e agrupamento.|  
|[Operações de log no Analysis Services](../../analysis-services/instances/log-operations-in-analysis-services.md)|Descreve os logs e explica como configurá-los.|  
  
  
## <a name="see-also"></a>Consulte também  
 [Comparando soluções tabulares e multidimensionais &#40;SSAS&#41;](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Ferramentas de configuração do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
