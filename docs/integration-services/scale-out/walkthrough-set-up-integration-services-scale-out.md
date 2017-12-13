---
title: 'Passo a passo: Configurar o SQL Server Integration Services Scale Out | Microsoft Docs'
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec9744a1efb0e78aca55e85e7f9f3eca007de5a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>Passo a passo: configurar a Expansão do Integration Services
Configure o [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] Scale Out concluindo as tarefas a seguir. 

> [!NOTE]
> Se estiver instalando o Scale Out em um computador, instale os recursos de Mestre e Trabalho do Scale Out ao mesmo tempo. Quando você instala os recursos ao mesmo tempo, o ponto de extremidade é gerado automaticamente para se conectar ao Mestre de Expansão. 

* [Instalar o Mestre de Expansão](#InstallMaster)

* [Instalar o Trabalho de Expansão](#InstallWorker)

* [Instalar certificado de cliente do Trabalho de Expansão](#InstallCert)

* [Abrir porta do firewall](#Firewall)

* [Iniciar o serviço Mestre de Expansão e Trabalho de Expansão do SQL Server](#Start)

* [Habilitar o Mestre de Expansão](#EnableMaster)

* [Habilitar o modo de autenticação do SQL Server](#EnableAuth)

* [Habilitar o Trabalho de Expansão](#EnableWorker)

## <a name="InstallMaster"></a> Instalar o Mestre de Expansão

Para habilitar a funcionalidade de Mestre do Scale Out, você deve instalar os Serviços do Mecanismo de Banco de Dados, o [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] e seu recurso de Mestre do Scale Out ao configurar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. 

Para obter informações sobre como configurar os Serviços de Mecanismo de Banco de Dados e [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], consulte [Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md), e [Instalar o Integration Services](../install-windows/install-integration-services.md).
> [!NOTE]
> Para usar a conta de autenticação padrão do SQL para log do Scale Out, selecione o Modo Misto para o modo de autenticação na página Configuração do Mecanismo de Banco de Dados durante a instalação do Mecanismo de Banco de Dados. Consulte [Alterar a conta para log do Scale Out](change-logdb-account.md) para obter mais informações.

**Para instalar o recurso Mestre de Expansão, use o Assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou o prompt de comando.**

- Etapas para o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  Na página **Seleção de Recursos**, selecione **Mestre do Scale Out**, que está listado no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Mestre de Seleção de Recurso](media/feature-select-master.PNG)
  
  2.  Na página **Configuração do Servidor** , selecione a conta para executar o **serviço Mestre de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.  
  ![Configuração do servidor](media/server-config.PNG)
  3.  Na página **Configuração do Mestre de Expansão do Integration Services** especifique o número da porta usada pelo Mestre de Expansão para se comunicar com o Mestre de Trabalho. O número da porta padrão é 8391.  
  ![Configuração do Mestre](media/master-config.PNG "Master Config")
  4.  Especifique o certificado SSL usado para proteger a comunicação entre o Mestre e o Trabalho do Scale Out realizando um dos procedimentos a seguir.
    * Permita que o processo de instalação crie um certificado SSL padrão autoassinado clicando em **Criar um novo certificado SSL**.  O certificado padrão é instalado em Autoridades de Certificação Confiáveis, Computador Local. Você pode especificar os CNs nesse certificado. O nome do host do ponto de extremidade mestre deve ser incluído nos CNs. Por padrão, o nome do computador e o IP do Nó Mestre estão incluídos.
    * Selecione um Certificado SSL existente no computador local clicando em **Usar um certificado SSL existente** e, em seguida, clicando em **Procurar** para selecionar um certificado. A impressão digital do certificado é exibida na caixa de texto. Clicar em **Procurar** exibe os certificados que estão armazenados em Autoridades de Certificação Confiáveis, Computador Local. O certificado selecionado deve estar armazenado aqui.       
![Configuração do Mestre 2](media/master-config-2.PNG "Master Config 2")
  5.  Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Etapas do prompt de comando

    Siga as instruções em [Instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros relacionados ao Mestre de Expansão, fazendo o seguinte.
  1.  Adicione IS_Master no parâmetro /FEATURES
  2.  Configure a Mestre do Scale Out especificando os seguintes parâmetros e seus valores: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN (opcional), /ISMASTERSVCTHUMBPRINT (opcional).

> [!Note]
> Se o Mestre do Scale Out não estiver instalado junto com o Mecanismo de Banco de Dados e o Mecanismo de Banco de Dados for uma instância nomeada, você precisará configurar SqlServerName no arquivo de configuração de serviço Mestre do Scale Out após a instalação. Consulte [Mestre do Scale Out](integration-services-ssis-scale-out-master.md) para obter detalhes.

## <a name="InstallWorker"></a> Instalar o Trabalho de Expansão
 
Para habilitar a funcionalidade de Trabalho de Expansão, você deve instalar [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] e seu recurso de Trabalho de Expansão na instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

**Para instalar o recurso Trabalho de Expansão, use o Assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou o prompt de comando.**

- Etapas para o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  Na página **Seleção de Recursos**, selecione **Trabalho do Scale Out**, que está listado no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Trabalho de Seleção de Recurso](media/feature-select-worker.PNG)
  2. Na página **Configuração do Servidor** , selecione a conta para executar o **serviço Trabalho de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.    
  ![Configuração de servidor 2](media/server-config-2.PNG "Server Config 2")
  3. Na página de **Configuração de Trabalho de Expansão do Integration Services** especifique o ponto de extremidade para se conectar ao Mestre de Expansão. 
      > [!Note]
      > Ignore a configuração do Nó de Trabalho (etapas 3 e 4) aqui e associe o Trabalho do Scale Out ao Mestre do Scale Out com o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md) após a instalação.

    - Para um ambiente de **um computador**, o ponto de extremidade é gerado automaticamente quando o Mestre do Scale Out e o Trabalho do Scale Out são instalados ao mesmo tempo. 
    - Para um ambiente de **vários computadores**, o ponto de extremidade consiste no nome ou IP do computador com o Mestre do Scale Out instalado e o número da porta especificado durante a instalação do Mestre do Scale Out.    
   ![Configuração do Trabalho 1](media/worker-config.PNG "Worker Config 1")    

  4. Para um ambiente de **vários computadores**, especifique o certificado SSL do cliente que é usado para validar o Mestre do Scale Out. Para um ambiente de **um computador**, não é necessário especificar o certificado SSL do cliente. 
  
     > [!NOTE]
     > Quando o certificado SSL usado pelo Mestre do Scale Out é autoassinado, é necessário instalar um certificado SSL do cliente correspondente no computador com o Trabalho do Scale Out. Se você fornecer o caminho do arquivo para o Certificado SSL do cliente na página **Configuração de Trabalho do Integration Services Scale Out**, o certificado será instalado automaticamente; caso contrário, você precisará instalá-lo manualmente mais tarde. 
     
     Clique em **Procurar** para localizar o arquivo de certificado (*.cer). Para usar o certificado SSL padrão, selecione o arquivo SSISScaleOutMaster.cer localizado em \<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn no computador em que o Mestre do Scale Out está instalado.   
   ![Configuração do Trabalho 2](media/worker-config-2.PNG "Worker Config 2")
  5. Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Etapas do prompt de comando

    Siga as instruções em [Instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros relacionados ao Trabalho de Expansão, fazendo o seguinte.
    1.  Adicione IS_Worker no parâmetro /FEATURES
    2. Configure o Trabalho do Scale Out especificando os seguintes parâmetros e seus valores: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (opcional), /ISWORKERSVCCERT (opcional).

 
## <a name="InstallCert"></a> Instalar certificado de cliente do Trabalho de Expansão

Durante a instalação do Trabalho do Scale Out, um certificado de trabalho será criado automaticamente e instalado no computador. Além disso, um certificado de cliente correspondente, SSISScaleOutWorker.cer, é instalado em \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn. Para que o Mestre do Scale Out autentique o Trabalho do Scale Out, é necessário adicionar esse certificado do cliente ao repositório Raiz do computador local com o Mestre do Scale Out.
  
Para adicionar o certificado de cliente ao repositório raiz, clique duas vezes no arquivo .cer e, em seguida, clique em **Instalar Certificado** na caixa de diálogo. É exibido o **Assistente para Importação de Certificados** .  

## <a name="Firewall"></a> Abrir porta do firewall

Abra a porta especificada durante a instalação do Mestre do Scale Out e a porta do SQL Server (1433, por padrão), usando o Firewall do Windows no computador do Mestre do Scale Out.
    
## <a name="Start"></a> Iniciar os serviços Mestre de Expansão e Trabalho de Expansão do SQL Server

Se o tipo de inicialização dos serviços não estiver definido como Automático durante a instalação, inicie os serviços: Mestre do SQL Server Integration Services Scale Out 14.0 (SSISScaleOutMaster140) e Trabalho do SQL Server Integration Services Scale Out 14.0 (SSISScaleOutWorker140). 

> [!Note]
> Depois de abrir a porta do firewall, você também precisa reiniciar o serviço Trabalho do Scale Out.
   
## <a name="EnableMaster"></a> Habilitar o Mestre de Expansão

Clique em **Habilitar este servidor como Mestre de Expansão do SSIS** na caixa de diálogo **Criar Catálogo**, quando você criar o catálogo SSISDB no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]. Como alternativa, o Mestre do Scale Out pode ser habilitado com o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md) após a criação do catálogo.

## <a name="EnableAuth"></a> Habilitar o modo de autenticação do SQL Server
Se a autenticação do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] não for habilitada durante a instalação do Mecanismo de Banco de Dados, habilite o modo de autenticação do SQL Server na instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que hospeda o catálogo SSISDB. 

A execução de pacote não é bloqueada quando a autenticação do SQL Server está desabilitada. No entanto, o log de execução não poderá gravar em SSISDB.

## <a name="EnableWorker"></a> Habilitar o Trabalho de Expansão

O Trabalho do Scale Out pode ser habilitado por meio do [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md), que fornece a GUI ou habilitado por meio do procedimento armazenado (veja abaixo).

Para habilitar um Trabalho de Expansão, execute o procedimento armazenado *[catalog].[enable_worker_agent]* com o **WorkerAgentId** como o parâmetro. 

Você obtém o valor **WorkerAgentId** da exibição do banco de dados de *[catalog].[worker_agents]* no SSISDB, depois que o Trabalho de Expansão se registra no Mestre de Expansão. O registro leva alguns minutos depois que os serviços Mestre de Expansão e Trabalho de Expansão são iniciados.

#### <a name="example"></a>Exemplo
Este exemplo habilita o Trabalho do Scale Out no computadorA.
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
A configuração do recurso de Expansão é concluída. Agora você pode executar pacotes no Scale Out. Para obter mais informações, consulte [Executar pacotes na Expansão do Integration Services (SSIS)](run-packages-in-integration-services-ssis-scale-out.md).
