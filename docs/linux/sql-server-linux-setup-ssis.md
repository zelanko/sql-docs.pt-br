---
title: Instalar o SQL Server Integration Services no Linux | Microsoft Docs
description: Este artigo descreve como instalar o SQL Server Integration Services (SSIS) no Linux.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 13bd5bde7e4e4ec63bb7e3bd7d8959440f499672
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar o SQL Server Integration Services (SSIS) no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Siga as etapas neste artigo para instalar o SQL Server Integration Services (`mssql-server-is`) no Linux. Para obter informações sobre os recursos com suporte nesta versão dos serviços de integração para Linux, consulte o [notas de versão](sql-server-linux-release-notes.md).

Instale servidores de integração do SQL Server para sua plataforma:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a>Instalar o SSIS no Ubuntu
Para instalar o `mssql-server-is` pacote no Ubuntu, siga estas etapas:

1. Importe as chaves GPG repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre o repositório do Microsoft SQL Server Ubuntu.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Execute os comandos a seguir para instalar o SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Depois de instalar o Integration Services, execute `ssis-conf`. Para obter mais informações, consulte [configurar SSIS no Linux com o ssis conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Após a configuração, defina o caminho.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Atualização do SSIS
Se você já tiver `mssql-server-is` instalado, você pode atualizar a versão mais recente com o seguinte comando:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Remover o SSIS
Para remover `mssql-server-is`, você pode executar o seguinte comando:
```bash
sudo apt-get remove msssql-server-is
```

## <a name="RHEL"></a>Instalar o SSIS em RHEL
Para instalar o `mssql-server-is` o pacote em RHEL, siga estas etapas:

1. Baixe o arquivo de configuração de repositório do Microsoft SQL Server Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Execute os comandos a seguir para instalar o SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Após a instalação, execute `ssis-conf`. Para obter mais informações, consulte [configurar SSIS no Linux com o ssis conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. Quando a configuração estiver concluída, defina o caminho.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Atualização do SSIS
Se você já tiver `mssql-server-is` instalado, você pode atualizar a versão mais recente com o seguinte comando:

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>Remover o SSIS
Para remover `mssql-server-is`, você pode executar o seguinte comando:
```bash
sudo yum remove mssql-server-is
```

## <a name="next-steps"></a>Próximas etapas

Para executar pacotes SSIS no Linux, consulte [extrair, transformar e carregar dados para o SQL Server no Linux com o SSIS](sql-server-linux-migrate-ssis.md).

Para definir configurações adicionais de SSIS no Linux, consulte [configurar o SQL Server Integration Services no Linux com o ssis conf](sql-server-linux-configure-ssis.md).
