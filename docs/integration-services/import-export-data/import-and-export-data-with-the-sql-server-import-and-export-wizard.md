---
title: "Importar e exportar dados com o Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exportando dados"
  - "mapeando arquivos [Integration Services]"
  - "Assistente de Importação e Exportação do SQL Server"
  - "pacotes do SSIS, criando"
  - "pacotes [Integration Services], copiando"
  - "pacotes de Integration Services, criando"
  - "pacotes [Integration Services], criando"
  - "pacotes do SQL Server Integration Services, criando"
  - "Assistente de Importação e Exportação"
  - "copiando dados [Integration Services]"
  - "importando dados, pacotes do SSIS"
  - "fontes [Integration Services], copiando dados"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# Importar e exportar dados com o Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Assistente de Importação e Exportação é uma maneira simples de copiar dados de uma origem para um destino. Você não precisa ter o SQL Server instalado para executar o assistente. Esta visão geral descreve as fontes de dados das quais você pode importar dados ou para as quais pode exportar dados usando o assistente e as permissões necessárias para executar o assistente.

Este tópico fornece apenas uma **visão geral** do assistente.
-   Se você está pronto para executar o assistente e apenas deseja saber como iniciá-lo, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).
-   Se você estiver procurando informações sobre as etapas no assistente, selecione a página desejada no menu de navegação de conteúdo. Há uma página separada da documentação para cada página do assistente. Ou pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.

