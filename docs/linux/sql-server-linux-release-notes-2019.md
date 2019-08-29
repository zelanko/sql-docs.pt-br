---
title: Notas sobre a versão do SQL Server 2019 em Linux
description: Este artigo contém as notas sobre a versão e os recursos com suporte do SQL Server 2019 em execução no Linux. As notas sobre a versão aqui incluídas são para a versão mais recente, bem como para diversas versões anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: af3b6f82e3b76e2dd2b11403bccf4b3e0885912e
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890897"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>Notas sobre a versão do SQL Server 2019 em Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

As notas sobre a versão a seguir se aplicam ao SQL Server 2019 em execução no Linux. Este artigo está dividido em seções para cada versão. Cada versão tem um link para um artigo de suporte que descreve as alterações da CU, bem como links para os downloads dos pacotes do Linux.

> [!TIP]
> Para saber mais sobre os novos recursos do Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

## <a name="supported-platforms"></a>Plataformas compatíveis

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 ou 7.6 Server | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8+ no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais informações, examine os [requisitos do sistema](sql-server-linux-setup.md#system) para SQL Server em Linux. Para obter a política de suporte mais recente para o SQL Server 2017, confira a [Política de suporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Ferramentas

A maioria das ferramentas de cliente existentes que se destinam ao SQL Server pode se direcionar diretamente ao SQL Server em execução no Linux. Algumas ferramentas podem ter um requisito de versão específico para funcionar bem com o Linux. Para obter uma lista completa de ferramentas do SQL Server, confira [Ferramentas e utilitários de SQL para SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Histórico de versões

A tabela a seguir lista o histórico de lançamento da versão prévia do SQL Server 2019.

| Versão                   | Versão       | Data de liberação |
|---------------------------|---------------|--------------|
| [Versão Release Candidate](#rc)  | 15.0.1900.25  | 2019-8-21    |
| [CTP 3.2](#CTP32)         | 15.0.1800.32  | 24/7/2019    |
| [CTP 3.1](#CTP31)         | 15.0.1700.37  | 26/6/2019    |
| [CTP 3.0](#CTP30)         | 15.0.1600.8   | 22/5/2019    |
| [CTP 2.5](#CTP25)         | 15.0.1500.28  | 24/4/2019    |
| [CTP 2.4](#CTP24)         | 15.0.1400.75  | 27/3/2019    |
| [CTP 2.3](#CTP23)         | 15.0.1300.359 | 1/3/2019    |
| [CTP 2.2](#CTP22)         | 15.0.1200.24  | 11/12/2018   |
| [CTP 2.1](#CTP21)         | 15.0.1100.94  | 6/11/2018   |
| [CTP 2.0](#CTP20)         | 15.0.1000.34  | 24/9/2018   |

## <a id="cuinstall"></a> Como instalar atualizações

Se você configurou o repositório da versão prévia (**mssql-server-preview**), obterá os pacotes mais recentes de CTP do SQL Server ao executar novas instalações. Se você precisar de imagens de contêiner do Docker, vejas as imagens oficiais para [Microsoft SQL Server em Linux para Docker Engine](https://hub.docker.com/r/microsoft/mssql-server/). Para obter mais informações sobre a configuração do repositório, confira [Configurar repositórios para SQL Server em Linux](sql-server-linux-change-repo.md).

Se você estiver atualizando pacotes de SQL Server existentes, execute o comando de atualização adequado para cada pacote a fim de obter a CU mais recente. Para obter instruções de atualização específicas para cada pacote, confira os seguintes guias de instalação:

- [Instalar pacote do SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar pacote de Pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Instalar o suporte ao R e Python dos Serviços de Machine Learning da versão prévia do SQL Server 2019 no Linux](sql-server-linux-setup-machine-learning.md)
- [Instalar pacote do PolyBase](../relational-databases/polybase/polybase-linux-setup.md)
- [Habilitar o SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="rc"></a> Versão Release Candidate (agosto de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão Release Candidate. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1900.25-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1900.25-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1900.25-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a id="CTP32"></a> CTP 3.2 (julho de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 3.2. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1800.32-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1800.32-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1800.32-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1800.32-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1800.32-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1800.32-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1800.32-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1800.32-1_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1800.32-1_amd64.deb)|

## <a id="CTP31"></a> CTP 3.1 (junho de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 3.1. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1700.37-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1700.37-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1700.37-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0 (maio de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 3.0. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1600.8-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1600.8-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1600.8-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a id="CTP25"></a> CTP 2.5 (abril de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 2.5. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1500.28-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1500.28-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1500.28-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a id="CTP24"></a> CTP 2.4 (março de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 2.4. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1400.75-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1400.75-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1400.75-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a id="CTP23"></a> CTP 2.3 (fevereiro de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 2.3. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1300.359-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1300.359-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1300.359-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a id="CTP22"></a> CTP 2.2 (dezembro de 2018)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 2.2. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1200.24-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1200.24-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1200.24-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a id="msdtc"></a> Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a id="CTP21"></a> CTP 2.1 (novembro de 2018)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 2.1. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1100.94-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1100.94-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1100.94-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a name="microsoft-distributed-transaction-coordinator"></a>Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a id="CTP20"></a> CTP 2.0 (setembro de 2018)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão de CTP 2.0. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1000.34-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1000.34-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1000.34-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conhecidos

#### <a name="microsoft-distributed-transaction-coordinator"></a>Coordenador de Transações Distribuídas da Microsoft

Atualmente, o MSDTC requer que as transações sejam não autenticadas. Por exemplo, se você estiver usando um servidor vinculado do SQL Server no Windows para SQL Server em Linux ou usar um aplicativo cliente do Windows para iniciar uma transação distribuída em relação ao SQL Server em Linux, o MSDTC no servidor/cliente Windows deverá usar a opção "Nenhuma Autenticação Necessária".

## <a name="next-steps"></a>Próximas etapas

Para começar, confira os seguintes guias de início rápido:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md).
