---
title: "Especificar c&#243;pia ou consulta de tabela (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.specifytablecopyorquery.f1"
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 65
---
# Especificar c&#243;pia ou consulta de tabela (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
  Depois de fornecer informações sobre o destino dos dados e sobre como se conectar a eles, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Especificar cópia ou consulta de tabela**. Nesta página, escolha uma das opções a seguir.
-   **Copiar dados de uma ou mais tabelas ou exibições**
-   **Gravar uma consulta para especificar os dados a serem transferidos**
    
> [!TIP] Se você precisar copiar mais de um banco de dados ou objetos de banco de dados diferentes de tabelas e exibições, use o Assistente para Copiar Banco de Dados em vez do Assistente de Importação e Exportação. Para obter mais informações, consulte [Usar o Assistente para Copiar Banco de Dados](../../relational-databases/databases/use-the-copy-database-wizard.md).     
 
## <a name="screen-shot-of-the-specify-table-copy-or-query-page"></a>Captura de tela da página Especificar Cópia ou Consulta de Tabela    
 A captura de tela a seguir mostra a página **Especificar Cópia ou Consulta de Tabela** do assistente.    
    
 ![Table copy or query page of the Import and Export Wizard](../../integration-services/import-export-data/media/table-copy-or-query.png "Table copy or query page of the Import and Export Wizard")    
    
## <a name="specify-whether-to-copy-an-entire-table-or-write-a-query"></a>Especificar se deseja copiar uma tabela inteira ou gravar uma consulta 
 **Copiar dados de uma ou mais tabelas ou exibições**    
 Selecione esta opção se você desejar copiar todos os dados na fonte sem filtrar ou ordenar registros. Depois de clicar em **Avançar**, selecione as tabelas a serem copiadas na página **Selecionar tabelas de origem e exibições**. Para obter mais informações, consulte [Selecionar Tabelas e Exibições de Origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).    

Quando você seleciona **Copiar dados de uma ou mais tabelas ou exibições**, você pode copiar de uma tabela ou exibição para a tabela de destino ou de várias tabelas ou exibições para várias tabelas de destino.    
    
 **Gravar uma consulta para especificar os dados a serem transferidos**    
 Selecione esta opção se você deseja filtrar ou classificar os dados de origem antes de copiá-los para o destino. Depois de clicar em **Avançar**, forneça uma instrução SQL para especificar colunas e selecione as linhas na caixa de diálogo **Fornecer uma consulta de origem**. Para obter mais informações, consulte [Fornecer uma consulta de origem](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md).    
    
Quando você seleciona **Gravar uma consulta para especificar os dados a serem transferidos**, você só pode copiar os resultados de uma consulta para a tabela de destino.    
    
## <a name="why-isnt-the-copy-option-available"></a>Por que a opção Copiar não está disponível?    
 A opção **Copiar dados de uma ou mais tabelas ou exibições** pode não estar disponível quando o assistente usa um provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para se conectar à sua fonte de dados. Isso acontece quando o assistente não tem informações suficientes sobre o provedor de dados para solicitar uma lista de tabelas e exibições da fonte de dados.    
    
 A opção **Copiar dados de uma ou mais tabelas ou exibições** só está disponível para os provedores que têm uma seção ProviderDescription no arquivo ProviderDescriptors.xml. (Por padrão, esse arquivo está em \<*drive*>:\Arquivos de programas\Microsoft SQL Server\130\DTS\ProviderDescriptors.) Cada seção ProviderDescription deste arquivo contém informações necessárias para recuperar metadados do provedor correspondente.    
    
 Por padrão, o arquivo ProviderDescriptors.xml contém uma seção ProviderDescription só para os provedores da lista a seguir.    
    
-   Provedor de dados .Net Framework para SQL Server (System.Data.SqlClient)    
    
-   Provedor de dados .Net Framework para Oracle (System.Data.OracleClient)    
    
-   Provedor de dados .Net Framework para ODBC (System.Data.Odbc)    
    
-    System.Data.OleDb (que se aplica a todos os provedores OLE DB)    
    
-   Provedor Microsoft para DB2 instalado pelo Microsoft Host Integration Server (Microsoft.HostIntegration.MsDb2Client.MsDb2Connection)    
    
 Os desenvolvedores de terceiros podem disponibilizar a opção **Copiar dados de uma ou mais tabelas ou exibições** para seu provedor adicionando uma seção ProviderDescriptor ao arquivo ProviderDescriptors.xml. Para verificar as exigências da seção ProviderDescriptor, consulte o arquivo de esquema ProviderDescriptors.xsd que, por padrão, está localizado na mesma pasta do arquivo ProviderDescriptors.xml.    
    
## <a name="whats-next"></a>O que vem a seguir?    
 Depois de especificar se deseja copiar uma tabela inteira ou fornecer uma consulta, a próxima página depende da opção que você escolher nesta página e também do destino dos dados.    
    
-   Se você selecionou **Copiar dados de uma ou mais tabelas ou exibições**, para a maioria dos destinos, a próxima página é **Selecionar tabelas de origem e exibições**. Nessa página, você seleciona as tabelas e exibições existentes a serem copiadas da fonte de dados para o destino. Para obter mais informações, consulte [Selecionar Tabelas e Exibições de Origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).    
    
-   Se você selecionou **Copiar dados de uma ou mais tabelas ou exibições** e seu destino é um arquivo simples, a próxima página é **Configurar destino arquivo simples**. Nessa página, especifique opções de formatação para o arquivo simples de destino. (Em seguida, após configurar o arquivo simples, a página seguinte é **Selecionar Tabelas e Exibições de Origem**.) Para obter mais informações, consulte [Configurar destino arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).    
    
-   Se você selecionou **Gravar uma consulta para especificar os dados a serem transferidos**, a próxima página é **Fornecer uma consulta de origem**. Nessa página, você grava e testa a instrução SQL que seleciona os dados a serem copiados da fonte de dados para o destino. (Em seguida, após fornecer uma consulta, a página seguinte é **Selecionar Tabelas e Exibições de Origem**.) Para obter mais informações, consulte [Fornecer uma consulta de origem](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md).    
