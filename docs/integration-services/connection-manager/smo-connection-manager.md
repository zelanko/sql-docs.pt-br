---
title: "Gerenciador de conex&#245;es SMO | Microsoft Docs"
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
  - "conexões [Integration Services], SMO"
  - "gerenciador de conexões SMO"
  - "gerenciadores de conexões [Integration Services], SMO"
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# Gerenciador de conex&#245;es SMO
  Um gerenciador de conexões SMO habilita um pacote para conexão a um servidor do SQL Management Object (SMO). As tarefas de transferência que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui utilizam um gerenciador de conexões do SMO. Por exemplo, a tarefa Transferir Logons que transfere os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um gerenciador de conexões do SMO.  
  
 Quando você adiciona um gerenciador de conexões SMO a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do SMO no momento da execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção do **Connections** no pacote. A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **SMOServer**.  
  
 Você pode configurar um gerenciador de conexões SMO das seguintes maneiras:  
  
-   Especifique o nome de um servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
-   Selecione o modo de autenticação para a conexão com o servidor.  
  
## Configuração do gerenciador de conexões SMO  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], consulte [Editor do Gerenciador de Conexões do SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  