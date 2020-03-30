---
title: Acessar armazenamentos de dados e compartilhamentos de arquivos com a autenticação do Windows | Microsoft Docs
description: Saiba como configurar o Catálogo do SSIS no Banco de Dados SQL e o Azure-SSIS Integration Runtime no Azure Data Factory para executar pacotes que se acessam armazenamento de dados e compartilhamentos de arquivos com a Autenticação do Windows.
ms.date: 3/22/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 009a65c7c4381440dd7af6bb627fe2db70a16918
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68007956"
---
# <a name="access-data-stores-and-file-shares-with-windows-authentication-from-ssis-packages-in-azure"></a>Acessar armazenamentos de dados e compartilhamentos de arquivos com a Autenticação do Windows de pacotes SSIS no Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Você pode usar a Autenticação do Windows para acessar armazenamentos de dados, como SQL Servers, compartilhamentos de arquivos, Arquivos do Azure etc. em pacotes SSIS em execução no seu Azure-SSIS IR (Integration Runtime) no ADF (Azure Data Factory). Seus armazenamentos de dados podem estar no local, hospedados em VMs (máquinas virtuais) do Azure ou em execução no Azure como serviços gerenciados. Se eles estiverem no local, você precisará vincular o Azure-SSIS IR a uma rede virtual (VNet) conectada à sua rede local; confira [Vincular o Azure-SSIS IR a uma VNet](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Há quatro métodos para acessar armazenamentos de dados com a Autenticação do Windows em pacotes SSIS em execução no Azure-SSIS IR:

| Método de conexão | Escopo efetivo | Etapa de configuração | Método de acesso em pacotes | Número de conjuntos de credenciais e recursos conectados | Tipo de recursos conectados | 
|---|---|---|---|---|---|
| Como configurar um contexto de execução no nível da atividade | Por atividade Executar pacote do SSIS | Configure a propriedade **Autenticação do Windows** para definir um contexto de "Execução/Executar como" ao executar o pacotes SSIS como atividades Executar pacote SSIS em pipelines do ADF.<br/><br/> Confira mais informações em [Configurar a atividade Executar pacote SSIS](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity). | Acesse recursos diretamente em pacotes por meio do caminho UNC, por exemplo, se você usar compartilhamentos de arquivos ou arquivos do Azure: `\\YourFileShareServerName\YourFolderName` ou `\\YourAzureStorageAccountName.file.core.windows.net\YourFolderName` | Suporte a apenas um conjunto de credenciais para todos os recursos conectados | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> – SQL Servers no local/VMs Azure com a autenticação do Windows<br/><br/> – Outros recursos com Autenticação do Windows |
| Como configurar um contexto de execução de nível de catálogo | Por Azure-SSIS IR, mas será substituído quando também houver a configuração de um contexto de execução no nível da atividade (veja acima) | Execute o procedimento armazenado `catalog.set_execution_credential` do SSISDB para configurar um contexto de "Execução/Executar como".<br/><br/> Para saber mais, confira o restante deste artigo abaixo. | Acesse recursos diretamente em pacotes por meio do caminho UNC, por exemplo, se você usar compartilhamentos de arquivos ou arquivos do Azure: `\\YourFileShareServerName\YourFolderName` ou `\\YourAzureStorageAccountName.file.core.windows.net\YourFolderName` | Suporte a apenas um conjunto de credenciais para todos os recursos conectados | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> – SQL Servers no local/VMs Azure com a autenticação do Windows<br/><br/> – Outros recursos com Autenticação do Windows |
| Credenciais persistentes por meio do comando `cmdkey` | Por Azure-SSIS IR, mas será substituído quando também houver a configuração de um contexto de execução no nível da atividade/catálogo (veja acima) | Execute o comando `cmdkey` em um script de instalação personalizada (`main.cmd`) ao provisionar/reconfigurar o IR do Azure-SSIS, por exemplo, se você usar compartilhamentos de arquivos ou arquivos do Azure: `cmdkey /add:YourFileShareServerName /user:YourDomainName\YourUsername /pass:YourPassword` ou `cmdkey /add:YourAzureStorageAccountName.file.core.windows.net /user:azure\YourAzureStorageAccountName /pass:YourAccessKey`.<br/><br/> Para saber mais, confira [Personalizar a instalação para o Azure-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup). | Acesse recursos diretamente em pacotes por meio do caminho UNC, por exemplo, se você usar compartilhamentos de arquivos ou arquivos do Azure: `\\YourFileShareServerName\YourFolderName` ou `\\YourAzureStorageAccountName.file.core.windows.net\YourFolderName` | Suporte a vários conjuntos de credenciais para diferentes recursos conectados | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> – SQL Servers no local/VMs Azure com a autenticação do Windows<br/><br/> – Outros recursos com Autenticação do Windows |
| Montagem de unidades no tempo de execução do pacote (não persistente) | Por pacote | Execute o comando `net use` em Executar Processo de Tarefa, que será adicionado ao início do fluxo de controle em seus pacotes, por exemplo, `net use D: \\YourFileShareServerName\YourFolderName` | Acessar compartilhamentos de arquivos por meio de unidades mapeadas | Suporte a várias unidades para compartilhamentos de arquivos diferentes | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) |
|||||||

> [!WARNING]
> Se você não usar nenhum dos métodos acima para acessar armazenamentos de dados com a Autenticação do Windows, os pacotes que dependerem da Autenticação do Windows não poderão acessá-los e falharão no tempo de execução. 

O restante deste artigo descreve como configurar o catálogo do SSIS (SSISDB) hospedado no servidor de Banco de Dados SQL do Azure/Instância gerenciada para executar pacotes no Azure-SSIS IR que usam a Autenticação do Windows para acessar armazenamentos de dados. 

