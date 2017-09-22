---
title: "Integration Services (serviço SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssiseditserverregistration.connectionproperties.f1
- sql13.swb.connecttodts.connectionproperties.f1
- sql13.swb.connection.login.dtsserver.f1
- sql13.swb.connecttodts.login.f1
- sql13.swb.connecttodtsserver.login.f1
helpviewer_keywords:
- Integration Services service, about Integration Services service
- SQL Server Integration Services service
- service [Integration Services],about Integration Services service
- service [Integration Services]
- SQL Server Integration Services, service
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 0ec83d1e567c44abba880716bbd700af2810be60
ms.contentlocale: pt-br
ms.lasthandoff: 09/21/2017

---
# <a name="integration-services-service-ssis-service"></a>Serviço do Integration Services (Serviço SSIS)
  Os tópicos desta seção discutem o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um serviço do Windows para gerenciamento de pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Este serviço não é exigido para criar, salvar e executar pacotes do Integration Services. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] dá suporte ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para compatibilidade com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazena objetos, configurações e dados operacionais no banco de dados **SSISDB** para projetos que você implantou no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o modelo de implantação de projetos. O servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que é uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , hospeda o banco de dados. Para obter mais informações sobre o banco de dados, consulte [Catálogo do SSIS](../../integration-services/service/ssis-catalog.md). Para obter mais informações sobre como implantar projetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server, consulte [implantar Integration Services (SSIS) projetos e pacotes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
## <a name="management-capabilities"></a>Recursos de gerenciamento  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um serviço Windows para gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está disponível apenas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 A execução do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece os seguintes recursos de gerenciamento:  
  
-   Início dos pacotes armazenados local e remoto  
  
-   Interrupção dos pacotes em execução local e remoto  
  
-   Monitoramento dos pacotes em execução local e remoto.  
  
-   Importação e exportação de pacotes  
  
-   Gerenciamento do armazenamento de pacotes  
  
-   Personalização das pastas de armazenamento  
  
-   Interrupção de pacotes em execução quando o serviço é interrompido  
  
-   Exibição do log de Eventos do Windows  
  
-   Conectar-se a vários servidores [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
## <a name="startup-type"></a>Tipo de inicialização
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado quando você instala o componente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático. O serviço deve estar em execução para monitorar os pacotes armazenados no Repositório de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] . O Repositório de Pacotes [!INCLUDE[ssIS](../../includes/ssis-md.md)] pode estar no banco de dados msdb em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou nas pastas designadas no sistema de arquivos.  
  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não será necessário se você só quiser projetar e executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Porém, o serviço é necessário para listar e monitorar pacotes usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  

## <a name="manage-the-service"></a>Gerenciar o serviço
  
 Quando você instala o componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também é instalado. Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático. Porém, você também precisa instalar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para usar o serviço para gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em execução e armazenados.  
  
> [!NOTE]
> Para se conectar diretamente a uma instância do Serviço Integration Services herdado, você precisa usar a versão do SSMS (SQL Server Management Studio) alinhada com a versão do SQL Server na qual o Serviço Integration Services está em execução. Por exemplo, para se conectar ao Serviço Integration Services herdados executados em uma instância do SQL Server 2016, você precisa usar a versão do SSMS liberada para o SQL Server 2016. [Baixe o SSMS (SQL Server Management Studio)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms).
>
>   Na caixa de diálogo **Conectar ao Servidor** do SSMS, não é possível inserir o nome de um servidor no qual uma versão anterior do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esteja em execução. No entanto, para gerenciar pacotes armazenados em um servidor remoto, não é necessário se conectar à instância do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nesse servidor remoto. Em vez disso, edite o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de forma que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exiba os pacotes armazenados no servidor remoto.   
  
 Você pode instalar apenas uma única instância do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador. O serviço não é específico de uma determinada instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Você se conecta ao serviço usando o nome do computador no qual ele está sendo executado.  
  
 Você pode gerenciar o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando um dos seguintes snap-ins do MMC (Console de Gerenciamento Microsoft): SQL Server Configuration Manager ou Serviços. Antes que você possa gerenciar pacotes em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é preciso se certificar que o serviço foi iniciado.  
  
 Por padrão, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para gerenciar pacotes no banco de dados msdb de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que é instalada ao mesmo tempo em que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não for instalada ao mesmo tempo, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será configurado para gerenciar pacotes no banco de dados msdb de uma instância local padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para gerenciar pacotes que estão armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)], ou em várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)], é preciso modificar o arquivo de configuração para o serviço.
  
 Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está configurado para interromper a execução de pacotes quando o serviço estiver parado. Entretanto, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não espera que os pacotes parem e alguns pacotes podem continuar executando após o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ser interrompido.  
  
 Se o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] for interrompido, você poderá continuar executando pacotes com o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , o Utilitário de Execução de Pacotes e o utilitário de prompt de comando **dtexec** (dtexec.exe). Porém, você não pode monitorar os pacotes em execução.  
  
 Por padrão, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] executa no contexto da conta de SERVIÇO DE REDE.  
  
 O serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] grava no log de evento do Windows. Você pode exibir eventos de serviço em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode exibir eventos de serviço usando Visualizador de Eventos do Windows.  
  
