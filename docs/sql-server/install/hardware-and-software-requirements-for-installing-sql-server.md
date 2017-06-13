---
title: "Requisitos de hardware e software para a instalação do SQL Server 2016 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
caps.latest.revision: 333
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 70bdaa29578874c6a795199347cb082606e14c5c
ms.openlocfilehash: 6aa732f1ab8633af453e6b12d45285bbc94233ad
ms.contentlocale: pt-br
ms.lasthandoff: 04/21/2017

---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>Requisitos de hardware e software para a instalação do SQL Server
  Este tópico lista os requisitos mínimos de hardware e software para a instalação e execução de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

 > Para conteúdo relacionado a versões anteriores do SQL Server, consulte [requisitos de Hardware e Software para instalar o SQL Server 2014](https://msdn.microsoft.com/library/ms143506(v=sql.120).aspx). 
  
 **Experimente:**  
  
-   Baixar o SQL Server do [**Centro de Avaliação**.](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
  
-    Criar uma Máquina Virtual com o [**SQL Server 2016**](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) já instalado.  
  
 **As seguintes considerações se aplicam a todas as edições:**  
  
-   Recomendamos executar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em computadores com os formatos de arquivo NTFS ou ReFS. Há suporte para a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um computador com o sistema de arquivos FAT32, mas ela não é recomendada, pois é menos segura do que o sistema de arquivos NTFS ou ReFS.  
  
-   A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueará instalações em unidades somente leitura, mapeadas ou compactadas.  
  
-   A instalação falhará se você iniciar a instalação por meio da Conexão de Área de Trabalho Remota com a mídia em um recurso local no cliente RDC. Para instalar remotamente, a mídia deve estar em um compartilhamento de rede ou local para a máquina virtual ou física. A mídia de instalação[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode estar em um compartilhamento de rede, uma unidade mapeada, uma unidade local ou ser apresentada como um arquivo ISO em uma máquina virtual.  
  
-   A instalação[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exige a instalação do .NET 4.6.1 como um pré-requisito. O .NET 4.6.1 será instalado automaticamente pela instalação quando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] for selecionado.  
  
-   A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala os seguintes componentes de software necessários ao produto:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arquivos de suporte à instalação  
  
-   Para saber os requisitos mínimos da versão para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em [!INCLUDE[win8srv](../../includes/win8srv-md.md)] ou em [!INCLUDE[win8](../../includes/win8-md.md)], consulte [Instalando o SQL Server no Windows Server 2012 ou no Windows 8](http://support.microsoft.com/kb/2681562) (http://support.microsoft.com/kb/2681562).  
  
 Este tópico contém as seguintes seções:  
  
-   [Requisitos de Hardware e Software](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#hwswr)  
  
-   [Requisitos de processador, de memória e do sistema operacional](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)  
  
-   [Suporte em qualquer idioma](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#CrossLanguageSupport)  
  
-   [Requisitos de espaço em disco rígido](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)  
  
-   [Tipos de armazenamento de arquivos de dados](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)  
  
-   [Instalando o SQL Server em um controlador de domínio](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#DC_support)  
  
##  <a name="hwswr"></a> Requisitos de Hardware e Software  
 Os seguintes requisitos se aplicam a todas as instalações:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|.NET Framework|O RC1[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e posteriores exigem o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 para o Mecanismo de Banco de Dados, Master Data Services ou Replicação. A instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 instala automaticamente o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Você também pode instalar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] manualmente por meio do [Microsoft .NET Framework 4.6 (Instalador da Web) para Windows](http://support.microsoft.com/kb/3045560).<br/><br/> Para obter mais informações, recomendações e diretrizes sobre o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6, consulte o [Guia de implantação do .NET Framework para desenvolvedores](http://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx).<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)], e [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] exigem o [KB2919355](http://support.microsoft.com/kb/2919355) antes de instalar o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.|  
|Software de rede|Os sistemas operacionais com suporte para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] têm software de rede interno. As instâncias nomeadas e padrão de uma instalação autônoma dão suporte aos seguintes protocolos de rede: memória compartilhada, pipes nomeados, TCP/IP e VIA.<br/><br/> Observação: não há suporte para memória compartilhada e VIA em clusters de failover.<br/><br/> Observe também que o protocolo VIA foi preterido. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> <br/><br/> Para obter mais informações sobre protocolos de rede e bibliotecas de rede, consulte [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md).|  
|Disco rígido|O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requer no mínimo 6 GB de espaço disponível no disco rígido.<br/><br/> Os requisitos de espaço em disco variam de acordo com os componentes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalados. Para obter mais informações, consulte [Requisitos de espaço em disco rígido](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) posteriormente neste tópico. Para obter mais informações sobre tipos de armazenamento de arquivos de dados com suporte, consulte [Tipos de armazenamento para arquivos de dados](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Unidade|É necessária uma unidade de DVD, conforme apropriado, para a instalação a partir de disco.|  
|Monitor|O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requer um monitor com resolução Super-VGA (800 x 600) ou superior.|  
|Internet|A funcionalidade de Internet requer acesso à Internet (a cobrança de taxas poderá ser aplicável).|  
  
 Observação: executar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma máquina virtual será mais lento que executar nativamente, devido à sobrecarga de virtualização.  
  
 Há requisitos adicionais de hardware e software para o recurso PolyBase. Para obter mais informações, consulte [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
##  <a name="pmosr"></a> Requisitos de processador, de memória e do sistema operacional  
 Os requisitos de memória e processador a seguir aplicam-se a todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Memória*|**Mínimo:**<br/><br/> Edições Express: 512 MB<br/><br/> Todas as outras edições: 1 GB<br/><br/> **Recomendado:**<br/><br/> Edições Express: 1 GB<br/><br/> Todas as outras edições: pelo menos 4 GB e deve ser aumentado à medida que o banco de dados cresce para garantir um ótimo desempenho.|  
|Velocidade do processador|**Mínimo:** processador x64: 1,4 GHz<br/><br/> **Recomendável:** : 2,0 GHz ou mais rápido|  
|Tipo de processador|Processador x64: AMD Opteron, AMD Athlon 64, Intel Xeon com suporte Intel EM64T, Intel Pentium IV com suporte EM64T|  
  
> [!NOTE]  
>  A instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tem suporte apenas em processadores x64. Ela não tem mais suporte com processadores x86.  
  
 *A memória mínima exigida para instalar o componente do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] no [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) é de 2 GB de RAM, diferente do requisito mínimo de memória do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obter informações sobre como instalar o DQS, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 **Suporte a WOW64:**  
  
 O WOW64 (Windows de 32 bits no Windows de 64 bits) é um recurso de edições de 64 bits do Windows que permite que aplicativos de 32 bits sejam executados nativamente no modo de 32 bits. Os aplicativos funcionam no modo de 32 bits mesmo que o sistema operacional subjacente esteja em execução em um sistema operacional de 64 bits. Não há suporte para o WOW64 em instalações do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . No entanto, as Ferramentas de Gerenciamento têm suporte no WOW64.  
  
 **Suporte do sistema operacional:**  
  
 As edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] são classificadas da seguinte maneira:  
  
-   [Edições Principais do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [Edições de Amplitude do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
> [!NOTE]  
>  Os recursos de Business Intelligence a seguir são exceções ao suporte do sistema operacional observado nesta seção e podem ser instalados no Windows Server 2008 R2 SP1 ou posterior:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – SharePoint  
  
-   Suplemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint  
  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>Recursos com suporte nos sistemas operacionais cliente de 32 bits  
 Sistemas operacionais cliente do Windows, por exemplo, Windows 10 e Windows 8.1, estão disponíveis como arquiteturas de 32 ou 64 bits.   Todos os recursos do SQL Server têm suporte em sistemas operacionais cliente de 64 bits. Em sistemas operacionais cliente de 32 bits com suporte, a Microsoft dá suporte aos seguintes recursos:  
  
-   Cliente Data Quality  
  
-   Conectividade das ferramentas de cliente  
  
-   Integration Services  
  
-   Compatibilidade das Ferramentas de Cliente com Versões Anteriores  
  
-   SDK de Ferramentas de cliente  
  
-   Componentes de documentação  
  
-   Componentes Distributed Replay  
  
-   Distributed Replay Controller  
  
-   Distributed Replay Client  
  
-   SDK de Conectividade de Cliente do SQL  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] e sistemas operacionais de servidor posteriores não estão disponíveis como arquiteturas de 32 bits. Todos os sistemas operacionais de servidor com suporte estão disponíveis somente em 64 bits. Todos os recursos têm suporte em sistemas operacionais de servidor de 64 bits.  
  
###  <a name="TOP_Principal"></a> Principal Editions of [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 A tabela a seguir mostra os requisitos de sistema operacional para as edições principais do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Edição do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Sistema operacional com suporte|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
###  <a name="TOP_Breadth"></a> Breadth Editions of [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 A tabela a seguir mostra os requisitos de sistema operacional para as edições de amplitude do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Edição do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Sistema operacional com suporte|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
  
##  <a name="CrossLanguageSupport"></a> Suporte em qualquer idioma  
 Para obter mais informações sobre o suporte em vários idiomas e as considerações sobre a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em idiomas localizados, consulte [Versões de idiomas locais no SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
##  <a name="HardDiskSpace"></a> Requisitos de espaço em disco rígido  
 Durante a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o Windows Installer cria arquivos temporários na unidade do sistema. Antes de executar a Instalação para instalar ou atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se você tem pelo menos 6,0 GB de espaço em disco disponível na unidade do sistema para esses arquivos. Esse requisito é aplicado mesmo se você instalar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma unidade não padrão.  
  
 Os requisitos reais de espaço em disco dependem da configuração do seu sistema e dos recursos que decidir instalar. A tabela a seguir fornece os requisitos de espaço em disco para componentes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|**Recurso**|**Requisito de espaço em disco**|  
|-----------------|--------------------------------|  
|O[!INCLUDE[ssDE](../../includes/ssde-md.md)] e arquivos de dados, Replicação, Pesquisa de Texto Completo e Data Quality Services|1.480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como acima) com os Serviços de R (no banco de dados)|2.744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como acima) com o Serviço de Consulta PolyBase para Dados Externos|4.194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e arquivos de dados|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (Autônomo)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – SharePoint|1.203 MB|  
|Suplemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|Conectividade das ferramentas de cliente|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|Componentes cliente (exceto os componentes dos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as ferramentas do Integration Services)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|Componentes dos Manuais Online do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exibir e gerenciar o conteúdo da ajuda*|27 MB|  
|Todos os recursos|8.030 MB|  
  
 *O requisito de espaço em disco para o conteúdo dos Manuais Online baixado é de 200 MB.  
  
##  <a name="StorageTypes"></a> Tipos de armazenamento de arquivos de dados  
 Os tipos de armazenamento de arquivos de dados com suporte são:  
  
-   Disco local  
  
-   Armazenamento compartilhado  

-   [S2D \(Espaços de Armazenamento Diretos\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)
  
-   Compartilhamento de arquivos SMB  
  
    > [!NOTE]  
    >  O armazenamento SMB não tem suporte para arquivos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em instalações autônomas ou clusterizadas. Em vez disso, use o armazenamento de conexão direta, uma rede de área de armazenamento ou o S2D.  
  
    > [!IMPORTANT]  
    >  O armazenamento SMB pode ser hospedado por um servidor de arquivos do Windows ou por um dispositivo de armazenamento SMB de terceiros. Se o servidor de arquivos do Windows for usado, sua versão deve ser 2008 ou posterior. Para obter mais informações sobre como instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um compartilhamento de arquivos SMB como uma opção de armazenamento, consulte [Install SQL Server with SMB Fileshare as a Storage Option](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
    > [!WARNING]  
    >  A instalação de cluster de failover do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] só dá suporte a Disco Local para a instalação de arquivos tempdb. Verifique se o caminho especificado para os dados tempdb e os arquivos de log são válidos em todos os nós de cluster. Durante o failover, se os diretórios tempdb não estiverem disponíveis no nó do destino de failover, o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não ficará online.  
  
##  <a name="DC_support"></a> Installing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] on a Domain Controller  
 Por motivos de segurança, é recomendável não instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um controlador de domínio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueará a instalação em um computador que seja um controlador de domínio, mas as seguintes limitações se aplicam:  
  
-   Você não pode executar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio sob uma conta de serviço local.  
  
-   Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado em um computador, você não poderá alterar o computador de um membro do domínio para um controlador de domínio. Você deve desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de alterar o computador host para um controlador de domínio.  
  
-   Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado em um computador, você não poderá alterar o computador de um controlador de domínio para um membro do domínio. Você deve desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de alterar o computador host para um membro do domínio.  
  
-   Não há suporte às instâncias de cluster de failover do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que os nós de agrupamento sejam controladores de domínio.  
  
- Não há suporte ao[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio somente leitura. A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode criar grupos de segurança ou provisionar contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio somente leitura. Nesse cenário, haverá falha na Instalação.  

- Não há suporte para a instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente no qual apenas um controlador de domínio somente leitura é acessível. 
  
## <a name="see-also"></a>Consulte também  
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Especificações do produto para SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
  
  

