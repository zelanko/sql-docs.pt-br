---
title: "Notas de versão do SQL Server 2017 no Linux | Microsoft Docs"
description: "Este tópico contém as notas de versão e recursos com suporte para 2017 do SQL Server em execução no Linux. Notas de versão estão incluídas para RC2 e em versões anteriores."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: baa5826e9722bfb23afacf729d80bebf88985ed3
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de versão do SQL Server 2017 no Linux

As notas de versão a seguir se aplicam a 2017 do SQL Server em execução no Linux. Esta versão dá suporte a muitos dos recursos do mecanismo de banco de dados do SQL Server para Linux. O tópico a seguir é dividido em seções para cada liberação, começando com a versão mais recente, RC2. Consulte as informações em cada seção para problemas conhecidos, ferramentas, recursos e plataformas com suporte.

A tabela a seguir lista as versões do SQL Server 2017 abordados neste tópico.

| Versão | Versão | Data de lançamento |
|-----|-----|-----|
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| [CTP 2.1](#ctp21) | 14.0.600.250 | 5-2017 |
| [CTP 2.0](#ctp20) | 14.0.500.272 | 4-2017 |
| [CTP 1.4](#ctp14) | 14.0.405.198 | 3-2017 |
| [CTP 1.3](#ctp13) | 14.0.304.138 | 2-2017 |
| [CTP 1.2](#ctp12) | 14.0.200.24 | 1-2017 |
| [CTP 1.1](#ctp11) | 14.0.100.187 | 12-2016 |
| [CTP 1.0](#ctp10) | 14.0.1.246 | 11-2016 |

## <a id="RC2"></a>RC2 (agosto de 2017)

A versão do mecanismo do SQL Server para esta versão é 14.0.900.75.

### <a name="supported-platforms"></a>Plataformas com suporte

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE]
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1,5 TB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote

Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.900.75-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.900.75-1 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.900.75-1 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.900.75-1_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.900.75-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.900.75-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.900.75-1_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | mais recente |

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte

Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação transacional |
| &nbsp; | Replicação de mesclagem |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuída com conexões 3ª parte |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| &nbsp; | Extensão do pool de buffers |
| **SQL Server Agent** |  Subsistemas: CmdExec, PowerShell, leitor de fila, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de Leitor de Log |
| &nbsp; | Change Data Capture |
| &nbsp; | Backup Gerenciado |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Gerenciamento Extensível de Chaves |
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 RC2 no Linux.

#### <a name="general"></a>Geral

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

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

- Certos algoritmos (conjuntos de codificação) para segurança de camada de transporte (TLS) não funcionam corretamente com o SQL Server no Linux. Isso resulta em falhas de conexão ao tentar se conectar ao SQL Server, bem como problemas para estabelecer conexões entre réplicas em grupos de alta disponibilidade.

   - **Resolução**: modificar o **mssql.conf** script de configuração para o SQL Server no Linux para desabilitar conjuntos de codificação problemático, fazendo o seguinte:

      1. Adicione o seguinte ao /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers=ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

      1. Reinicie o SQL Server com o comando a seguir.
   
      ```
      sudo systemctl restart mssql-server
      ```

- Bancos de dados do SQL Server 2014 no Windows que usam OLTP na memória não podem ser restaurados no SQL Server 2017 no Linux. Para restaurar um banco de dados do SQL Server 2014 que usa o OLTP na memória, primeiro atualize os bancos de dados para SQL Server 2016 ou 2017 do SQL Server no Windows antes de movê-los para o SQL Server no Linux por meio de backup/restauração ou anexar/desanexar.

#### <a name="remote-database-files"></a>Arquivos de banco de dados remoto

- Não há suporte para a hospedagem de arquivos de banco de dados em um servidor NFS nesta versão. Isso inclui usar o NFS disco compartilhado para clustering de failover, bem como bancos de dados em instâncias não clusterizado. Estamos trabalhando em Habilitar o suporte do servidor NFS nas versões futuras.

#### <a name="localization"></a>Localização

- Se sua localidade não for inglês (en_us) durante a instalação, você deve usar a codificação UTF-8 em sua sessão/terminal bash. Se você usar a codificação ASCII, você verá um erro semelhante à seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se você não pode usar a codificação UTF-8, execute a instalação usando a variável de ambiente MSSQL_LCID para especificar sua preferência de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name="full-text-search"></a>Pesquisa de Texto Completo
- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
Você pode executar pacotes SSIS no Linux. Para obter mais informações, consulte os seguintes artigos:
-   [Anúncio de postagem de blog SSIS oferecem suporte para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)

Observe os seguintes problemas conhecidos com esta versão.

- O **mssql servidor é** pacote tem suporte no Ubuntu e Red Hat Enterprise Linux (RHEL) nesta versão.

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

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="RC1"></a>RC1 (julho de 2017)
A versão do mecanismo do SQL Server para esta versão é 14.0.800.90.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE]
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1 TB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.800.90-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.800.90-2 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.800.90-2 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.800.90-2_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.800.90-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.800.90-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.800.90-2_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | mais recente |

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação transacional |
| &nbsp; | Replicação de mesclagem |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Serviços de aprendizado de máquina |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **SQL Server Agent** |  Subsistemas: CmdExec, PowerShell, leitor de fila, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de Leitor de Log |
| &nbsp; | Change Data Capture |
| &nbsp; | Backup Gerenciado |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| &nbsp; | Atualização sem interrupção do grupo de disponibilidade |
| **Segurança** | Gerenciamento Extensível de Chaves |
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 RC1 no Linux.

#### <a name="general"></a>Geral
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

- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="remote-database-files"></a>Arquivos de banco de dados remoto

- Não há suporte para a hospedagem de arquivos de banco de dados em um servidor NFS nesta versão. Isso inclui usar o NFS disco compartilhado para clustering de failover, bem como bancos de dados em instâncias não clusterizado. Estamos trabalhando em Habilitar o suporte do servidor NFS nas versões futuras.

#### <a name="cross-platform-availability-groups-and-distributed-availability-groups"></a>Grupos de disponibilidade da plataforma cruzada e grupos de disponibilidade distribuída

- Devido a um problema conhecido, criando grupos de disponibilidade com réplicas em instâncias hospedadas no Windows e Linux não estiver nesta versão. Isso inclui grupos de disponibilidade distribuída. A correção estará disponível na compilação de candidato a próxima versão. 

#### <a name="server-collation"></a>Agrupamento do Servidor

- Quando usar o MSSQL_COLLATION substituir ou ao fazer uma instalação localizada de (não em inglês), é possível do SQL Server atingirá um deadlock ao tentar definir o agrupamento do servidor, que gera um despejo de memória. Instalação concluída com êxito, porém o agrupamento do servidor é não definido. A solução alternativa é simplesmente executar. / conf mssql set-agrupamento e insira o nome do agrupamento desejado quando solicitado (o nome do agrupamento pode ser encontrado no log de erros na linha de: "Tentativa de alterar o agrupamento padrão para..."). 
 
#### <a name="localization"></a>Localização

- Se sua localidade não for inglês (en_us) durante a instalação, você deve usar a codificação UTF-8 em sua sessão/terminal bash. Se você usar a codificação ASCII, você verá um erro semelhante à seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se você não pode usar a codificação UTF-8, execute a instalação usando a variável de ambiente MSSQL_LCID para especificar sua preferência de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name = "fci"></a>Atualização de instância de cluster de disco de compartilhado

No RC1 o agente de recursos de cluster define o nome do servidor virtual como ele faz em uma instância de Cluster de Failover no Windows. Antes do RC1 `@@servername` em um disco de cluster retornado no nó específico nomear isso após o failover `@@servername` retornou um valor diferente. No RC1 serverName da instância do cluster de disco compartilhado é atualizado com o nome do recurso quando o recurso é adicionado ao cluster. Por isso, o cluster precisará reiniciar o SQL Server após o failover manual durante a atualização - como as seguintes etapas:

1. Atualize primeiro o nó secundário (passivo) de cluster.
   - Atualizar **mssql server** pacote.
   - Atualizar **mssql-server-ha** pacote.
1. Executar failover manualmente para o nó atualizado.
   `pcs resource move <resourceName>`
   - Inicialmente, o recurso falhar porque o agente de recurso verifica se o nome do servidor real e esperado. O nome esperado do servidor será diferente.
   - Cluster reiniciará o recurso do SQL Server no mesmo nó. Isso atualizará o nome do servidor.
1. Atualize o outro nó. 
   - Atualizar **mssql server** pacote.
   - Atualizar **mssql-server-ha** pacote.
1. Remova a restrição adicionada pela mudança manual de recursos. Consulte [manualmente, o cluster de Failover](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md#failManual).
2. Se desejar, falhe no nó primário original. 

#### <a name="availability-group"></a>Grupo de disponibilidade

No Linux, a atualização do SQL Server de 2017 CTP 2.1 sem interrupção RC1 não é suportada. Depois de atualizar a réplica secundária, desconectará da réplica primária até que a réplica primária seja atualizada. A Microsoft pretende resolver esse problema para uma versão futura.

#### <a name="full-text-search"></a>Pesquisa de Texto Completo
- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- O **mssql servidor é** pacote não é suportado no SUSE nesta versão. Há suporte atualmente no Ubuntu e no Red Hat Enterprise Linux (RHEL).

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

Para obter mais informações sobre o SSIS no Linux, consulte os seguintes artigos:
-   [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp21"></a>CTP 2.1 (maio de 2017)
A versão do mecanismo do SQL Server para esta versão é 14.0.600.250.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE]
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1 TB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.600.250-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.600.250-2 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.600.250-2 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.600.250-2_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.600.250-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.600.250-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.600.250-2_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (1.12) |

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 CTP 2.1 no Linux.

#### <a name="general"></a>Geral
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
- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="always-on-availability-group"></a>Sempre no grupo de disponibilidade
- `sys.fn_hadr_backup_is_preffered_replica`não funciona para `CLUSTER_TYPE=NONE` ou `CLUSTER_TYPE=EXTERNAL` porque ele se baseia no registro de cluster WSFC replicada de chave que não está disponível. Estamos trabalhando em fornecer uma funcionalidade semelhante a uma função diferente. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo
- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-agent"></a>SQL Agent
- Os seguintes componentes e subsistemas de trabalhos do SQL Agent não têm suporte no momento no Linux:

    - Subsistemas: CmdExec, PowerShell, distribuidor de replicação, instantâneo, mesclagem, Queue Reader, SSIS, SSAS, SSRS
    - Alertas
    - Email de banco de dados
    - Agente de Leitor de Log 
    - Change Data Capture

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer a especificação de um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "tmp/sqlpackage. \<código \> /sistema/system32 "pasta. 

  - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

#### <a name="ssis"></a> SQL Server Integration Services (SSIS)
Você pode executar pacotes SSIS no Linux. Para obter mais informações, consulte o [anúncio de postagem de blog SSIS oferecem suporte para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Observe os seguintes problemas conhecidos com esta versão.

- O **mssql servidor é** pacote só tem suporte no Ubuntu neste momento.

- Não há suporte para os seguintes recursos durante a execução de pacotes do SSIS no Linux:
  - Banco de dados de catálogo do SSIS
  - Agendar a execução de pacotes pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Drivers ODBC de terceiros
  - O Gerenciador de Conexão do ODBC, origem e destino (compatível com o SSIS na atualização do Linux CTP 2.1)
  - Change Data Capture (CDC)
  - Escalar horizontalmente
  - Feature Pack do Azure
  - Hadoop e HDFS suporte
  - Microsoft Connector for SAP BW

Com o SSIS na atualização do Linux CTP 2.1, seus pacotes SSIS podem usar conexões ODBC no Linux. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp20"></a>CTP 2.0 (abril de 2017)
A versão do mecanismo do SQL Server para esta versão é 14.0.500.272.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS e 16.10 | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1 TB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação a seguir:

- [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.500.272-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.500.272-2 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.500.272-2 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |
| Pacote Debian Ubuntu 16.10 | 14.0.500.272-2 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - versão Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools para Visual Studio - versão Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (0.2.1) |

> [!NOTE] 
> As versões do SQL Server Management Studio e SQL Server Data Tools especificadas acima são candidatos de versão, portanto, não recomendado para uso em produção.

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 CTP 2.0 no Linux.

#### <a name="general"></a>Geral
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
- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="always-on-availability-group"></a>Sempre no grupo de disponibilidade
- Todas as configurações de HA - que significa que o grupo de disponibilidade é adicionado como um recurso a um cluster de Pacemaker - criado com anterior à CTP 2.0 pacotes não são compatíveis com o novo pacote. Exclua todos os recursos de cluster configurados anteriormente e criar novos grupos de disponibilidade com `CLUSTER_TYPE=EXTERNAL`. Consulte [configurar sempre no grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md).
- Grupos de disponibilidade criados com `CLUSTER_TYPE=NONE` e não adicionados como recursos no cluster continuarão a funcionar após a atualização. Use para cenários de escala de leitura. Consulte [configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md).
- `sys.fn_hadr_backup_is_preffered_replica`não funciona para `CLUSTER_TYPE=NONE` ou `CLUSTER_TYPE=EXTERNAL` porque ele se baseia no registro de cluster WSFC replicada de chave que não está disponível. Estamos trabalhando em fornecer uma funcionalidade semelhante a uma função diferente. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo
- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

- O separador de palavras coreano leva alguns segundos para carregar e gera um erro no primeiro uso. Depois deste erro inicial, ele deve funcionar normalmente.

#### <a name="sql-agent"></a>SQL Agent
- Os seguintes componentes e subsistemas de trabalhos do SQL Agent não têm suporte no momento no Linux:

    - Subsistemas: CmdExec, PowerShell, distribuidor de replicação, instantâneo, mesclagem, Queue Reader, SSIS, SSAS, SSRS
    - Alertas
    - Email de banco de dados
    - Agente de Leitor de Log 
    - Change Data Capture

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer a especificação de um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "tmp/sqlpackage. \<código \> /sistema/system32 "pasta. 

    - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp14"></a>CTP 1.4 (março de 2017)
A versão do mecanismo do SQL Server para esta versão é 14.0.405.198.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS e 16.10 | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1 TB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que você não precisa baixar esses pacotes diretamente se você usar as etapas nos guias de instalação abaixo
-   [Instalar o pacote do SQL Server](sql-server-linux-setup.md)
-   [Instalar o pacote de pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
-   [Instalar o pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.405.200-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.405.200-1 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[Pacote RPM do SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.405.200-1 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |
| Pacote Debian Ubuntu 16.10 | 14.0.405.200-1 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - versão Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools para Visual Studio - versão Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (0.2.1) |

> [!NOTE] 
> As versões do SQL Server Management Studio e SQL Server Data Tools especificadas acima são candidatos de versão, portanto, não recomendado para uso em produção.

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 CTP 1.4 no Linux.

#### <a name="general"></a>Geral
- O comprimento do nome de host em que o SQL Server é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: alterar o nome em nome do host/etc/para algo 15 caracteres ou menos.

- Não execute o comando `ALTER SERVICE MASTER KEY REGENERATE`. Há um bug conhecido que fará com que o SQL Server para se tornar instável. Se você precisar regenerar a chave mestra de serviço, você deve fazer backup de seus arquivos de banco de dados, desinstalar e, em seguida, reinstale o SQL Server e, em seguida, restaure os arquivos de banco de dados novamente.

- Definir manualmente a hora do sistema para trás no tempo fará com que o SQL Server para interromper a atualização a hora do sistema interno no SQL Server.

    - **Resolução**: reinicie o SQL Server.

- Alguns nomes de fuso horário no Linux não mapeiam exatamente aos nomes de fuso horário do Windows.

    - **Resolução**: usar nomes de fuso horário da coluna TZID na ' mapeamento para: tabela seção Windows o [página de documentação do site Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Mecanismo do SQL Server espera que linhas nos arquivos de texto a ser encerrada com CR-LF (formatação da linha do estilo do Windows).

- Há suporte apenas a instalações de única instância.

    - **Resolução**: se desejar ter mais de uma instância em um determinado host, considere o uso de máquinas virtuais ou contêineres do Docker. 

- Todos os arquivos de log e logs de erros são codificados em UTF-16.

- SQL Server Configuration Manager não pode se conectar ao SQL Server no Linux.

- **CREATE ASSEMBLY** não funcionará durante a tentativa de usar um arquivo. Use o **FROM \<bits\>**  método em vez disso, por enquanto. 

#### <a name="databases"></a>Bancos de dados
- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="always-on-availability-group"></a>Sempre no grupo de disponibilidade
- Grupo de disponibilidade AlwaysOn recursos clusterizados em Linux que foram criados com o CTP 1.3 falhará após a atualização do pacote HA (mssql-server-ha). 

   - **Resolução**: antes de atualizar o pacote de alta disponibilidade, defina o parâmetro de recurso de cluster `notify=true`. 
   
      - O exemplo a seguir define o parâmetro de recurso de cluster em um recurso chamado **ag1** em RHEL ou Ubuntu: 

      ```bash
      sudo pcs resource update ag1-master notify=true
      ```

      - Para SLES, atualize a configuração do recurso de grupo de disponibilidade para adicionar `notify=true`.  

      ```bash
      crm configure edit ms-ag_cluster 
      ```

      Adicionar `notify=true` e salvar a configuração de recurso.

- Grupos de disponibilidade AlwaysOn no Linux pode estar sujeito a perda de dados se as réplicas estão no modo de confirmação síncrona. Consulte detalhes conforme apropriado para sua distribuição do Linux. 

   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

#### <a name="full-text-search"></a>Pesquisa de Texto Completo
- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

- O separador de palavras coreano leva alguns segundos para carregar e gera um erro no primeiro uso. Depois deste erro inicial, ele deve funcionar normalmente.

#### <a name="sql-agent"></a>SQL Agent
- Os seguintes componentes e subsistemas de trabalhos do SQL Agent não têm suporte no momento no Linux:
    - Subsistemas: CmdExec, PowerShell, distribuidor de replicação, instantâneo, mesclagem, Queue Reader, SSIS, SSAS, SSRS
    - Alertas
    - Email de banco de dados
    - Envio de log
    - Agente de Leitor de Log 
    - Change Data Capture

#### <a name="in-memory-oltp"></a>OLTP na memória
- Bancos de dados OLTP na memória somente podem ser criados no diretório /var/opt/mssql. Para obter mais informações, visite o [tópico de OLTP na memória](sql-server-linux-performance-get-started.md#use-in-memory-oltp).

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer a especificação de um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "tmp/sqlpackage. \<código \> /sistema/system32 "pasta. 

    - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- O navegador de arquivos é restrito para o "c:\\" escopo, que resolve var/opt/mssql/no Linux. Para usar outros caminhos, gerar scripts da operação de interface do usuário e substitua a unidade c:\\ caminhos com caminhos do Linux. No SSMS, em seguida, execute o script manualmente.

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp13"></a>CTP 1.3 (fevereiro de 2017)
A versão do mecanismo do SQL Server para esta versão é 14.0.304.138.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS e 16.10 | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server foi testado até 1 TB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que não é necessário baixá-las diretamente pacotes se você usar as etapas a [guias de instalação](sql-server-linux-setup.md).

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.304.138-1 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[pacote de RPM de alta disponibilidade MSSQL-server-ha](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[pacote de RPM de pesquisa de texto completo de fts do MSSQL server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Pacote RPM SLES | 14.0.304.138-1 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[pacote de RPM de alta disponibilidade MSSQL-server-ha](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[pacote de RPM de pesquisa de texto completo de fts do MSSQL server](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Pacote Debian Ubuntu 16.04 | 14.0.304.138-1 | [pacote Debian do mecanismo de servidor MSSQL](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[MSSQL-server-alta disponibilidade alta disponibilidade Debian pacote](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[pacote Debian do fts do MSSQL server pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |
| Pacote Debian Ubuntu 16.10 | 14.0.304.138-1 | [pacote Debian do mecanismo de servidor MSSQL](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[MSSQL-server-alta disponibilidade alta disponibilidade Debian pacote](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[pacote Debian do fts do MSSQL server pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - versão Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools para Visual Studio - versão Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (0.2.1) |

> [!NOTE] 
> As versões do SQL Server Management Studio e SQL Server Data Tools especificadas acima são candidatos de versão, portanto, não recomendado para uso em produção.

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Agent |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 CTP 1.3 no Linux.

#### <a name="general"></a>Geral
- O comprimento do nome de host em que o SQL Server é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: alterar o nome em nome do host/etc/para algo 15 caracteres ou menos.

- Não execute o comando `ALTER SERVICE MASTER KEY REGENERATE`. Há um bug conhecido que fará com que o SQL Server para se tornar instável. Se você precisar regenerar a chave mestra de serviço, você deve fazer backup de seus arquivos de banco de dados, desinstalar e, em seguida, reinstale o SQL Server e, em seguida, restaure os arquivos de banco de dados novamente.

- Definir manualmente a hora do sistema para trás no tempo fará com que o SQL Server para interromper a atualização a hora do sistema interno no SQL Server.

    - **Resolução**: reinicie o SQL Server.

- Alguns nomes de fuso horário no Linux não mapeiam exatamente aos nomes de fuso horário do Windows.

    - **Resolução**: usar nomes de fuso horário da coluna TZID na ' mapeamento para: tabela seção Windows o [página de documentação do site Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Mecanismo do SQL Server espera que linhas nos arquivos de texto a ser encerrada com CR-LF (formatação da linha do estilo do Windows).

- Há suporte apenas a instalações de única instância.

    - **Resolução**: se desejar ter mais de uma instância em um determinado host, considere o uso de máquinas virtuais ou contêineres do Docker. 

- Todos os arquivos de log e logs de erros são codificados em UTF-16.

- SQL Server Configuration Manager não pode se conectar ao SQL Server no Linux.

- **CREATE ASSEMBLY** não funcionará durante a tentativa de usar um arquivo. Use o **FROM \<bits\>**  método em vez disso, por enquanto. 

#### <a name="databases"></a>Bancos de dados
- Não há suporte para alterar os locais de arquivos de log e de dados TempDB.

- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

- Grupos de disponibilidade AlwaysOn no Linux pode estar sujeito a perda de dados se as réplicas estão no modo de confirmação síncrona. Consulte 
 
   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   
#### <a name="full-text-search"></a>Pesquisa de Texto Completo
- Nem todos os filtros estão disponíveis com esta versão, inclusive filtros para documentos do Office. Para obter uma lista de filtros com suporte, consulte [instalar pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

- O separador de palavras coreano leva alguns segundos para carregar e gera um erro no primeiro uso. Depois deste erro inicial, ele deve funcionar normalmente.

#### <a name="in-memory-oltp"></a>OLTP na memória
- Bancos de dados OLTP na memória somente podem ser criados no diretório /var/opt/mssql. Para obter mais informações, visite o [tópico de OLTP na memória](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer a especificação de um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "/tmp/sqlpackage./ <code/> /sistema/system32" pasta. 

    - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP e ODBC 
- Ferramentas de linha de comando do SQL Server (mssql-tools) e o Driver ODBC (msodbcsql) depende de um Gerenciador de Driver de unixODBC personalizado. Isso faz com que conflitos se você tiver um Gerenciador de Driver do unixODBC instalado anteriormente. 

    - **Resolução**: no Ubuntu, o conflito será resolvido automaticamente. Quando solicitado se deseja desinstalar o Gerenciador de Driver unixODBC existente, digite 'y' e continuar com a instalação. Em RedHat, você precisará remover manualmente o Gerenciador de Driver unixODBC existente usando `yum remove unixODBC`. Estamos trabalhando para corrigir essa limitação para RHEL e SUSE e deve ter uma atualização para você em breve.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- O SQL Server Agent ainda não é suportado. Portanto, a funcionalidade do SQL Server Agent no SSMS não funciona no Linux no momento.

- O navegador de arquivos é restrito para o "c:\\" escopo, que resolve var/opt/mssql/no Linux. Para usar outros caminhos, gerar scripts da operação de interface do usuário e substitua a unidade c:\\ caminhos com caminhos do Linux. No SSMS, em seguida, execute o script manualmente.

- Número de arquivos de log para reter não pode ser modificado.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp12-ctp-12-january-2017"></a><a id="ctp12">CTP 1.2 (janeiro de 2017)
A versão do mecanismo do SQL Server para esta versão é 14.0.200.24.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.3 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS e 16.10 | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server só foi testado até 256GB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que não é necessário baixá-las diretamente pacotes se você usar as etapas a [guias de instalação](sql-server-linux-setup.md).

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM | 14.0.200.24-2 | [pacote de RPM mecanismo 14.0.200.24-2 MSSQL server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.200.24-2.x86_64.rpm)</br>[pacote de RPM de alta disponibilidade do servidor MSSQL 14.0.200.24-2](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.200.24-2.x86_64.rpm) | 
| Pacote Debian | 14.0.200.24-2 | [pacote Debian do mecanismo MSSQL server 14.0.200.24-2](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.200.24-2_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - versão Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools para Visual Studio - versão Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (0.2) |

> [!NOTE] 
> As versões do SQL Server Management Studio e SQL Server Data Tools especificadas acima são candidatos de versão, portanto, não recomendado para uso em produção.

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Pesquisa de Texto Completo |
| &nbsp; | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Grupos de Disponibilidade AlwaysOn |
| &nbsp; | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Agent |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 CTP 1.2 no Linux.

#### <a name="general"></a>Geral
- O comprimento do nome de host em que o SQL Server é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: alterar o nome em nome do host/etc/para algo 15 caracteres ou menos.

- Não execute o comando `ALTER SERVICE MASTER KEY REGENERATE`. Há um bug conhecido que fará com que o SQL Server para se tornar instável. Se você precisar regenerar a chave mestra de serviço, você deve fazer backup de seus arquivos de banco de dados, desinstalar e, em seguida, reinstale o SQL Server e, em seguida, restaure os arquivos de banco de dados novamente.

- Nome do recurso para o recurso SQL alterado de ocf:sql:fci para ocf:mssql:fci. Para obter mais detalhes sobre como configurar um cluster de failover de disco compartilhado que você pode encontrar [aqui](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure).

- Definir manualmente a hora do sistema para trás no tempo fará com que o SQL Server para interromper a atualização a hora do sistema interno no SQL Server.

    - **Resolução**: reinicie o SQL Server.

- Alguns nomes de fuso horário no Linux não mapeiam exatamente aos nomes de fuso horário do Windows.

    - **Resolução**: usar nomes de fuso horário da coluna TZID na ' mapeamento para: tabela seção Windows o [página de documentação do site Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Mecanismo do SQL Server espera que linhas nos arquivos de texto a ser encerrada com CR-LF (formatação da linha do estilo do Windows).

- Há suporte apenas a instalações de única instância.

    - **Resolução**: se desejar ter mais de uma instância em um determinado host, considere o uso de máquinas virtuais ou contêineres do Docker. 

- Todos os arquivos de log e logs de erros são codificados em UTF-16.

- SQL Server Configuration Manager não pode se conectar ao SQL Server no Linux.

- **CREATE ASSEMBLY** não funcionará durante a tentativa de usar um arquivo. Use o **FROM \<bits\>**  método em vez disso, por enquanto. 

#### <a name="databases"></a>Bancos de dados
- Não há suporte para alterar os locais de arquivos de log e de dados TempDB.

- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="in-memory-oltp"></a>OLTP na memória
- Bancos de dados OLTP na memória somente podem ser criados no diretório /var/opt/mssql. Esses bancos de dados também precisam ter o "c:\\" notação quando chamado. Para obter mais informações, visite o [tópico de OLTP na memória](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer a especificação de um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "tmp/sqlpackage. \<código \> /sistema/system32 "pasta. 

    - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP e ODBC 
- Se você tiver uma versão anterior das ferramentas de linha de comando do SQL Server (mssql ferramentas) e o Driver ODBC (msodbcsql), talvez você tenha instalado um Gerenciador de Driver (unixODBC-utf16) de unixODBC personalizado. Isso pode causar um conflito potencial que não usamos um Gerenciador de driver personalizado. 

    - **Resolução**: no Ubuntu e SLES, os conflitos serão resolvidos automaticamente. Quando solicitado se deseja desinstalar o Gerenciador de Driver unixODBC existente, digite 'y' e continuar com a instalação. Em RedHat, você precisará remover manualmente o Gerenciador de Driver unixODBC existente usando `yum remove unixODBC-utf16 unixODBC-utf16-devel` e tente novamente a instalação.
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- O SQL Server Agent ainda não é suportado. Portanto, a funcionalidade do SQL Server Agent no SSMS não funciona no Linux no momento.

- O navegador de arquivos é restrito para o "c:\\" escopo, que resolve var/opt/mssql/no Linux. Para usar outros caminhos, gerar scripts da operação de interface do usuário e substitua a unidade c:\\ caminhos com caminhos do Linux. No SSMS, em seguida, execute o script manualmente.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp11-ctp-11-december-2016"></a><a id="ctp11">CTP 1.1 (dezembro de 2016)
A versão do mecanismo do SQL Server para esta versão é 14.0.100.187.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS e 16.10 | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server só foi testado até 256GB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que não é necessário baixá-las diretamente pacotes se você usar as etapas a [guias de instalação](sql-server-linux-setup.md).

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM | 14.0.100.187-1 | [pacote de RPM mecanismo 14.0.100.187-1 MSSQL server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.100.187-1.x86_64.rpm)</br>[pacote de RPM de alta disponibilidade do servidor MSSQL 14.0.100.187-1](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.100.187-1.x86_64.rpm) | 
| Pacote Debian | 14.0.100.187-1 | [pacote Debian do mecanismo MSSQL server 14.0.100.187-1](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.100.187-1_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - versão Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools para Visual Studio - versão Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (0.2) |

> [!NOTE] 
> As versões do SQL Server Management Studio e SQL Server Data Tools especificadas acima são candidatos de versão, portanto, não recomendado para uso em produção.

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Pesquisa de Texto Completo |
| &nbsp; | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Grupos de Disponibilidade AlwaysOn |
| &nbsp; | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Agent |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do CTP do SQL Server de 2017 1.1 no Linux.

#### <a name="general"></a>Geral
- O comprimento do nome de host em que o SQL Server é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: alterar o nome em nome do host/etc/para algo 15 caracteres ou menos.

- Não execute o comando `ALTER SERVICE MASTER KEY REGENERATE`. Há um bug conhecido que fará com que o SQL Server para se tornar instável. Se você precisar regenerar a chave mestra de serviço, você deve fazer backup de seus arquivos de banco de dados, desinstalar e, em seguida, reinstale o SQL Server e, em seguida, restaure os arquivos de banco de dados novamente.

- Nome do recurso para o recurso SQL alterado de ocf:sql:fci para ocf:mssql:fci. Para obter mais detalhes sobre como configurar um cluster de failover de disco compartilhado que você pode encontrar [aqui](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure).

- Definir manualmente a hora do sistema para trás no tempo fará com que o SQL Server para interromper a atualização a hora do sistema interno no SQL Server.

    - **Resolução**: reinicie o SQL Server.

- Alguns nomes de fuso horário no Linux não mapeiam exatamente aos nomes de fuso horário do Windows.

    - **Resolução**: usar nomes de fuso horário da coluna TZID na ' mapeamento para: tabela seção Windows o [página de documentação do site Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Mecanismo do SQL Server espera que linhas nos arquivos de texto a ser encerrada com CR-LF (formatação da linha do estilo do Windows).

- Há suporte apenas a instalações de única instância.

    - **Resolução**: se desejar ter mais de uma instância em um determinado host, considere o uso de máquinas virtuais ou contêineres do Docker. 

- Todos os arquivos de log e logs de erros são codificados em UTF-16.

- SQL Server Configuration Manager não pode se conectar ao SQL Server no Linux.

- **CREATE ASSEMBLY** não funcionará durante a tentativa de usar um arquivo. Use o **FROM \<bits\>**  método em vez disso, por enquanto. 

#### <a name="databases"></a>Bancos de dados
- Não há suporte para alterar os locais de arquivos de log e de dados TempDB.

- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="in-memory-oltp"></a>OLTP na memória
- Bancos de dados OLTP na memória somente podem ser criados no diretório /var/opt/mssql. Esses bancos de dados também precisam ter o "c:\" notação quando chamado. Para obter mais informações, visite o [tópico de OLTP na memória](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer a especificação de um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "tmp/sqlpackage. \<código \> /sistema/system32 "pasta. 

    - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP e ODBC 
- Ferramentas de linha de comando do SQL Server (mssql-tools) e o Driver ODBC (msodbcsql) depende de um Gerenciador de Driver de unixODBC personalizado. Isso faz com que conflitos se você tiver um Gerenciador de Driver do unixODBC instalado anteriormente. 

    - **Resolução**: no Ubuntu, o conflito será resolvido automaticamente. Quando solicitado se deseja desinstalar o Gerenciador de Driver unixODBC existente, digite 'y' e continuar com a instalação. Em RedHat, você precisará remover manualmente o Gerenciador de Driver unixODBC existente usando `yum remove unixODBC`. Estamos trabalhando para corrigir essa limitação para RHEL e SUSE e deve ter uma atualização para você em breve.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- O SQL Server Agent ainda não é suportado. Portanto, a funcionalidade do SQL Server Agent no SSMS não funciona no Linux no momento.

- O navegador de arquivos é restrito para o "c:\\" escopo, que resolve var/opt/mssql/no Linux. Para usar outros caminhos, gerar scripts da operação de interface do usuário e substitua a unidade c:\\ caminhos com caminhos do Linux. No SSMS, em seguida, execute o script manualmente.

v

![Gráfico de barras de separação](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp10-ctp-10-november-2016"></a><a id="ctp10">CTP 1.0 (novembro de 2016)
A versão do mecanismo do SQL Server para esta versão é 14.0.1.246.

### <a name="supported-platforms"></a>Plataformas com suporte 

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Área de trabalho, servidor e estação de trabalho do Red Hat Enterprise Linux 7.2 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS | EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Mecanismo do docker 1.8 + no Windows, Mac ou Linux | N/A | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
> Mecanismo do SQL Server só foi testado até 256GB de memória no momento.

### <a name="package-details"></a>Detalhes do pacote
Detalhes do pacote e locais de download para os pacotes RPM e Debian são listados na tabela a seguir. Observe que não é necessário baixá-las diretamente pacotes se você usar as etapas a [guias de instalação](sql-server-linux-setup.md).

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM | 14.0.1.246-6 | [pacote de RPM mecanismo 14.0.1.246-6 MSSQL server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.1.246-6.x86_64.rpm)</br>[pacote de RPM de alta disponibilidade do servidor MSSQL 14.0.1.246-6](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.1.246-6.x86_64.rpm) | 
| Pacote Debian | 14.0.1.246-6 | [pacote Debian do mecanismo MSSQL server 14.0.1.246-6](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.1.246-6_amd64.deb) |

### <a name="supported-client-tools"></a>Ferramentas de cliente com suporte

| Ferramenta | Versão mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - versão Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools para Visual Studio - versão Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Código do Visual Studio](https://code.visualstudio.com) com o [mssql extensão](https://aka.ms/mssql-marketplace) | Versão mais recente (0.1.5) |

> [!NOTE] 
> As versões do SQL Server Management Studio e SQL Server Data Tools especificadas acima são candidatos de versão, portanto, não recomendado para uso em produção.

### <a name="unsupported-features-and-services"></a>Serviços e recursos sem suporte
Os seguintes recursos e serviços não estão disponíveis no Linux neste momento. Suporte a esses recursos será habilitado cada vez durante a cadência mensal de atualizações do programa de visualização.

| Área | Não há suporte para recurso ou serviço |
|-----|-----|
| **Mecanismo de banco de dados** | Pesquisa de Texto Completo |
| &nbsp; | Replicação |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta Distribuída |
| &nbsp; | Sistema os procedimentos armazenados estendidos (XP_CMDSHELL, etc.) |
| &nbsp; | Tabela de arquivos |
| &nbsp; | O conjunto de assemblies do CLR com o EXTERNAL_ACCESS ou UNSAFE permissão |
| **Alta disponibilidade** | Grupos de Disponibilidade AlwaysOn |
| &nbsp; | Espelhamento de banco de dados  |
| **Segurança** | Autenticação do Active Directory |
| &nbsp; | Autenticação do Windows |
| &nbsp; | Gerenciamento Extensível de Chaves |
| &nbsp; | Uso de certificado fornecido pelo usuário para o SSL ou TLS |
| **Serviços** | SQL Server Agent |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conhecidos
As seções a seguir descrevem problemas conhecidos com esta versão do SQL Server de 2017 CTP1 no Linux.

#### <a name="general"></a>Geral
- O comprimento do nome de host em que o SQL Server é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução**: alterar o nome em nome do host/etc/para algo 15 caracteres ou menos.

- Definir manualmente a hora do sistema para trás no tempo fará com que o SQL Server para interromper a atualização a hora do sistema interno no SQL Server.

    - **Resolução**: reinicie o SQL Server.

- Alguns nomes de fuso horário no Linux não mapeiam exatamente aos nomes de fuso horário do Windows.

    - **Resolução**: usar nomes de fuso horário da coluna TZID na ' mapeamento para: tabela seção Windows o [página de documentação do site Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Mecanismo do SQL Server espera que linhas nos arquivos de texto a ser encerrada com CR-LF (formatação da linha do estilo do Windows).

- Há suporte apenas a instalações de única instância.

    - **Resolução**: se desejar ter mais de uma instância em um determinado host, considere o uso de máquinas virtuais ou contêineres do Docker. 

- Todos os arquivos de log e logs de erros são codificados em UTF-16.

- SQL Server Configuration Manager não pode se conectar ao SQL Server no Linux.

- **CREATE ASSEMBLY** não funcionará durante a tentativa de usar um arquivo. Use o **FROM \<bits\>**  método em vez disso, por enquanto.

#### <a name="databases"></a>Bancos de dados
- Não há suporte para alterar os locais de arquivos de log e de dados TempDB.

- Bancos de dados do sistema não podem ser movidos com o utilitário mssql conf.

- Ao restaurar um banco de dados cujo backup foi feito no SQL Server no Windows, você deve usar o **WITH MOVE** cláusula na instrução Transact-SQL.

- Não há suporte para transações distribuídas exigir que o serviço Coordenador de transações distribuídas da Microsoft no SQL Server em execução no Linux. SQL Server para SQL Server, há suporte para transações distribuídas.

#### <a name="in-memory-oltp"></a>OLTP na memória
- Bancos de dados OLTP na memória somente podem ser criados no diretório /var/opt/mssql. Esses bancos de dados também precisam ter o "c:\\" notação quando chamado. Para obter mais informações, visite o [tópico de OLTP na memória](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Usando SqlPackage requer para especificar um caminho absoluto para arquivos. Usar caminhos relativos mapeará os arquivos sob a "tmp/sqlpackage. \<código \> /sistema/system32 "pasta. 

    - **Resolução**: usar caminhos de arquivo absolutos.

- SqlPackage mostra o local dos arquivos com um "c:\\" prefixo.

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP e ODBC 
- Ferramentas de linha de comando do SQL Server (mssql-tools) e o Driver ODBC (msodbcsql) depende de um Gerenciador de Driver de unixODBC personalizado. Isso faz com que conflitos se você tiver um Gerenciador de Driver do unixODBC instalado anteriormente. 

    - **Resolução**: no Ubuntu, o conflito será resolvido automaticamente. Quando solicitado se deseja desinstalar o Gerenciador de Driver unixODBC existente, digite 'y' e continuar com a instalação. Em RedHat, você precisará remover manualmente o Gerenciador de Driver unixODBC existente usando `yum remove unixODBC`. Estamos trabalhando para corrigir essa limitação para RHEL e SUSE e deve ter uma atualização para você em breve.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
As seguintes limitações se aplicam a SSMS no Windows conectados ao SQL Server no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para o gerenciamento MDW (Data Warehouse) e o coletor de dados no SSMS. 

- Componentes SSMS UI com autenticação do Windows ou opções de log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL Server. 

- O SQL Server Agent ainda não é suportado. Portanto, a funcionalidade do SQL Server Agent no SSMS não funciona no Linux no momento.

- O navegador de arquivos é restrito para o "c:\\" escopo, que resolve var/opt/mssql/no Linux. Para usar outros caminhos, gerar scripts da operação de interface do usuário e substitua a unidade c:\\ caminhos com caminhos do Linux. No SSMS, em seguida, execute o script manualmente.

### <a name="next-steps"></a>Próximas etapas

Para começar, consulte os seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