## <a name="set-the-properties-of-the-service"></a>Definir as propriedades do serviço
  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gerencia e monitora pacotes no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando você instala o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]pela primeira vez, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é iniciado e o tipo de inicialização do serviço é definido como automático.  
  
 Após a instalação do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode definir as propriedades do serviço usando o SQL Server Configuration Manager ou o snap-in MMC dos Serviços.  
  
 Para configurar outros recursos importantes do serviço, incluindo os locais onde armazena e gerencia pacotes, é necessário modificar o arquivo de configuração do serviço.
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>Para definir propriedades do serviço do Integration Services usando o SQL Server Configuration Manager  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, **Microsoft SQL Server**, **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No snap-in **SQL Server Configuration Manager** , localize **SQL Server Integration Services** na lista de serviços, clique com o botão direito do mouse em **SQL Server Integration Services**e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Integration Services** , você pode fazer o seguinte:  
  
    -   Clique na guia **Fazer Logon** para exibir informações de logon, como o nome de conta.  
  
    -   Clique na guia **Serviço** para exibir informações sobre o serviço, como o nome do computador host, e para especificar o modo inicial do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
        > [!NOTE]  
        >  A guia **Avançado** não contém nenhuma informação do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
4.  Clique em **OK**.  
  
5.  No menu **Arquivo** , clique em **Sair** para fechar o snap-in **SQL Server Configuration Manager** .  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>Para definir as propriedades do serviço do Integration Services usando Serviços  
  
1.  No **Painel de Controle**, se você estiver usando o Modo de exibição Clássico, clique em **Ferramentas Administrativas**ou, se estiver usando o Modo exibição de Categoria, clique em **Desempenho e Manutenção** e em **Ferramentas Administrativas**.  
  
2.  Clique em **Serviços**.  
  
3.  No snap-in **Serviços** , localize **SQL Server Integration Services** na lista de serviços, clique com o botão direito do mouse em **SQL Server Integration Services**e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server Integration Services** , você pode fazer o seguinte:  
  
    -   Clique na guia **Geral** . Para habilitar o serviço, selecione o tipo de inicialização automática ou manual. Para desabilitar o serviço, selecione Desabilitar na caixa **Tipo de inicialização** . A seleção de Desabilitar não interromperá o serviço se ele estiver em execução.  
  
         Se o serviço já estiver habilitado, você poderá clicar em **Parar** para interromper o serviço ou clicar em **Iniciar** para iniciar o serviço.  
  
    -   Clique na guia **Fazer Logon** para exibir ou editar as informações de logon.  
  
    -   Clique na guia **Recuperação** para exibir as respostas do computador padrão para a falha de serviço. Você pode modificar essas opções para adequar ao seu ambiente.  
  
    -   Clique na guia **Dependências** para exibir uma lista de serviços dependentes. O serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não tem nenhuma dependência.  
  
