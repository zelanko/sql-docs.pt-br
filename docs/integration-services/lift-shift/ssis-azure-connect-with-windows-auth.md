---
title: Conectar-se a fontes de dados e compartilhamentos de arquivos com a Autenticação do Windows | Microsoft Docs
description: Saiba como configurar o Catálogo do SSIS no Banco de Dados SQL e o Tempo de Execução de Integração do Azure-SSIS para executar pacotes que se conectam a fontes de dados e compartilhamentos de arquivos com a Autenticação do Windows.
ms.date: 10/11/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 61d4d29b0dfc7fe67097c6cb61547c1c65dd79f1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411873"
---
# <a name="connect-to-data-sources-and-file-shares-with-windows-authentication-from-ssis-packages-in-azure"></a>Conectar-se a fontes de dados e a compartilhamentos de arquivos com a Autenticação do Windows de pacotes SSIS no Azure
Você pode usar a autenticação do Windows para se conectar a fontes de dados e compartilhamentos de arquivos na mesma rede virtual que o Azure SSIS IR (Integration Runtime), em máquinas virtuais locais/do Azure e em Arquivos do Azure. Há três métodos de se conectar a fontes de dados e compartilhamentos de arquivos com a Autenticação do Windows de pacotes SSIS em execução no Azure-SSIS IR:

| Método de conexão | Escopo efetivo | Etapa de configuração | Método de acesso em pacotes | Número de conjuntos de credenciais e recursos conectados | Tipo de recursos conectados | 
|---|---|---|---|---|---|
| Credenciais persistentes por meio do comando `cmdkey` | Por Azure-SSIS IR | Execute o comando `cmdkey` em um script de instalação personalizada (`main.cmd`) ao provisionar/reconfigurar o IR do Azure-SSIS, por exemplo, `cmdkey /add:fileshareserver /user:xxx /pass:yyy`.<br/><br/> Para saber mais, confira [Personalizar a instalação para o Azure-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup). | Acessar os recursos diretamente em pacotes por meio do caminho UNC, por exemplo,  `\\fileshareserver\folder` | Suporte a vários conjuntos de credenciais para diferentes recursos conectados | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server com Autenticação do Windows<br/><br/> - Outros recursos com Autenticação do Windows |
| Como configurar um contexto de execução de nível de catálogo | Por Azure-SSIS IR | Execute o procedimento armazenado `catalog.set_execution_credential` do SSISDB para configurar um contexto de "execução como".<br/><br/> Para saber mais, confira o restante deste artigo abaixo. | Acessar os recursos diretamente em pacotes | Suporte a apenas um conjunto de credenciais para todos os recursos conectados | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) <br/><br/> - SQL Server com Autenticação do Windows<br/><br/> - Outros recursos com Autenticação do Windows | 
| Montagem de unidades no tempo de execução do pacote (não persistência) | Por pacote | Execute o comando `net use` em Executar Processo de Tarefa, que será adicionado ao início do fluxo de controle em seus pacotes, por exemplo, `net use D: \\fileshareserver\sharename` | Acessar compartilhamentos de arquivos por meio de unidades mapeadas | Suporte a várias unidades para compartilhamentos de arquivos diferentes | - Compartilhamentos de arquivos no local/VMs do Azure<br/><br/> - Arquivos do Azure; confira [Usar um compartilhamento de arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows) |
|||||||

> [!WARNING]
> Se você não usar nenhum dos métodos acima para se conectar as fontes de dados e aos compartilhamentos de arquivos com a Autenticação do Windows, os pacotes que dependerem da Autenticação do Windows não poderão se conectar a eles e falharão em tempo de execução. 

O restante deste artigo descreve como configurar o catálogo do SSIS no Banco de Dados SQL do Azure para executar pacotes que usam a autenticação do Windows para se conectar a compartilhamentos de arquivos e a fontes de dados. 

## <a name="you-can-only-use-one-set-of-credentials"></a>Você só pode usar um conjunto de credenciais
Ao usar a autenticação do Windows em um pacote SSIS, você pode usar apenas um conjunto de credenciais em um pacote. As credenciais de domínio que você fornece ao seguir as etapas neste artigo se aplicam a todas as execuções de pacote, interativas ou agendadas, no Azure-SSIS IR até você alterar ou remover as credenciais. Se o pacote precisar se conectar a várias fontes de dados e compartilhamentos de arquivos com diferentes conjuntos de credenciais, talvez você precise considerar os métodos alternativos acima.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Forneça credenciais de domínio para Autenticação do Windows
Para fornecer credenciais de domínio que permitem que os pacotes usam a autenticação do Windows para se conectar a fontes de dados locais/compartilhamentos de arquivos, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS). Para obter mais informações, consulte [Conectar-se ao SSISDB (Catálogo do SSIS) no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado a seguir e forneça credenciais de domínio apropriadas:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Executar seus pacotes SSIS. Os pacotes usam as credenciais que você forneceu para se conectar a fontes de dados locais/compartilhamentos de arquivos com a Autenticação do Windows.

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
3.  Para se conectar com a Autenticação do Windows, verifique se seu Azure SSIS IR pertence a uma rede virtual que também inclui o SQL Server local.  Para obter mais informações, consulte [Unir um Azure-SSIS Integration Runtime a uma rede virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Em seguida, use `catalog.set_execution_credential` para fornecer credenciais, conforme descrito neste artigo.

## <a name="connect-to-an-on-premises-file-share"></a>Conectar-se a um compartilhamento de arquivos local
Para testar se você pode se conectar a um compartilhamento de arquivos local, faça o seguinte:

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

Para se conectar a um compartilhamento de arquivos em Arquivos do Azure, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado `catalog.set_execution_credential` conforme descrito nas seguintes opções:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Próximas etapas
- Implante um pacote. Para obter mais informações, consulte [Implantar um projeto do SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-deploy-ssms.md).
- Execute um pacote. Para obter mais informações, consulte [Executar um pacote SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-run-ssms.md).
- Agende um pacote. Para obter mais informações, confira [Agendar pacotes SSIS no Azure](ssis-azure-schedule-packages.md).
