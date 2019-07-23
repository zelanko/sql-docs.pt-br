---
title: Notas de versão do SQL Server 2017 no Linux
description: Este artigo contém as notas de versão e os recursos com suporte para o SQL Server 2017 em execução no Linux. As notas de versão são incluídas para a versão mais recente e várias versões anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 5b6fce0bdde7e320eea0371125a61627652de80d
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388405"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de versão do SQL Server 2017 no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As notas de versão a seguir [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] se aplicam ao em execução no Linux. Este artigo é dividido em seções para cada versão. A versão de GA tem suporte detalhado e problemas conhecidos listados. Cada atualização cumulativa (CU) ou GDR (versão de distribuição geral) tem um link para um artigo de suporte que descreve as CU alterações, bem como links para os downloads de pacote do Linux.

> [!TIP]
> Essas notas de versão são especificamente [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] para versões. Para obter mais informações sobre o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]novo, consulte [notas de versão para o SQL Server 2019 Preview no Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Plataformas com suporte

| Plataforma | Sistema de arquivos | Guia de Instalação |
|-----|-----|-----|
| Red Hat Enterprise Linux o servidor 7,3, 7,4, 7,5 ou 7,6 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do Docker 1.8 + no Windows, Mac ou Linux | N/D | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais informações, examine os requisitos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [sistema](sql-server-linux-setup.md#system) do no Linux. Para obter a política de suporte [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]mais recente para o, consulte a [política de suporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Ferramentas

A maioria das ferramentas de cliente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] existentes que visam [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser direcionada diretamente em execução no Linux. Algumas ferramentas podem ter um requisito de versão específico para funcionar bem com o Linux. Para obter uma lista completa [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de ferramentas, consulte [ferramentas e utilitários SQL para SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Histórico de lançamentos

A tabela a seguir lista o histórico de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]lançamento do.

| Versão               | Version       | Data de liberação |
|-----------------------|---------------|--------------|
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
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
| [3º](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a>Como instalar atualizações

Se você tiver configurado o repositório cu (**MSSQL-Server-2017**), obterá a cu mais recente dos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacotes ao executar novas instalações. O cu Repository é o padrão para todos os artigos de instalação [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de pacotes do no Linux. Se você tiver configurado o repositório GDR (**MSSQL-Server-2017-GDR**), você só obterá atualizações de segurança críticas lançadas desde a GA. Se você precisar de atualizações do contêiner do Docker CU ou GDR, consulte imagens oficiais para [Microsoft SQL Server em Linux para o mecanismo do Docker](https://hub.docker.com/r/microsoft/mssql-server). Para obter mais informações sobre a configuração do repositório, consulte [configurar repositórios para SQL Server em Linux](sql-server-linux-change-repo.md).

Se você estiver atualizando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacotes existentes, execute o comando de atualização apropriado para cada pacote para obter o cu mais recente. Para obter instruções de atualização específicas para cada pacote, consulte os seguintes guias de instalação:

- [Instalar SQL Server pacote](sql-server-linux-setup.md#upgrade)
- [Instalar pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a>CU15 (maio de 2019)

Esta é a versão da atualização cumulativa 15 (CU15) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3162.1. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3162.1-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3162.1-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3162.1-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a>CU14 (mar 2019)

Esta é a versão da atualização cumulativa 14 (CU14) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3076.1. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3076.1-2 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3076.1-2 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3076.1-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a>CU13 (DEC 2018)

Esta é a versão de atualização cumulativa 13 (CU13) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3048.4. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3048.4-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3048.4-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3048.4-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a>CU12 (outubro de 2018)

Esta é a versão da atualização cumulativa 12 (CU12) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3045.24. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3045.24-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3045.24-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3045.24-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a>CU11 (setembro de 2018)

Esta é a versão da atualização cumulativa 11 (CU11) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3038.14. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3038.14-2 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3038.14-2 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3038.14-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a>CU10 (agosto de 2018)

Esta é a versão de atualização cumulativa 10 (CU10) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3037.1. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3037.1-2 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3037.1-2 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3037.1-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a>CU9-GDR2 (agosto de 2018)

Esta é uma atualização de segurança que também inclui a CU (CU9) lançada anteriormente [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]para o. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3035.2. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3035.2-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Pacote de RPM do SLES | 14.0.3035.2-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3035.2-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a>GDR2 (agosto de 2018)

Esta é uma atualização de segurança que inclui apenas as correções de segurança GDR2 (e [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]GDR1) para o.  A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.2002.14. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.2002.14-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.2002.14-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.2002.14-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a>CU9 (julho de 2018)

Esta é a versão da atualização cumulativa 9 (CU9) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3030.27. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3030.27-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3030.27-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3030.27-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a>CU8 (Jun 2018)

Esta é a versão da atualização cumulativa 8 (CU8) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3029.16. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3029.16-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3029.16-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3029.16-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a>CU7 (maio de 2018)

Esta é a versão da atualização cumulativa 7 (CU7) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3026.27. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3026.27-2 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3026.27-2 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3026.27-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a>CU6 (abril de 2018)

Esta é a versão da atualização cumulativa 6 (CU6) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3025.34. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3025.34-3 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3025.34-3 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3025.34-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a>CU5 (mar 2018)

Esta é a versão de atualização cumulativa 5 (CU5) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3023.8. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643)consulte.

### <a name="known-upgrade-issue"></a>Problema de atualização conhecido

Quando você atualiza de uma versão anterior para CU5, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode falhar ao iniciar com o seguinte erro:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para resolver esse erro, habilite SQL Server Agent e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reinicie com os seguintes comandos:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3023.8-5 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3023.8-5 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3023.8-5 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a>CU4 (fevereiro de 2018)

Esta é a versão da atualização cumulativa 4 (CU4) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3022.28. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> A partir de CU4, o SQL Server Agent não é mais instalado como um pacote separado. Ele é instalado com o pacote do mecanismo e deve ser habilitado para usar o.

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3022.28-2 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3022.28-2 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3022.28-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a>GDR1 (Jan 2018)

Esta é uma atualização de segurança que inclui apenas as correções de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]segurança GDR1 para o. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.2000.63. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.2000.63-3 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.2000.63-3 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.2000.63-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a>CU3 (Jan 2018)

Esta é a versão da atualização cumulativa 3 (CU3) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3015.40. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3015.40-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3015.40-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3015.40-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Pacote SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a>CU2 (novembro de 2017)

Esta é a versão da atualização cumulativa 2 (CU2) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3008.27. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3008.27-1 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3008.27-1 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3008.27-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Pacote SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a>CU1 (outubro de 2017)

Esta é a versão de atualização cumulativa 1 (CU1) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.3006.16. Para obter informações sobre as correções e melhorias nesta versão, [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)consulte.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.3006.16-3 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.3006.16-3 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.3006.16-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Pacote SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (outubro de 2017)

Esta é a versão de disponibilidade geral (GA) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]do. A [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versão desta versão é 14.0.1000.169.

### <a name="package-details"></a>Detalhes do pacote

Os detalhes do pacote e os locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se usar as etapas nos seguintes guias de instalação:

- [Instalar SQL Server pacote](sql-server-linux-setup.md)
- [Instalar pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Agent pacote](sql-server-linux-setup-sql-agent.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote do Red Hat RPM | 14.0.1000.169-2 | [Pacote de RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote de RPM do SLES | 14.0.1000.169-2 | [MSSQL-pacote de RPM do mecanismo de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de alta disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Pacote Ubuntu 16, 4 Debian | 14.0.1000.169-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Pacote SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a>Recursos sem suporte & serviços

Os seguintes recursos e serviços não estão disponíveis no Linux no momento da versão GA. O suporte desses recursos será habilitado cada vez mais ao longo do tempo.

| Área | Recurso ou serviço sem suporte |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação transacional |
| &nbsp; | Replicação de mesclagem |
| &nbsp; | Captura de dados de alterações (consulte SQL Server Agent) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | Consulta distribuída com conexões de terceiros |
| &nbsp; | Servidores vinculados a fontes de dados diferentes de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Procedimentos armazenados estendidos do sistema (XP_CMDSHELL, etc.) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Assemblies CLR com o conjunto de permissões EXTERNAL_ACCESS ou Unsafe |
| &nbsp; | Buffer Pool Extension |
| **SQL Server Agent** |  Subsistemas CmdExec, PowerShell, leitor de fila, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de Leitor de Log |
| &nbsp; | Change Data Capture (CDC) |
| &nbsp; | Backup Gerenciado |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Gerenciamento Extensível de Chaves |
| &nbsp; | Autenticação do AD para servidores vinculados | 
| &nbsp; | Autenticação do AD para grupos de disponibilidade (AGs) | 
| &nbsp; | ferramentas de anúncios de terceiros (Centrify, Vintela, PowerBroker) | 
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Coordenador de Transações Distribuídas (DTC) |

## <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem problemas conhecidos com a versão GA (disponibilidade geral) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] do no Linux.

#### <a name="general"></a>Geral

- O comprimento do nome de host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] onde o é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: Altere o nome em/etc/hostname para algo de 15 caracteres de comprimento ou menor.

- Definir manualmente a hora do sistema [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para trás no tempo causará a interrupção da atualização da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]hora interna do sistema no.

    - **Resolução**: Reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Há suporte apenas para instalações de instância única.

    - **Resolução**: Se você quiser ter mais de uma instância em um determinado host, considere usar VMs ou contêineres do Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Configuration Manager não pode se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conectar ao no Linux.

- O idioma padrão do logon **SA** é o inglês.

    - **Resolução**: Altere o idioma do logon **SA** com a instrução **ALTER LOGIN** .

#### <a name="databases"></a>Bancos de dados

- O banco de dados mestre não pode ser movido com o utilitário MSSQL-conf. Outros bancos de dados do sistema podem ser movidos com MSSQL-conf.

- Ao restaurar um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] qual foi feito backup no Windows, você deve usar a cláusula **with move** na instrução Transact-SQL.

- Não há suporte para transações distribuídas que exigem o serviço Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] coordenador de transações distribuídas em execução no Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] servidores vinculados, há suporte a menos que envolvam o DTC. Para obter mais informações, consulte as [transações distribuídas que exigem o serviço Microsoft coordenador de transações distribuídas não têm suporte no SQL Server em execução no Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Determinados algoritmos (conjuntos de codificação) para TLS (segurança de camada de transporte) não [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] funcionam corretamente com o no Linux. Isso resulta em falhas de conexão ao tentar se conectar a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], bem como problemas de estabelecimento de conexões entre réplicas em grupos de alta disponibilidade.

   - **Resolução**: Modifique o script de configuração **MSSQL. conf** para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para desabilitar conjuntos de codificação problemáticos, fazendo o seguinte:

      1. Adicione o seguinte a/var/opt/MSSQL/MSSQL.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o comando a seguir.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]bancos de dados no Windows que usam OLTP na memória não podem ser restaurados [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] no Linux. Para restaurar um [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] banco de dados que usa o OLTP na memória, primeiro atualize os bancos de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] dados [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] para ou no Windows antes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] movê-los para o no Linux por meio de backup/restauração ou desanexar/anexar.

- A permissão de usuário **administrar operações em massa** não tem suporte no Linux no momento.

#### <a name="networking"></a>Rede

Os recursos que envolvem conexões TCP de saída do processo sqlservr, como servidores vinculados ou grupos de disponibilidade, podem não funcionar se ambas as condições a seguir forem atendidas:

1. O servidor de destino é especificado como um nome de host e não um endereço IP.

1. A instância de origem tem IPv6 desabilitado no kernel. Para verificar se o sistema tem o IPv6 habilitado no kernel, todos os testes a seguir devem passar:

   - `cat /proc/cmdline`imprimirá o cmdline de inicialização do kernel atual. A saída não deve conter `ipv6.disable=1`.
   - O diretório/proc/sys/net/IPv6/deve existir.
   - Um programa C que chama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` deve ter êxito-o syscall deve retornar um FD! =-1 e não falhar com EAFNOSUPPORT.

O erro exato depende do recurso. Para servidores vinculados, isso se manifesta como um erro de tempo limite de logon. Para grupos de disponibilidade, `ALTER AVAILABILITY GROUP JOIN` o DDL no secundário falhará após 5 minutos com um erro de tempo limite de configuração de download.

Para contornar esse problema, siga um destes procedimentos:

1. Use IPs em vez de nomes de host para especificar o destino da conexão TCP.

1. Habilite o IPv6 no kernel removendo `ipv6.disable=1` da inicialização cmdline. A maneira de fazer isso depende da distribuição do Linux e do carregador de pacarregado, como o grub. Se você quiser que o IPv6 seja desabilitado, ainda poderá desabilitá-lo `net.ipv6.conf.all.disable_ipv6 = 1` Configurando `sysctl` na configuração `/etc/sysctl.conf`(por exemplo,). Isso ainda impedirá que o adaptador de rede do sistema receba um endereço IPv6, mas permitirá que os recursos sqlservr funcionem.

#### <a name="network-file-system-nfs"></a>NFS (sistema de arquivos de rede)
Se você usar compartilhamentos remotos **NFS (Network File System)** em produção, observe os seguintes requisitos de suporte:

- Use o NFS versão **4,2 ou superior**. As versões mais antigas do NFS não dão suporte aos recursos necessários, como fallocate e criação de arquivos esparsos, comuns aos sistemas de arquivos modernos.
- Localize somente os diretórios **/var/opt/MSSQL** na montagem NFS. Não há suporte para outros arquivos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como os binários do sistema.
- Verifique se os clientes NFS usam a opção ' NOLOCK ' ao montar o compartilhamento remoto.

#### <a name="localization"></a>Localização

- Se sua localidade não for inglês (en_US) durante a instalação, você deverá usar a codificação UTF-8 em sua sessão/terminal Bash. Se você usar a codificação ASCII, você poderá ver um erro semelhante ao seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se você não puder usar a codificação UTF-8, execute a instalação usando a variável de ambiente MSSQL_LCID para especificar sua escolha de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Ao executar a instalação do MSSQL-conf e executar uma instalação diferente do inglês [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]do, caracteres estendidos incorretos são exibidos após o texto localizado, "Configurando SQL Server...". Ou, para instalações não baseadas em Latin, a sentença pode estar ausente completamente. A sentença ausente deve exibir a seguinte cadeia de caracteres localizada: "O PID de licenciamento foi processado com êxito. A nova edição é [\<name\> Edition] ". Essa cadeia de caracteres é saída apenas para fins informativos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a próxima atualização cumulativa resolverá isso para todos os idiomas. Isso não afeta a instalação bem-sucedida do de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forma alguma. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo

- Nem todos os filtros estão disponíveis nesta versão, incluindo filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar SQL Server pesquisa de texto completo no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- O pacote **MSSQL-Server-is** não tem suporte no SUSE nesta versão. Atualmente, ele tem suporte no Ubuntu e no Red Hat Enterprise Linux (RHEL).

- Com [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a atualização do Linux CTP 2,1 e posterior [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , os pacotes podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com os [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] drivers ODBC do e MySQL, mas também deve funcionar com qualquer driver ODBC Unicode que observa a especificação ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de conexão para se conectar aos dados ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte a postagem no [blog anunciando o suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Os recursos a seguir não têm suporte nesta versão quando você executa pacotes do SSIS no Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Banco de dados do catálogo
  - Execução de pacote agendado pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Scale Out
  - Feature Pack do Azure para SSIS
  - Suporte para Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para obter uma lista de componentes internos do SSIS que não têm suporte no momento ou que têm suporte com limitações, consulte [limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md#components).

Para obter mais informações sobre o SSIS no Linux, consulte os seguintes artigos:
-   [Postagem de blog anunciando o suporte do SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SSMS (SQL Server Management Studio)

As seguintes limitações se aplicam ao [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no Windows conectado ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o data warehouse de gerenciamento (mdw [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ) e o coletor de dados no. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]Os componentes da interface do usuário que têm a autenticação do Windows ou as opções do log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL. 

- O número de arquivos de log a serem retidos não pode ser modificado.

## <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes guias de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

Para obter respostas para perguntas frequentes, consulte as [perguntas frequentes SQL Server em Linux](sql-server-linux-faq.md).