5.  Clique em **OK**.  
  
6.  Opcionalmente, se o tipo de inicialização for Manual ou Automático, você poderá clicar com o botão direito do mouse em **SQL Server Integration Services** e clicar em **Iniciar, Parar ou Reiniciar**.  
  
7.  No menu **Arquivo** , clique em **Sair** para fechar o snap-in **Serviços** .  

## <a name="grant-permissions-to-the-service"></a>Conceder permissões para o serviço
  Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por padrão, quando você instalava o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , todos os usuários no grupo Usuários tinham acesso ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando você instala a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os usuários não têm acesso ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por padrão, o serviço é protegido. Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado, o administrador deve conceder acesso ao serviço.  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Para conceder acesso ao serviço Integration Services  
  
1.  Execute Dcomcnfg.exe. Dcomcnfg.exe fornece uma interface do usuário para modificar certas configurações no Registro.  
  
2.  Na caixa de diálogo **Serviços de Componentes**, expanda o nó Serviços de Componentes > Computadores > Meu Computador > Configuração de DCOM.  
  
3.  Clique com o botão direito do mouse em **Microsoft SQL Server Integration Services 13.0** e clique em **Propriedades**.  
  
4.  Na guia **Segurança** , clique em **Editar** na área **Permissões de Inicialização e Ativação** .  
  
5.  Adicione os usuários e atribua permissões apropriadas e clique em Ok.  
  
6.  Repita as etapas 4 a 5 para Permissões de Acesso.  
  
7.  Reinicie o SQL Server Management Studio.  
  
8.  Reinicie o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  

## <a name="configure-the-service"></a>Configurar o serviço
 
Ao instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o processo de instalação cria e instala o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Este arquivo de configuração contém as seguintes configurações:  
  
-   Um comando de parada é enviado aos pacotes quando o serviço para.  
  
-   As pastas raiz para exibir para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são as pastas MSDB e Sistema de arquivos.  
  
-   Os pacotes no sistema de arquivos que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] serviço gerencia estão localizados em %ProgramFiles%\Microsoft SQL Server\130\DTS\Packages.  
  
 Esse arquivo de configuração também especifica qual banco de dados msdb contém os pacotes que o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] administrará. Por padrão, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para gerenciar pacotes no banco de dados msdb de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que é instalada ao mesmo tempo em que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não for instalada ao mesmo tempo, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será configurado para gerenciar pacotes no banco de dados msdb de uma instância local padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
### <a name="default-configuration-file-example"></a>Exemplo de arquivo de configuração padrão  
 O exemplo a seguir mostra um arquivo de configuração padrão que especifica as seguintes configurações:  
  
-   Pacotes deixam de executar quando o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para.  
  
-   As pastas raiz do armazenamento do pacote no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são MSDB e Arquivos do Sistema.  
  
-   O serviço gerencia pacotes que estão armazenados no banco de dado msdb da instância local padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O serviço administra pacotes que estão armazenados no sistema de arquivos na pasta Pacotes.  
  
 **Exemplo de um arquivo de configuração padrão**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file"></a>Modificar o arquivo de configuração  
 Você pode modificar o arquivo de configuração para permitir que pacotes continuem sendo executados se o serviço for interrompido, para exibir pastas raiz adicionais no Pesquisador de Objetos ou para especificar uma pasta diferente ou pastas adicionais no sistema de arquivos gerenciado pelo serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por exemplo, você pode criar pastas raiz adicionais do tipo **SqlServerFolder**para gerenciar pacotes nos bancos de dados msdb de instâncias adicionais do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
