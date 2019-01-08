---
title: Configurando a integração de serviços (serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- configuration files [Integration Services]
- service [Integration Services], configuring
- default configuration files
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4fd38d33bf0ed5d074fe2784dfba38348342df98
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359678"
---
# <a name="configuring-the-integration-services-service-ssis-service"></a>Configurando o serviço Integration Services (serviço SSIS)
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 O serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] depende de um arquivo de configuração para suas configurações. Por padrão, o nome para esse arquivo de configuração é MsDtsSrvr. ini e o arquivo está localizado na pasta %ProgramFiles%\Microsoft SQL Server\120\DTS\Binn.  
  
 Normalmente, você não tem que fazer alterações neste arquivo de configuração, nem no local padrão dele. Porém, será necessário modificar o arquivo de configuração se seus pacotes estiverem armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../includes/ssde-md.md)]ou em várias instâncias do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Além disso, se você mover o arquivo de configuração para um local que não o padrão, será necessário modificar a chave do Registro que especifica o local do arquivo.  
  
## <a name="configuration-file-contents"></a>Conteúdo do arquivo de configuração  
 Ao instalar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], o processo de instalação cria e instala o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Este arquivo de configuração contém as seguintes configurações:  
  
-   Um comando de parada é enviado aos pacotes quando o serviço para.  
  
-   As pastas raiz para exibir para [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] são as pastas MSDB e Sistema de arquivos.  
  
-   Os pacotes no sistema de arquivos que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] serviço gerencia estão localizados em %ProgramFiles%\Microsoft SQL Server\120\DTS\Packages.  
  
 Esse arquivo de configuração também especifica qual banco de dados msdb contém os pacotes que o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administrará. Por padrão, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é configurado para gerenciar pacotes no banco de dados msdb de uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] que é instalada ao mesmo tempo em que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] não for instalada ao mesmo tempo, o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] será configurado para gerenciar pacotes no banco de dados msdb de uma instância local padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
### <a name="default-configuration-file-example"></a>Exemplo de arquivo de configuração padrão  
 O exemplo a seguir mostra um arquivo de configuração padrão que especifica as seguintes configurações:  
  
-   Pacotes deixam de executar quando o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para.  
  
-   As pastas raiz do armazenamento do pacote no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são MSDB e Arquivos do Sistema.  
  
-   O serviço gerencia pacotes que estão armazenados no banco de dado msdb da instância local padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   O serviço administra pacotes que estão armazenados no sistema de arquivos na pasta Pacotes.  
  
 **Exemplo de um arquivo de configuração padrão**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file"></a>Modificação do arquivo de configuração.  
 Você pode modificar o arquivo de configuração para permitir que pacotes continuem sendo executados se o serviço for interrompido, para exibir pastas raiz adicionais no Pesquisador de Objetos ou para especificar uma pasta diferente ou pastas adicionais no sistema de arquivos gerenciado pelo serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Por exemplo, você pode criar pastas raiz adicionais de tipo, `SqlServerFolder`, para gerenciar pacotes nos bancos de dados msdb de instâncias adicionais do [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
> [!NOTE]  
>  Alguns caracteres não são válidos em nomes de pasta. Caracteres válidos para nomes de pastas são determinados pela classe [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] **System.IO.Path** e pelo campo **GetInvalidFilenameChars** . O campo **GetInvalidFilenameChars** fornece uma matriz de caracteres específica da plataforma que não pode ser especificada em argumentos de cadeia de caracteres de caminho passados para membros da classe **Path** . O conjunto de caracteres inválidos pode variar por sistema de arquivos. Normalmente, os caracteres inválidos são aspas ("), caractere menos que (<) e caractere pipe (|).  
  
 No entanto você precisa modificar o arquivo de configuração para gerenciar pacotes que são armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Se você não atualizar o arquivo de configuração, não será possível usar o **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para exibir pacotes armazenados no banco de dados msdb na instância nomeada ou remota. Se você tentar usar o **Pesquisador de Objetos** para exibir esses pacotes, receberá a seguinte mensagem de erro:  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 Para modificar o arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , use um editor de texto.  
  
> [!IMPORTANT]  
>  Depois de modificar o arquivo de configuração de serviço, você deve reiniciar o serviço para usar a configuração de serviço atualizada.  
  
### <a name="modified-configuration-file-example"></a>Exemplo de arquivo de configuração modificado  
 O exemplo a seguir mostra um arquivo de configuração modificado do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Este arquivo destina-se a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] chamada `InstanceName` em um servidor nomeado `ServerName`.  
  
 **Exemplo de um arquivo de configuração modificado para uma instância nomeada do SQL Server**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file-location"></a>Modificação do local do arquivo de configuração  
A chave do registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\ServiceConfigFile** Especifica o local e o nome para a configuração de arquivo que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] serviço usa. É o valor padrão da chave do registro **C:\Program Files\Microsoft SQL Server\120\DTS\Binn\MsDtsSrvr.ini.xml**. Você pode atualizar o valor da chave do Registro para usar um nome e local diferentes para o arquivo de configuração. Observe que o número de versão no caminho (120 para o SQL Server [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]) irá variar dependendo da versão do SQL Server. 
  
  
> [!CAUTION]  
>  A edição incorreta do Registro pode provocar problemas sérios que exigem a reinstalação do sistema operacional. [!INCLUDE[msCoName](../includes/msconame-md.md)] não pode garantir que os problemas resultantes da edição incorreta do Registro podem ser resolvidos. Antes de editar o Registro, faça backup de todos os dados valiosos. Para obter informações sobre como fazer backup, restaurar e editar o Registro, consulte o artigo da Base de Dados de Conhecimento sobre o [!INCLUDE[msCoName](../includes/msconame-md.md)] , [Descrição do Registro do Microsoft Windows](https://support.microsoft.com/kb/256986).  
  
 O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] carrega o arquivo de configuração quando o serviço é iniciado. Qualquer alteração na entrada do Registro exige que o serviço seja reiniciado.  
  
  
