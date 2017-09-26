---
title: "Selecionar tabelas de origem e exibições (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 96
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9a0c3c4fc8d41206ea077498dafb755e7b433a78
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Selecionar tabelas de origem e exibições (Assistente de Importação e Exportação do SQL Server)
  Depois de especificar que deseja copiar uma tabela inteira ou de fornecer uma consulta, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Selecionar Tabelas e Exibições de Origem**. Nessa página, você seleciona as tabelas e as exibições existentes que deseja copiar. Em seguida, mapeia as tabelas de origem para tabelas de destino novas ou existentes. Opcionalmente, você também examina o mapeamento de colunas individuais e visualiza dados de exemplo.

> [!TIP]
> Se você precisa copiar mais de um banco de dados do SQL Server ou objetos de banco de dados do SQL Server que não sejam de tabelas e modos de exibição, use o Assistente para cópia de banco de dados em vez do Assistente de importação e exportação. Para obter mais informações, consulte [Usar o Assistente para Copiar Banco de Dados](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Captura de tela - se você pretende copiar tabelas  
 A captura de tela a seguir mostra um exemplo da **selecionar tabelas de origem e exibições** página do assistente quando você tiver selecionado o **copiar dados de uma ou mais tabelas ou exibições** opção o ** Especifique a cópia da tabela ou consulta** página. Na lista, você pode ver todas as tabelas e as exibições disponíveis na fonte de dados.
 
Neste exemplo, o **fonte** lista contém todas as tabelas no banco de dados de exemplo AdventureWorks. A linha selecionada mostra que o usuário deseja copiar o **Sales. Customer** tabela da origem para o novo **Sales.CustomerNew** tabela no destino. 
   
 ![Página Selecione as tabelas do Assistente de importação e exportação](../../integration-services/import-export-data/media/select-tables1.png "página Selecione as tabelas do Assistente de importação e exportação")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Captura de tela - se você forneceu uma consulta  
 A captura de tela a seguir mostra um exemplo da **selecionar tabelas de origem e exibições** página do assistente quando você tiver selecionado o **escrever uma consulta para especificar os dados a serem transferidos** opção no **Especificar cópia da tabela ou consulta** página. O **fonte** lista contém apenas uma única linha, onde o item nomeado `[Query]` representa a consulta que você forneceu no **fornecer uma consulta de origem** página.
 
Neste exemplo, o usuário deseja copiar os resultados de consulta da origem para a tabela **Sales.CustomerNew** no destino.  
    
 ![Página Selecione as tabelas do Assistente de importação e exportação](../../integration-services/import-export-data/media/select-tables2.png "página Selecione as tabelas do Assistente de importação e exportação")  

## <a name="select-source-and-destination-tables"></a>Selecionar tabelas de origem e de destino 
**Origem**  
Usando as caixas de seleção, selecione da lista de tabelas e exibições disponíveis para copiar para o destino. Por padrão, os dados da fonte de dados são copiados sem alterações. Se você criar uma nova tabela de destino, o esquema para a nova tabela - ou seja, a lista de colunas e suas propriedades - também é copiado sem alteração da fonte de dados.

Se você forneceu uma consulta, a lista contém apenas um item com o nome `[Query]`. 

**Destino**  
 Selecione uma tabela de destino na lista para cada tabela ou consulta de origem, ou digite o nome de uma nova tabela que você deseja que o Assistente crie. Se você selecionar uma tabela de destino existente, a tabela deverá ter colunas com os tipos de dados compatíveis com os dados de origem.  

> [!NOTE]
> Se o assistente for interrompido no momento da criação de uma nova tabela manualmente no banco de dados de destino usando uma ferramenta externa (como  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), a nova tabela não ficará visível imediatamente na lista de tabelas de destino disponíveis. Para atualizar a lista de tabelas de destino, volte até a página **Escolha um Destino** , selecione novamente o banco de dados de destino para atualizar a lista de tabelas disponíveis e prossiga novamente até a página **Selecionar Tabelas e Exibições de Origem** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Opcionalmente, revise os mapeamentos de coluna e visualizar dados
**Editar mapeamentos**   
Opcionalmente, clique em **editar mapeamentos** para exibir o **mapeamentos de coluna** caixa de diálogo para a tabela selecionada. Use a caixa de diálogo **Mapeamentos de Coluna** para fazer o seguinte,
-   Examine o mapeamento de colunas individuais entre a origem e o destino.
-   Copie apenas um subconjunto de colunas selecionando **ignore** para as colunas que você não deseja copiar.

Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Visualização**  
Opcionalmente, clique em **visualização** para visualizar até 200 linhas de dados de exemplo no **visualizar dados** caixa de diálogo. Isso confirma se o assistente vai copiar os dados que você deseja copiar. Para obter mais informações, consulte [Visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Depois de visualizar os dados, é recomendável alterar as opções selecionadas nas páginas anteriores do assistente. Para fazer essas alterações, retorne à página **Selecionar Tabelas e Exibições de Origem** , clique em **Voltar** para retornar às páginas anteriores, nas quais é possível alterar as seleções.  

## <a name="select-source-and-destination-tables-for-excel"></a>Selecionar tabelas de origem e de destino para Excel

### <a name="excel-source-tables"></a>Tabelas de origem do Excel
A lista de tabelas e de exibições de origem para uma fonte de dados do Excel inclui dois tipos de objetos do Excel.
-   **Planilhas**. Os nomes de planilha são seguidos pelo cifrão ($), por exemplo, **'Sheet1$'**.
-   **Intervalos nomeados.** Os intervalos nomeados, caso haja algum, são listados por nome.

Se desejar carregar dados de ou para um intervalo de células específico sem nome, por exemplo, de ou para **[Sheet1$A1:B4]**, você precisará gravar uma consulta. Volte à página **Especificar Cópia ou Consulta de Tabela** e clique em **Gravar uma consulta para especificar os dados a serem transferidos**.

#### <a name="prepare-the-excel-source-data"></a>Preparar os dados de origem do Excel
Independentemente de você especificar uma planilha ou um intervalo como a tabela de origem, o driver lerá o bloco *contíguo* de células começando pela primeira célula não vazia no canto superior esquerdo da planilha ou do intervalo. Como isso, você não pode ter linhas vazias nos dados de origem. Por exemplo, você não pode ter uma linha vazia entre os cabeçalhos de coluna e as linhas de dados. Se você tiver um título seguido por linhas vazias na parte superior da planilha acima dos seus dados, não será possível consultar a planilha. No Excel, você deve atribuir um nome ao intervalo de dados e consultar o intervalo nomeado em vez da planilha.

### <a name="excel-destination-tables"></a>Tabelas de destino do Excel
Se você estiver exportando dados para o Excel, será possível especificar o destino de uma das três maneiras a seguir.
-   **Planilha.** Para especificar uma planilha, acrescente o caractere $ ao final do nome da planilha e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$]**.
-   **Intervalo nomeado.** Para especificar um intervalo nomeado, basta usar o nome do intervalo, por exemplo, **MyDataRange**.
-   **Intervalo sem nome.** Para especificar um intervalo de células ainda não nomeado, acrescente o caractere $ ao final do nome da planilha, adicione a especificação do intervalo e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$A1:B4]**.

