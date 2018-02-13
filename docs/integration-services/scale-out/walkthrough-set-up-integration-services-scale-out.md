---
title: 'Passo a passo: Configurar o SQL Server Integration Services Scale Out | Microsoft Docs'
ms.description: This article walks you through the setup and configuration of SSIS Scale Out
ms.custom: 
ms.date: 12/13/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8abf2424f8bb1c9c8fb2e04d649e385dd30a024
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="walkthrough-set-up-integration-services-ssis-scale-out"></a>Passo a passo: Configurar o SSIS (Integration Services) Scale Out
Configure o SSIS ([!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]) Scale Out concluindo as tarefas a seguir. 

> [!TIP]
> Caso esteja instalando o Scale Out em um único computador, instale os recursos Mestre e Trabalho do Scale Out ao mesmo tempo. Quando você instala os recursos ao mesmo tempo, o ponto de extremidade é gerado automaticamente para se conectar ao Mestre de Expansão. 

* [Instalar o Mestre de Expansão](#InstallMaster)

* [Instalar o Trabalho de Expansão](#InstallWorker)

* [Instalar certificado de cliente do Trabalho de Expansão](#InstallCert)

* [Abrir porta do firewall](#Firewall)

* [Iniciar o serviço Mestre de Expansão e Trabalho de Expansão do SQL Server](#Start)

* [Habilitar o Mestre de Expansão](#EnableMaster)

* [Habilitar o modo de autenticação do SQL Server](#EnableAuth)

* [Habilitar o Trabalho de Expansão](#EnableWorker)

## <a name="InstallMaster"></a> Instalar o Mestre de Expansão

Para configurar o Mestre do Scale Out, você precisa instalar os Serviços de Mecanismo de Banco de Dados, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] e o recurso Mestre do Scale Out do SSIS ao configurar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. 

Para obter informações sobre como configurar o Mecanismo de Banco de Dados e o [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], consulte [Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md) e [Instalar o Integration Services](../install-windows/install-integration-services.md).

> [!NOTE]
> Para usar a conta de autenticação padrão do SQL Server para o log do Scale Out, selecione Modo Misto como o modo de autenticação na página **Configuração do Mecanismo de Banco de Dados** durante a instalação do Mecanismo de Banco de Dados. Consulte [Alterar a conta para log do Scale Out](change-logdb-account.md) para obter mais informações.

Para instalar o recurso Mestre do Scale Out, use o assistente de instalação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou o prompt de comando.

### <a name="install-scale-out-master-with-the-sql-server-installation-wizard"></a>Instalar o Mestre do Scale Out com o assistente de instalação do SQL Server
1.  Na página **Seleção de Recursos**, selecione **Mestre do Scale Out**, que está listado no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  
    ![Seleção de Recursos do Mestre](media/feature-select-master.PNG)
  
2.  Na página **Configuração do Servidor** , selecione a conta para executar o **serviço Mestre de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.  
    ![Configuração do servidor](media/server-config.PNG)

3.  Na página **Configuração do Mestre de Expansão do Integration Services** especifique o número da porta usada pelo Mestre de Expansão para se comunicar com o Mestre de Trabalho. O número da porta padrão é 8391.  

    ![Configuração do Mestre](media/master-config.PNG "Master Config")

4.  Especifique o certificado SSL usado para proteger a comunicação entre o Mestre e o Trabalho do Scale Out realizando um dos procedimentos a seguir.
    * Permita que o processo de instalação crie um certificado SSL padrão autoassinado clicando em **Criar um novo certificado SSL**.  O certificado padrão é instalado em Autoridades de Certificação Confiáveis, Computador Local. Você pode especificar os CNs nesse certificado. O nome do host do ponto de extremidade mestre deve ser incluído nos CNs. Por padrão, o nome do computador e o IP do Nó Mestre estão incluídos.
    * Selecione um Certificado SSL existente no computador local clicando em **Usar um certificado SSL existente** e, em seguida, clicando em **Procurar** para selecionar um certificado. A impressão digital do certificado é exibida na caixa de texto. Clicar em **Procurar** exibe os certificados que estão armazenados em Autoridades de Certificação Confiáveis, Computador Local. O certificado selecionado deve estar armazenado aqui.       

    ![Configuração do Mestre 2](media/master-config-2.PNG "Master Config 2")
  
5.  Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

### <a name="install-scale-out-master-from-the-command-prompt"></a>Instalar o Mestre do Scale Out por meio do prompt de comando

Siga as instruções em [Instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros para o Mestre do Scale Out seguindo estas etapas:
 
1.  Adicionar `IS_Master` ao parâmetro `/FEATURES`

2.  Configure o Mestre do Scale Out especificando os seguintes parâmetros e seus valores:
    -   `/ISMASTERSVCACCOUNT`
    -   `/ISMASTERSVCPASSWORD`
    -   `/ISMASTERSVCSTARTUPTYPE`
    -   `/ISMASTERSVCPORT`
    -   `/ISMasterSVCSSLCertCN` (opcional)
    -   `/ISMASTERSVCTHUMBPRINT` (opcional)

    > [!NOTE]
    > Se o Mestre do Scale Out não estiver instalado junto com o Mecanismo de Banco de Dados e a instância do Mecanismo de Banco de Dados for uma instância nomeada, você precisará configurar `SqlServerName` no arquivo de configuração de serviço do Mestre do Scale Out após a instalação. Para obter mais informações, consulte [Mestre do Scale Out](integration-services-ssis-scale-out-master.md).

## <a name="InstallWorker"></a> Instalar o Trabalho de Expansão
 
Para configurar o Trabalho do Scale Out, você precisa instalar o [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] e seu recurso Trabalho do Scale Out na instalação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Para instalar o recurso Trabalho do Scale Out, use o assistente de instalação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou o prompt de comando.

### <a name="install-scale-out-worker-with-the-sql-server-installation-wizard"></a>Instalar o Trabalho do Scale Out com o assistente de instalação do SQL Server

1.  Na página **Seleção de Recursos**, selecione **Trabalho do Scale Out**, que está listado no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

    ![Seleção de Recursos do Trabalho](media/feature-select-worker.PNG)

2.  Na página **Configuração do Servidor** , selecione a conta para executar o **serviço Trabalho de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.

    ![Configuração de servidor 2](media/server-config-2.PNG "Server Config 2")

3.  Na página de **Configuração de Trabalho de Expansão do Integration Services** especifique o ponto de extremidade para se conectar ao Mestre de Expansão. 

    - Para um ambiente de **um único computador**, o ponto de extremidade é gerado automaticamente quando o Mestre e o Trabalho do Scale Out são instalados ao mesmo tempo. 

    - Para um ambiente de **vários computadores**, o ponto de extremidade consiste no nome ou IP do computador com o Mestre do Scale Out instalado e o número da porta especificado durante a instalação do Mestre do Scale Out.
   
    ![Configuração do Trabalho 1](media/worker-config.PNG "Worker Config 1")    

    > [!NOTE]
    > Também é possível ignorar a configuração do Trabalho neste momento e associar o Trabalho do Scale Out ao Mestre do Scale Out usando o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md) após a instalação.

4. Para um ambiente de **vários computadores**, especifique o certificado SSL do cliente usado para validar o Mestre do Scale Out. Para um ambiente de **um único computador**, não é necessário especificar um certificado SSL do cliente. 
  
    Clique em **Procurar** para localizar o arquivo de certificado (*.cer). Para usar o certificado SSL padrão, selecione o arquivo `SSISScaleOutMaster.cer` localizado em `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` no computador em que o Mestre do Scale Out está instalado.   

    ![Configuração do Trabalho 2](media/worker-config-2.PNG "Worker Config 2")

    > [!NOTE]
    > Quando o certificado SSL usado pelo Mestre do Scale Out for autoassinado, um certificado SSL do cliente correspondente precisará ser instalado no computador com o Trabalho do Scale Out. Se você fornecer o caminho do arquivo para o Certificado SSL do cliente na página **Configuração de Trabalho do Integration Services Scale Out**, o certificado será instalado automaticamente; caso contrário, você precisará instalá-lo manualmente mais tarde. 
     
5. Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

### <a name="install-scale-out-worker-from-the-command-prompt"></a>Instalar o Trabalho do Scale Out por meio do prompt de comando

Siga as instruções em [Instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros para o Trabalho do Scale Out seguindo estas etapas:

1.  Adicione IS_Worker ao parâmetro `/FEATURES`.

2. Configure o Trabalho do Scale Out especificando os seguintes parâmetros e seus valores:
    -   `/ISWORKERSVCACCOUNT`
    -   `/ISWORKERSVCPASSWORD`
    -   `/ISWORKERSVCSTARTUPTYPE`
    -   `/ISWORKERSVCMASTER` (opcional)
    -   `/ISWORKERSVCCERT` (opcional)
 
## <a name="InstallCert"></a> Instalar certificado de cliente do Trabalho de Expansão

Durante a instalação do Trabalho do Scale Out, um certificado de trabalho é criado automaticamente e instalado no computador. Além disso, um certificado do cliente correspondente, SSISScaleOutWorker.cer, é instalado em `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn`. Para que o Mestre do Scale Out autentique o Trabalho do Scale Out, é necessário adicionar esse certificado do cliente ao repositório Raiz do computador local com o Mestre do Scale Out.
  
Para adicionar o certificado do cliente ao repositório Raiz, clique duas vezes no arquivo .cer e, em seguida, clique em **Instalar Certificado** na caixa de diálogo Certificado. O **Assistente para Importação de Certificados** será aberto.  

## <a name="Firewall"></a> Abrir porta do firewall

No computador do Mestre do Scale Out, abra a porta especificada durante a instalação do Mestre do Scale Out e a porta do SQL Server (1433, por padrão) no Firewall do Windows.

> [!Note]
> Depois de abrir a porta do firewall, você também precisa reiniciar o serviço Trabalho do Scale Out.
    
## <a name="Start"></a> Iniciar os serviços Mestre de Expansão e Trabalho de Expansão do SQL Server

Se você não definir o tipo de inicialização dos serviços como **Automático** durante a instalação, inicie os seguintes serviços:

-   Mestre do SQL Server Integration Services Scale Out 14.0 (SSISScaleOutMaster140S)

-   Trabalho do SQL Server Integration Services Scale Out 14.0 (SSISScaleOutWorker140)

## <a name="EnableMaster"></a> Habilitar o Mestre de Expansão

Ao criar o catálogo do SSISDB no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)], selecione **Habilitar este servidor como mestre do SSIS Scale Out** na caixa de diálogo **Criar Catálogo**.

Depois que o catálogo for criado, habilite o Mestre do Scale Out com o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md).

## <a name="EnableAuth"></a> Habilitar o modo de autenticação do SQL Server
Se você não habilitou a autenticação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] durante a instalação do Mecanismo de Banco de Dados, habilite o modo de autenticação do SQL Server na instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que hospeda o catálogo do SSISDB. 

A execução de pacote não é bloqueada quando a autenticação do SQL Server está desabilitada. No entanto, o log de execução não pode ser gravado no banco de dados SSISDB.

## <a name="EnableWorker"></a> Habilitar o Trabalho de Expansão

Habilite o Trabalho do Scale Out com o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md), que fornece uma interface gráfica do usuário ou com um procedimento armazenado.

Para habilitar um Trabalho do Scale Out com um procedimento armazenado, execute o procedimento armazenado `[catalog].[enable_worker_agent]` com **WorkerAgentId** como o parâmetro. 

Obtenha o valor **WorkerAgentId** na exibição `[catalog].[worker_agents]` do SSISDB depois que o Trabalho do Scale Out for registrado no Mestre do Scale Out. O registro leva alguns minutos depois que os serviços Mestre e Trabalho do Scale Out são iniciados.

#### <a name="example"></a>Exemplo
O exemplo a seguir habilita o Trabalho do Scale Out em `computerA`.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="next-steps"></a>Próximas etapas
-   [Executar pacotes no SSIS (Integration Services) Scale Out](run-packages-in-integration-services-ssis-scale-out.md).
