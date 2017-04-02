---
title: "Gerenciador de conex&#245;es HTTP | Microsoft Docs"
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
  - "Gerenciador de conexões HTTP"
  - "Conexões do site [Integration Services]"
  - "gerenciadores de conexões [Integration Services], HTTP"
  - "Conexões do servidor Web [Integration Services]"
  - "conexões [Integration Services], HTTP"
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Gerenciador de conex&#245;es HTTP
  Uma conexão HTTP permite que um pacote acesse um servidor Web usando o HTTP para enviar ou receber arquivos. A tarefa Serviço da Web incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa esse gerenciador de conexões.  
  
 Quando você adiciona um gerenciador de conexões HTTP a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que será resolvido para uma conexão HTTP em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **HTTP.**  
  
 Você pode configurar um gerenciador de conexões HTTP das seguintes maneiras:  
  
-   Use credenciais. Se o gerenciador de conexões HTTP usar credenciais, suas propriedades incluirão o nome de usuário, a senha e o domínio.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
-   Use um certificado do cliente. Se o gerenciador de conexões usar um certificado do cliente, suas propriedades incluirão o nome de certificado.  
  
-   Forneça um tempo limite para conexão com o servidor e um tamanho da parte para gravar dados.  
  
-   Use um servidor proxy. O servidor proxy também pode ser configurado para usar credenciais e ignorar o servidor proxy com o uso de endereços locais em seu lugar.  
  
## Configuração do gerenciador de conexões HTTP  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
-   [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## Consulte também  
 [Tarefa Serviços Web](../../integration-services/control-flow/web-service-task.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  