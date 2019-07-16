---
title: Notas de versão do SQL Server 2017 no Linux
description: Este artigo contém as notas de versão e recursos com suporte para SQL Server 2017 em execução no Linux. Notas de versão são incluídas para a versão mais recente e várias versões anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 3f59495ffe4bc58ec673e643b0d011a501c51ba9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896170"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de versão do SQL Server 2017 no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As notas de versão a seguir se aplicam a [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] em execução no Linux. Este artigo é dividido em seções para cada versão. A versão GA tem detalhadas a capacidade de suporte e problemas listados conhecidos. Cada atualização cumulativa (CU) ou a versão de distribuição geral (GDR) tem um link para um artigo de suporte que descrevem alterações CU, bem como links para downloads de pacotes Linux.

> [!TIP]
> Essas notas de versão são específicas para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] libera. Para obter mais informações sobre os novos [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], consulte [notas de versão para versão prévia de 2019 do SQL Server no Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Plataformas com suporte

| Plataforma | Sistema de arquivos | Guia de Instalação |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 ou 7.6 Server | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8 + no Windows, Mac ou Linux | N/D | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais informações, examine os [requisitos do sistema](sql-server-linux-setup.md#system) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. Para a política de suporte mais recente do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], consulte o [política de suporte técnico para o Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Ferramentas

Mais existente das ferramentas de cliente que se destinam [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] perfeitamente pode direcionar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em execução no Linux. Algumas ferramentas podem ter um requisito de versão específico para funcionar bem com o Linux. Para obter uma lista completa dos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ferramentas, consulte [SQL ferramentas e utilitários para o SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Histórico de lançamento

A tabela a seguir lista o histórico de lançamento para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].

| Versão               | Version       | Data de liberação |
|-----------------------|---------------|--------------|
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 25-03-2019   |
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12 a 18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a> Como instalar atualizações

Se você tiver configurado o repositório CU (**mssql-server-2017**), em seguida, você obterá o CU mais recente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] quando você executar novas instalações de pacotes. O repositório do CU é o padrão de todos os pacotes de artigos de instalação para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. Se você tiver configurado o repositório GDR (**mssql-server 2017 gdr**), você só receberá atualizações críticas de segurança lançadas desde GA. Se você precisar de contêiner do Docker CU ou atualizações GDR, consulte as imagens oficiais para [Microsoft SQL Server no Linux para o mecanismo do Docker](https://hub.docker.com/r/microsoft/mssql-server). Para obter mais informações sobre a configuração do repositório, consulte [configurar repositórios para o SQL Server no Linux](sql-server-linux-change-repo.md).

Se você estiver atualizando existente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacotes, execute o comando de atualização apropriado para cada pacote obter o CU mais recente. Para obter instruções de atualização específica para cada pacote, consulte os guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar o SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a> CU15 (maio de 2018)

Esta é a versão de 15 de atualização cumulativa (CU15) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3162.1. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/en-us/help/4498951 ](https://support.microsoft.com/en-us/help/4498951).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3162.1-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3162.1-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3162.1-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a> CU14 (março de 2018)

Esta é a versão 14 de atualização cumulativa (CU14) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3076.1. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4484710 ](https://support.microsoft.com/help/4484710).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3076.1-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3076.1-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3076.1-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a> CU13 (dezembro de 2018)

Esta é a versão de 13 de atualização cumulativa (CU13) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3048.4. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4466404 ](https://support.microsoft.com/help/4466404).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3048.4-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3048.4-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3048.4-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12 (outubro de 2018)

Esta é a versão de 12 de atualização cumulativa (CU12) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3045.24. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4464082 ](https://support.microsoft.com/help/4464082).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3045.24-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3045.24-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3045.24-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11 (setembro de 2018)

Esta é a versão de 11 de atualização cumulativa (CU11) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3038.14. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4462262 ](https://support.microsoft.com/help/4462262).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3038.14-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3038.14-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3038.14-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (agosto de 2018)

Esta é a versão de atualização cumulativa 10 (CU10) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3037.1. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4342123 ](https://support.microsoft.com/help/4342123).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3037.1-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3037.1-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3037.1-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9-GDR2 (agosto de 2018)

Esta é uma atualização de segurança que também inclui o CU lançado anteriormente (CU9) para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3035.2. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4293805 ](https://support.microsoft.com/help/4293805).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3035.2-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Pacote RPM SLES | 14.0.3035.2-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3035.2-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (agosto de 2018)

Esta é uma atualização de segurança que inclui somente as correções de segurança GDR2 (e GDR1) para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].  O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.2002.14. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4293803 ](https://support.microsoft.com/help/4293803).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.2002.14-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.2002.14-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.2002.14-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9 (julho de 2018)

Esta é a versão de atualização cumulativa 9 (CU9) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3030.27. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4341265 ](https://support.microsoft.com/help/4341265).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3030.27-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3030.27-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3030.27-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (junho de 2018)

Esta é a versão de atualização cumulativa 8 (CU8) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3029.16. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4338363 ](https://support.microsoft.com/help/4338363).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3029.16-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3029.16-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3029.16-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (maio de 2018)

Esta é a versão de atualização cumulativa 7 (CU7) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3026.27. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4229789 ](https://support.microsoft.com/help/4229789).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3026.27-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3026.27-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3026.27-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (abril de 2018)

Esta é a versão de atualização cumulativa 6 (CU6) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3025.34. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3025.34-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3025.34-3 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3025.34-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (março de 2018)

Esta é a versão de atualização cumulativa 5 (CU5) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3023.8. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643).

