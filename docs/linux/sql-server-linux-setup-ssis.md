---
title: Instalar o SQL Server Integration Services no Linux
description: Este artigo descreve como instalar o SQL Server Integration Services (SSIS) no Linux.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 68f3497e9f3f47d7e43c2bda0083bc25632d8221
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032446"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar o SQL Server Integration Services (SSIS) no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Siga as etapas neste artigo para instalar o SQL Server Integration Services (`mssql-server-is`) no Linux. Para obter informações sobre os recursos com suporte nesta versão dos serviços de integração para Linux, consulte o [notas de versão](sql-server-linux-release-notes.md).

Instale servidores de integração do SQL Server para sua plataforma:

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Instalar o SSIS no Ubuntu
Para instalar o `mssql-server-is` do pacote no Ubuntu, siga estas etapas:

1. Importe as chaves GPG repositório público.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registre o repositório do Microsoft SQL Server Ubuntu.

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. Execute os seguintes comandos para instalar o SQL Server Integration Services.

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. Após a instalação do Integration Services, execute `ssis-conf`. Para obter mais informações, consulte [configurar o SSIS no Linux com o ssis-conf](sql-server-linux-configure-ssis.md).

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. Depois que a configuração estiver concluída, defina o caminho.

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>Atualização do SSIS
Se você já tiver `mssql-server-is` instalado, você pode atualizar a versão mais recente com o seguinte comando:

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>Remover o SSIS
Para remover `mssql-server-is`, você pode executar o comando a seguir:
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> Instale o SSIS no RHEL
Para instalar o `mssql-server-is` do pacote no RHEL, siga estas etapas:

1. Baixe o arquivo de configuração de repositório do Microsoft SQL Server Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. Execute os seguintes comandos para instalar o SQL Server Integration Services.

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. Após a instalação, execute `ssis-conf`. Para obter mais informações, consulte [configurar o SSIS no Linux com o ssis-conf](sql-server-linux-configure-ssis.md).

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
Para remover `mssql-server-is`, você pode executar o comando a seguir:
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>Instalação autônoma
Para executar uma instalação autônoma quando você executa `ssis-conf setup`, faça o seguinte:
1.  Especifique o `-n` (nenhum prompt) opção.
2.  Forneça os valores necessários ao definir variáveis de ambiente.

O exemplo a seguir faz o seguinte:
-   Instala o SSIS.
-   Especifica a edição de desenvolvedor, fornecendo um valor para o `SSIS_PID` variável de ambiente.
-   Aceita o EULA, fornecendo um valor para o `ACCEPT_EULA` variável de ambiente.
-   Executa uma instalação autônoma, especificando o `-n` (nenhum prompt) opção.

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variáveis de ambiente para uma instalação autônoma

| Variável de ambiente | Descrição |
|---|---|
| **ACCEPT_EULA** | Aceita o contrato de licença do SQL Server quando definido como qualquer valor (por exemplo, `Y`).|
| **SSIS_PID** | Define a chave de produto ou edição do SQL Server. Aqui estão os valores possíveis:<br/>Evaluation<br/>Desenvolvedor<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>Uma chave do produto<br/><br/>Se você especificar uma chave do produto, a chave do produto deve estar no formato `#####-#####-#####-#####-#####`, onde `#` for uma letra ou um número.  |
| | |

## <a name="next-steps"></a>Próximas etapas

Para executar pacotes do SSIS no Linux, consulte [extração, transformação e carga de dados para SQL Server no Linux com o SSIS](sql-server-linux-migrate-ssis.md).

Para configurar as configurações adicionais do SSIS no Linux, consulte [configurar o SQL Server Integration Services no Linux com o ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre SSIS no Linux
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com o ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
-   [SQL Server Integration Services de agenda a execução no Linux com cron do pacote](sql-server-linux-schedule-ssis-packages.md)
