---
title: Trabalhar com várias versões e instâncias
description: É possível instalar várias instâncias do SQL Server ou instalar o SQL Server em um computador em que versões anteriores do SQL Server já estão instaladas.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- concurrent installations [SQL Server]
- versions [SQL Server], multiple
- side-by-side installations [SQL Server]
- multiple SQL Server component versions
- installing SQL Server, side-by-side installations
- Setup [SQL Server], side-by-side installations
- 64-bit edition [SQL Server]
- 32-bit edition [SQL Server]
- editions [SQL Server], side-by-side installations
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3067b285a1d821808323cff524b109f782172e84
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899621"
---
# <a name="work-with-multiple-versions-and-instances-of-sql-server"></a>Trabalhar com várias versões e instâncias do SQL Server

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

É possível instalar várias instâncias do SQL Server ou instalar o SQL Server em um computador em que versões anteriores do SQL Server já estão instaladas.

Os seguintes itens relacionados ao SQL Server são compatíveis com a instalação de várias instâncias no mesmo computador:

- Mecanismo de Banco de Dados

- Serviços de análise

- Reporting Services (no SQL Server 2016 e anteriores). A partir do SQL Server 2016. O SSRS (SQL Server Reporting Services) tem uma instalação separada. 


É possível atualizar versões anteriores do SQL Server em um computador em que outras versões anteriores do SQL Server já estão instaladas. Para ver os cenários de atualização com suporte, confira [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).
  
## <a name="version-components-and-numbering"></a>Componentes de versão e numeração

 Os conceitos a seguir são úteis para entender o comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias lado a lado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
 O formato de versão de produto padrão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é MM.nn.bbbb.rr onde cada segmento é definido como:
  
 MM - versão principal  
  
 nn - versão secundária  
  
 bbbb - número da compilação  
  
 rr - número de revisão da compilação  
  
 Em cada versão principal ou secundária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], há um incremento ao número de versão para diferenciá-la de versões anteriores. Esta alteração para a versão é usada para muitos propósitos. Isto inclui exibir informações de versão na interface do usuário, controlar como são substituídos os arquivos durante a atualização, aplicar pacotes de serviço e também como um mecanismo para diferenciação funcional entre as versões sucessivas.
  
### <a name="components-shared-by-all-versions-of-ssnoversion"></a>Componentes compartilhados por todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 Alguns componentes são compartilhados por todas as instâncias de todas as versões instaladas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando você instalar versões diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lado a lado na mesma máquina, esses componentes serão atualizados automaticamente para a versão mais recente. Esses componentes são geralmente desinstalados automaticamente quando a última instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é desinstalada.
  
 Exemplos: Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Gravador VSS do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
### <a name="components-shared-across-all-instances-of-the-same-major-version-of-ssnoversion"></a>Componentes compartilhados por todas as instâncias da mesma versão principal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As versões que têm a mesma versão principal compartilham alguns componentes em todas as instâncias. Se os componentes compartilhados forem selecionados durante a atualização, os componentes existentes serão atualizados para a versão mais recente.
  
Exemplos: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
### <a name="components-shared-across-minor-versions"></a>Componentes compartilhados em versões secundárias

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As versões que têm os mesmos componentes compartilhados de versão principal.secundária.
  
Exemplo: Arquivos de suporte à Instalação.
  
### <a name="components-specific-to-an-instance-of-ssnoversion"></a>Componentes específicos de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Alguns componentes ou serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são específicos de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles também são conhecidos como capazes de reconhecimento de instância. Eles compartilham a mesma versão que a instância que os hospeda e são usados exclusivamente para aquela instância.
  
Exemplos: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### <a name="components-that-are-independent-of-the-ssnoversion-versions"></a>Componentes que são independentes das versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Alguns componentes são instalados durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas são independentes das versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles podem ser compartilhados por versões principais ou por todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

Exemplos: Microsoft Sync Framework, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
Para obter mais informações sobre a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, veja [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md). Para obter mais informações sobre como desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, veja [Desinstalar uma instância existente do SQL Server &#40;Instalação&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## <a name="using-ssnoversion-side-by-side-with-previous-versions-of-ssnoversion"></a>Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lado a lado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador que já está executando instâncias de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se já existir uma instância padrão no computador, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser instalado como uma instância nomeada.  

A tabela a seguir mostra o suporte lado a lado para cada versão do SQL Server nas versões comumente suportadas do Windows com as versões necessárias do .NET instaladas:

| Instância existente | Suporte lado a lado| 
|-------------------|----------------------------|
| SQL Server 2019 | SQL Server 2008 até SQL Server 2017| 
| Microsoft SQL Server 2017 | SQL Server 2008 até SQL Server 2016| 
| SQL Server 2016 | SQL Server 2008 até SQL Server 2014| 

Para obter mais informações, confira [Usar o SQL Server no Windows 8 e posteriores](https://support.microsoft.com/help/2681562/using-sql-server-in-windows-8-and-later-versions-of-windows-operating). 

  
> [!CAUTION]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O SysPrep não dá suporte à instalação lado a lado de instâncias preparadas do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo computador. Por exemplo, você não pode preparar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] lado a lado com uma instância preparada do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. No entanto, você pode instalar diversas instâncias preparadas da mesma versão principal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lado a lado no mesmo computador. Para obter mais informações, consulte [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>
> O SQL Server 2016 e posteriores não podem ser instalados lado a lado com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador que executa o Windows Server 2008 R2 Server Core SP1. Para obter mais informações sobre instalações Server Core, veja [Instalar o SQL Server 2016 no Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  


## <a name="preventing-ip-address-conflicts"></a>Impedindo conflitos de endereço IP

Quando uma Instância de Cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalada lado a lado com uma instância autônoma do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], procure evitar conflitos de número de porta TCP nos endereços IP. Conflitos normalmente ocorrem quando duas instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são ambas configuradas para usar a porta TCP padrão (1433). Para evitar conflitos, configure uma instância para usar uma porta fixa não padrão. A configuração de uma porta fixa é normalmente mais fácil na instância autônoma. A configuração do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar portas diferentes impedirá um conflito inesperado do Endereço IP/porta TCP que bloqueie uma inicialização de instância quando uma Instância de Cluster de Failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhar no nó em espera.
  
## <a name="see-also"></a>Consulte Também

* [Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
* [Instalar o SQL Server por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
* [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)
* [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
* [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
* [Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
* [Compatibilidade com versões anteriores_excluída](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)