### <a name="known-upgrade-issue"></a>Problema de upgrade conhecido

Quando você atualiza de uma versão anterior para CU5, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode falhar ao iniciar com o seguinte erro:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para resolver esse erro, habilite o SQL Server Agent e reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com os seguintes comandos:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3023.8-5 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3023.8-5 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3023.8-5 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (fevereiro de 2018)

Esta é a versão de atualização cumulativa 4 (4) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3022.28. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4056498 ](https://support.microsoft.com/help/4056498).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

> [!NOTE]
> A partir de CU4, SQL Server Agent não está mais instalado como um pacote separado. Ele é instalado com o pacote de mecanismo e deve ser habilitado para usar.

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3022.28-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3022.28-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3022.28-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (de janeiro de 2018)

Esta é uma atualização de segurança que inclui somente as correções de segurança de GDR1 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.2000.63. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4057122 ](https://support.microsoft.com/help/4057122).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.2000.63-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.2000.63-3 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.2000.63-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3 (de janeiro de 2018)

Esta é a versão de atualização cumulativa 3 (CU3) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3015.40. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4052987 ](https://support.microsoft.com/help/4052987).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3015.40-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3015.40-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3015.40-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (novembro de 2017)

Esta é a versão de atualização cumulativa 2 (CU2) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3008.27. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3008.27-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3008.27-1 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3008.27-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (outubro de 2017)

Esta é a versão de atualização cumulativa 1 (CU1) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.3006.16. Para obter informações sobre as correções e aprimoramentos nesta versão, consulte [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes Debian e RPM com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3006.16-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3006.16-3 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3006.16-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> Disponibilidade geral (outubro de 2017)

Esta é a versão de GA (disponibilidade geral) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão para esta versão é 14.0.1000.169.

### <a name="package-details"></a>Detalhes do pacote

Detalhes do pacote e locais de download para os pacotes Debian e RPM são listados na tabela a seguir. Observe que não é necessário baixar esses pacotes diretamente se você usar as etapas nos seguintes guias de instalação:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.1000.169-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.1000.169-2 | [pacote de RPM do mecanismo de MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.1000.169-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Pacote de alta disponibilidade de Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> Serviços e recursos sem suporte

Os seguintes recursos e serviços não estão disponíveis no Linux no momento da versão GA. Suporte a esses recursos será habilitado cada vez mais ao longo do tempo.

| Área | Recurso sem suporte ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação transacional |
| &nbsp; | Replicação de mesclagem |
| &nbsp; | Change Data Capture (consulte SQL Server Agent) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | Consulta distribuída com conexões 3ª parte |
| &nbsp; | Servidores vinculados a fontes de dados diferente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Sistema (XP_CMDSHELL, etc.) de procedimentos armazenados estendido |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| &nbsp; | Buffer Pool Extension |
| **SQL Server Agent** |  Subsistemas: CmdExec, PowerShell, leitor de fila, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de Leitor de Log |
| &nbsp; | Change Data Capture (CDC) |
| &nbsp; | Backup Gerenciado |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Gerenciamento Extensível de Chaves |
| &nbsp; | Autenticação do AD para servidores vinculados | 
| &nbsp; | Autenticação do AD para grupos de disponibilidade (grupos de disponibilidade) | 
| &nbsp; | ferramentas de terceiros AD 3ª (Centrify, Vintela, Powerbroker) | 
| **serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Coordenador de transações distribuídas (DTC) |

## <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem problemas conhecidos com o lançamento da disponibilidade geral (GA) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] no Linux.

#### <a name="general"></a>Geral

- O comprimento do nome do host no qual [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é instalada precisa ser de 15 caracteres ou menos. 

    - **Resolução**: Altere o nome no /etc/hostname para algo 15 caracteres ou menos.

- Configurar manualmente a hora do sistema para trás no tempo fará com que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para parar de atualizar a hora do sistema interno dentro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

    - **Resolução**: Reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Há suporte para apenas a instalações de instância única.

    - **Resolução**: Se você quiser ter mais de uma instância em um determinado host, considere o uso de VMs ou contêineres do Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gerenciador de configuração não pode se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux.

- O idioma padrão do **sa** logon está em inglês.

    - **Resolução**: Alterar o idioma do **sa** login com as **ALTER LOGIN** instrução.

#### <a name="databases"></a>Bancos de dados

- O banco de dados mestre não pode ser movido com o utilitário mssql-conf. Outros bancos de dados do sistema podem ser movidos com mssql-conf.

- Ao restaurar um banco de dados que foi feito em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço de coordenador de transações distribuídas da Microsoft em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em execução no Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] servidores vinculados têm suporte, a menos que eles envolvem o DTC. Para obter mais informações, consulte [não há suporte para transações distribuídas exigir que o serviço de coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Determinados algoritmos (conjuntos de codificação) para segurança de camada de transporte (TLS) não funcionam corretamente com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. Isso resulta em falhas de conexão quando tentar se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], bem como problemas para estabelecer conexões entre réplicas em grupos de alta disponibilidade.

   - **Resolução**: Modificar a **mssql.conf** script de configuração para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para desabilitar conjuntos de codificação problemático, fazendo o seguinte:

      1. Adicione o seguinte ao /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reiniciar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o comando a seguir.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] bancos de dados no Windows que usam OLTP na memória não podem ser restaurados [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] no Linux. Para restaurar um [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] banco de dados que usa o OLTP na memória, primeiro atualize os bancos de dados [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] no Windows antes de movê-los para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux por meio de backup/restauração ou anexar/desanexar.

- Permissão de usuário **ADMINISTER BULK OPERATIONS** não tem suporte no Linux no momento.

#### <a name="networking"></a>Rede

Recursos que envolvem as conexões TCP de saída do processo do sqlservr, como servidores vinculados ou grupos de disponibilidade, podem não funcionar se as seguintes condições forem atendidas:

1. O servidor de destino é especificado como um nome de host e não um endereço IP.

1. A instância de origem tem IPv6 desabilitado no kernel. Para verificar se o seu sistema tem IPv6 habilitado no kernel, os seguintes testes devem passar:

   - `cat /proc/cmdline` imprimirá o cmdline boot do kernel atual. A saída não deve conter `ipv6.disable=1`.
   - O proc/sys/net/ipv6/diretório deve existir.
   - Um programa em C que chama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` deve ter sucesso – a syscall deve retornar um fd! = -1 e não uma falha com EAFNOSUPPORT.

O erro exato depende do recurso. Para servidores vinculados, isso se manifesta como um erro de tempo limite de logon. Para grupos de disponibilidade, o `ALTER AVAILABILITY GROUP JOIN` DDL no secundário falhará após 5 minutos com um erro de tempo limite de configuração de download.

Para contornar esse problema, siga um destes procedimentos:

1. Use IPs, em vez de nomes de host para especificar o destino da conexão de TCP.

1. Habilitar o IPv6 no kernel, removendo `ipv6.disable=1` de cmdline boot. A maneira de fazer isso depende da distribuição do Linux e o carregador de inicialização, como o grub. Se você quiser IPv6 a ser desabilitado, você ainda pode desabilitá-lo definindo `net.ipv6.conf.all.disable_ipv6 = 1` no `sysctl` configuração (por exemplo, `/etc/sysctl.conf`). Isso ainda será impedir o adaptador de rede do sistema de um endereço IPv6, mas permitir que o sqlservr recursos funcionem.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Se você usar **sistema de arquivos de rede (NFS)** compartilhamentos remotos em produção, observe os seguintes requisitos de suporte:

- Use a versão do NFS **4.2 ou versão posterior**. Versões mais antigas do NFS não suportam os recursos necessários, como criação de arquivo esparso, comuns aos sistemas de arquivos modernos e fallocate.
- Localize somente as **/var/opt/mssql** diretórios em que a montagem do NFS. Outros arquivos, como o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] binários do sistema, não têm suporte.
- Certifique-se de que os clientes NFS usem a opção 'nolock' ao montar o compartilhamento remoto.

#### <a name="localization"></a>Localização

- Se sua localidade não for inglês (en_us) durante a instalação, você deve usar a codificação UTF-8 em sua sessão/terminal bash. Se você usar a codificação ASCII, você poderá ver um erro semelhante ao seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se você não pode usar a codificação UTF-8, execute a instalação usando a variável de ambiente MSSQL_LCID para especificar sua preferência de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Ao executar a instalação do mssql-conf e executar uma instalação diferente do inglês do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], incorretos caracteres estendidos são exibidos após o texto localizado, "Configurando o SQL Server...". Ou, com base em instalações não latinos, a frase pode estar ausente completamente. A frase ausente deve exibir a seguinte cadeia de caracteres localizada: "O PID de licenciamento foi processado com êxito. A nova edição é [\<nome\> edition] ". Essa cadeia de caracteres é a saída para fins informativos e o próximo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atualização cumulativa resolver isso para todos os idiomas. Isso não afeta a instalação bem-sucedida do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de qualquer forma. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo

- Nem todos os filtros estão disponíveis com esta versão, incluindo filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- O **mssql-server-está** pacote não tem suporte no SUSE nesta versão. Atualmente, há suporte no Ubuntu e no Red Hat Enterprise Linux (RHEL).

- Com o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sobre a atualização do Linux CTP 2.1 e versões posteriores, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pacotes podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os drivers de ODBC do MySQL, mas também é esperada para funcionar com qualquer driver de ODBC Unicode que observa a especificação de ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de caracteres de conexão para se conectar aos dados ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte o [postagem do blog anunciando o suporte ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Os recursos a seguir não têm suporte nesta versão, quando você executa pacotes do SSIS no Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Banco de dados do catálogo
  - Execução de pacotes agendados pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Escalar horizontalmente
  - Azure Feature Pack para SSIS
  - Suporte de Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para obter uma lista de componentes SSIS internos que não têm suporte no momento ou que são compatíveis com as limitações, consulte [limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md#components).

Para obter mais informações sobre o SSIS no Linux, consulte os seguintes artigos:
-   [Anunciando de postagem de blog suporte do SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SSMS (SQL Server Management Studio)

As seguintes limitações se aplicam a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no Windows conectado ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux.

- Não há suporte para planos de manutenção.

- Gerenciamento MDW (Data Warehouse) e o coletor de dados de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] não têm suporte. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Componentes da interface do usuário com a autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- Número de arquivos de log a serem retidos não pode ser modificado.

## <a name="next-steps"></a>Próximas etapas

Para começar, consulte os inícios rápidos a seguir:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).
