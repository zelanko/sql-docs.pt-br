---
title: "Editor do Destino SQL (p&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sqlserverdestadapter.connection.f1"
helpviewer_keywords: 
  - "Editor de Destino SQL"
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Editor do Destino SQL (p&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos SQL** para especificar informações de fonte de dados e visualizar os resultados. O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega dados em tabelas ou exibições em um banco de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações sobre destino do SQL Server, consulte [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md).  
  
## Opções  
 **gerenciador de conexões OLE DB**  
 Selecione uma conexão existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB**.  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela**.  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta**. A visualização pode exibir até 200 linhas.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destinos SQL &#40;página Mapeamentos&#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [Editor de Destinos SQL &#40;página Avançado&#41;](../../integration-services/data-flow/sql-destination-editor-advanced-page.md)   
 [Carregar dados em massa por meio do destino do SQL Server](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  