> [!NOTE]  
>  Alguns caracteres não são válidos em nomes de pasta. Caracteres válidos para nomes de pastas são determinados pela classe [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **System.IO.Path** e pelo campo **GetInvalidFilenameChars** . O campo **GetInvalidFilenameChars** fornece uma matriz de caracteres específica da plataforma que não pode ser especificada em argumentos de cadeia de caracteres de caminho passados para membros da classe **Path** . O conjunto de caracteres inválidos pode variar por sistema de arquivos. Normalmente, os caracteres inválidos são aspas ("), caractere menos que (<) e caractere pipe (|).  
  
 No entanto você precisa modificar o arquivo de configuração para gerenciar pacotes que são armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Se você não atualizar o arquivo de configuração, não será possível usar o **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibir pacotes armazenados no banco de dados msdb na instância nomeada ou remota. Se você tentar usar o **Pesquisador de Objetos** para exibir esses pacotes, receberá a seguinte mensagem de erro:  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 Para modificar o arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , use um editor de texto.  
  
> [!IMPORTANT]  
>  Depois de modificar o arquivo de configuração de serviço, você deve reiniciar o serviço para usar a configuração de serviço atualizada.  
  
### <a name="modified-configuration-file-example"></a>Exemplo de arquivo de configuração modificado  
 O exemplo a seguir mostra um arquivo de configuração modificado do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Este arquivo destina-se a uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada `InstanceName` em um servidor nomeado `ServerName`.  
  
 **Exemplo de um arquivo de configuração modificado para uma instância nomeada do SQL Server**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file-location"></a>Modificar o local do arquivo de configuração  
 A chave do registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\ServiceConfigFile** Especifica o local e o nome para a configuração de arquivo que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] serviço usa. O valor padrão da chave do registro é **C:\Program Files\Microsoft SQL Server\130\DTS\Binn\MsDtsSrvr.ini.xml**. Você pode atualizar o valor da chave do Registro para usar um nome e local diferentes para o arquivo de configuração. Observe que o número de versão no caminho (120 para o SQL Server [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)], 130 para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], etc.) irão variar dependendo da versão do SQL Server.
  
> [!CAUTION]  
>  A edição incorreta do Registro pode provocar problemas sérios que exigem a reinstalação do sistema operacional. [!INCLUDE[msCoName](../../includes/msconame-md.md)] não pode garantir que os problemas resultantes da edição incorreta do Registro podem ser resolvidos. Antes de editar o Registro, faça backup de todos os dados valiosos. Para obter informações sobre como fazer backup, restaurar e editar o Registro, consulte o artigo da Base de Dados de Conhecimento sobre o [!INCLUDE[msCoName](../../includes/msconame-md.md)] , [Descrição do Registro do Microsoft Windows](http://support.microsoft.com/kb/256986).  
  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] carrega o arquivo de configuração quando o serviço é iniciado. Qualquer alteração na entrada do Registro exige que o serviço seja reiniciado.  

## <a name="connect-to-the-local-service"></a>Conecte-se ao serviço local
  Antes de você se conectar ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o administrador deve conceder a você acesso para o serviço. 
  
### <a name="to-connect-to-the-integration-services-service"></a>Para se conectar ao serviço do Integration Services  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Clique em **Pesquisador de Objetos** no menu **Exibir** .  
  
3.  Na barra de ferramentas do Pesquisador de Objetos, clique em **Conectar**e, depois, em **Integration Services**.  
  
4.  Na caixa de diálogo **Conectar ao Servidor** , forneça um nome de servidor. Você pode usar um ponto (.), (local) ou **localhost** para indicar o servidor local.  
  
5.  Clique em **Conectar**.  

## <a name="connect-to-a-remote-ssis-server"></a>Conectar a um servidor remoto do SSIS
  
 Para se conectar a uma instância do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um servidor remoto, a partir do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou de outro aplicativo de gerenciamento, é necessário um conjunto específico de direitos no servidor para os usuários do aplicativo.  
  
