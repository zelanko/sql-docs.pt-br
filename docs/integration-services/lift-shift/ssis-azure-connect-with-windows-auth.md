---
title: "Conectar-se às fontes de dados e compartilhamentos de arquivo do Azure locais com a Autenticação do Windows | Microsoft Docs"
ms.date: 09/25/2017
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
ms.openlocfilehash: 9235ffd3225e76ee94067519c72e997c451d9893
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Conectar-se às fontes de dados e compartilhamentos de arquivo do Azure locais com a Autenticação do Windows
Este artigo descreve como configurar o catálogo do SSIS no Banco de Dados SQL do Azure para executar pacotes que usam a autenticação do Windows para se conectar a compartilhamentos de arquivos do Azure e fontes de dados locais.

As credenciais de domínio que você fornece ao seguir as etapas neste artigo se aplicam a todas as execuções de pacote na instância do Banco de Dados SQL até você alterar ou remover as credenciais.

## <a name="connect-to-on-premises-data-sources"></a>Conectar-se a fontes de dados locais

### <a name="prerequisite"></a>Pré-requisito
Antes de configurar as credenciais de domínio para Autenticação do Windows, verifique se um computador não ingressado no domínio pode se conectar à fonte de dados local no modo `runas`.

#### <a name="connecting-to-sql-server"></a>Conectar-se ao SQL Server
Para verificar se você pode se conectar a um SQL Server local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o seguinte comando para iniciar o SSMS (SQL Server Management Studio) com as credenciais de domínio que você deseja usar:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  No SSMS, verifique se você pode se conectar ao SQL Server local que você deseja usar.

#### <a name="connecting-to-a-file-share"></a>Conectar-se a um compartilhamento de arquivos
Para verificar se você pode se conectar a um compartilhamento de arquivos local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o comando a seguir. Este comando abre uma janela de prompt de comando com as credenciais de domínio que você deseja usar e, em seguida, testa a conectividade ao compartilhamento de arquivos obtendo uma listagem de diretórios.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Verifique se a listagem de diretórios é retornada para o compartilhamento de arquivos local que você deseja usar.

### <a name="provide-domain-credentials"></a>Fornecer credenciais de domínio
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

## <a name="connect-to-file-shares"></a>Conectar-se a compartilhamentos de arquivos
Você pode usar a Autenticação do Windows para se conectar a compartilhamentos de arquivos na mesma rede virtual usada pelo Azure SSIS Integration Runtime, tanto localmente quanto em máquinas virtuais do Azure e em Arquivos do Azure. Para obter mais informações sobre o Arquivos do Azure, consulte [Arquivos do Azure](https://azure.microsoft.com/services/storage/files/).

Para se conectar a um compartilhamento de arquivos em uma máquina virtual do Azure ou compartilhamento de arquivos do Azure, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado `catalog.set_execution_credential` conforme descrito nas seguintes opções:

    a.  Para se conectar a um compartilhamento de arquivos em uma máquina virtual do Azure, execute o seguinte procedimento armazenado:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

    b.  Para se conectar a um compartilhamento de arquivos do Azure (ou seja, em Arquivos do Azure), execute o seguinte procedimento armazenado:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Próximas etapas
- Implante um pacote. Para obter mais informações, consulte [Implantar um projeto do SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-deploy-ssms.md).
- Execute um pacote. Para obter mais informações, consulte [Executar um pacote SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-run-ssms.md).
- Agende um pacote. Para obter mais informações, consulte [Agendar execução de pacote SSIS no Azure](ssis-azure-schedule-packages.md).
