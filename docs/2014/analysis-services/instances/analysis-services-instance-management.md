---
title: Gerenciamento de instâncias do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac0c6637dd08dc2ea8927853b7a6bf8dccca454d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080346"
---
# <a name="analysis-services-instance-management"></a>Gerenciamento de instância do Analysis Services
  Uma instância do Analysis Services é uma cópia do executável `msmdsrv.exe` que é executada como um serviço do sistema operacional. Cada instância é completamente independente de outras instâncias no mesmo servidor, tendo seus próprios parâmetros de configuração, permissões, portas, contas de inicialização, armazenamento de arquivo e propriedades de modo de servidor.  
  
 Cada instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executada como um serviço do Windows, Msmdsrv.exe, no contexto de segurança de uma conta de logon definida.  
  
-   O nome de serviço da instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é MSSQLServerOLAPService.  
  
-   O nome de serviço de cada instância nomeada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é MSOLAP$InstanceName.  
  
> [!NOTE]  
>  Se várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] estiverem instaladas, a configuração também instalará um serviço de redirecionamento, que é integrado com o serviço do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O serviço de redirecionamento é responsável por direcionar os clientes à instância nomeada adequada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O serviço do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é executado no contexto de segurança da conta de Serviço Local, uma conta de usuário limitada usada pelo Windows para serviços que não acessam recursos fora do computador local.  
  
 A expressão várias instâncias significa que você pode aumentar a escala instalando várias instâncias de servidor no mesmo hardware. Para o Analysis Services em particular, isso também significa que você pode dar suporte a diferentes modos de servidor tendo várias instâncias no mesmo servidor, cada uma configurada para ser executada em um modo específico.  
  
 Modo de servidor é uma propriedade de servidor que determina qual armazenamento e arquitetura de memória são usados para aquela instância. Um servidor que é executado em modo Multidimensional usa a camada de gerenciamento de recurso que foi criada para bancos de dados de cubo multidimensionais e modelos de mineração de dados. Em contraste, o modo de servidor de Tabela usa o mecanismo analítico na memória xVelocity (VertiPaq) e a compactação de dados para agregar dados conforme eles forem solicitados.  
  
 As diferenças no armazenamento e na arquitetura de memória significam que uma única instância do Analysis Services será executada em bancos de dados tabulares ou bancos de dados multidimensionais, mas não ambos. A propriedade de modo de servidor determina qual o tipo de banco de dados executado na instância.  
  
 O modo de servidor é definido durante a instalação quando você especifica o tipo de banco de dados que será executado no servidor. Para dar suporte a todos os modos disponíveis, você pode instalar várias instâncias do Analysis Services, cada uma implantada em um modo de servidor que corresponde aos projetos que você está criando.  
  
 Como regra geral, a maioria das tarefas administrativas que você deve executar não variam por modo. Como administrador de sistema do Analysis Services, você pode usar os mesmos procedimentos e scripts para gerenciar qualquer instância do Analysis Services em sua rede independentemente de como tenha sido instalado.  
  
> [!NOTE]  
>  A exceção é o PowerPivot para SharePoint. A administração de servidor de uma implantação do PowerPivot sempre está dentro do contexto de um farm do SharePoint. O PowerPivot difere de outros modos de servidor porque sempre é de instância única e sempre gerenciada por meio da Administração Central do SharePoint ou da Ferramenta de Configuração do PowerPivot. Embora seja possível conectar-se ao PowerPivot para SharePoint no SQL Server Management Studio ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], isso não é desejável. Um farm do SharePoint inclui infraestrutura que sincroniza o estado de servidor e supervisiona a disponibilidade do servidor. Usar outras ferramentas pode interferir com estas operações. Para obter mais informações sobre a administração de servidor do PowerPivot, consulte [PowerPivot para SharePoint &#40;SSAS&#41;](../power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Link|Descrição da tarefa|  
|----------|----------------------|  
|[Configuração de pós-instalação &#40;Analysis Services&#41;](post-install-configuration-analysis-services.md)|Descreve as tarefas necessárias e opcionais que completam ou modificam uma instalação do Analysis.|  
|[Conectar ao Analysis Services](connect-to-analysis-services.md)|Descreve as propriedades de cadeia de conexão, as bibliotecas de cliente, as metodologias de autenticação, e as etapas para estabelecer ou limpar conexões.|  
|[Monitorar uma instância do Analysis Services](monitor-an-analysis-services-instance.md)|Descreve ferramentas e técnicas por monitorar uma instância de servidor, inclusive como usar o Desempenho do Sistema e o SQL Server Profiler.|  
|[Script de tarefas administrativas no Analysis Services](../script-administrative-tasks-in-analysis-services.md)|Explica como automatizar muitas tarefas administrativas, inclusive processamento.|  
|[Cenários de globalização para Analysis Services multidimensional](../globalization-scenarios-for-analysis-services-multiidimensional.md)|Explica o suporte ao idioma e à ordenação, as etapas para alterar ambas as propriedades e dicas para definir e testar comportamentos de idioma e de ordenação.|  
|[Operações de log no Analysis Services](log-operations-in-analysis-services.md)|Descreve os logs e explica como configurá-los.|  
  
## <a name="see-also"></a>Consulte também  
 [Comparando soluções tabulares e multidimensionais &#40;SSAS&#41;](../comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Ferramentas de configuração do PowerPivot](../power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [Administração de servidor do PowerPivot e a configuração na Administração Central](../power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
