---
title: "Conecte-se a fontes de dados local com a autenticação do Windows | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 25113093ccd068a9afe661e160ae3319025b7534
ms.contentlocale: pt-br
ms.lasthandoff: 09/25/2017

---
# <a name="connect-to-on-premises-data-sources-with-windows-authentication"></a>Conecte-se a fontes de dados local com a autenticação do Windows
Este artigo descreve como configurar o catálogo do SSIS no banco de dados SQL Azure para executar pacotes que usam a autenticação do Windows para se conectar a fontes de dados local.

As credenciais de domínio que você fornecer ao seguir as etapas neste artigo se aplicam a todas as execuções de pacote na instância do banco de dados SQL até você alterar ou remove as credenciais.

## <a name="prerequisite"></a>Pré-requisito
Antes de configurar as credenciais de domínio para autenticação do Windows, verifique se um computador ingressado no domínio pode se conectar às suas fontes de dados locais no `runas` modo. Por exemplo, para verificar se você pode se conectar a um SQL Server no local, siga estas etapas:

1.  Para executar esse teste, localizar um computador ingressado no domínio.

2.  No computador ingressado no domínio, execute o seguinte comando para iniciar o SQL Server Management Studio (SSMS) com as credenciais de domínio que você deseja usar:

   ```cmd
   runas.exe /netonly /user:<domain>\<username> SSMS.exe
   ```

3.  No SSMS, verifique se você pode se conectar ao SQL Server no local que você deseja usar.

## <a name="provide-domain-credentials"></a>Forneça credenciais de domínio
Para fornecer credenciais de domínio que permitem que os pacotes usam a autenticação do Windows para se conectar a fontes de dados local, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao banco de dados SQL que hospeda o banco de dados do catálogo do SSIS (SSISDB). Para obter mais informações, consulte [conectar-se ao banco de dados de catálogo do SSISDB no Azure](ssis-azure-connect-to-catalog-database.md).

2.  Com o SSISDB do banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado e fornecer credenciais de domínio apropriado:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  Execute os pacotes do SSIS. Os pacotes usam as credenciais que você forneceu para se conectar a fontes de dados locais com a autenticação do Windows.

## <a name="view-domain-credentials"></a>Credenciais de domínio de modo de exibição
Para exibir as credenciais de domínio do active, siga estas etapas:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao banco de dados SQL que hospeda o banco de dados do catálogo do SSIS (SSISDB).

2.  Com o SSISDB do banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado e verifique a saída:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

## <a name="clear-domain-credentials"></a>Credenciais de domínio limpar
Para limpar e remover as credenciais que você forneceu conforme descrito neste artigo, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao banco de dados SQL que hospeda o banco de dados do catálogo do SSIS (SSISDB).

2.  Com o SSISDB do banco de dados atual, abra uma janela de consulta.

3.  Execute o seguinte procedimento armazenado:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="next-steps"></a>Próximas etapas
- Implante um pacote. Para obter mais informações, consulte [implantar um projeto do SSIS com o SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Execute um pacote. Para obter mais informações, consulte [executar um pacote do SSIS com o SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Agende um pacote. Para obter mais informações, consulte [SSIS de agendamento de execução de pacote no Azure](ssis-azure-schedule-packages.md)

