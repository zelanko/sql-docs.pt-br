---
title: Instalar o SQL Server Integration Services no Linux | Microsoft Docs
description: "Este tópico descreve como instalar o SQL Server Integration Services no Linux."
author: leolimsft
ms.author: lle
manager: craigg
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c3943870ec10b8430ac4819398908c5459a8b03c
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Instalar o SQL Server Integration Services (SSIS) no Linux


Siga as etapas neste artigo para instalar o SQL Server Integration Services (`mssql-server-is`) no Linux. Para obter informações sobre os recursos com suporte nesta versão dos serviços de integração para Linux, consulte o [notas de versão](sql-server-linux-release-notes.md).

Instale servidores de integração do SQL Server para sua plataforma:

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)



## <a name="ubuntu"></a>Instalar o SSIS no Ubuntu
Para instalar o `mssql-server-is` pacote no Ubuntu, siga estas etapas:


1.  Importe as chaves GPG repositório público.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```


2.  Registre o repositório do Microsoft SQL Server Ubuntu.

    ```bash
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
    ```


3.  Execute os comandos a seguir para instalar o SQL Server Integration Services.

    ```bash
    sudo apt-get update
    sudo apt-get install -y mssql-server-is
    ```


4.  Depois de instalar o Integration Services, execute `ssis-conf`.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


5.  Após a configuração, defina o caminho.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


Se você já tiver `mssql-server-is` instalado, você pode atualizar a versão mais recente com o seguinte comando:

```bash
sudo apt-get install mssql-server-is
```


Para remover `mssql-server-is`, você pode executar o seguinte comando:
```bash
sudo apt-get remove msssql-server-is
```



## <a name="RHEL"></a>Instalar o SSIS em RHEL
Para instalar o `mssql-server-is` o pacote em RHEL, siga estas etapas:


1.  Entre no modo de superusuário.

    ```bash
    sudo su
    ```


2.  Baixe o arquivo de configuração de repositório do Microsoft SQL Server Red Hat.

    ```bash
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
    ```


3.  Sair do modo de superusuário.

    ```bash
    exit
    ```


4.  Execute os comandos a seguir para instalar o SQL Server Integration Services.

    ```bash
    sudo yum install -y mssql-server-is
    ```


5.  Após a instalação, execute `ssis-conf`.

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


6.  Quando a configuração estiver concluída, defina o caminho.

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


Se você já tiver `mssql-server-is` instalado, você pode atualizar a versão mais recente com o seguinte comando:

```bash
sudo yum update mssql-server-is
```


Para remover `mssql-server-is`, você pode executar o seguinte comando:
```bash
sudo yum remove msssql-server-is
```




## <a name="run-a-package"></a>Executar um pacote
Copie o pacote do SSIS para o computador Linux. Em seguida, use o seguinte comando para executar o pacote.

```bash
dtexec /F <package name> /DE <protection password>
```



## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o SSIS para extrair, transformar e carregar dados no Linux, consulte [extrair, transformar e carregar dados para o SQL Server no Linux com o SSIS](sql-server-linux-migrate-ssis.md).
