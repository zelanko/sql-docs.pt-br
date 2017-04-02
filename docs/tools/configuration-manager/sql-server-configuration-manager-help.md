---
title: "Ajuda do SQL Server Configuration Manager | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Configuration Manager, ajuda"
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Ajuda do SQL Server Configuration Manager
  Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para configurar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e configurar a conectividade de rede. Para criar ou gerenciar objetos de banco de dados, configurar a segurança e escrever consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] , use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Esta seção contém os tópicos da Ajuda F1 para as caixas de diálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager não pode configurar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager gerencia serviços relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora muitas dessas tarefas possam ser realizadas com a caixa de diálogo Serviços do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, é importante observar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager executa operações adicionais nos serviços que gerencia, como aplicar as permissões corretas quando a conta do serviço é alterada. O uso da caixa de diálogo normal Serviços do Windows para configurar quaisquer serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderia prejudicar o funcionamento do serviço.  
  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas de serviços:  
  
-   Iníciar, parar e pausar serviços  
  
-   Configurar serviços para iniciar automática ou manualmente, desabilitar os serviços ou alterar outras configurações de serviço  
  
-   Alterar as senhas das contas usadas pelos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando sinalizadores de rastreamento (parâmetros de linha de comando)  
  
-   Exibir as propriedades dos serviços  
  
## Configuração de rede do SQL Server  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas relacionadas aos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador:  
  
-   Habilitar ou desabilitar um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Configurar um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
> [!NOTE]  
>  Para obter um breve tutorial sobre como configurar protocolos e conectar-se ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], consulte [Tutorial: Introdução ao mecanismo de banco de dados](../../relational-databases/tutorial-getting-started-with-the-database-engine.md).  
  
## Configuração do SQL Server Native Client  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a biblioteca de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas relacionadas aos aplicativos clientes neste computador:  
  
-   Para aplicativos cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador, especifique a ordem dos protocolos, ao conectar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Configure protocolos de conexão de cliente.  
  
-   Para aplicativos cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , crie aliases para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para que os clientes possam se conectar usando uma cadeia de conexão padrão.  
  
 Para obter mais informações sobre cada uma dessas tarefas, consulte a ajuda F1 de cada tarefa.  
  
#### Para abrir o SQL Server Configuration Manager  
  
-   No menu **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server** (versão), aponte para **Ferramentas de Configuração** e clique em **SQL Server Configuration Manager**.  
  
## Consulte também  
 [Serviços do SQL Server](../../tools/configuration-manager/sql-server-services.md)   
 [Configuração de rede do SQL Server](../../tools/configuration-manager/sql-server-network-configuration.md)   
 [Configuração do SQL Native Client 11.0](../../tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [Escolhendo um protocolo de rede](../Topic/Choosing%20a%20Network%20Protocol.md)  
  
  