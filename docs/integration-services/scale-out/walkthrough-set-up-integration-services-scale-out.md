---
title: "Passo a passo: Configurar o SQL Server Integration Services de expansão | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9cc5c653fe454b45148583f2e17654657a85b0a5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>Passo a passo: configurar a Expansão do Integration Services
Configurar [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] expansão concluindo as seguintes tarefas. 

> [!NOTE]
> Se você estiver instalando expansão em um computador, instale os recursos de escala Out mestre e de escala Out trabalho ao mesmo tempo. Quando você instala os recursos ao mesmo tempo, o ponto de extremidade é gerado automaticamente para se conectar ao Mestre de Expansão. 

* [Instalar o Mestre de Expansão](#InstallMaster)

* [Instalar o Trabalho de Expansão](#InstallWorker)

* [Instalar certificado de cliente do Trabalho de Expansão](#InstallCert)

* [Abrir porta do firewall](#Firewall)

* [Iniciar o serviço Mestre de Expansão e Trabalho de Expansão do SQL Server](#Start)

* [Habilitar o Mestre de Expansão](#EnableMaster)

* [Habilitar o modo de autenticação do SQL Server](#EnableAuth)

* [Habilitar o Trabalho de Expansão](#EnableWorker)

## <a name="InstallMaster"></a> Instalar o Mestre de Expansão

Para habilitar a funcionalidade de escala Out mestre, você deve instalar os serviços de mecanismo de banco de dados, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]e seu recurso de escala Out mestre ao configurar [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. 

Para obter informações sobre como configurar os Serviços de Mecanismo de Banco de Dados e [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], consulte [Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md), e [Instalar o Integration Services](../install-windows/install-integration-services.md).
> [!NOTE]
> Para usar a conta de autenticação padrão do SQL para expansão log, selecione o modo misto para o modo de autenticação na página de configuração do mecanismo de banco de dados durante a instalação do mecanismo de banco de dados. Consulte [alterar a conta de expansão log](change-logdb-account.md) para obter mais informações.

**Para instalar o recurso Mestre de Expansão, use o Assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou o prompt de comando.**

- Etapas para o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  No **seleção de recursos** página, selecione **escala Out mestre**, que é listado em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Mestre de Seleção de Recurso](media/feature-select-master.PNG)
  
  2.  Na página **Configuração do Servidor** , selecione a conta para executar o **serviço Mestre de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.  
  ![Configuração do servidor](media/server-config.PNG)
  3.  Na página **Configuração do Mestre de Expansão do Integration Services** especifique o número da porta usada pelo Mestre de Expansão para se comunicar com o Mestre de Trabalho. O número da porta padrão é 8391.  
  ![Configuração do mestre](media/master-config.PNG "configuração mestre")
  4.  Especifique o certificado SSL usado para proteger a comunicação entre o mestre fora de escala e de escala Out trabalho seguindo um destes procedimentos.
    * Permitir que o processo de instalação cria um padrão, o certificado SSL autoassinado clicando **criar um novo certificado SSL**.  O certificado padrão é instalado em Autoridades de Certificação Confiáveis, Computador Local. Você pode especificar o CNs deste certificado. O nome do host do ponto de extremidade mestre deve ser incluído no CNs. Por padrão, o nome do computador e o ip do nó mestre são incluídos.
    * Selecione um Certicate SSL existente no computador local, clicando em **usar um certificado SSL existente** e, em seguida, clicando em **procurar** para selecionar um certificado. A impressão digital do certificado é exibida na caixa de texto. Clicar em **Procurar** exibe os certificados que estão armazenados em Autoridades de Certificação Confiáveis, Computador Local. O certificado selecionado deve estar armazenado aqui.       
![Configuração mestre 2](media/master-config-2.PNG "mestre configuração 2")
  5.  Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Etapas do prompt de comando

    Siga as instruções em [Instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros relacionados ao Mestre de Expansão, fazendo o seguinte.
  1.  Adicione IS_Master no parâmetro /FEATURES
  2.  Configurar a escala Out mestre especificando os seguintes parâmetros e seus valores: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN(optional), /ISMASTERSVCTHUMBPRINT(optional).

> [!Note]
> Se o mestre de fora da escala não é instalado junto com o mecanismo de banco de dados e o mecanismo de banco de dados é uma instância nomeada, você precisa configurar SqlServerName no arquivo de configuração do serviço de escala Out mestre após a instalação. Consulte [escala Out mestre](integration-services-ssis-scale-out-master.md) para obter detalhes.

## <a name="InstallWorker"></a> Instalar o Trabalho de Expansão
 
Para habilitar a funcionalidade de Trabalho de Expansão, você deve instalar [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] e seu recurso de Trabalho de Expansão na instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

**Para instalar o recurso Trabalho de Expansão, use o Assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou o prompt de comando.**

- Etapas para o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  No **seleção de recursos** página, selecione **escala Out trabalho**, que é listado em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Trabalho de Seleção de Recurso](media/feature-select-worker.PNG)
  2. Na página **Configuração do Servidor** , selecione a conta para executar o **serviço Trabalho de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.    
  ![Configuração de servidor 2](media/server-config-2.PNG "2 de configuração do servidor")
  3. Na página de **Configuração de Trabalho de Expansão do Integration Services** especifique o ponto de extremidade para se conectar ao Mestre de Expansão. 
      > [!Note]
      > Você pode ignorar a configuração do nó do operador (etapa 3 e 4) aqui e associar o trabalhador escala Out escala Out mestre com [escala Out Manager](integration-services-ssis-scale-out-manager.md) após a instalação.

    - Para uma **um computador** ambiente, o ponto de extremidade é gerado automaticamente quando a escala Out mestre e escala Out trabalho são instalados ao mesmo tempo. 
    - Para uma **vários computadores** ambiente, o ponto de extremidade consiste de IP do computador ou do nome com escala Out mestre instalado e o número da porta especificada durante a instalação de escala Out mestre.    
   ![Configuração de trabalho 1](media/worker-config.PNG "trabalho configuração 1")    

  4. Para uma **vários computadores** ambiente, especifique o certificado SSL de cliente que é usado para validar o mestre de fora da escala. Para uma **um computador** ambiente, não é necessário especificar o certificado SSL do cliente. 
  
     > [!NOTE]
     > Quando o certificado SSL usado pelo mestre de fora da escala é autoassinado, um certificado SSL de cliente correspondente é necessário para ser instalado no computador com escala fora do trabalho. Se você fornecer o caminho do arquivo para o certificado SSL de cliente no **escala Out trabalho configuração do Integration Services** página, o certificado será instalado automaticamente; caso contrário, você precisa instalar o certificado manualmente mais tarde. 
     
     Clique em **Procurar** para localizar o arquivo de certificado (*.cer). Para usar o certificado SSL padrão, selecione o arquivo SSISScaleOutMaster.cer localizado na \<unidade\>: \Program Files\Microsoft Server\140\DTS\Binn SQL no computador em que a escala Out mestre está instalado.   
   ![Configuração de trabalho 2](media/worker-config-2.PNG "configuração de trabalho 2")
  5. Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Etapas do prompt de comando

    Siga as instruções em [Instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros relacionados ao Trabalho de Expansão, fazendo o seguinte.
    1.  Adicione IS_Worker no parâmetro /FEATURES
    2. Configurar a escala Out trabalho especificando os seguintes parâmetros e seus valores: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER(optional), /ISWORKERSVCCERT(optional).

 
## <a name="InstallCert"></a> Instalar certificado de cliente do Trabalho de Expansão

Durante a instalação da escala fora do trabalho, um certificado do trabalhador será automaticamente criado e instalado no computador. Além disso, um certificado de cliente correspondente, SSISScaleOutWorker.cer, é instalado em \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn. Para escala Out mestre autenticar o trabalho de fora de escala, você deve adicionar esse certificado de cliente para o repositório de raiz do computador local com escala Out mestre.
  
Para adicionar o certificado de cliente ao repositório raiz, clique duas vezes no arquivo .cer e, em seguida, clique em **Instalar Certificado** na caixa de diálogo. É exibido o **Assistente para Importação de Certificados** .  

## <a name="Firewall"></a> Abrir porta do firewall

Abra a porta especificada durante a instalação de escala Out mestre e a porta do SQL Server (1433, por padrão), usando o Firewall do Windows no computador escala Out mestre.
    
## <a name="Start"></a> Iniciar os serviços Mestre de Expansão e Trabalho de Expansão do SQL Server

Se o tipo de inicialização dos serviços não está definido como automático durante a instalação, inicie os serviços: SQL Server Integration Services escala Out mestre 14.0 (SSISScaleOutMaster140) e o SQL Server Integration Services escala Out trabalho 14.0 (SSISScaleOutWorker140). 

> [!Note]
> Depois de abrir a porta do firewall, você também precisa reiniciar o serviço de escala fora do trabalho.
   
## <a name="EnableMaster"></a> Habilitar o Mestre de Expansão

Clique em **Habilitar este servidor como Mestre de Expansão do SSIS** na caixa de diálogo **Criar Catálogo**, quando você criar o catálogo SSISDB no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]. Como alternativa, o mestre de fora da escala podem ser habilitada com [escala Out Manager](integration-services-ssis-scale-out-manager.md) depois de catálogo é criado.

## <a name="EnableAuth"></a> Habilitar o modo de autenticação do SQL Server
Se [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] autenticação não é habilitada durante a instalação do mecanismo de banco de dados, ativar o modo de autenticação do SQL Server a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância que hospeda o catálogo SSISDB. 

A execução de pacote não é bloqueada quando a autenticação do SQL Server está desabilitada. No entanto, o log de execução não poderá gravar em SSISDB.

## <a name="EnableWorker"></a> Habilitar o Trabalho de Expansão

Escala Out trabalho pode ser habilitado por meio de [escala Out Manager](integration-services-ssis-scale-out-manager.md), que fornece a interface gráfica do usuário; ou habilitado por meio do procedimento armazenado, consulte abaixo.

Para habilitar um Trabalho de Expansão, execute o procedimento armazenado *[catalog].[enable_worker_agent]* com o **WorkerAgentId** como o parâmetro. 

Você obtém o valor **WorkerAgentId** da exibição do banco de dados de *[catalog].[worker_agents]* no SSISDB, depois que o Trabalho de Expansão se registra no Mestre de Expansão. O registro leva alguns minutos depois que os serviços Mestre de Expansão e Trabalho de Expansão são iniciados.

#### <a name="example"></a>Exemplo
Este exemplo habilita a escala Out trabalhador em ComputadorA.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Próximas etapas
A configuração do recurso de Expansão é concluída. Agora você pode executar pacotes em expansão. Para obter mais informações, consulte [Executar pacotes na Expansão do Integration Services (SSIS)](run-packages-in-integration-services-ssis-scale-out.md).
