---
title: "Conectar-se a fontes de dados e compartilhamentos de arquivos com a Autenticação do Windows | Microsoft Docs"
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b84fdd15fa4a6393b2350aaf75985653b6273f31
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Conectar-se às fontes de dados e compartilhamentos de arquivo do Azure locais com a Autenticação do Windows
Este artigo descreve como configurar o catálogo do SSIS no Banco de Dados SQL do Azure para executar pacotes que usam a autenticação do Windows para se conectar a compartilhamentos de arquivos do Azure e fontes de dados locais. Você pode usar a autenticação do Windows para se conectar a fontes de dados na mesma rede virtual usada pelo Azure SSIS Integration Runtime, tanto localmente quanto em máquinas virtuais do Azure e em Arquivos do Azure.

As credenciais de domínio que você fornece ao seguir as etapas neste artigo se aplicam a todas as execuções de pacote na instância do Banco de Dados SQL até você alterar ou remover as credenciais.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Forneça credenciais de domínio para Autenticação do Windows
Para fornecer credenciais de domínio que permitem que os pacotes usam a autenticação do Windows para se conectar a fontes de dados locais, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS). Para obter mais informações, consulte [Conectar-se ao banco de dados do Catálogo do SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado a seguir e forneça credenciais de domínio apropriadas:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Executar seus pacotes SSIS. Os pacotes usam as credenciais que você forneceu para se conectar a fontes de dados locais com a Autenticação do Windows.

### <a name="view-domain-credentials"></a>Exibir credenciais de domínio
Para exibir as credenciais de domínio ativas, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado e verifique a saída:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>Limpar credenciais de domínio
Para limpar e remover as credenciais que você forneceu conforme descrito neste artigo, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-an-on-premises-sql-server"></a>Conecte-se a um SQL Server local
Para verificar se você pode se conectar a um SQL Server local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o seguinte comando para iniciar o SSMS (SQL Server Management Studio) com as credenciais de domínio que você deseja usar:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  No SSMS, verifique se você pode se conectar ao SQL Server local que você deseja usar.

### <a name="prerequisites"></a>Prerequisites
Para se conectar a um SQL Server local de um pacote em execução no Azure, você deve habilitar os seguintes pré-requisitos:

1.  No SQL Server Configuration Manager, habilite o protocolo TCP/IP.
2.  Permita o acesso pelo firewall do Windows. Para obter mais informações, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).
3.  Para se conectar com a Autenticação do Windows, certifique-se de que o Azure SSIS Integration Runtime pertence a uma rede virtual (VNet) que também inclui o SQL Server local.  Para obter mais informações, consulte [Unir um Azure-SSIS Integration Runtime a uma rede virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Em seguida, use `catalog.set_execution_credential` para fornecer credenciais, conforme descrito neste artigo.

## <a name="connect-to-an-on-premises-file-share"></a>Conectar-se a um compartilhamento de arquivos local
Para verificar se você pode se conectar a um compartilhamento de arquivos local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o comando a seguir. Este comando abre uma janela de prompt de comando com as credenciais de domínio que você deseja usar e, em seguida, testa a conectividade ao compartilhamento de arquivos obtendo uma listagem de diretórios.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Verifique se a listagem de diretórios é retornada para o compartilhamento de arquivos local que você deseja usar.

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>Conectar-se a um compartilhamento de arquivos em uma VM do Azure
Para se conectar a um compartilhamento de arquivos em uma máquina virtual do Azure, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado `catalog.set_execution_credential` conforme descrito nas seguintes opções:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Conectar-se a um compartilhamento de arquivos nos Arquivos do Azure
Para obter mais informações sobre o Arquivos do Azure, consulte [Arquivos do Azure](https://azure.microsoft.com/services/storage/files/).

Para se conectar a um compartilhamento de arquivos em um compartilhamento de arquivos do Azure, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado `catalog.set_execution_credential` conforme descrito nas seguintes opções:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Próximas etapas
- Implante um pacote. Para obter mais informações, consulte [Implantar um projeto do SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-deploy-ssms.md).
- Execute um pacote. Para obter mais informações, consulte [Executar um pacote SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-run-ssms.md).
- Agende um pacote. Para obter mais informações, consulte [Agendar execução de pacote SSIS no Azure](ssis-azure-schedule-packages.md).
