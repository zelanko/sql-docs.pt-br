---
title: "Instru&#231;&#227;o Create Table SQL (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.createtablesql.f1"
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
caps.latest.revision: 67
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 62
---
# Instru&#231;&#227;o Create Table SQL (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
Se você selecionar **Criar tabela de destino** e, em seguida, selecionar **Editar SQL** na caixa de diálogo **Mapeamentos de Colunas**, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará a caixa de diálogo **Instrução SQL Create Table**. Nessa página, examine e, opcionalmente, personalize o comando **CREATE TABLE** que o assistente executará para criar a nova tabela de destino.
  
> [!NOTE] Se você estiver procurando informações sobre a instrução CREATE TABLE do [!INCLUDE[tsql](../../includes/tsql-md.md)], não sobre a caixa de diálogo **Instrução Create Table do SQL** do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). 
  
## <a name="screen-shot-of-the-create-table-sql-statement-page"></a>Captura de tela da página Criar Instrução SQL de Tabela  
 A captura de tela a seguir mostra a caixa de diálogo **Instrução Create Table do SQL** do Assistente.
 
Neste exemplo, a caixa **Instrução SQL** contém a instrução **CREATE TABLE** padrão gerada pelo assistente. Essa instrução cria uma nova tabela de destino que é uma cópia da tabela de origem **Person.Address**. 
  
 ![Create table page of the Import and Export Wizard](../../integration-services/import-export-data/media/create-table.png "Create table page of the Import and Export Wizard")  
  
## <a name="review-or-regenerate-the-create-table-statement"></a>Examinar ou gerar novamente a instrução CREATE TABLE  
 **Instrução SQL**  
 Exibe a instrução SQL gerada automaticamente e permite que ela seja personalizada. Para obter mais informações sobre a instrução CREATE TABLE e a sintaxe, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 Se você alterar o comando CREATE TABLE padrão, também precisará alterar os mapeamentos de coluna associados.  
  
 Para incluir um retorno de carro no texto da instrução SQL, pressione CTRL+ENTER. Se você pressionar somente ENTER, a caixa de diálogo será fechada.  
  
 **Gerar automaticamente**  
 Restaure a instrução SQL padrão, caso ela tenha sido modificada, clicando em **Gerar Automaticamente**.  
  
## <a name="create-a-table-that-includes-a-filestream-column"></a>Criar uma tabela que inclui uma coluna FILESTREAM  
 O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. Essa instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo se a tabela de origem tiver uma coluna FILESTREAM. Para copiar uma coluna FILESTREAM usando o assistente, primeiro implemente o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM manualmente à instrução CREATE TABLE na caixa de diálogo **Instrução SQL Create Table**. Para obter mais informações sobre FILESTREAM, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de examinar e personalizar o comando CREATE TABLE e clicar em **OK**, a caixa de diálogo **Instrução Create Table do SQL** retornará a caixa de diálogo **Mapeamentos de Coluna**. Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