> [!IMPORTANT]
> Para se conectar diretamente a uma instância do Serviço Integration Services herdado, você precisa usar a versão do SSMS (SQL Server Management Studio) alinhada com a versão do SQL Server na qual o Serviço Integration Services está em execução. Por exemplo, para se conectar ao Serviço Integration Services herdados executados em uma instância do SQL Server 2016, você precisa usar a versão do SSMS liberada para o SQL Server 2016. [Baixe o SSMS (SQL Server Management Studio)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms).
>
>  Para gerenciar pacotes armazenados em um servidor remoto, você não precisa conectar-se à instância do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] naquele servidor remoto. Em vez disso, edite o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de forma que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exiba os pacotes armazenados no servidor remoto.
  
### <a name="connecting-to-integration-services-on-a-remote-server"></a>Conectando-se ao Integration Services em um servidor remoto  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>Para se conectar ao Integration Services em um servidor remoto  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Selecione **Arquivo**, **Conectar Pesquisador de Objetos** para exibir a caixa de diálogo **Conectar ao Servidor** .  
  
3.  Selecione **Integration Services** na lista **Tipo de servidor** .  
  
4.  Digite o nome de um servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] na caixa de texto **Nome do servidor** .  
  
    > [!NOTE]  
    >  O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não é específico da instância. Você se conecta ao serviço usando o nome do computador no qual o serviço Integration Services está sendo executado.  
  
5.  Clique em **Conectar**.  
  
> [!NOTE]  
>  A caixa de diálogo **Procurar Servidores** não exibe instâncias remotas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Além disso, as opções disponíveis na guia **Opções de conexão** da caixa de diálogo **Conectar ao Servidor** , exibida ao clicar no botão **Opções** , não é aplicável às conexões [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### <a name="eliminating-the-access-is-denied-error"></a>Eliminando o erro “Acesso negado”  
 Quando um usuário sem direitos suficientes tenta se conectar a uma instância do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um servidor remoto, o servidor responde com uma mensagem de erro “Acesso negado”. Você pode evitar essa mensagem de erro verificando se os usuários têm as permissões DCOM exigidas.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>Para configurar direitos para os usuários remotos no Windows Server 2003 ou no Windows XP  
  
1.  Se o usuário não for um membro do grupo local Administradores, adicione o usuário ao grupo Usuários de COM Distribuída. Você pode fazer isso no snap-in do MMC do Gerenciamento do Computador acessado pelo menu **Ferramentas Administrativas** .  
  
2.  Abra o Painel de Controle, clique duas vezes em **Ferramentas Administrativas** e clique duas vezes em **Serviços de Componentes** para iniciar o snap-in do MMC dos Serviços de Componentes.  
  
3.  Expanda o nó **Serviços de Componentes** no painel esquerdo do console. Expanda o nó **Computadores** , expanda **Meu Computador**e clique no nó **Configuração de DCOM** .  
  
4.  Selecione o nó **Configuração de DCOM** e selecione SQL Server Integration Services 11.0 na lista de aplicativos que podem ser configurados.  
  
5.  Clique com o botão direito do mouse em SQL Server Integration Services 11.0 e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Propriedades do SQL Server Integration Services 11.0** , selecione a guia **Segurança** .  
  
7.  Em **Permissões de Inicialização e Ativação**, selecione **Personalizar**e clique em **Editar** para abrir a caixa de diálogo **Permissão de Inicialização** .  
  
8.  Na caixa de diálogo **Permissão de Inicialização** , adicione ou exclua usuários e atribua as permissões adequadas aos usuários e grupos apropriados. As permissões disponíveis são Inicialização Local, Inicialização Remota, Ativação Local e Ativação Remota. Os direitos de Inicialização concedem ou negam permissão para iniciar e parar o serviço; os direitos de Ativação concedem ou negam permissão para conexão com o serviço.  
  
9. Clique em OK para fechar a caixa de diálogo.  
  
10. Em **Permissões de acesso**, repita as etapas 7 e 8 para atribuir as permissões adequadas aos usuários e grupos apropriados.  
  
11. Feche o snap-in do MMC.  
  
12. Reinicie o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>Para configurar direitos para usuários remotos no Windows 2000 com os service packs mais recentes  
  
1.  Executar **dcomcnfg.exe** no prompt de comando.  
  
2.  Na página **Aplicativos** da caixa de diálogo **Propriedades de Configuração de COM Distribuída** , selecione SQL Server Integration Services 11.0 e clique em **Propriedades**.  
  
3.  Selecione a página **Segurança** .  
  
4.  Use as duas caixas de diálogo separadas para configurar as **Permissões de acesso** e as **Permissões de Inicialização**. Você não pode distinguir entre acesso remoto e local – as permissões de Acesso incluem acesso local e remoto e as permissões de Inicialização incluem inicialização local e remota.  
  
5.  Feche as caixas de diálogo e **dcomcnfg.exe**.  
  
6.  Reinicie o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### <a name="connecting-by-using-a-local-account"></a>Conectando-se através de uma conta local  
 Se você estiver trabalhando em uma conta local do Windows em um computador cliente, só poderá se conectar ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador remoto se houver uma conta local com o mesmo nome e senha e os direitos apropriados no computador remoto.  
  
### <a name="by-default-the-ssis-service-does-not-support-delegation"></a>Por padrão, o serviço SSIS não oferece suporte para delegação  
Por padrão, o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não oferece suporte para delegação de credenciais ou o que às vezes é conhecido como salto duplo. Nesse cenário, você está trabalhando em um computador cliente, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está em execução em um segundo computador e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução em um terceiro computador. Primeiro, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] passa com sucesso as credenciais do computador cliente para o segundo computador no qual o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está em execução. Em seguida, no entanto, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não pode delegar suas credenciais do segundo computador para o terceiro computador no qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução.

