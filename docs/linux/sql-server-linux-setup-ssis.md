---
title: Instalar o SQL Server Integration Services em Linux
description: Este artigo descreve como instalar o SQL Server Integration Services no Linux.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 0f400667e73effb73ff41c3c7270e3f89a2ca0da
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76162637"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar o SSIS (SQL Server Integration Services) no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Siga as etapas neste artigo para instalar o SQL Server Integration Services (**mssql-server-is**) no Linux. Para obter informações sobre os recursos compatíveis nesta versão do Integration Services para Linux, confira as [Notas sobre a versão](sql-server-linux-release-notes.md).

Você pode instalar o SQL Server Integration Services nestas plataformas:

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="install-ssis-on-ubuntu"></a><a name="ubuntu"></a> Instalar o SSIS no Ubuntu

Para instalar o pacote **mssql-server-is** no Ubuntu, siga estas etapas:

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Importe as chaves GPG do repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório do Ubuntu do SQL Server.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

1. Execute os comandos a seguir para instalar o SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. Depois de instalar o Integration Services, execute **ssis-conf**. Para obter mais informações, confira [Configurar o SSIS no Linux com ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Depois que a configuração for concluída, defina a variável de ambiente PATH.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Importe as chaves GPG do repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registre o repositório do Ubuntu do SQL Server.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```

1. Execute os comandos a seguir para instalar o SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. Depois de instalar o Integration Services, execute **ssis-conf**. Para obter mais informações, confira [Configurar o SSIS no Linux com ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Depois que a configuração for concluída, defina a variável de ambiente PATH.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>Atualizar o SSIS

Se você já tiver **mssql-server-is** instalado, poderá atualizar para a versão mais recente com este comando:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Remover SSIS

Para remover **mssql-server-is**, execute o seguinte comando:

```bash
sudo apt-get remove mssql-server-is
```

## <a name="install-ssis-on-rhel"></a><a name="RHEL"></a> Instalar o SSIS no RHEL
Para instalar o pacote **mssql-server-is** no RHEL, siga estas etapas:

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Baixe o arquivo de configuração do repositório do Red Hat do SQL Server.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Execute o comando a seguir para instalar o SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. Após a instalação, execute **ssis-conf**. Para obter mais informações, confira [Configurar o SSIS no Linux com ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Depois que a configuração for concluída, defina a variável de ambiente PATH.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Baixe o arquivo de configuração do repositório do Red Hat do SQL Server.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

1. Execute o comando a seguir para instalar o SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. Após a instalação, execute **ssis-conf**. Para obter mais informações, confira [Configurar o SSIS no Linux com ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Depois que a configuração for concluída, defina a variável de ambiente PATH.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>Atualizar o SSIS

Se você já tiver **mssql-server-is** instalado, poderá atualizar para a versão mais recente usando este comando:

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>Remover SSIS
Para remover **mssql-server-is**, execute o seguinte comando:

```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>Instalação autônoma

Para executar **ssis-conf-setup** como uma instalação autônoma, execute as seguintes etapas:

1. Especifique a opção **-n** (sem prompt).
1. Informe os valores necessários definindo as variáveis de ambiente.

O seguinte exemplo executa estas ações:

- Instala o SSIS
- Especifica a edição do Desenvolvedor fornecendo um valor para a variável de ambiente SSIS_PID
- Aceita os termos de licença para software Microsoft fornecendo um valor para a variável de ambiente ACCEPT_EULA
- Executa uma instalação autônoma especificando a opção **-n** (sem prompt)

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variáveis de ambiente para instalação autônoma

| Variável de ambiente | DESCRIÇÃO |
|---|---|
| ACCEPT_EULA | Aceita os termos de licença SQL Server quando definidos para qualquer valor como "Y".|
| SSIS_PID | Define a edição do SQL Server ou a chave do produto (Product Key). Estes são os valores possíveis:<ul><li>Avaliação</li><li>Desenvolvedor</li><li>Express</li><li>Web</li><li>Standard</li><li>Enterprise</li><li>Uma chave do produto (Product Key)</li></ul>Se você especificar uma chave do produto (Product Key), ela deverá estar no formato *#####* - *#####* - *#####* - *#####* - *#####* , em que *#* é uma letra ou um dígito.  |
| | |

## <a name="next-steps"></a>Próximas etapas

Para executar pacotes do SSIS no Linux, confira [Extrair, transformar e carregar dados para SQL Server em Linux com o SSIS](sql-server-linux-migrate-ssis.md).

Para definir configurações adicionais do SSIS no Linux, confia [Configurar SQL Server Integration Services no Linux com ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre o SSIS no Linux

- [Extrair, transformar e carregar dados no Linux com o SSIS](sql-server-linux-migrate-ssis.md)
- [Configurar o SQL Server Integration Services no Linux com ssis-conf](sql-server-linux-configure-ssis.md)
- [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
- [Agendar a execução de pacotes do SQL Server Integration Services no Linux com cron](sql-server-linux-schedule-ssis-packages.md)