## <a name="special-considerations-for-excel-sources-and-destinations"></a>Considerações especiais para origens e destinos do Excel
Ao usar o Excel como uma origem ou destino, é uma boa ideia clicar em **Editar Mapeamentos** e examinar os mapeamentos de tipo de dados na página **Mapeamentos de Colunas** . 

**Tipos de dados em pastas de trabalho do Excel**. O Excel não é um banco de dados típico. As colunas dele não têm tipos de dados fixos. O assistente reconhece apenas um conjunto limitado de tipos de dados no Excel: numérico, moeda, booliano, data/hora, cadeia de caracteres (255 caracteres ou menos) e memorando (mais de 255 caracteres). O Assistente de amostras de um determinado número de linhas (por padrão, as oito primeiras linhas) em uma fonte de dados existente do Excel para determinar o tipo de dados de cada coluna.

Quando o assistente precisa fazer conversões explícitas de tipos de dados para carregar para ou do Excel, ele tipicamente exibe a página **Revisar Mapeamento de Tipo de Dados** , na qual você pode examinar as conversões. As conversões podem incluir o seguinte.
-   Conversão entre colunas numéricas de precisão dupla e outros tipos de colunas numéricas do Excel.
-   Conversão entre colunas de cadeia de 255 caracteres e de comprimentos diferentes do Excel.
-   Conversão entre colunas de cadeia de caracteres Unicode Excel e as colunas de cadeia de caracteres não Unicode que usam páginas de código específicas.