Você pode habilitar a delegação de credenciais concedendo o direito **Confiar neste usuário para delegação a qualquer serviço (apenas Kerberos)** para a conta de serviço do SQL Server, que inicia o serviço do Integration Services (ISServerExec.exe) como um processo filho. Antes de conceder esse direito, considere se ele atende aos requisitos de segurança de sua organização.

Para obter mais informações, consulte [Getting Cross Domain Kerberos and Delegation working with SSIS Package (Obtendo entre Kerberos do domínio e delegação de trabalhar com o pacote do SSIS)](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/).
 
## <a name="configure-the-firewall"></a>Configurar o firewall
  
 O sistema de firewall do Windows ajuda a evitar acesso não autorizado aos recursos do computador em uma conexão de rede. Para acessar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] por meio desse firewall, você precisa configurar o firewall para habilitar o acesso.  
  
> [!IMPORTANT]  
>  Para gerenciar pacotes armazenados em um servidor remoto, você não precisa conectar-se à instância do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] naquele servidor remoto. Em vez disso, edite o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de forma que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exiba os pacotes armazenados no servidor remoto.
  
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa o protocolo DCOM. Para obter mais informações sobre como o protocolo DCOM funciona por meio de firewalls, consulte o artigo “[Usando COM distribuída com firewalls](http://go.microsoft.com/fwlink/?LinkId=12490)”, na Biblioteca MSDN.  
  
 Há muitos sistemas de firewall disponíveis. Se você estiver executando um firewall diferente do firewall do Windows, consulte a documentação do firewall para obter informações específicas para o sistema que você está usando.  
  
 Se o firewall oferecer suporte a filtros no nível de aplicativo, você poderá usar a interface do usuário que o Windows fornece para especificar as exceções permitidas pelo firewall, como programas e serviços. Caso contrário, você precisará configurar o DCOM para usar um conjunto limitado de portas TCP. O link do site da Microsoft fornecido anteriormente inclui informações sobre como especificar as portas TCP a serem usadas.  
  
 O serviço Integration Services usa a porta 135, e ela não pode ser alterada. Você precisa abrir a porta TCP 135 para acessar o SCM (Gerenciador de Controle de Serviços). O SCM executa tarefas como iniciar e parar os serviços [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e transmitir solicitações de controle ao serviço em execução.  
  
 As informações na seção a seguir são específicas para o firewall do Windows. Você pode configurar o sistema de firewall do Windows ao executar um comando no prompt de comando, ou definindo propriedades na caixa de diálogo firewall do Windows.  
  
 Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="configuring-a-windows-firewall"></a>Configurando um firewall do Windows  
 Você pode usar os comandos a seguir para abrir a porta TCP 135, adicionar o MsDtsSrvr.exe à lista de exceções e especificar o escopo de desbloqueio para o firewall.  
  
#### <a name="to-configure-a-windows-firewall-using-the-command-prompt-window"></a>Para configurar um Firewall do Windows usando a janela do prompt de comando  
  
1.  Execute o seguinte comando:

    ```dos
    netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET
    ```
  
2.  Execute o seguinte comando:

    ```dos
    netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET
    ```
  
    > [!NOTE]  
    >  Para abrir o firewall em todos os computadores e, também, para os computadores na Internet, substitua scope=SUBNET por scope=ALL.  
  
 O procedimento a seguir descreve como usar a interface do usuário do Windows para abrir a porta TCP 135, adicionar o MsDtsSrvr.exe à lista de exceções e especificar o escopo de desbloqueio para o firewall.  
  
#### <a name="to-configure-a-firewall-using-the-windows-firewall-dialog-box"></a>Para configurar um firewall usando a caixa de diálogo firewall do Windows  
  
1.  No Painel de Controle, clique duas vezes em **Firewall do Windows**.  
  
2.  Na caixa de diálogo **Firewall do Windows** , clique na guia **Exceções** e em **Adicionar Programa.**  
  
3.  Na caixa de diálogo **Adicionar um Programa** , clique em **Procurar**, navegue até a pasta Arquivos de Programas\Microsoft SQL Server\100\DTS\Binn, clique em MsDtsSrvr.exe e em **Abrir**. Clique em **OK** para fechar a caixa de diálogo **Adicionar um Programa** .  
  
4.  Na guia **Exceções** , clique em **Adicionar Porta.**  
  
5.  Na caixa de diálogo **Adicionar uma Porta** , digite **RPC (TCP/135)** ou outro nome descritivo na caixa **Nome**, digite **135** na caixa **Número da porta** e selecione o **TCP**.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] O serviço sempre usa a porta 135. Não é possível especificar uma porta diferente.  
  
6.  Na caixa de diálogo **Adicionar uma Porta** , opcionalmente, você pode clicar em **Alterar Escopo** para modificar o escopo padrão.  
  
7.  Na caixa de diálogo **Alterar Escopo** , selecione **Minha rede (somente sub-rede)** ou digite uma lista personalizada e clique em **OK**.  
  
8.  Para fechar a caixa de diálogo **Adicionar uma Porta** , clique em **OK**.  
  
9. Para fechar a caixa de diálogo **Firewall do Windows** , clique em **OK**.  
  
    > [!NOTE]  
    >  Para configurar o firewall do Windows, esse procedimento usa o **Firewall do Windows** item no painel de controle. O item **Firewall do Windows** configura apenas o firewall do perfil do local de rede local. No entanto, você também pode configurar o firewall do Windows usando o **netsh** ferramenta de linha de comando ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] snap-in Management Console (MMC) denominado firewall do Windows com segurança avançada. Para obter mais informações sobre como fazer isso, consulte [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  

