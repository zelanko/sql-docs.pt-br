---
description: Selecionar tabelas de origem e exibições (Assistente de Importação e Exportação do SQL Server)
title: Selecionar tabelas de origem e exibições (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57485f68a1e9418e3d9d2402257599bf54e1ad7b
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439310"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Selecionar tabelas de origem e exibições (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Depois de especificar que deseja copiar uma tabela inteira ou de fornecer uma consulta, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Selecionar Tabelas e Exibições de Origem** . Nessa página, você seleciona as tabelas e as exibições existentes que deseja copiar. Em seguida, mapeia as tabelas de origem para tabelas de destino novas ou existentes. Opcionalmente, você também examina o mapeamento de colunas individuais e visualiza dados de exemplo.

> [!TIP]
> Se precisar copiar mais de um banco de dados do SQL Server ou objetos de banco de dados do SQL Server diferentes de tabelas e exibições, use o Assistente para Copiar Banco de Dados em vez do Assistente de Importação e Exportação. Para obter mais informações, consulte [Usar o Assistente para Copiar Banco de Dados](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Captura de tela – se você pretende copiar tabelas  
 A captura de tela a seguir mostra um exemplo da página **Selecionar Tabelas e Exibições de Origem** do assistente depois de selecionar a opção **Copiar dados de uma ou mais tabelas ou exibições** na página **Especificar Cópia de Tabela ou Consulta** . Na lista, você pode ver todas as tabelas e as exibições disponíveis na fonte de dados.
 
Neste exemplo, a lista **Origem** contém todas as tabelas do banco de dados de exemplo AdventureWorks. A linha selecionada mostra que o usuário deseja copiar a tabela **Sales.Customer** da origem para a nova tabela **Sales.CustomerNew** no destino. 
   
 ![Captura de tela mostrando a página Selecionar tabelas do Assistente de Importação e Exportação usada para copiar tabelas.](../../integration-services/import-export-data/media/select-tables1.png "Página Selecionar tabelas do Assistente de Importação e Exportação")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Captura de tela – se você forneceu uma consulta  
 A captura de tela a seguir mostra um exemplo da página **Selecionar Tabelas e Exibições de Origem** do assistente depois de selecionar a opção **Gravar uma consulta para especificar os dados a serem transferidos** na página **Especificar Cópia de Tabela ou Consulta** . A lista **Origem** contém apenas uma única linha, na qual o item nomeado `[Query]` representa a consulta fornecida na página **Fornecer uma Consulta de Origem** .
 
Neste exemplo, o usuário deseja copiar os resultados de consulta da origem para a tabela **Sales.CustomerNew** no destino.  
    
 ![Captura de tela mostrando a página Selecionar tabelas do Assistente de Importação e Exportação se você forneceu uma consulta.](../../integration-services/import-export-data/media/select-tables2.png "Página Selecionar tabelas do Assistente de Importação e Exportação")  

## <a name="select-source-and-destination-tables"></a>Selecionar tabelas de origem e de destino 
**Origem**  
Usando as caixas de seleção, selecione da lista de tabelas e exibições disponíveis para copiar para o destino. Por padrão, os dados da fonte de dados são copiados sem alterações. Se você criar uma nova tabela de destino, o esquema para a nova tabela – ou seja, a lista de colunas e suas propriedades – também será copiado sem alteração da fonte de dados.

Se você forneceu uma consulta, a lista contém somente um item com o nome `[Query]`. 

**Destino**  
 Selecione uma tabela de destino na lista para cada tabela ou consulta de origem, ou digite o nome de uma nova tabela que você deseja que o Assistente crie. Se você selecionar uma tabela de destino existente, a tabela deverá ter colunas com os tipos de dados compatíveis com os dados de origem.  

> [!NOTE]
> Se o assistente for interrompido no momento da criação de uma nova tabela manualmente no banco de dados de destino usando uma ferramenta externa (como  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), a nova tabela não ficará visível imediatamente na lista de tabelas de destino disponíveis. Para atualizar a lista de tabelas de destino, volte até a página **Escolha um Destino** , selecione novamente o banco de dados de destino para atualizar a lista de tabelas disponíveis e prossiga novamente até a página **Selecionar Tabelas e Exibições de Origem** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Opcionalmente, examine os mapeamentos de coluna e visualize os dados
**Editar mapeamentos**   
Opcionalmente, clique em **Editar mapeamentos** para exibir a caixa de diálogo **Mapeamentos de Coluna** para a tabela selecionada. Use a caixa de diálogo **Mapeamentos de Coluna** para fazer o seguinte,
-   Examine o mapeamento de colunas individuais entre a origem e o destino.
-   Copie apenas um subconjunto de colunas selecionando **ignore** para as colunas que você não deseja copiar.

Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Visualização**  
Opcionalmente, clique em **Visualização** para visualizar até 200 linhas de dados de exemplo na caixa de diálogo **Visualizar Dados** . Isso confirma se o assistente vai copiar os dados que você deseja copiar. Para obter mais informações, consulte [Visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Depois de visualizar os dados, é recomendável alterar as opções selecionadas nas páginas anteriores do assistente. Para fazer essas alterações, retorne à página **Selecionar Tabelas e Exibições de Origem** , clique em **Voltar** para retornar às páginas anteriores, nas quais é possível alterar as seleções.  

## <a name="select-source-and-destination-tables-for-excel"></a>Selecionar tabelas de origem e de destino para Excel

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

### <a name="excel-source-tables"></a>Tabelas de origem do Excel
A lista de tabelas e de exibições de origem para uma fonte de dados do Excel inclui dois tipos de objetos do Excel.
-   **Planilhas** . Os nomes de planilha são seguidos pelo cifrão ($), por exemplo, **'Sheet1$'** .
-   **Intervalos nomeados.** Os intervalos nomeados, caso haja algum, são listados por nome.

Se desejar carregar dados de ou para um intervalo de células específico sem nome, por exemplo, de ou para **[Sheet1$A1:B4]** , você precisará gravar uma consulta. Volte à página **Especificar Cópia ou Consulta de Tabela** e clique em **Gravar uma consulta para especificar os dados a serem transferidos** .

### <a name="excel-destination-tables"></a>Tabelas de destino do Excel
Se você estiver exportando dados para o Excel, será possível especificar o destino de uma das três maneiras a seguir.
-   **Planilha.** Para especificar uma planilha, acrescente o caractere $ ao final do nome da planilha e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$]** .
-   **Intervalo nomeado.** Para especificar um intervalo nomeado, basta usar o nome do intervalo, por exemplo, **MyDataRange** .
-   **Intervalo sem nome.** Para especificar um intervalo de células ainda não nomeado, acrescente o caractere $ ao final do nome da planilha, adicione a especificação do intervalo e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$A1:B4]** .

> [!TIP]
> Ao usar o Excel como uma origem ou destino, é uma boa ideia clicar em **Editar Mapeamentos** e examinar os mapeamentos de tipo de dados na página **Mapeamentos de Colunas** . 

## <a name="whats-next"></a>E agora?  
 Depois de selecionar as tabelas e exibições existentes para copiar e mapeá-las para seus destinos, a próxima página será **Salvar e Executar Pacote** . Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da sua configuração, você também poderá salvar o pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criado pelo assistente para personalizá-lo e reutilizá-lo posteriormente. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Confira também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)



