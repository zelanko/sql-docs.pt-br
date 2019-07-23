---
title: Importar e exportar dados com o Assistente de Importação e Exportação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 21aad290ff47b93903ae9ed76c03d9ff953de3fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044561"
---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>Importar e exportar dados com o Assistente de Importação e Exportação do SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Assistente de Importação e Exportação é uma maneira simples de copiar dados de uma origem para um destino. Esta visão geral descreve as fontes de dados que o assistente pode usar como origens e destinos, bem como as permissões necessárias para executar o assistente.

## <a name="get-the-wizard"></a>Obter o assistente
Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="what-happens-when-i-run-the-wizard"></a>O que acontece quando eu executo o assistente?
-    **Consulte a lista de etapas.** Para obter uma descrição das etapas do assistente, consulte [Etapas do Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Há também uma página separada da documentação para cada página do assistente.  
    \- ou \-
-   **Veja um exemplo.** Para obter uma visão rápida das várias telas exibidas em uma sessão típica, dê uma olhada neste exemplo simples em uma única página – [Introdução a este exemplo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).  

##  <a name="wizardSources"></a> Quais origens e destinos posso usar?  
 O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode copiar dados entre as fontes de dados listadas na tabela a seguir. Para se conectar a algumas dessas fontes de dados, talvez você precise baixar e instalar arquivos adicionais.
 
| Fonte de dados | É necessário baixar outros arquivos? |
|-------------|-----------------------------------------|
|**Bancos de dados corporativos**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 e outros.|O SQL Server ou o SSDT (SQL Server Data Tools) instala os arquivos necessários para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, o SSDT não instala todos os arquivos necessários para se conectar a outros bancos de dados empresariais, como Oracle ou IBM DB2.<br/><br/>Para se conectar a um banco de dados empresarial, geralmente, você precisa ter duas coisas:<br/><br/>1. **Software cliente**. Se você já tiver o software cliente instalado para o seu sistema de banco de dados corporativo, normalmente você terá o que precisa para realizar uma conexão. Se você não tiver instalado o software cliente, pergunte ao administrador de banco de dados como instalar uma cópia licenciada.<br/><br/>2. **Drivers ou provedores**. A Microsoft instala drivers e provedores para se conectar ao Oracle. Para se conectar ao IBM DB2, obtenha o Provedor Microsoft® OLEDB para DB2 v5.0 para o Microsoft SQL Server no [Feature pack do Microsoft SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=52676).<br/><br/>Para obter mais informações, consulte [Conectar-se a uma fonte de dados do SQL Server](connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md) ou [Conectar-se a uma fonte de dados do Oracle](connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md).|
|**Arquivos de texto** (arquivos simples)|Não é necessário ter arquivos adicionais.<br/><br/>Para obter mais informações, consulte [Conectar-se a uma fonte de dados de arquivo simples](connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md).|
|**Arquivos do Microsoft Excel e do Microsoft Access**|O Microsoft Office não instala todos os arquivos que você precisa para se conectar a arquivos de Excel e Access como fontes de dados. Obtenha o seguinte download – [Pacotes Redistribuíveis do Mecanismo de Banco de Dados do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=54920).<br/><br/>Para obter mais informações, consulte [Conectar-se a uma fonte de dados do Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) ou [Conectar-se a uma fonte de dados do Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md).|
|**Fontes de dados do Azure**<br/>Atualmente apenas o Armazenamento de blobs do Azure.|O SQL Server Data Tools não instala os arquivos necessários para se conectar ao Armazenamento de Blobs do Azure como uma fonte de dados. Baixe o seguinte download – [Feature Pack do Microsoft SQL Server 2016 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=49492).<br/><br/>Para obter mais informações, veja [Conectar-se ao Armazenamento de Blobs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md).|
|**Bancos de dados de software livre**<br/>PostgreSQL, MySql e outros.|Para se conectar a essas fontes de dados, você precisa baixar arquivos adicionais.<br/><br/>- Para **PostgreSQL**, consulte [Conectar-se a uma fonte de dados do PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md).<br/>- Para **MySql**, consulte [Conectar-se a uma fonte de dados do MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md).|
|**Qualquer outra fonte de dados para a qual um driver ou provedor está disponível**|Normalmente, é necessário baixar arquivos adicionais para se conectar aos seguintes tipos de fontes de dados.<br/><br/>- Qualquer fonte para a qual um **Driver ODBC** está disponível. Para obter mais informações, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).<br/>- Qualquer fonte para a qual um **Provedor de Dados .NET Framework** está disponível.<br/>- Qualquer fonte para a qual um **Provedor OLE DB** está disponível.<br/><br/>Às vezes, componentes de terceiros que fornecem funcionalidades de origem e destino para outras fontes de dados são comercializados como produtos complementares do SSIS (SQL Server Integration Services).|

## <a name="how-do-i-connect-to-my-data"></a>Como fazer para me conectar aos meus dados?
Para obter informações sobre como se conectar a uma fonte de dados usada com frequência, consulte uma das seguintes páginas:
-   [Conectar ao SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se a arquivos simples (arquivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Armazenamento de Blobs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


Para obter informações sobre como se conectar a uma fonte de dados que não está listada aqui, consulte [A referência de cadeias de conexão](https://www.connectionstrings.com/). Esse site de terceiros contém cadeias de conexão de exemplo e mais informações sobre provedores de dados e as informações de conexão exigidas por elas.

## <a name="what-permissions-do-i-need"></a>Quais permissões são necessárias?  
 Para executar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com sucesso, você deve ter pelo menos as seguintes permissões. Se você já trabalha com a sua fonte de dados e o destino, você provavelmente já tem as permissões necessárias.
  
|Você precisa de permissões para fazer essas coisas|Se você estiver se conectando ao SQL Server, precisará destas permissões específicas |  
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

## <a name="see-also"></a>Confira também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)


