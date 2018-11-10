---
title: Notas de versão para versão prévia de 2019 do SQL Server no Linux | Microsoft Docs
description: Este artigo contém as notas de versão e recursos com suporte para visualização de 2019 do SQL Server em execução no Linux. Notas de versão são incluídas para a versão mais recente e várias versões anteriores.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b22e52d68c1d2b10005e69e2e70c41e73c173dca
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269829"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>Notas de versão para versão prévia de 2019 do SQL Server no Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

As notas de versão a seguir se aplicam à visualização de 2019 do SQL Server em execução no Linux. Este artigo é dividido em seções para cada versão. Cada versão tem um link para um artigo de suporte que descrevem alterações CU, bem como links para downloads de pacotes Linux.

> [!TIP]
> Para saber sobre novos recursos de Linux do SQL Server 2019, consulte [o que há de novo no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sqllinux).

## <a name="supported-platforms"></a>Plataformas compatíveis

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 ou 7.4 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais informações, examine os [requisitos de sistema](sql-server-linux-setup.md#system) para o SQL Server no Linux. Para a política de suporte mais recente do SQL Server 2017, consulte o [política de suporte técnico para o Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Ferramentas

A maioria das ferramentas de cliente existentes que o SQL Server de destino diretamente pode direcionar o SQL Server em execução no Linux. Algumas ferramentas podem ter um requisito de versão específico para funcionar bem com o Linux. Para obter uma lista completa de ferramentas do SQL Server, consulte [SQL ferramentas e utilitários para o SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Histórico de lançamento

A tabela a seguir lista o histórico de versão de visualização do SQL Server 2019 que versões CTP.

| Versão               | Versão       | Data de liberação |
|-----------------------|---------------|--------------|
| [CTP 2.1](#CTP21)     | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)     | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> Como instalar atualizações

Se você tiver configurado o repositório de versão prévia (**mssql-server-visualização**), você receberá os pacotes mais recentes do CTP do SQL Server quando você executar novas instalações. Se você precisar de imagens de contêiner do Docker, consulte as imagens oficiais para [Microsoft SQL Server no Linux para o mecanismo do Docker](https://hub.docker.com/r/microsoft/mssql-server/). Para obter mais informações sobre a configuração do repositório, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

Se você estiver atualizando os pacotes existentes do SQL Server, execute o comando de atualização apropriado para cada pacote obter o CU mais recente. Para obter instruções de atualização específica para cada pacote, consulte os guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Instalar a visualização de 2019 do SQL Server R Services do Machine Learning e o suporte do Python no Linux](sql-server-linux-setup-machine-learning.md)
- [Habilitar o SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CTP21"></a> CTP 2.1 (novembro de 2018)

As seções a seguir fornecem os locais de pacote e problemas conhecidos para o CTP 2.1 versão. Para saber mais sobre os novos recursos para Linux no SQL Server 2019, consulte o [o que há de novo no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1100.94-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Pacote RPM SLES | 15.0.1100.94-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1100.94-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de extensibilidade de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de transações distribuídas da Microsoft

Atualmente, o MSDTC requer transações não autenticados. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para o SQL Server no Linux ou usa um aplicativo de cliente do Windows para iniciar uma transação distribuída no SQL Server no Linux, em seguida, MSDTC no servidor/cliente Windows é necessário para usar a opção "não Autenticação necessária".

## <a id="CTP20"></a> CTP 2.0 (setembro de 2018)

As seções a seguir fornecem os locais de pacote e problemas conhecidos do 2.0 CTP versão. Para saber mais sobre os novos recursos para Linux no SQL Server 2019, consulte o [o que há de novo no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1000.34-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Pacote RPM SLES | 15.0.1000.34-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1000.34-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de extensibilidade de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de transações distribuídas da Microsoft

Atualmente, o MSDTC requer transações não autenticados. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para o SQL Server no Linux ou usa um aplicativo de cliente do Windows para iniciar uma transação distribuída no SQL Server no Linux, em seguida, MSDTC no servidor/cliente Windows é necessário para usar a opção "não Autenticação necessária".

## <a name="next-steps"></a>Próximas etapas

Para começar, consulte os inícios rápidos a seguir:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).