## <a name="you-can-only-use-one-set-of-credentials"></a>Você só pode usar um conjunto de credenciais
Ao usar a autenticação do Windows em um pacote SSIS, você pode usar apenas um conjunto de credenciais. As credenciais de domínio que você fornece ao seguir as etapas neste artigo se aplicam a todas as execuções de pacote, interativas ou agendadas, no Azure-SSIS IR até você alterá-las ou removê-las. Se o pacote precisar se conectar a vários armazenamentos de dados com diferentes conjuntos de credenciais, considere os métodos alternativos acima.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Forneça credenciais de domínio para Autenticação do Windows
Para fornecer credenciais de domínio que permitem que os pacotes usam a autenticação do Windows para acessar armazenamentos de dados locais, faça o seguinte:

1.  Com o SSMS (SQL Server Management Studio) ou outra ferramenta, conecte-se ao servidor do Banco de Dados SQL do Azure/Instância gerenciada que hospeda o SSISDB. Confira mais informações em [Conectar ao SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado a seguir e forneça credenciais de domínio apropriadas:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Executar seus pacotes SSIS. Os pacotes usarão as credenciais que você forneceu para acessar armazenamentos de dados no local com a Autenticação do Windows.

### <a name="view-domain-credentials"></a>Exibir credenciais de domínio
Para exibir as credenciais de domínio ativas, faça o seguinte:

1.  Com o SSMS ou outra ferramenta, conecte-se ao servidor do Banco de Dados SQL do Azure/Instância gerenciada que hospeda o SSISDB. Confira mais informações em [Conectar ao SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado e verifique a saída:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>Limpar credenciais de domínio
Para limpar e remover as credenciais que você forneceu conforme descrito neste artigo, faça o seguinte:

1.  Com o SSMS ou outra ferramenta, conecte-se ao servidor do Banco de Dados SQL do Azure/Instância gerenciada que hospeda o SSISDB. Confira mais informações em [Conectar ao SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-a-sql-server-on-premises"></a>Conectar a um SQL Server local 
Para verificar se você pode se conectar a um SQL Server local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o seguinte comando para iniciar o SSMS com as credenciais de domínio que você deseja usar:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  No SSMS, verifique se você pode se conectar ao SQL Server local.

### <a name="prerequisites"></a>Prerequisites
Para acessar um SQL Server local nos pacotes em execução no Azure, faça o seguinte:

1.  No SQL Server Configuration Manager, habilite o protocolo TCP/IP.
2.  Permita o acesso pelo firewall do Windows. Confira mais informações em [Configurar o firewall do Windows para acessar o SQL Server](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).
3.  Vincule o Azure-SSIS IR a uma VNet conectada ao SQL Server local.  Confira mais informações em [Vincular o Azure-SSIS IR a uma VNet](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Use o procedimento armazenado `catalog.set_execution_credential` do SSISDB para fornecer credenciais, conforme descrito neste artigo.

## <a name="connect-to-a-file-share-on-premises"></a>Conectar-se a um compartilhamento de arquivos no local 
Para verificar se você pode se conectar a um compartilhamento de arquivos local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o comando a seguir. Esses comandos abrem uma janela de prompt de comando com as credenciais de domínio que você deseja usar e, em seguida, testam a conectividade ao compartilhamento de arquivos local obtendo uma listagem de diretórios.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Verifique se a listagem de diretórios é retornada para o compartilhamento de arquivos local.

### <a name="prerequisites"></a>Prerequisites
Para acessar um compartilhamento de arquivo local nos pacotes em execução no Azure, faça o seguinte:

1.  Permita o acesso pelo firewall do Windows.
2.  Vincule o Azure-SSIS IR a uma VNet conectada ao compartilhamento de arquivo local.  Confira mais informações em [Vincular o Azure-SSIS IR a uma VNet](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
3.  Use o procedimento armazenado `catalog.set_execution_credential` do SSISDB para fornecer credenciais, conforme descrito neste artigo.

## <a name="connect-to-a-file-share-on-azure-vm"></a>Conectar-se a um compartilhamento de arquivos em uma VM do Azure
Para acessar um compartilhamento de arquivo na VM do Azure nos pacotes em execução no Azure, faça o seguinte:

1.  Com o SSMS ou outra ferramenta, conecte-se ao servidor do Banco de Dados SQL do Azure/Instância gerenciada que hospeda o SSISDB. Confira mais informações em [Conectar ao SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado a seguir e forneça credenciais de domínio apropriadas:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Conectar-se a um compartilhamento de arquivos nos Arquivos do Azure
Para obter mais informações sobre o Arquivos do Azure, consulte [Arquivos do Azure](https://azure.microsoft.com/services/storage/files/).

Para acessar um compartilhamento de arquivo nos Arquivos do Azure nos pacotes em execução no Azure, faça o seguinte:

1.  Com o SSMS ou outra ferramenta, conecte-se ao servidor do Banco de Dados SQL do Azure/Instância gerenciada que hospeda o SSISDB. Confira mais informações em [Conectar ao SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado a seguir e forneça credenciais de domínio apropriadas:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Próximas etapas
- Implante seus pacotes. Confira mais informações em [Implantar um projeto do SSIS no Azure com o SSMS](../ssis-quickstart-deploy-ssms.md).
- Execute os pacotes. Confira mais informações em [Executar pacotes SSIS no Azure com o SSMS](../ssis-quickstart-run-ssms.md).
- Agende seus pacotes. Para obter mais informações, confira [Agendar pacotes SSIS no Azure](ssis-azure-schedule-packages.md).
