---
title: "Gerenciador de conex&#245;es ODBC | Microsoft Docs"
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
  - "conexões [Integration Services], ODBC"
  - "gerenciador de conexões ODBC"
  - "fontes de dados [Integration Services], conexões"
  - "gerenciadores de conexões [Integration Services], ODBC"
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Gerenciador de conex&#245;es ODBC
  Um gerenciador de conexões ODBC permite que um pacote se conecte com vários sistemas de gerenciamento de banco de dados que usam a especificação ODBC (Conectividade Aberta de Banco de Dados).  
  
 Quando você adiciona um gerenciador de conexões ODBC a um pacote e define as propriedades do gerenciador de conexões, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** do pacote. No tempo de execução, o gerenciador de conexões é resolvido como uma conexão física ODBC.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **ODBC**.  
  
 Você pode configurar um gerenciador de conexões ODBC das seguintes formas:  
  
-   Forneça uma cadeia de caracteres de conexão que faça referência a um usuário ou a um nome de fonte de dados do sistema.  
  
-   Especifique o servidor a ser conectado.  
  
-   Indique se a conexão é retida no tempo de execução.  
  
## Configuração do gerenciador de conexões ODBC  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)], clique em um dos seguintes tópicos:  
  
-   [Referência da interface do usuário do Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  