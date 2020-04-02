---
title: 'SQL Server 2019: Requisitos de software e de hardware'
description: Uma lista de requisitos de hardware, de software e de sistema operacional para instalar e executar o SQL Server 2019.
ms.custom: sqlfreshmay19
ms.date: 02/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4dce96a698b9d4c84adbfdafdfbb7ac9056aac05
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79428167"
---
# <a name="sql-server-2019-hardware-and-software-requirements"></a>SQL Server 2019: Requisitos de hardware e software
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O artigo lista os requisitos mínimos de hardware e software para instalação e execução do SQL Server 2019 no sistema operacional Windows.

Para obter os requisitos de hardware e software para outras versões do SQL Server, confira:
- [SQL Server 2016 e 2017](hardware-and-software-requirements-for-installing-sql-server.md)
- [SQL Server em Linux](../../linux/sql-server-linux-setup.md#system)
- [Cluster de Big Data](../../big-data-cluster/deployment-guidance.md)

##  <a name="hardware-requirements"></a><a name="pmosr"></a> Requisitos de hardware  
 Os requisitos de memória e processador a seguir aplicam-se a todas as edições do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Disco rígido|O[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requer no mínimo 6 GB de espaço disponível no disco rígido.<br/><br/> Os requisitos de espaço em disco variam de acordo com os componentes do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] instalados. Para obter mais informações, consulte [Requisitos de espaço em disco rígido](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) posteriormente neste artigo. Para obter mais informações sobre tipos de armazenamento de arquivos de dados com suporte, consulte [Tipos de armazenamento para arquivos de dados](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).|  
|Monitoramento|O[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requer um monitor com resolução Super-VGA (800 x 600) ou superior.|  
|Internet|A funcionalidade de Internet requer acesso à Internet (a cobrança de taxas poderá ser aplicável).|  
|Memória \*|**Mínimo:**<br/><br/> Edições Express: 512 MB<br/><br/> Todas as outras edições: 1 GB<br/><br/> **Recomendado:**<br/><br/> Edições Express: 1 GB<br/><br/> Todas as outras edições: Pelo menos 4 GB e deve ser aumentado à medida que o tamanho do banco de dados aumenta para garantir um ótimo desempenho.|  
|Velocidade do processador|**Mínimo:** processador x64: 1,4 GHz<br/><br/> **Recomendado:** 2,0 GHz ou mais rápido|  
|Tipo de processador|Processador x64: AMD Opteron, AMD Athlon 64, Intel Xeon com suporte Intel EM64T, Intel Pentium IV com suporte EM64T|  
  
> [!NOTE]  
> A instalação do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] tem suporte apenas em processadores x64. Ela não tem mais suporte com processadores x86.  
  
 \* A memória mínima exigida para instalar o componente do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] no [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) é de 2 GB de RAM, diferente do requisito mínimo de memória do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]. Para obter informações sobre como instalar o DQS, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  


##  <a name="software-requirements"></a><a name="hwswr"></a> Requisitos de software  

Os seguintes requisitos se aplicam a todas as instalações:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Sistema operacional|Windows 10 TH1 1507 ou superior<br/><br>Windows Server 2016 ou superior<br/><br/>
|.NET Framework|Os sistemas operacionais mínimos incluem o .NET Framework no mínimo.|  
|Software de rede|Os sistemas operacionais com suporte para [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] têm software de rede interno. As instâncias nomeadas e padrão de uma instalação autônoma são compatíveis com os seguintes protocolos de rede: Memória compartilhada, Pipes nomeados e TCP/IP.<br/><br/> |  

A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala os seguintes componentes de software necessários ao produto:  
  
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client    
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arquivos de suporte à instalação  


> [!IMPORTANT]
> Há requisitos adicionais de hardware e software para o recurso PolyBase. Para obter mais informações, consulte [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  

##  <a name="operating-system-support"></a><a name="TOP_Principal"></a> Suporte do sistema operacional 

A tabela a seguir mostra quais edições do SQL Server 2019 são compatíveis com quais versões do Windows:  
  

| Edição do SQL Server:               | Enterprise | Desenvolvedor | Standard | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    Sim     |    Sim    |    Sim   | Sim |   Sim   |
| Windows Server 2019 Standard      |    Sim     |    Sim    |    Sim   | Sim |   Sim   |
| Windows Server 2019 Essentials    |    Sim     |    Sim    |    Sim   | Sim |   Sim   |
| Windows Server 2016 Datacenter    |    Sim     |    Sim    |    Sim   | Sim |   Sim   |
| Windows Server 2016 Standard      |    Sim     |    Sim    |    Sim   | Sim |   Sim   |
| Windows Server 2016 Essentials    |    Sim     |    Sim    |    Sim   | Sim |   Sim   |
| Windows 10 Enterprise             |    Não      |    Sim    |    Sim   | Não  |   Sim   |
| Windows 10 Professional           |    Não      |    Sim    |    Sim   | Não  |   Sim   |
| Windows 10 Home                   |    Não      |    Sim    |    Sim   | Não  |   Sim   |
| &nbsp; | &nbsp; |


### <a name="server-core-support"></a>Suporte do Server Core

A instalação do SQL Server 2019 no modo Server Core é compatível com as seguintes edições do Windows Server:

|                              |
| :------------------------  |
| Windows Server 2019 Core | 
| Windows Server 2016 Core |
| &nbsp; | 

Para obter mais informações sobre a instalação do SQL Server no Server Core, confira [Instalar o SQL Server no Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md). 


##  <a name="cross-language-support"></a><a name="CrossLanguageSupport"></a> Suporte em qualquer idioma  
 Para obter mais informações sobre o suporte em vários idiomas e as considerações sobre a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em idiomas localizados, consulte [Versões de idiomas locais no SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
##  <a name="disk-space-requirements"></a><a name="HardDiskSpace"></a> Requisitos de espaço em disco  
 Durante a instalação do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)], o Windows Installer cria arquivos temporários na unidade do sistema. Antes de executar a Instalação para instalar ou atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se você tem pelo menos 6,0 GB de espaço em disco disponível na unidade do sistema para esses arquivos. Esse requisito é aplicado mesmo se você instalar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma unidade não padrão.  
  
 Os requisitos reais de espaço em disco dependem da configuração do seu sistema e dos recursos que decidir instalar. A tabela a seguir fornece os requisitos de espaço em disco para componentes do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] .  
  
