---
title: "Passo a passo: configurar a Expans&#227;o do Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cabb78a2-f234-46c3-842d-53aa2df8dfb3
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Passo a passo: configurar a Expans&#227;o do Integration Services

Você configura a expansão do [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] concluindo as seguintes tarefas. 

> [!NOTE] Se você estiver instalando a Expansão em um computador, é recomendável que você instale os recursos Mestre de Expansão e Trabalho de Expansão ao mesmo tempo. Quando você instala os recursos ao mesmo tempo, o ponto de extremidade é gerado automaticamente para se conectar ao Mestre de Expansão. 

* [Instalar o Mestre de Expansão](#InstallMaster)

* [Instalar o Trabalho de Expansão](#InstallWorker)

* [Instalar certificado de cliente do Trabalho de Expansão](#InstallCert)

* [Abrir porta do firewall](#Firewall)

* [Iniciar o serviço Mestre de Expansão e Trabalho de Expansão do SQL Server](#Start)

* [Habilitar o Mestre de Expansão](#EnableMaster)

* [Habilitar o modo de autenticação do SQL Server](#EnableAuth)

* [Habilitar o Trabalho de Expansão](#EnableWorker)

## <a name="a-nameinstallmastera-install-scale-out-master"></a><a name="InstallMaster"></a> Instalar o Mestre de Expansão

Para habilitar a funcionalidade Mestre de Expansão, você deve instalar os Serviços de Mecanismo de Banco de Dados, [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] e seu recurso Mestre de Expansão ao configurar [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]. 

Para obter informações sobre como configurar os Serviços de Mecanismo de Banco de Dados e [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)], consulte [Instalar o Mecanismo de Banco de Dados do SQL Server](../database-engine/install-windows/install-sql-server-database-engine.md), e [Instalar o Integration Services](../integration-services/install-windows/install-integration-services.md).
> [!NOTE]
> Durante a instalação do Mecanismo de Banco de Dados, selecione Modo Misto para o Modo de autenticação na página de Configuração do Mecanismo de Banco de Dados. 

**Para instalar o recurso Mestre de Expansão, use o Assistente de instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] ou o prompt de comando.**

- Etapas para o assistente de instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  Na página **Seleção de Recursos**, selecione **Mestre de Expansão** que está listado em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].   
  ![Mestre de Seleção de Recurso](../integration-services/media/feature-select-master.PNG)
  
  2.  Na página **Configuração do Servidor**, selecione a conta para executar o **serviço Mestre de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.  
  ![Configuração do servidor](../integration-services/media/server-config.PNG)
  3.  Na página **Configuração do Mestre de Expansão do Integration Services** especifique o número da porta usada pelo Mestre de Expansão para se comunicar com o Mestre de Trabalho. O número da porta padrão é 8391.  
  ![Master Config](../integration-services/media/master-config.PNG "Master Config")
  4.  Especifique o certificado SSL usado para proteger a comunicação entre o Mestre de Expansão e o Trabalho de Expansão, seguindo um destes procedimentos.
    * Permitir que o processo de instalação crie um certificado SSL padrão, autoassinado, clicando em **Criar um novo certificado SSL**. O certificado padrão é instalado em Autoridades de Certificação Confiáveis, Computador Local.
    * Selecione um Certificado SSL existente no computador local, clicando em **Usar um certificado SSL existente** e, em seguida, clicando em **Procurar**. A impressão digital do certificado é exibida na caixa de texto. Clicar em **Procurar** exibe os certificados que estão armazenados em Autoridades de Certificação Confiáveis, Computador Local. O certificado selecionado deve estar armazenado aqui.       
![Master Config 2](../integration-services/media/master-config-2.PNG "Master Config 2")
  5.  Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].
- Etapas do prompt de comando

    Siga as instruções em [Instalar o SQL Server do Prompt de comando](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros relacionados ao Mestre de Expansão, fazendo o seguinte.
  1.  Adicione IS_Master no parâmetro /FEATURES
  2.  Configurar o Mestre de Expansão com parâmetros: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMASTERSVCTHUMBPRINT (opcional).
  
## <a name="a-nameinstallworkera-install-scale-out-worker"></a><a name="InstallWorker"></a> Instalar o Trabalho de Expansão
 
Para habilitar a funcionalidade de Trabalho de Expansão, você deve instalar [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] e seu recurso de Trabalho de Expansão na instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].

**Para instalar o recurso Trabalho de Expansão, use o Assistente de instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] ou o prompt de comando.**

- Etapas para o assistente de instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  Na página **Seleção de Recursos**, selecione **Trabalho de Expansão** que está listado em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].   
  ![Trabalho de Seleção de Recurso](../integration-services/media/feature-select-worker.PNG)
  2. Na página **Configuração do Servidor**, selecione a conta para executar o **serviço Trabalho de Expansão do SQL Server Integration Services** e selecione o **Tipo de Inicialização**.    
  ![Server Config 2](../integration-services/media/server-config-2.PNG "Server Config 2")
  3. Na página de **Configuração de Trabalho de Expansão do Integration Services** especifique o ponto de extremidade para se conectar ao Mestre de Expansão. 
    - Para um ambiente **one-box**, o ponto de extremidade é gerado automaticamente quando o Mestre de Expansão e o Trabalho de Expansão são instalados ao mesmo tempo. 
    - Para um ambiente de **vários computadores**, o ponto de extremidade consiste no nome ou IP do computador com o Mestre de Expansão instalado e o número da porta especificado durante a instalação do Mestre de Expansão.    
   ![Worker Config 1](../integration-services/media/worker-config-1.PNG "Worker Config 1")
    
  4. Para um ambiente de **vários computadores**, especifique o certificado SSL de cliente que é usado para validar o Mestre de Expansão. Em um ambiente **one-box**, não é necessário especificar o certificado SSL de cliente. 
  
     > [!NOTE] Quando o certificado SSL usado pelo Mestre de Expansão é autoassinado, é necessário instalar um certificado SSL de cliente correspondente no computador com o Trabalho de Expansão. Se você fornecer o caminho do arquivo para o certificado SSL de cliente na página **Configuração de Trabalho de Expansão do Integration Services**, ele será instalado automaticamente; caso contrário, você precisa instalar o certificado manualmente depois. 
     
     Clique em **Procurar** para localizar o arquivo de certificado (*.cer). Para usar o certificado SSL padrão, selecione o arquivo SSISScaleOutMaster.cer localizado em \<unidade\>:\Program Files\Microsoft SQL Server\140\DTS\Binn no computador em que o Mestre de Expansão está instalado.   
   ![Worker Config 2](../integration-services/media/worker-config-2.PNG "Worker Config 2")
  5. Conclua o assistente de instalação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].
- Etapas do prompt de comando

    Siga as instruções em [Instalar o SQL Server do Prompt de comando](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Defina os parâmetros relacionados ao Trabalho de Expansão, fazendo o seguinte.
    1.  Adicione IS_Worker no parâmetro /FEATURES
    2. Configurar o Trabalho de Expansão com parâmetros: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (opcional), /ISWORKERSVCCERT (opcional).

 
## <a name="a-nameinstallcerta-install-scale-out-worker-client-certificate"></a><a name="InstallCert"><a/> Instalar certificado de cliente do Trabalho de Expansão

Durante a instalação do Trabalho de Expansão, um certificado de trabalho será automaticamente criado e instalado no computador. Além disso, um certificado de cliente correspondente, SSISScaleOutWorker.cer, é instalado em \<driver\>:\Program Files\Microsoft SQL Server\140\DTS\Binn. Para autenticar o Trabalho de Expansão no Mestre de Expansão, você deve adicionar o certificado de cliente no repositório raiz do computador local com o Mestre de Expansão.
  
Para adicionar o certificado de cliente ao repositório raiz, clique duas vezes no arquivo .cer e, em seguida, clique em **Instalar Certificado** na caixa de diálogo. É exibido o **Assistente para Importação de Certificados**.  

## <a name="a-namefirewalla-open-firewall-port"></a><a name="Firewall"><a/> Abrir porta do firewall

Abra a porta especificada durante a instalação do Mestre de Expansão, usando o Firewall do Windows no computador do Mestre de Expansão.
    
## <a name="a-namestarta-start-sql-server-scale-out-master-and-worker-services"></a><a name="Start"></a> Iniciar os serviços Mestre de Expansão e Trabalho de Expansão do SQL Server

Se o tipo de inicialização dos serviços não estiver definido como automático durante a instalação acima, inicie os serviços: Mestre de Expansão do SQL Server Integration Services 14.0 (SSISScaleOutMaster140) e o Mestre de Trabalho do SQL Server Integration Services 14.0 (SSISScaleOutWorker140). 

> [!NOTE]
>Depois de abrir a porta do firewall, você precisa reiniciar o serviço Trabalho de Expansão.
   
## <a name="a-nameenablemastera-enable-scale-out-master"></a><a name="EnableMaster"></a> Habilitar o Mestre de Expansão

Clique em **Habilitar este servidor como Mestre de Expansão do SSIS** na caixa de diálogo **Criar Catálogo**, quando você criar o catálogo SSISDB no [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)].

## <a name="a-nameenableautha-enable-sql-server-authentication-mode"></a><a name="EnableAuth"></a> Habilitar o modo de autenticação do SQL Server
Se a autenticação [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] não for habilitada durante a instalação do Mecanismo de Banco de Dados, habilite o modo de autenticação do SQL Server na instância [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] que hospeda o catálogo SSISDB. 

A execução de pacote não é bloqueada quando a autenticação do SQL Server está desabilitada. No entanto, o log de execução não poderá gravar em SSISDB.

## <a name="a-nameenableworkera-enable-scale-out-worker"></a><a name="EnableWorker"></a> Habilitar o Trabalho de Expansão
Para habilitar um Trabalho de Expansão, execute o procedimento armazenado *[catalog].[enable_worker_agent]* com o **WorkerAgentId** como o parâmetro. 

Você obtém o valor **WorkerAgentId** da exibição do banco de dados de *[catalog].[worker_agents]* no SSISDB, depois que o Trabalho de Expansão se registra no Mestre de Expansão. O registro leva alguns minutos depois que os serviços Mestre de Expansão e Trabalho de Expansão são iniciados.

### <a name="example"></a>Exemplo
Este exemplo habilita o Trabalho de Expansão no ComputadorA.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Próximas etapas
A configuração do recurso de Expansão é concluída. Agora você pode executar pacotes em Expansão. Para obter mais informações, consulte [Executar pacotes na Expansão do Integration Services (SSIS)](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).

