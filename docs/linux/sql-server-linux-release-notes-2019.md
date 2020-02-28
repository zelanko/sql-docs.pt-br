---
title: Notas sobre a versão do SQL Server 2019 em Linux
description: Este artigo contém as notas sobre a versão e os recursos com suporte do SQL Server 2019 em execução no Linux. As notas sobre a versão aqui incluídas são para a versão mais recente, bem como para diversas versões anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 95289a3c4ad263e2c3ef063e54984a4481cf6109
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77256769"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>Notas sobre a versão do SQL Server 2019 em Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

As notas sobre a versão a seguir se aplicam ao SQL Server 2019 em execução no Linux. Este artigo está dividido em seções para cada versão. Cada versão tem um link para um artigo de suporte que descreve as alterações da CU, bem como links para os downloads dos pacotes do Linux.

> [!TIP]
> Para saber mais sobre os novos recursos do Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

## <a name="supported-platforms"></a>Plataformas compatíveis

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5, 7.6 ou 8 Server | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2, SP3 ou SP4 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8+ no Windows, Mac ou Linux | N/D | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais informações, examine os [requisitos do sistema](sql-server-linux-setup.md#system) para SQL Server em Linux. Para obter a política de suporte mais recente para o SQL Server 2017, confira a [Política de suporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Ferramentas

A maioria das ferramentas de cliente existentes que se destinam ao SQL Server pode se direcionar diretamente ao SQL Server em execução no Linux. Algumas ferramentas podem ter um requisito de versão específico para funcionar bem com o Linux. Para obter uma lista completa de ferramentas do SQL Server, confira [Ferramentas e utilitários de SQL para SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Histórico de versões

A tabela a seguir lista o histórico de versões do SQL Server 2019.

| Versão                   | Versão       | Data de liberação |
|---------------------------|---------------|--------------|
| [CU2](#cu2)               | 15.0.4013.40  | 2020-02-13   |
| [CU1](#cu1)               | 15.0.4003.23  | 2020-01-07   |
| [GA](#ga)                 | 15.0.2000.5   | 2019-11-04   |
| [Versão Release Candidate](#rc)  | 15.0.1900.25  | 2019-08-21   |

## <a id="cuinstall"></a> Como instalar atualizações

Se tiver configurado o repositório da CU (mssql-server-2019), você obterá a CU mais recente dos pacotes do SQL Server quando executar novas instalações. Se você precisar de imagens de contêiner do Docker, confira as imagens oficiais para [Microsoft SQL Server em Linux para Docker Engine](https://hub.docker.com/r/microsoft/mssql-server/). Para obter mais informações sobre a configuração do repositório, confira [Configurar repositórios para SQL Server em Linux](sql-server-linux-change-repo.md).

Se você estiver atualizando pacotes de SQL Server existentes, execute o comando de atualização adequado para cada pacote a fim de obter a CU mais recente. Para obter instruções de atualização específicas para cada pacote, confira os seguintes guias de instalação:

- [Instalar pacote do SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar pacote de Pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Instalar o suporte ao R e Python dos Serviços de Machine Learning do SQL Server 2019 no Linux](sql-server-linux-setup-machine-learning.md)
- [Instalar pacote do PolyBase](../relational-databases/polybase/polybase-linux-setup.md)
- [Habilitar o SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="cu2"></a> CU2 (fevereiro de 2020)

Esta é a versão da CU2 (Atualização Cumulativa 2) do SQL Server 2019 (15.x). A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.4013.40. Para obter informações sobre as correções e aprimoramentos, confira <https://support.microsoft.com/help/4536075>

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> Da CU1 em diante, os links de instalação do pacote offline para Red Hat estão apontando para pacotes do RHEL 8. Se você estiver procurando pacotes do RHEL 7, consulte o caminho de download <https://packages.microsoft.com/rhel/7/mssql-server-2019/>

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.4013.40-8 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4013.40-8.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.4013.40-8 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4013.40-8.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4013.40-8.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.4013.40-8 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4013.40-8_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4013.40-8_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4013.40-8_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4013.40-8_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4013.40-8_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4013.40-8_amd64.deb)|

## <a id="cu1"></a> CU1 (janeiro de 2020)

Esta é a versão da CU1 (Atualização Cumulativa 1) do SQL Server 2019 (15.x). A versão do Mecanismo de Banco de Dados do SQL Server para essa versão é 15.0.4003.23. Para obter informações sobre as correções e aprimoramentos nesta versão, confira <https://support.microsoft.com/en-us/help/4527376>

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> Da CU1 em diante, os links de instalação do pacote offline para Red Hat estão apontando para pacotes do RHEL 8. Se você estiver procurando pacotes do RHEL 7, consulte o caminho de download <https://packages.microsoft.com/rhel/7/mssql-server-2019/>

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.4003.23-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-ha-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-fts-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-extensibility-java-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/8/mssql-server-2019/mssql-server-polybase-15.0.4003.23-3.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.4003.23-3 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.4003.23-3.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.4003.23-3.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.4003.23-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.4003.23-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.4003.23-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.4003.23-3_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.4003.23-3_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.4003.23-3_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.4003.23-3_amd64.deb)|

## <a id="ga"></a> GA (Novembro de 2019)

Esta é a versão de GA (disponibilidade geral) do SQL Server 2019 (15.x). Esta versão do Mecanismo de Banco de Dados do Microsoft SQL Server é a 15.0.2000.5.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.2000.5-5 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.2000.5-5 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.2000.5-5 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.2000.5-5_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.2000.5-5_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.2000.5-5_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.2000.5-5_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.2000.5-5_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.2000.5-5_amd64.deb)|

## <a id="rc"></a> Versão Release Candidate (agosto de 2019)

As seções a seguir fornecem locais de pacote e problemas conhecidos para a versão Release Candidate. Para saber mais sobre os novos recursos para o Linux no SQL Server 2019, confira [Novidades no SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 15.0.1900.25-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Pacote RPM do SLES | 15.0.1900.25-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM de extensibilidade do Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Pacote Debian do Ubuntu 16.04 | 15.0.1900.25-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de extensibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Pacote Debian de extensibilidade do Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[Pacote RPM do PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem problemas conhecidos com a versão de GA (Disponibilidade geral) do SQL Server 2019 (15.x) no Linux.

### <a name="general"></a>Geral

- O comprimento do nome do host em que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução:** altere o nome em /etc/hostname para algo com 15 caracteres de comprimento ou menos.

- Definir manualmente a hora do sistema de maneira a voltar no tempo fará com que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pare de atualizar a hora do sistema interno dentro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

    - **Resolução:** Reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Há suporte apenas para instalações de instância única.

    - **Resolução:** Se quiser ter mais de uma instância em um determinado host, considere usar VMs ou contêineres do Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] O Configuration Manager não pode se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux.

- O idioma padrão do logon de **sa** é inglês.

    - **Resolução:** Altere o idioma do logon do **sa** usando a instrução **ALTER LOGIN**.

- O provedor OLEDB registra em log o seguinte aviso: `Failed to verify the Authenticode signature of 'C:\binn\msoledbsql.dll'. Signature verification of SQL Server DLLs will be skipped. Genuine copies of SQL Server are signed. Failure to verify the Authenticode signature might indicate that this is not an authentic release of SQL Server. Install a genuine copy of SQL Server or contact customer support.`

   - **Resolução:** Nenhuma ação é necessária. O provedor OLEDB é assinado usando SHA256. O Mecanismo de banco de dados do SQL Server não valida a .dll assinada corretamente.

### <a name="databases"></a>Bancos de dados

- O banco de dados mestre não pode ser movido com o utilitário mssql-conf. Outros bancos de dados do sistema podem ser movidos usando mssql-conf.

- Ao restaurar um banco de dados do qual foi feito backup no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Windows, você deve usar a cláusula **WITH MOVE** na instrução Transact-SQL.

- Determinados algoritmos (pacotes de criptografia) para o protocolo TLS não funcionam corretamente com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux. Isso causa falhas de conexão ao tentar se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], bem como problemas de estabelecimento de conexões entre réplicas em grupos de alta disponibilidade.

   - **Resolução:** modifique o script de configuração **mssql.conf** para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para desabilitar pacotes de criptografia problemáticos, fazendo o seguinte:

      1. Adicione o seguinte a /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o seguinte comando.

      ```bash
      sudo systemctl restart mssql-server
      ```

- Bancos de dados do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] no Windows que usam OLTP in-memory não podem ser restaurados no SQL Server 2019 (15.x) no Linux. Para restaurar um banco de dados do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] que usa OLTP in-memory, primeiro atualize os bancos de dados para o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], o SQL Server 2017 ou o SQL Server 2019 no Windows antes de movê-los para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux por meio de backup/restauração ou de desanexar/anexar.

- A permissão de usuário **ADMINISTRAR OPERAÇÕES EM MASSA** não tem suporte no Linux no momento.

### <a name="networking"></a>Rede

Recursos que envolvem conexões TCP de saída do processo sqlservr, como servidores vinculados ou Grupos de Disponibilidade, poderão não funcionar se ambas as condições a seguir forem atendidas:

1. O servidor de destino é especificado como um nome de host e não como um endereço IP.

1. A instância de origem tem IPv6 desabilitado no kernel. Para verificar se o sistema tem o IPv6 habilitado no kernel, todos os testes a seguir precisam ser aprovados:

   - `cat /proc/cmdline` imprimirá o cmdline de inicialização do kernel atual. A saída não deve conter `ipv6.disable=1`.
   - O diretório /proc/sys/net/ipv6/ deve existir.
   - Um programa em C que chama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` deve ter êxito – syscall deve retornar um fd != -1 e não falhar com EAFNOSUPPORT.

O erro exato depende do recurso. Para servidores vinculados, isso se manifesta como um erro de tempo limite de logon. Para grupos de disponibilidade, o DDL do `ALTER AVAILABILITY GROUP JOIN` no secundário falhará após 5 minutos com um erro de tempo limite de configuração de download.

Para contornar esse problema, adote uma das seguintes medidas:

1. Use IPs em vez de nomes do host para especificar o destino da conexão TCP.

1. Habilite o IPv6 no kernel removendo `ipv6.disable=1` da inicialização de cmdline. A maneira de fazer isso depende da distribuição do Linux e do carregador de inicialização, como o grub. Se você deseja que o IPv6 seja desabilitado, ainda pode desativá-lo definindo `net.ipv6.conf.all.disable_ipv6 = 1` na configuração `sysctl` (por exemplo, `/etc/sysctl.conf`). Isso ainda impedirá que o adaptador de rede do sistema receba um endereço IPv6, mas permitirá que os recursos do sqlservr funcionem.

#### <a name="network-file-system-nfs"></a>NFS (sistema de arquivos de rede)
Se você usar compartilhamentos remotos **NFS (Network File System)** em produção, observe os seguintes requisitos de suporte:

- Use o NFS versão **4.2 ou superior**. As versões mais antigas do NFS não dão suporte aos recursos necessários, como `fallocate` e criação de arquivos esparsos, comuns aos sistemas de arquivos modernos.
- Localize somente os diretórios **/var/opt/mssql** na montagem NFS. Não há suporte para outros arquivos, como os binários do sistema [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
- Verifique se os clientes NFS usam a opção `nolock` ao montar o compartilhamento remoto.

### <a name="localization"></a>Localização

- Se a sua localidade não for inglês (en_us) durante a instalação, você precisará usar a codificação UTF-8 em sua sessão/terminal de Bash. Se usar a codificação ASCII, você poderá ver um erro semelhante ao seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se não for possível usar a codificação UTF-8, você deverá executar a instalação usando a variável de ambiente MSSQL_LCID para especificar sua escolha de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Ao executar a instalação de mssql-conf e executar uma instalação de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com idioma diferente do inglês, caracteres estendidos incorretos são exibidos após o texto localizado, "Configurando o SQL Server...". Ou, para instalações não baseadas em latim, a frase pode estar completamente ausente. A frase ausente deve exibir a seguinte cadeia de caracteres localizada: "O PID de licenciamento foi processado com êxito. A nova edição é [\<Nome\> edição]". Essa cadeia de caracteres é fornecida apenas para fins informativos e a próxima Atualização Cumulativa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] resolverá isso para todos os idiomas. Isso não afetará o êxito da instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de forma alguma. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo

- Nem todos os filtros estão disponíveis nesta versão, incluindo filtros para documentos do Office. Para obter uma lista de filtros com suporte, confira [Instalar a pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- O pacote **mssql-server-is** não tem suporte no SUSE nesta versão. Atualmente, ele tem suporte no Ubuntu e no RHEL (Red Hat Enterprise Linux).

- Com o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] na Atualização CTP 2.1 do Linux e posterior, os pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os drivers ODBC do MySQL, mas também espera-se que ela funcione com qualquer driver ODBC Unicode que observa a especificação ODBC. Em tempo de design, é possível fornecer um DSN ou uma cadeia de conexão para conectar-se aos dados ODBC; também é possível usar a autenticação do Windows. Para saber mais, confira a [postagem no blog que anunciou o suporte do ODBC para Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Não há suporte para os seguintes recursos nesta versão ao executar pacotes SSIS no Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Banco de dados de catálogo
  - Execução de pacotes agendada pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out
  - Feature Pack do Azure para SSIS
  - Suporte para Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para obter uma lista de componentes internos do SSIS que não têm suporte no momento ou que têm suporte com limitações, confira [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md#components).

Para saber mais sobre o SSIS no Linux, confira os seguintes artigos:
-   [Postagem no blog anunciando o suporte do SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados no Linux com o SSIS](sql-server-linux-migrate-ssis.md)

### <a id="ssms"></a> SSMS (SQL Server Management Studio)

As seguintes limitações se aplicam ao [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no Windows conectado ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para a extensão MDW (Data Warehouse de Gerenciamento) e o coletor de dados no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. 

- Componentes da interface do usuário do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] que têm as opções de Autenticação do Windows ou log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL. 

- O número de arquivos de log a serem retidos não pode ser modificado.

## <a name="next-steps"></a>Próximas etapas

Para começar, confira os seguintes guias de início rápido:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md).
