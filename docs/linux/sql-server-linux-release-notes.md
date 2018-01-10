---
title: "Notas de versão do SQL Server 2017 no Linux | Microsoft Docs"
description: "Este tópico contém as notas de versão e recursos com suporte para 2017 do SQL Server em execução no Linux. Notas de versão são incluídas para a versão mais recente e várias versões anteriores."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 01/09/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.workload: Active
ms.openlocfilehash: 5b66fa7db6547bfbb9340ce5738dff064f6a48c9
ms.sourcegitcommit: b4b7cd787079fa3244e77c1e9e3c68723ad30ad4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de versão do SQL Server 2017 no Linux

As notas de versão a seguir se aplicam a 2017 do SQL Server em execução no Linux. O tópico a seguir é dividido em seções para cada versão. A versão GA tem detalhadas de suporte e problemas listados. Cada versão de atualização cumulativa (CU) tem um link para um tópico de suporte que descrevem alterações CU, bem como links para o download do pacote do Linux.

## <a name="supported-platforms"></a>Plataformas com suporte

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 ou 7.4 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais detalhes, analise o [requisitos de sistema](sql-server-linux-setup.md#system) para SQL Server no Linux. Para a política de suporte mais recente para o SQL Server 2017, consulte o [política de suporte técnico para o Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | mais recente |

## <a name="release-history"></a>Histórico de lançamento

A tabela a seguir lista o histórico de versão do SQL Server 2017.

| Versão | Versão | Data de lançamento |
|-----|-----|-----|
| [CU3](#CU3) | 14.0.3015.40| 1-2018 |
| [CU2](#CU2) | 14.0.3008.27 | 11-2017 |
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <a id="cuinstall"></a>Como instalar atualizações cumulativas

Se você tiver configurado o repositório de atualização cumulativa, em seguida, você obterá a atualização cumulativa mais recente dos pacotes do SQL Server quando você executar novas instalações. O repositório de atualização cumulativa é o padrão para todos os artigos de instalação do pacote para o SQL Server no Linux. Para obter mais informações sobre a configuração do repositório, consulte [repositórios de origem](sql-server-linux-setup.md#repositories).

Se você estiver atualizando os pacotes existentes do SQL Server, executados o comando de atualização apropriado para cada pacote obter a atualização cumulativa mais recente. Para obter instruções de atualização específica para cada pacote, consulte os guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)

## <A id="CU2"></a>Atualização cumulativa 3 (janeiro de 2018)

Esta é a versão de atualização cumulativa 3 (CU3) do SQL Server 2017. A versão do mecanismo do SQL Server para esta versão é 14.0.3015.40. Para obter informações sobre as correções e aperfeiçoamentos desta versão, consulte [https://support.microsoft.com/en-us/help/4052987](https://support.microsoft.com/en-us/help/4052987).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3015.40-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3015.40-1 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.3015.40-1 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <A id="CU2"></a>Atualização cumulativa 2 (novembro de 2017)

Esta é a versão de atualização cumulativa 2 (CU2) do SQL Server 2017. A versão do mecanismo do SQL Server para esta versão é 14.0.3008.27. Para obter informações sobre as correções e aperfeiçoamentos desta versão, consulte [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3008.27-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3008.27-1 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.3008.27-1 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <A id="CU1"></a>A atualização cumulativa 1 (outubro de 2017)

Esta é a versão de atualização cumulativa 1 (CU1) do SQL Server 2017. A versão do mecanismo do SQL Server para esta versão é 14.0.3006.16. Para obter informações sobre as correções e aperfeiçoamentos desta versão, consulte [https://support.microsoft.com/help/4038634](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacote manual ou off-line, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3006.16-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.3006.16-3 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.3006.16-3 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (outubro de 2017)

Esta é a versão de disponibilidade geral (GA) do SQL Server 2017. A versão do mecanismo do SQL Server para esta versão é 14.0.1000.169.

### <a name="package-details"></a>Detalhes do pacote

Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.1000.169-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.1000.169-2 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.1000.169-2 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

### <a name="Unsupported"></a>Serviços e recursos sem suporte

Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez mais ao longo do tempo.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação transacional |
| &nbsp; | Replicação de mesclagem |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuída com conexões 3ª parte |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos, FILESTREAM |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| &nbsp; | Extensão do pool de buffers |
| **SQL Server Agent** |  Subsistemas: CmdExec, PowerShell, leitor de fila, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de Leitor de Log |
| &nbsp; | Change Data Capture |
| &nbsp; | Backup Gerenciado |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Gerenciamento Extensível de Chaves |
| &nbsp; | Autenticação do AD para servidores vinculados | 
| &nbsp; | Autenticação do AD para grupos de disponibilidade (grupos de disponibilidade) | 
| &nbsp; | ferramentas de terceiros AD 3º (Centrify, Vintela, Powerbroker) | 
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem problemas conhecidos com a versão de disponibilidade geral (GA) do SQL Server 2017 no Linux.

#### <a name="general"></a>Geral

- Atualizações para a versão de lançamento do SQL Server 2017 têm suporte apenas do CTP 2.1 ou posterior. 

- O comprimento do nome de host em que o SQL Server é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: alterar o nome em nome do host/etc/para algo 15 caracteres ou menos.

- Definir manualmente a hora do sistema para trás no tempo fará com que o SQL Server para interromper a atualização a hora do sistema interno no SQL Server.

    - **Resolução**: reinicie o SQL Server.

- Há suporte apenas a instalações de única instância.

    - **Resolução**: se desejar ter mais de uma instância em um determinado host, considere o uso de máquinas virtuais ou contêineres do Docker. 

- SQL Server Configuration Manager não pode se conectar ao SQL Server no Linux.

- O idioma padrão do **sa** logon é o inglês.

    - **Resolução**: alterar o idioma do **sa** logon com a **ALTER LOGIN** instrução.

#### <a name="databases"></a>Bancos de dados

- O banco de dados mestre não pode ser movido com o utilitário mssql conf. Outros bancos de dados do sistema podem ser movidos com conf mssql

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, servidores vinculados têm suporte, a menos que eles envolvem o DTC. Para obter mais informações, consulte [não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Certos algoritmos (conjuntos de codificação) para segurança de camada de transporte (TLS) não funcionam corretamente com o SQL Server no Linux. Isso resulta em falhas de conexão ao tentar se conectar ao SQL Server, bem como problemas para estabelecer conexões entre réplicas em grupos de alta disponibilidade.

   - **Resolução**: modificar o **mssql.conf** script de configuração para o SQL Server no Linux para desabilitar conjuntos de codificação problemático, fazendo o seguinte:

      1. Adicione o seguinte ao /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reinicie o SQL Server com o comando a seguir.

      ```bash
      sudo systemctl restart mssql-server
      ```

- Bancos de dados do SQL Server 2014 no Windows que usam OLTP na memória não podem ser restaurados no SQL Server 2017 no Linux. Para restaurar um banco de dados do SQL Server 2014 que usa o OLTP na memória, primeiro atualize os bancos de dados para SQL Server 2016 ou 2017 do SQL Server no Windows antes de movê-los para o SQL Server no Linux por meio de backup/restauração ou anexar/desanexar.

- Permissão de usuário **ADMINISTER BULK OPERATIONS** não tem suporte no Linux neste momento.

#### <a name="networking"></a>Rede

Recursos que envolvem conexões TCP de saída do processo de sqlservr, como servidores vinculados ou grupos de disponibilidade, podem não funcionar se as seguintes condições forem atendidas:

1. O servidor de destino é especificado como um nome de host e não um endereço IP.

1. A instância de origem tem IPv6 desabilitado no kernel. Para verificar se o sistema tem IPv6 habilitado no kernel, devem passar a todos os testes a seguir:

   - `cat /proc/cmdline`imprimirá cmdline a inicialização do kernel do atual. A saída não deve conter `ipv6.disable=1`.
   - O proc/sys/rede/ipv6/diretório deve existir.
   - Um programa em C que chama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` devem ser bem-sucedidos - o syscall deve retornar um fd! = -1 e não falhar com EAFNOSUPPORT.

O erro exato depende do recurso. Para servidores vinculados, isso se manifesta como um erro de tempo limite de logon. Para grupos de disponibilidade, o `ALTER AVAILABILITY GROUP JOIN` DDL no secundário falhará após 5 minutos com um erro de tempo limite de configuração de download.

Para contornar esse problema, siga um destes procedimentos:

1. Use IPs em vez de nomes de host para especificar o destino da conexão de TCP.

1. Habilite o IPv6 no kernel, removendo `ipv6.disable=1` de cmdline a inicialização. A maneira de fazer isso depende da distribuição do Linux e do carregador de inicialização, como grub. Se você quiser IPv6 a ser desabilitado, você ainda pode desabilitá-lo definindo `net.ipv6.conf.all.disable_ipv6 = 1` no `sysctl` configuração (por exemplo, `/etc/sysctl.conf`). Isso será ainda impedir o adaptador de rede do sistema de um endereço IPv6, mas permitir que os recursos sqlservr funcionem.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Se você usar **sistema de arquivos de rede (NFS)** compartilhamentos remotos em produção, observe os seguintes requisitos de suporte:

- Versão do NFS Use **4.2 ou superior**. Versões mais antigas do NFS não dão suporte a recursos obrigatórios, como fallocate e criação de arquivo esparso, comum para sistemas de arquivos modernos.
- Localizar somente o **/var/opt/mssql** diretórios na montagem do NFS. Não há suporte para outros arquivos, como os binários do sistema do SQL Server.
- Certifique-se de que os clientes NFS usem a opção 'nolock' ao montar o compartilhamento remoto.

#### <a name="localization"></a>Localização

- Se sua localidade não for inglês (en_us) durante a instalação, você deve usar a codificação UTF-8 em sua sessão/terminal bash. Se você usar a codificação ASCII, você verá um erro semelhante à seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se você não pode usar a codificação UTF-8, execute a instalação usando a variável de ambiente MSSQL_LCID para especificar sua preferência de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Quando executando a instalação conf mssql e executar uma instalação diferente do inglês do SQL Server, incorreto caracteres estendidos são exibidos após o texto localizado, "Configurando o SQL Server …". Ou, com base em instalações não latinos, a frase pode estar ausente completamente. A sentença ausente deve exibir a seguinte cadeia de caracteres localizada: "o PID de licenciamento foi processado com êxito.  É a nova edição [\<nome\> edição] ". Essa cadeia de caracteres de saída é fornecida somente para fins informativos e a atualização cumulativa do SQL Server próximo endereço isso para todos os idiomas. Isso não afeta a instalação bem-sucedida do SQL Server de forma alguma. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo

- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- O **mssql servidor é** pacote não é suportado no SUSE nesta versão. Há suporte atualmente no Ubuntu e no Red Hat Enterprise Linux (RHEL).

- Com o SSIS, sobre a atualização do Linux CTP 2.1 e posterior, os pacotes do SSIS podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o SQL Server e os drivers ODBC MySQL, mas também é esperada para funcionar com qualquer driver de ODBC Unicode que observa a especificação de ODBC. Em tempo de design, você pode fornecer um DSN ou uma cadeia de caracteres de conexão para conectar-se aos dados de ODBC; Você também pode usar a autenticação do Windows. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Os recursos a seguir não têm suporte nesta versão, quando você executar pacotes SSIS no Linux:
  - Banco de dados de catálogo do SSIS
  - Execução de pacotes agendados pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - Expansão do SSIS
  - Azure Feature Pack para SSIS
  - Suporte de Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para obter uma lista de componentes internos do SSIS que não são suportados atualmente ou que têm suporte com limitações, consulte [limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md#components).

Para obter mais informações sobre o SSIS no Linux, consulte os seguintes artigos:
-   [Anúncio de postagem de blog SSIS oferecem suporte para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
