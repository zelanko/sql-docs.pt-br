---
title: "Editor de Destino ADO NET (P&#225;gina Gerenciador de Conex&#245;es) | Microsoft Docs"
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
  - "sql13.dts.designer.adonetdest.connection.f1"
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# Editor de Destino ADO NET (P&#225;gina Gerenciador de Conex&#245;es)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino ADO NET** para selecionar a conexão [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
 Para obter mais informações sobre o destino ADO NET, consulte [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tenha o destino ADO NET.  
  
2.  Na guia **Fluxo de Dados**, clique duas vezes no destino ADO NET.  
  
3.  No **Editor de Destino ADO NET**, clique em **Gerenciador de Conexões**.  
  
## Opções estáticas  
 **Gerenciador de conexões**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões ADO NET**.  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova tabela clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova tabela ou exibição usando a caixa de diálogo **Criar Tabela**.  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta**. A visualização pode exibir até 200 linhas.  
  
 **Use a inserção em massa quando disponível**  
 Especifique se a interface <xref:System.Data.SqlClient.SqlBulkCopy> deve ser usada para melhorar o desempenho de operações de inserção em massa.  
  
 Somente os provedores ADO.NET que retornam um objeto <xref:System.Data.SqlClient.SqlConnection> dão suporte ao uso da interface <xref:System.Data.SqlClient.SqlBulkCopy>. O .NET Data Provider for SQL Server (SqlClient) retorna um objeto <xref:System.Data.SqlClient.SqlConnection> e um provedor personalizado pode retornar um objeto <xref:System.Data.SqlClient.SqlConnection>.  
  
 Você pode usar o Provedor de Dados .NET para o SQL Server (SqlClient) para conectar-se ao [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 Se você selecionar **Usar a inserção em massa quando disponível** e definir a opção **Erro** como **Redirecionar a linha**, o lote de dados que o destino redireciona à saída de erro poderá incluir linhas válidas. Para obter mais informações sobre o tratamento de erro em operações em massa, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md). Para obter mais informações sobre a opção **Erro**, consulte [Editor de Destino ADO NET &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  Se uma tabela de origem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Sybase incluir uma coluna de identidade, utilize as tarefas Executar SQL para executar uma instrução SET IDENTITY_INSERT antes e depois do destino ADO NET. A propriedade da coluna de identidade especifica um valor incremental para a coluna. A instrução SET IDENTITY_INSERT habilita os valores explícitos a serem inseridos na coluna de identidade. Para executar as instruções CREATE TABLE e SET IDENTITY na mesma conexão de banco de dados, defina a propriedade **RetainSameConnection** do gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] como **True**. Use também o mesmo gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para as tarefas Executar SQL e para o destino ADO NET.  
>   
>  Para obter mais informações, consulte [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) e [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md).  
  
## Recursos externos  
 Artigo técnico sobre o [Loading data to Windows Azure SQL Database the fast way](http://go.microsoft.com/fwlink/?LinkId=244333) (Carregando dados no Banco de Dados SQL do Microsoft Azure), em sqlcat.com  
  
## Consulte também  
 [Editor de Destino ADO NET &#40;página Mapeamentos&#41;](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [Editor de Destino ADO NET &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md)  
  
  