---
title: "Importar e exportar dados com o Assistente de exportação e importação do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: 22419ce21476588f4ff2859185c8b833306fa896
ms.contentlocale: pt-br
ms.lasthandoff: 08/17/2017

---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>Importar e exportar dados com o Assistente de Importação e Exportação do SQL Server

 > Para conteúdo relacionado a versões anteriores do SQL Server, consulte [executar o Assistente de exportação e importação do SQL Server](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx).

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Assistente de Importação e Exportação é uma maneira simples de copiar dados de uma origem para um destino. Esta visão geral descreve as fontes de dados que o assistente pode usar como origens e destinos, bem como as permissões que necessárias para executar o assistente.

## <a name="get-the-wizard"></a>Obter o Assistente
Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="what-happens-when-i-run-the-wizard"></a>O que acontece quando executar o Assistente?
-    **Consulte a lista de etapas.** Para obter uma descrição das etapas no assistente, consulte [as etapas no Assistente para exportação e do SQL Server Import](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Também é uma página separada da documentação de cada página do assistente.  
    \-ou\-
-   **Veja um exemplo simples.** Para obter uma visão rápida em várias telas que você ver em uma sessão típica, dar uma olhada neste exemplo de ponta a ponta simples em uma única página - [começar com esse exemplo simples de Assistente de importação e exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).  

##  <a name="wizardSources"></a>Quais fontes e destinos posso usar?  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard podem copiar dados de e para as fontes de dados listadas na tabela a seguir. Para se conectar a algumas das fontes de dados, você precisará baixar e instalar arquivos adicionais.
 
| Fonte de dados | É necessário baixar outros arquivos? |
|-------------|-----------------------------------------|
|**Bancos de dados corporativos**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 e outros.|SQL Server ou SQL Server Data Tools (SSDT) instala os arquivos que você precisa se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mas SSDT não instala todos os arquivos que você precisa se conectar a outros bancos de dados corporativos, como Oracle ou IBM DB2.<br/><br/>Para se conectar a um banco de dados da empresa, você geralmente precisa ter duas coisas:<br/><br/>1. **Software cliente**. Se você já tiver o software cliente instalado para o seu sistema de banco de dados corporativo, normalmente você terá o que precisa para realizar uma conexão. Se você não tiver instalado o software cliente, pergunte ao administrador de banco de dados como instalar uma cópia licenciada.<br/><br/>2. **Drivers ou provedores de**. Microsoft instala drivers e fornecedores para se conectar ao Oracle. Para se conectar ao DB2 da IBM, obter o provedor OLE DB do Microsoft® para DB2 v 5.0 para Microsoft SQL Server a partir de [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|
|**Arquivos de texto** (arquivos simples)|Não é necessário ter arquivos adicionais.|
|**Arquivos do Microsoft Excel e do Microsoft Access**|O Microsoft Office não instala todos os arquivos que você precisa para se conectar a arquivos de Excel e Access como fontes de dados. Obter o seguinte download - [redistribuível de 2016 do mecanismo de banco de dados Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920).<br/><br/>Para obter mais informações, consulte [conectar-se a uma fonte de dados do Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) ou [conectar-se a uma fonte de dados do Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md).|
|**Fontes de dados do Azure**<br/>Atualmente apenas o Armazenamento de blobs do Azure.|SQL Server Data Tools não instale os arquivos que você precisa para se conectar ao armazenamento de BLOBs do Azure como uma fonte de dados. Baixe o seguinte download – [Feature Pack do Microsoft SQL Server 2016 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=49492).<br/><br/>Para obter mais informações, consulte [conectar ao armazenamento do Azure Blog](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md).|
|**Bancos de dados de software livre**<br/>PostgreSQL, MySql e outros.|Você precisa baixar arquivos adicionais para se conectar a essas fontes de dados.<br/><br/>-Para **PostgreSQL**, consulte [conectar-se a uma fonte de dados PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md).<br/>-Para **MySql**, consulte [conectar-se a uma fonte de dados MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md).|
|**Qualquer outra fonte de dados para o qual um provedor ou driver está disponível**|Normalmente, é necessário baixar arquivos adicionais para se conectar aos seguintes tipos de fontes de dados.<br/><br/>- Qualquer fonte para a qual um **Driver ODBC** está disponível. Para obter mais informações, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).<br/>- Qualquer fonte para a qual um **Provedor de Dados .NET Framework** está disponível.<br/>- Qualquer fonte para a qual um **Provedor OLE DB** está disponível.<br/><br/>Componentes de terceiros que fornecem recursos de origem e destino para outras fontes de dados, às vezes, são comercializados como produtos complementares para SQL Server Integration Services (SSIS).|

## <a name="how-do-i-connect-to-my-data"></a>Como se conectar aos meus dados?
Para obter informações sobre como se conectar a uma fonte de dados usadas com frequência, consulte uma das seguintes páginas.
-   [Conectar ao SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se ao Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se a arquivos simples (arquivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se para o Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se para acesso](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar ao armazenamento de BLOBs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conecte-se com ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se ao PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar ao MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


Para obter informações sobre como se conectar a uma fonte de dados que não esteja listada aqui, consulte [a referência de cadeias de caracteres de Conexão](https://www.connectionstrings.com/). Este site de terceiros contém cadeias de caracteres de conexão de exemplo e obter mais informações sobre provedores de dados e as informações de conexão que eles exigem.

## <a name="what-permissions-do-i-need"></a>Quais permissões preciso?  
 Para executar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com sucesso, você deve ter pelo menos as seguintes permissões. Se você já trabalha com a sua fonte de dados e o destino, você provavelmente já tem as permissões necessárias.
  
|Você precisa de permissões para fazer essas coisas|Se você estiver se conectando ao SQL Server, você precisa essas permissões específicas |  
|-------------------------|----------------------------------------------------|  
|Conecte aos bancos de dados de origem e de destino ou compartilhamentos de arquivos.|Direitos de logon no servidor e no banco de dados.|  
|Exporte ou leia dados do banco de dados ou arquivo de origem.|Permissões SELECT nas tabelas de origem e exibições.|  
|Importe ou grave dados no banco de dados ou arquivo de destino.|Permissões INSERT nas tabelas de destino.|  
|Crie o banco de dados ou arquivo de destino, se aplicável.|Permissões CREATE DATABASE ou CREATE TABLE.|  
|Salve o pacote do SSIS criado pelo assistente, se aplicável.|Se você desejar salvar o pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permissões suficientes para salvar o pacote no banco de dados **msdb** .|  
  
## <a name="get-help-while-the-wizard-is-running"></a>Obter ajuda enquanto o assistente está em execução
> [!TIP]
> Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.   
  
##  <a name="wizardSSIS"></a> O assistente usa o SSIS (SQL Server Integration Services)  
 O Assistente usa o SSIS (SQL Server Integration Services) para copiar os dados. O SSIS é uma ferramenta para extrair, transformar e carregar dados (ETL). As páginas do assistente usam parte da linguagem do SSIS.
  
 No SSIS, a unidade básica é o **pacote**. O assistente cria um pacote do SSIS na memória ao percorrer as páginas do assistente e especificar as opções.    
  
No fim desse assistente, se você tiver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition ou superior instalado, você também terá a opção de salvar o pacote SSIS. Posteriormente, você pode reutilizar o pacote ou estendê-lo usando o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para adicionar tarefas, transformações e lógica controlada por evento. O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é a maneira mais simples de criar um pacote básico do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que copia os dados de uma origem para um destino.

Para obter mais informações sobre SSIS, consulte [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="whats-next"></a>O que vem a seguir?  
 Inicie o assistente. Para obter mais informações, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Consulte também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)



