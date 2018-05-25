---
title: Instalar o SQL Server Integration Services no Linux | Microsoft Docs
description: Este artigo descreve como instalar o SQL Server Integration Services (SSIS) no Linux.
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: d2e72c77ad5f200c07a6e71025a3461d6397032a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar o SQL Server Integration Services (SSIS) no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Siga as etapas neste artigo para instalar o SQL Server Integration Services (`mssql-server-is`) no Linux. Para obter informações sobre os recursos com suporte nesta versão dos serviços de integração para Linux, consulte o [notas de versão](sql-server-linux-release-notes.md).

Instale servidores de integração do SQL Server para sua plataforma:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> Instalar o SSIS no Ubuntu
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
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> Instalar o SSIS em RHEL
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

## <a name="unattended-installation"></a>Instalação autônoma
Para executar uma instalação autônoma quando você executa `ssis-conf setup`, faça o seguinte:
1.  Especifique o `-n` (nenhum prompt) opção.
2.  Fornece valores necessários definindo variáveis de ambiente.

O exemplo a seguir faz o seguinte:
-   Instala o SSIS.
-   Especifica a edição de desenvolvedor, fornecendo um valor para o `SSIS_PID` variável de ambiente.
-   Aceita o EULA, fornecendo um valor para o `ACCEPT_EULA` variável de ambiente.
-   Executa uma instalação autônoma, especificando o `-n` (nenhum prompt) opção.

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>Variáveis de ambiente para uma instalação autônoma

| Variável de ambiente | Description |
|---|---|
| **ACCEPT_EULA** | Aceita o contrato de licença do SQL Server quando definido como qualquer valor (por exemplo, `Y`).|
| **SSIS_PID** | Define a chave de produto ou edição do SQL Server. Aqui estão os valores possíveis:<br/>Evaluation<br/>Desenvolvedor<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>Uma chave do produto<br/><br/>Se você especificar uma chave do produto, a chave do produto deve estar no formato `#####-#####-#####-#####-#####`, onde `#` é uma letra ou um número.  |
| | |

## <a name="next-steps"></a>Próximas etapas

Para executar pacotes SSIS no Linux, consulte [extrair, transformar e carregar dados para o SQL Server no Linux com o SSIS](sql-server-linux-migrate-ssis.md).

Para definir configurações adicionais de SSIS no Linux, consulte [configurar o SQL Server Integration Services no Linux com o ssis conf](sql-server-linux-configure-ssis.md).

## <a name="related-content-about-ssis-on-linux"></a>Conteúdo relacionado sobre SSIS no Linux
-   [Extrair, transformar e carregar dados em Linux com o SSIS](sql-server-linux-migrate-ssis.md)
-   [Configurar o SQL Server Integration Services no Linux com conf ssis](sql-server-linux-configure-ssis.md)
-   [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md)
-   [A execução no Linux com cron do pacote de agendamento SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