**Obtenha o assistente.** Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!TIP] Se você precisar copiar mais de um banco de dados ou objetos de banco de dados diferentes de tabelas e exibições, use o Assistente para Copiar Banco de Dados em vez do Assistente de Importação e Exportação. Para obter mais informações, consulte [Usar o Assistente para Copiar Banco de Dados](../../relational-databases/databases/use-the-copy-database-wizard.md).

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>Exemplo de um caso de uso comum – Exportando dados para o Excel (vídeo)  
Um uso comum do assistente é exportar dados para o Excel. Assista a um vídeo de quatro minutos no YouTube que demonstra o assistente e explica como fazer isso, com instruções claras e simples – [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (Usando o Assistente de Importação e Exportação do SQL Server para exportar para o Excel).

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a> Quais fontes de dados e destinos posso usar?  
 O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem copiar dados de e para as seguintes fontes de dados. Para usar algumas dessas fontes de dados, você precisará baixar e instalar arquivos adicionais.

| Fonte de dados | É necessário baixar outros arquivos? |
|-------------|-----------------------------------------|
|**Bancos de dados corporativos**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle e outros.|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala os arquivos de que você precisa para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao Oracle, mas não instala os arquivos de que você precisa se conectar a outros bancos de dados corporativos, como IBM DB2 ou Informix.<br/>- Se você já tiver o software cliente instalado no seu sistema de banco de dados corporativo, normalmente você terá o que precisa para realizar uma conexão.<br/>- Se você não tiver o software cliente instalado, pergunte ao administrador de banco de dados como instalar uma cópia licenciada.|
|**Bancos de dados de software livre**<br/>MySql, PostgreSQL, SQLite e outros.|Você precisa baixar arquivos adicionais para se conectar a essas fontes de dados.<br/><br/>- Para **MySql**, consulte [MySQL Connectors](http://dev.mysql.com/downloads/connector/) (Conectores MySQL).<br/>- Para **PostgreSQL**, consulte [psqlODBC – PostgreSQL ODBC driver](https://odbc.postgresql.org/) (psqlODBC – Driver ODBC do PostgreSQL) e produtos de terceiros, como [Npgsql – .NET Data Provider for PostgreSQL](http://www.npgsql.org/) (Npgsql – Provedor de dados .NET para PostgreSQL).<br/>- Para **SQLite**, selecione entre os vários provedores de software livre e drivers disponíveis online.|
|**Arquivos de texto** (arquivos simples).|Não é necessário ter arquivos adicionais.|
|**Arquivos do Microsoft Excel e do Microsoft Access**|O Microsoft Office não instala todos os arquivos que você precisa para se conectar a arquivos de Excel e Access como fontes de dados. Baixe o seguinte – [Tempo de execução do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=50040).|
|**Fontes de dados do Azure**<br/>Atualmente apenas o Armazenamento de blobs do Azure.|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não instala os arquivos de que você precisa para se conectar ao Armazenamento de Blobs do Azure como uma fonte de dados. Baixe o seguinte download – [Feature Pack do Microsoft SQL Server 2016 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=49492).|
|**Qualquer outra fonte de dados está disponível para um conector**.|Normalmente, é necessário baixar arquivos adicionais para se conectar aos seguintes tipos de fontes de dados.<br/><br/>- Qualquer fonte para a qual um **Driver ODBC** está disponível. Crie uma conexão ODBC, selecionando o Provedor .Net Framework para Odbc na página **Escolher uma fonte de dados** ou **Escolha um destino** do assistente e forneça uma cadeia de conexão ou um DSN (Nome de Fonte de Dados) existente que faz referência ao driver ODBC.<br/>- Qualquer fonte para a qual um **Provedor OLE DB** está disponível.<br/>- Qualquer fonte para a qual um **Provedor de Dados .NET Framework** está disponível.<br/>- Outras fontes de dados para as quais **componentes de terceiros** fornecem funcionalidades de origem e de destino. Normalmente esses produtos de terceiros são comercializados como produtos complementares para o SSIS (SQL Server Integration Services).|
  
> [!TIP] Se a fonte de dados exigir uma cadeia de conexão, você poderá encontrar exemplos neste site de terceiros – [The Connection Strings Reference](https://www.connectionstrings.com/).  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>Quais permissões preciso para executar o assistente?  
 Para executar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com sucesso, você deve ter pelo menos as seguintes permissões. Se você já trabalha com a sua fonte de dados e o destino, você provavelmente já tem as permissões necessárias.
  
|Você precisa de permissões para fazer essas coisas|Se você estiver se conectando ao SQL Server, precisará dessas permissões |  
|-------------------------|----------------------------------------------------|  
|Conecte aos bancos de dados de origem e de destino ou compartilhamentos de arquivos.|Direitos de logon no servidor e no banco de dados.|  
|Exporte ou leia dados do banco de dados ou arquivo de origem.|Permissões SELECT nas tabelas de origem e exibições.|  
|Importe ou grave dados no banco de dados ou arquivo de destino.|Permissões INSERT nas tabelas de destino.|  
|Crie o banco de dados ou arquivo de destino, se aplicável.|Permissões CREATE DATABASE ou CREATE TABLE.|  
|Salve o pacote do SSIS criado pelo assistente, se aplicável.|Se você desejar salvar o pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permissões suficientes para salvar o pacote no banco de dados **msdb**.|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a> O assistente usa o SSIS (SQL Server Integration Services)  
 O Assistente usa o SSIS (SQL Server Integration Services) para copiar os dados. O SSIS é uma ferramenta para extrair, transformar e carregar dados (ETL). As páginas do assistente usam parte da linguagem do SSIS.
  
 No SSIS, a unidade básica é o **pacote**. O assistente cria um pacote do SSIS na memória ao percorrer as páginas do assistente e especificar as opções.    
  
No fim desse assistente, se você tiver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition ou superior instalado, você também terá a opção de salvar o pacote SSIS. Posteriormente, você pode reutilizar o pacote ou estendê-lo usando o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para adicionar tarefas, transformações e lógica controlada por evento. O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é a maneira mais simples de criar um pacote básico do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que copia os dados de uma origem para um destino.

Para obter mais informações sobre SSIS, consulte [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="get-help-while-the-wizard-is-running"></a>Obter ajuda enquanto o assistente está em execução
> [!TIP] Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.   
  
## <a name="whats-next"></a>O que vem a seguir?  
 Inicie o assistente. Para obter mais informações, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Consulte também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