|**Recurso**|**Requisito de espaço em disco**|  
|-----------------|--------------------------------|  
|O[!INCLUDE[ssDE](../../includes/ssde-md.md)] e arquivos de dados, Replicação, Pesquisa de Texto Completo e Data Quality Services|1\.480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como acima) com os Serviços de R (no banco de dados)|2\.744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como acima) com o Serviço de Consulta PolyBase para Dados Externos|4\.194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e arquivos de dados|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (Autônomo)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – SharePoint|1\.203 MB|  
|Suplemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|Conectividade das ferramentas de cliente|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|Componentes cliente (exceto os componentes dos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as ferramentas do Integration Services)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|Componentes dos Manuais Online do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exibir e gerenciar o conteúdo da ajuda*|27 MB|  
|Todos os recursos|8\.030 MB|  
  
 *O requisito de espaço em disco para o conteúdo dos Manuais Online baixado é de 200 MB.  
  
##  <a name="storage-types-for-data-files"></a><a name="StorageTypes"></a> Tipos de armazenamento de arquivos de dados  
 Os tipos de armazenamento de arquivos de dados com suporte são:  
  
- Disco local 
    - O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualmente dá suporte a unidades de disco que têm tamanhos de setor nativo padrão de 512 bytes e 4 KB.  Discos rígidos com tamanhos de setor maiores que 4 KB podem causar erros ao tentar armazenar arquivos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neles.  Veja [Limites de suporte ao tamanho de setor do disco rígido no SQL Server](https://support.microsoft.com/kb/926930) para saber mais sobre o suporte ao tamanho de setor do disco rígido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 
    - A instalação de cluster de failover do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] só dá suporte a Disco Local para a instalação de arquivos tempdb. Verifique se o caminho especificado para os dados tempdb e os arquivos de log são válidos em todos os nós de cluster. Durante o failover, se os diretórios tempdb não estiverem disponíveis no nó do destino de failover, o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não ficará online.
- Armazenamento compartilhado  
- [S2D \(Espaços de Armazenamento Diretos\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
- Compartilhamento de arquivos SMB  
    - O armazenamento SMB não tem suporte para arquivos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em instalações autônomas ou clusterizadas. Em vez disso, use o armazenamento de conexão direta, uma rede de área de armazenamento ou o S2D. 
    - O armazenamento SMB pode ser hospedado por um servidor de arquivos do Windows ou por um dispositivo de armazenamento SMB de terceiros. Se o servidor de arquivos do Windows for usado, sua versão deve ser 2008 ou posterior. Para obter mais informações sobre como instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um compartilhamento de arquivos SMB como uma opção de armazenamento, consulte [Instalar o SQL Server com o compartilhamento de arquivos SMB como uma opção de armazenamento](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="installing-ssnoversion-on-a-domain-controller"></a><a name="DC_support"></a> Instalando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio  
 Por motivos de segurança, é recomendável não instalar o [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] em um controlador de domínio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueará a instalação em um computador que seja um controlador de domínio, mas as seguintes limitações se aplicam:  
  
- Você não pode executar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio sob uma conta de serviço local.    
- Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado em um computador, você não poderá alterar o computador de um membro do domínio para um controlador de domínio. Você deve desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de alterar o computador host para um controlador de domínio.    
- Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado em um computador, você não poderá alterar o computador de um controlador de domínio para um membro do domínio. Você deve desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de alterar o computador host para um membro do domínio.   
- Não há suporte às instâncias de cluster de failover do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que os nós de agrupamento sejam controladores de domínio.   
- Não há suporte ao[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio somente leitura. A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode criar grupos de segurança ou provisionar contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio somente leitura. Nesse cenário, haverá falha na Instalação. 
- Não há suporte para a instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente no qual apenas um controlador de domínio somente leitura é acessível. 
  
## <a name="installation-media"></a>Mídia de instalação

Você pode obter a mídia de instalação relevante nos seguintes locais: 
  
- [Centro de avaliação do SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019)
- [Atualizações cumulativas mais recentes](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

Como alternativa, você pode criar uma [máquina virtual do Azure já em execução SQL Server](/azure/virtual-machines/windows/sql/quickstart-sql-vm-create-portal), embora o SQL Server em uma máquina virtual seja mais lento do que a execução nativa devido à sobrecarga da virtualização.


## <a name="next-steps"></a>Próximas etapas

Depois de examinar os requisitos de hardware e software para a instalação do SQL Server, você pode começar a [Planejar uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) ou examinar as [Considerações de segurança para o SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).


