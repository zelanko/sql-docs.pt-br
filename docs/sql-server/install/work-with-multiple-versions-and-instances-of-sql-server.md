---
title: "Trabalhar com v&#225;rias vers&#245;es e inst&#226;ncias do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instalações simultâneas [SQL Server]"
  - "versões [SQL Server], várias"
  - "instalações lado a lado [SQL Server]"
  - "várias versões de componente do SQL Server"
  - "Instalando o SQL Server, instalações lado a lado"
  - "Configuração [SQL Server], instalações lado a lado"
  - "edição de 64 bits [SQL Server]"
  - "edição de 32 bits [SQL Server]"
  - "edições [SQL Server], instalações lado a lado"
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 67
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 67
---
# Trabalhar com v&#225;rias vers&#245;es e inst&#226;ncias do SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo computador. Você também pode atualizar versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador em que versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já estejam instaladas. Para ver os cenários de atualização com suporte, confira [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
## Componentes de versão e numeração  
 Os conceitos a seguir são úteis para entender o comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias lado a lado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O formato de versão de produto padrão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é MM.nn.bbbb.rr onde cada segmento é definido como:  
  
 MM - versão principal  
  
 nn - versão secundária  
  
 bbbb - número da compilação  
  
 rr - número de revisão da compilação  
  
 Em cada versão principal ou secundária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], há um incremento ao número de versão para diferenciá-la de versões anteriores. Esta alteração para a versão é usada para muitos propósitos. Isto inclui exibir informações de versão na interface do usuário, controlar como são substituídos os arquivos durante a atualização, aplicar pacotes de serviço e também como um mecanismo para diferenciação funcional entre as versões sucessivas.  
  
### Componentes compartilhados por todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Alguns componentes são compartilhados por todas as instâncias de todas as versões instaladas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando você instalar versões diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lado a lado na mesma máquina, esses componentes serão atualizados automaticamente para a versão mais recente. Esses componentes são geralmente desinstalados automaticamente quando a última instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é desinstalada.  
  
 Exemplos: Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Gravador VSS do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### Componentes compartilhados por todas as instâncias da mesma versão principal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As versões que têm a mesma versão principal compartilham alguns componentes em todas as instâncias. Se os componentes compartilhados forem selecionados durante a atualização, os componentes existentes serão atualizados para a versão mais recente.  
  
 Exemplos: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### Componentes compartilhados em versões secundárias  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As versões que têm os mesmos componentes compartilhados de versão principal.secundária.  
  
 Exemplo: arquivos de suporte à instalação.  
  
### Componentes específicos de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Alguns componentes ou serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são específicos de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles também são conhecidos como capazes de reconhecimento de instância. Eles compartilham a mesma versão que a instância que os hospeda e são usados exclusivamente para aquela instância.  
  
 Exemplos: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### Componentes que são independentes das versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Alguns componentes são instalados durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas são independentes das versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles podem ser compartilhados por versões principais ou por todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Exemplos: Microsoft Sync Framework, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para obter mais informações sobre a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, veja [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md). Para obter mais informações sobre como desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, veja [Desinstalar uma instância existente do SQL Server &#40;Instalação&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lado a lado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador que já está executando instâncias de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se já existir uma instância padrão no computador, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser instalado como uma instância nomeada.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O SysPrep não dá suporte à instalação lado a lado de instâncias preparadas do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo computador. Por exemplo, você não pode preparar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lado a lado com uma instância preparada do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. No entanto, você pode instalar diversas instâncias preparadas da mesma versão principal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lado a lado no mesmo computador. Para obter mais informações, consulte [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não pode ser instalado lado a lado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador executando o Windows Server 2008 R2 Server Core SP1. Para obter mais informações sobre instalações Server Core, veja [Instalar o SQL Server 2016 no Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md).  
  
 A tabela a seguir mostra o suporte lado a lado para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Instância existente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Suporte lado a lado|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 32 bits<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 32 bits<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 32 bits<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 32 bits<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 32 bits<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
  
## Impedindo conflitos de endereço IP  
 Quando uma Instância de Cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalada lado a lado com uma instância autônoma do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], procure evitar conflitos de número de porta TCP nos endereços IP. Conflitos normalmente ocorrem quando duas instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são ambas configuradas para usar a porta TCP padrão (1433). Para evitar conflitos, configure uma instância para usar uma porta fixa não padrão. A configuração de uma porta fixa é normalmente mais fácil na instância autônoma. A configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar portas diferentes impedirá um conflito de Endereço IP/porta TCP inesperado que bloqueie uma inicialização de instância quando uma Instância de Cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhar para o nó em espera  
  
## Consulte também  
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)   
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Atualizar para o SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [Compatibilidade com versões anteriores_excluída](../Topic/Backward%20Compatibility_deleted.md)  
  
  