### <a name="special-considerations-for-excel-sources"></a>Considerações especiais para origens do Excel
**Valores nulos ou ausentes nos dados importados**. Quando uma coluna do Excel parece conter tipos de dados mistos nas oito primeiras linhas amostradas pelo Assistente - por exemplo, valores numéricos misturados com valores de texto - o assistente seleciona o tipo de dados principais, como o tipo de dados da coluna e retorna valores nulos para células esse contêiner n dados de outros tipos. Não é possível alterar esse comportamento do assistente.

**Cadeias de caracteres truncadas nos dados importados**. Quando o assistente determina que uma coluna do Excel contém dados de texto, o assistente seleciona o tipo de dados da coluna (cadeia de caracteres ou memorando) com base no valor mais longo amostrado nas oito primeiras linhas. Se o assistente não encontrar nenhum valor com mais de 255 caracteres nas linhas amostradas, ele tratará a coluna como uma coluna de cadeia de caracteres com 255 caracteres, em vez de uma coluna de memorando, e truncará os valores com mais de 255 caracteres. Para importar dados de uma coluna de memorando sem truncamento, você precisa certificar-se de que a coluna de memorando contém pelo menos um valor maior que 255 caracteres em oito primeiras linhas que serão amostradas pelo assistente.

### <a name="special-considerations-for-excel-destinations"></a>Considerações especiais para destinos do Excel
**Especificando um intervalo existente**. Quando você especificar um intervalo existente como o destino, você obterá um erro se o intervalo tem menos *colunas* dados de origem. No entanto, se o intervalo especificado por você tem menos *linhas* que os dados de origem, o assistente continua gravando linhas e estende a definição do intervalo para coincidir com o novo número de linhas.

**Salvando dados de memorando (ntext)**. Antes de salvar com êxito cadeias de caracteres com mais de 255 caracteres em uma coluna do Excel, o assistente deverá reconhecer o tipo de dados da coluna de destino como **memorando** , e não como **cadeia de caracteres**.
-   Se a tabela de destino já contém linhas de dados, as oito primeiras linhas que serão amostradas pelo assistente precisam conter pelo menos uma linha com um valor maior que 255 caracteres na coluna de memorando.
-   Se a tabela de destino é criada pelo assistente, o **CREATE TABLE** instrução deve usar **LONGTEXT** (ou um de seus sinônimos) como o tipo de dados de coluna de memorando. Verifique o **CREATE TABLE** instrução e revisá-lo, se necessário, clicando em **Editar SQL** lado a **criar tabela de destino** opção o **coluna Mapeamentos de** página.

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de selecionar as tabelas e exibições existentes para copiar e mapeá-las para seus destinos, a próxima página será **Salvar e Executar Pacote**. Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da sua configuração, você também poderá salvar o pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criado pelo assistente para personalizá-lo e reutilizá-lo posteriormente. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Consulte também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



