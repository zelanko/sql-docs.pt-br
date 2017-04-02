---
title: "Gerenciador de Conex&#245;es do SQL Server Compact Edition | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Compact, gerenciador de conexões"
  - "conexões [Integration Services], SQL Server Compact"
  - "gerenciadores de conexões [Integration Services], SQL Server Compact"
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# Gerenciador de Conex&#245;es do SQL Server Compact Edition
  Um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact permite que um pacote se conecte a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usa esse gerenciador de conexões para carregar dados em uma tabela no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  Em um computador de 64 bits, você deve executar pacotes que se conectam a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact no modo de 32 bits. O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para se conectar a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, só está disponível na versão de 32 bits.  
  
## Configuração do gerenciador de conexões do SQL Server Compact Edition  
 Quando você adiciona um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que resolverá uma conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção de **Conexões** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **SQLMOBILE**.  
  
 Você pode configurar um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão que especifique o local do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
-   Forneça uma senha para um banco de dados protegido por senha.  
  
-   Especifique o servidor no qual o banco de dados está armazenado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  