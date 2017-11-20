---
title: "As etapas no Assistente de exportação e importação do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 22d1f4b78fadab6d7b6659104b54a564f11da308
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Etapas no Assistente de exportação e importação do SQL Server
Este tópico descreve a sequência de etapas para importar e exportar dados com o Assistente para exportação e importação do SQL Server. Ele também contém links para as páginas individuais da documentação que descreve cada página ou caixa de diálogo exibida no assistente.

Este tópico descreve apenas o **etapas** no assistente. Se você estiver procurando por alguma outra coisa, consulte [relacionadas a tarefas e conteúdo](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Etapas para importar e exportar dados  
 A tabela a seguir lista as etapas para importar e exportar dados e as páginas correspondentes do assistente. Dependendo das opções que você seleciona no assistente, você normalmente não vir todas essas páginas.  

Para obter uma visão rápida em várias telas que você ver em uma sessão típica, dar uma olhada neste exemplo de ponta a ponta simples em uma única página - [começar com esse exemplo simples de Assistente de importação e exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

|Etapa|Páginas do Assistente|  
|----------|------------------|  
|**Bem-vindo**<br />Você não precisa realizar nenhuma ação nesta página.|[Bem-vindo ao Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Selecione a fonte** dos dados.|[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**Selecione o destino** para os dados.|[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**Configurar o destino**. (etapas opcionais)<br /><br /> -   Criar um novo banco de dados de destino.<br />-   Se você estiver copiando dados para um arquivo de texto, defina as configurações adicionais.|[Criar banco de dados](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Configurar destino arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Especifique o que você deseja copiar.**|[Especifique a cópia da tabela ou consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Selecionar tabelas de origem e exibições](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Forneça uma consulta de origem](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Configurar a operação de cópia**. (etapas opcionais)<br /><br /> -   Criar uma nova tabela de destino.<br />-Decida o que fazer se o assistente não sabe como mapear tipos de dados entre a origem e destino que você selecionou.<br />-   Examine os mapeamentos de coluna entre a origem e o destino.<br />-   Lidar com problemas com a conversão de tipos de dados entre origem e destino.<br />-   Visualizar os dados a serem copiados.|[Instrução Create Table SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Converter tipos sem verificação de conversão](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Caixa de diálogo de detalhes de conversão de coluna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Caixa de diálogo Visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Copie os dados.**<br /><br /> Opcionalmente, salve as configurações como um pacote do SQL Server Integration Services (SSIS).|[Salvar e executar pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[Salvar Pacote SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Conclua o Assistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Executando operação](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.

## <a name="related"></a>Conteúdo e tarefas relacionadas  
Aqui estão algumas outras tarefas básicas.
-   **Veja um exemplo rápido de como funciona o assistente.**

    -   **Se preferir ver capturas de tela.** Veja este exemplo de ponta a ponta simples em uma única página - [começar com esse exemplo simples de Assistente de importação e exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Se você preferir assistir um vídeo.** Assista a este vídeo de quatro minutos do YouTube que demonstra o assistente e explica claramente e simplesmente como exportar dados para Excel - [usando o SQL Server Assistente de importação e exportação para exportar para Excel](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Saiba mais sobre como funciona o assistente.**

    -   **Saiba mais sobre o assistente.** Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Saiba como se conectar a fontes de dados e destinos.** Se você estiver procurando informações sobre como conectar-se aos seus dados, selecione a página que você deseja na lista aqui - [conectar-se a fontes de dados com o SQL Server Assistente de importação e exportação](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Há uma página separada da documentação para cada uma das várias fontes de dados usadas com frequência. 

-   **Inicie o assistente.** Se você está pronto para executar o assistente e apenas deseja saber como iniciá-lo, consulte [Iniciar o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-     **Obtenha o assistente.** Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).



