---
title: Configurar propriedades de relatório para relatórios do Power View | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e353d941a009b4dce432a0e16fa2d0305311bb1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---configure-reporting-properties-for-power-view-reports"></a>Complementares lição - configurar propriedades de relatório para relatórios do Power View
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Esta lição suplementar, você definirá propriedades de relatório para o projeto de vendas pela Internet AW. As propriedades de relatório facilitam para os usuários finais o trabalho de selecionar e exibir dados de modelo no Power View. Você também definirá as propriedades para ocultarem determinadas colunas e tabelas, e criará novos dados para usar em gráficos.   
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Esta lição suplementar faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição suplementar, conclua todas as lições anteriores.  
Para concluir esta lição suplementar específica, você deverá ter o seguinte:  
  
-   O projeto de vendas pela Internet AW (concluído este tutorial) pronto para ser implantado ou já implantado em um servidor do Analysis Services.  
  
  
## <a name="model-properties-that-affect-reporting"></a>Propriedades do modelo que afetam o relatório  
Ao criar um modelo tabular, há determinadas propriedades que você pode definir em colunas individuais e tabelas para aprimorar a experiência de relatório do usuário final no Power View. Além disso, você pode criar dados de modelo adicionais para dar suporte à visualização de dados e outros recursos específicos para o cliente de relatório. Para o Modelo de Vendas pela Internet do Adventure Works de exemplo, aqui estão algumas das alterações que você fará:  
  
-   **Adicionar novos dados** – A adição de novos dados em uma coluna calculada usando uma fórmula DAX cria informações de data em um formato que é mais fácil de exibir em gráficos.  
  
-   **Ocultar tabelas e colunas que não são úteis para o usuário final** – A propriedade **Hidden** controla se as tabelas e colunas de tabela são exibidas no cliente de relatório. Os itens que estão ocultos ainda fazem parte do modelo e permanecem disponíveis para consultas e cálculos.  
  
-   **Habilitar tabelas de um clique** – Por padrão, nenhuma ação ocorrerá se um usuário final clicar em uma tabela na lista de campos. Para alterar este comportamento de modo que um clique na tabela adicione a tabela ao relatório, você definirá o Conjunto de Campos Padrão em cada coluna que você deseja incluir na tabela. Esta propriedade é definida nas colunas da tabela que os usuários finais provavelmente desejarão usar.  
  
-   **Definir o agrupamento quando necessário** – A propriedade **Keep Unique Rows** determina se os valores na coluna devem ser agrupados por valores em um campo diferente, como um campo de identificador. Para colunas que contêm valores duplicados como Nome de Cliente (por exemplo, vários clientes com o nome de Bruno Dias), é importante agrupar (manter linhas exclusivas) no campo **Identificador de Linha** para fornecer aos usuários finais os resultados corretos.  
  
-   **Definir tipos e formatos de dados** – Por padrão, o Power View aplica regras com base no tipo de dados de coluna para determinar se o campo pode ser usado como uma medida. Como cada visualização de dados no Power View também tem regras sobre em que local as medidas e as não medidas podem ser colocadas, é importante definir o tipo de dados no modelo ou substituir o padrão, para obter o comportamento desejado para o usuário final.  
  
-   **Definir a propriedade Sort by Column** – A propriedade **Sort By Column** especifica se os valores na coluna devem ser classificados por valores em um campo diferente. Por exemplo, na coluna Calendário do Mês que contém o nome do mês, classifique pela coluna Número do Mês.  
  
## <a name="hide-tables-from-client-tools"></a>Ocultar as tabelas das ferramentas de cliente  
Como já existe uma coluna calculada Categoria do Produto e Subcategoria do Produto na tabela Produto, não é necessário ter as tabelas Categoria do Produto e Subcategoria do Produto visível para aplicativos cliente.  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>Para ocultar as tabelas Categoria do Produto e Subcategoria do Produto  
  
1.  No designer de modelos, clique com o botão direito do mouse na tabela **Categoria do Produto** (guia) e clique em **Ocultar das Ferramentas de Cliente**.  
  
2.  Clique com o botão direito do mouse na tabela **Subcategoria do Produto** (guia) e clique em **Ocultar das Ferramentas de Cliente**.  
  
## <a name="create-new-data-for-charts"></a>Criar novos dados para gráficos  
Muitas vezes, pode ser necessário criar novos dados em seu modelo usando fórmulas DAX. Nesta tarefa, você adicionará duas novas colunas calculadas à tabela Data. Estas novas colunas fornecerão campos de data em um formato conveniente para serem usados em gráficos.  
  
#### <a name="to-create-new-data-for-charts"></a>Para criar novos dados para gráficos  
  
1.  Na tabela **Data** , role a tela para a extrema direita e clique em **Adicionar Coluna**.  
  
2.  Adicione duas novas colunas calculadas usando as fórmulas a seguir na barra de fórmulas:  
  
    |Nome da coluna|Fórmula|  
    |---------------|-----------|  
    |Ano Trimestre|= [Ano civil] & "Q" & [trimestre do calendário]|  
    |Ano Mês|= [Ano civil] & FORMAT([Mês],"#00")|  
  
## <a name="default-field-set"></a>Conjunto de Campos Padrão  
O conjunto de campos padrão é uma lista predefinida de colunas e medidas para uma tabela que são adicionadas automaticamente a uma tela de relatório quando a tabela é clicada na lista de campos de relatório. Essencialmente, você pode especificar as colunas padrão, as medidas e a ordenação de campos que os usuários desejarão ver quando esta tabela for visualizada em relatórios do Power View.  Para o modelo de Vendas pela Internet, você definirá um conjunto de campos padrão e ordem para as tabelas Customer, Geography e Product. Incluídas estão somente as colunas mais comuns que os usuários desejarão ver ao analisarem os dados de Vendas pela Internet do Adventure Works usando os relatórios do Power View.  
  
Para obter informações detalhadas sobre o conjunto de campos padrão, consulte [configurar conjunto de campos padrão para relatórios do Power View](../analysis-services/tabular-models/power-view-configure-default-field-set-for-reports.md) nos Manuais Online do SQL Server.  
  
#### <a name="to-set-default-field-set-for-tables"></a>Para definir o Conjunto de Campos Padrão para tabelas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Na janela **Propriedades** , em **Propriedades de Relatório**, na propriedade **Conjunto de Campos Padrão** , clique em **Clique para editar** para abrir a caixa de diálogo **Conjunto de Campos Padrão** .  
  
3.  Na caixa de diálogo **Conjunto de Campos Padrão** , na caixa de listagem **Campos na tabela** , pressione Ctrl e selecione os campos a seguir e clique em **Adicionar**.  
  
    **Birth Date**, **Customer Alternate Id**, **First Name**e **Last Name**.  
  
4.  Na janela **Campos padrão, na ordem** , use os botões Mover para Cima e Mover para Baixo para colocar na seguinte ordem:  
  
    **Customer Alternate Id**  
  
    **First Name**  
  
    **Last Name**  
  
    **Data de Nascimento**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Conjunto de Campos Padrão** da tabela **Customer** .  
  
6.  Realize estas mesmas etapas para a tabela **Geography** , selecionando os campos a seguir e colocando-os nesta ordem.  
  
    **City**, **State Province Code**e **Country Region Code**.  
  
7.  Por fim, realize estas mesmas etapas para a tabela **Product** , selecionando os campos a seguir e colocando-os nesta ordem.  
  
    **Product Alternate Id**e **Product Name**.  
  
## <a name="table-behavior"></a>Comportamento de tabela  
Usando as propriedades do Comportamento da Tabela, você pode alterar o comportamento padrão para diferentes tipos de visualização e o comportamento de agrupamento para tabelas usadas nos relatórios do Power View. Isto permite uma melhor colocação padrão de identificação de informações como nomes, imagens ou títulos em layouts de peça, cartão e gráfico.  
  
Para obter informações detalhadas sobre as propriedades de comportamento de tabela, consulte [configurar propriedades de comportamento de tabela para relatórios do Power View](../analysis-services/tabular-models/power-view-configure-table-behavior-properties-for-reports.md) nos Manuais Online do SQL Server.  
  
#### <a name="to-set-table-behavior"></a>Para definir o comportamento da tabela 
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Na janela **Propriedades** , na propriedade **Comportamento da Tabela** , clique em **Clique para editar**, para abrir a caixa de diálogo **Comportamento da Tabela** .  
  
3.  Na caixa de diálogo **Comportamento da Tabela** , na caixa de listagem suspensa **Identificador de Linha** , selecione a coluna **Customer Id** .  
  
4.  Na caixa de listagem **Manter Linhas Exclusivas** , selecione **First Name** e **Last Name**.  
  
    As configurações dessa propriedade especificam que essas colunas fornecem valores que devem ser tratados como exclusivos mesmo se forem duplicados (por exemplo, nome e sobrenome do funcionário, quando dois ou mais funcionários têm o mesmo nome).  
  
5.  Na caixa de listagem suspensa **Rótulo Padrão** , selecione a coluna **Last Name** .  
  
    As configurações dessa propriedade especificam que esta coluna fornece um nome para exibição para representar os dados de linha.  
  
6.  Repita estas etapas para a tabela **Geography** , selecionando a coluna **Geography Id** como o Identificador de Linha e a coluna **City** na caixa de listagem **Manter Linhas Exclusivas** . Você não precisa definir um Rótulo Padrão para esta tabela.  
  
7.  Repita estas etapas para a tabela **Product** , selecionando a coluna **Product Id** como o Identificador de Linha e a coluna **Product Name** na caixa de listagem **Manter Linhas Exclusivas** . Em **Rótulo Padrão**, selecione **Product Alternate Id**.  
  
## <a name="reporting-properties-for-columns"></a>Propriedades de relatório para colunas  
Há várias propriedades básicas de coluna e propriedades específicas de relatório nas colunas que você pode definir para melhorar a experiência de relatório do modelo. Por exemplo, pode não ser necessário que os usuários vejam todas as colunas em todas as tabelas. Da mesma maneira que você ocultou as tabelas Product Category e Product Subcategory anteriormente, usando a propriedade Oculto de uma coluna, você pode ocultar colunas específicas de uma tabela que seriam mostradas de outra forma. Outras propriedades, como Formato de Dados e Classificar por Coluna, também podem afetar o modo como os dados da coluna podem aparecer nos relatórios. Você definirá algumas dessas propriedades em colunas específicas agora. Outras colunas não exigem nenhuma ação e não são mostradas abaixo.  
  
Você somente definirá algumas propriedades de coluna diferentes aqui, mas há muitas outras. Para obter mais informações sobre a coluna de propriedades de relatório, consulte [propriedades de coluna](../analysis-services/tabular-models/column-properties-ssas-tabular.md) nos Manuais Online do SQL Server.  
  
#### <a name="to-set-properties-for-columns"></a>Para definir propriedades para colunas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Clique na coluna **Customer Id** para exibir as propriedades de coluna na janela **Propriedades** .  
  
3.  Na janela **Propriedades** , defina a propriedade **Hidden** como True. A coluna **Customer Id** torna-se acinzentada no designer de modelos.  
  
4.  Repita estas etapas, definindo a coluna e as propriedades de relatório a seguir para cada tabela especificada. Deixe todas as outras propriedades em suas configurações padrão.  
  
    Observação: para todas as colunas de data, verifique se o **Tipo de Dados** é **Date**.  
  
    **Cliente**  
  
    |Coluna|Propriedade|Value|  
    |----------|------------|---------|  
    |Geography Id|Oculto|Verdadeiro|  
    |Birth Date|Formato de Dados|Data Abreviada|  
  
    **Data**  
  
    > [!NOTE]  
    > Como a tabela Date foi selecionada como a tabela de datas do modelo usando a configuração Marcar como Tabela de Data, na Lição 7: Marcar como Tabela de Data, e a coluna Date na tabela Date como a coluna a ser usada como o identificador exclusivo, a propriedade Identificador de Linha para a coluna Date será automaticamente definida como True e não poderá ser alterada. Ao usar as funções de inteligência de tempo em fórmulas DAX, você deverá especificar uma tabela de data. Neste modelo, você criou várias medidas usando funções de inteligência de tempo para calcular dados de vendas para vários períodos como trimestres anterior e atual, e também para usar em KPIs. Para obter mais informações sobre como especificar uma tabela de data, consulte [especifique marcar como tabela de data para uso com inteligência de tempo](../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md) nos Manuais Online do SQL Server.  
  
    |Coluna|Propriedade|Value|  
    |----------|------------|---------|  
    |Data|Formato de Dados|Data Abreviada|  
    |Day Number of Week|Oculto|Verdadeiro|  
    |Day Name|Sort By Column|Day Number of Week|  
    |Day Of Week|Oculto|Verdadeiro|  
    |Day of Month|Oculto|Verdadeiro|  
    |Day of Year|Oculto|Verdadeiro|  
    |Month Name|Sort By Column|Month|  
    |Month|Oculto|Verdadeiro|  
    |Month Calendar|Oculto|Verdadeiro|  
    |Fiscal Quarter|Oculto|Verdadeiro|  
    |Fiscal Year|Oculto|Verdadeiro|  
    |Fiscal Semester|Hidden|Verdadeiro|  
  
    **Geography**  
  
    |Coluna|Propriedade|Value|  
    |----------|------------|---------|  
    |Geography Id|Oculto|Verdadeiro|  
    |Sales Territory Id|Oculto|Verdadeiro|  
  
    **Product**  
  
    |Coluna|Propriedade|Value|  
    |----------|------------|---------|  
    |Product Id|Oculto|Verdadeiro|  
    |Product Alternate Id|Rótulo Padrão|Verdadeiro|  
    |Product Subcategory Id|Oculto|Verdadeiro|  
    |Product Start Date|Formato de Dados|Data Abreviada|  
    |Product End Date|Formato de Dados|Data Abreviada|  
  
    **Internet Sales**  
  
    |Coluna|Propriedade|Value|  
    |----------|------------|---------|  
    |Product Id|Oculto|Verdadeiro|  
    |Customer Id|Oculto|Verdadeiro|  
    |Promotion Id|Oculto|Verdadeiro|  
    |Currency Id|Oculto|Verdadeiro|  
    |Sales Territory Id|Oculto|Verdadeiro|  
    |Order Quantity|Tipo de Dados<br /><br />Formato de Dados<br /><br />Casas Decimais|Número Decimal<br /><br />Número Decimal<br /><br />0|  
    |Data do Pedido|Formato de Dados|Data Abreviada|  
    |Due Date|Formato de Dados|Data Abreviada|  
    |Ship Date|Formato de Dados|Data Abreviada|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Reimplantar o modelo de tabela de vendas pela Internet da Adventure Works  
Como você alterou o modelo, deverá reimplantá-lo.  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Para reimplantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
-   No SSDT, clique no **criar** menu e clique **implantar a modelo de vendas do Adventure Works Internet**.  
  
    A caixa de diálogo **Implantar** será exibida com o status de implantação dos metadados, bem como cada tabela incluída no modelo.  
  
## <a name="next-steps"></a>Próximas etapas  
Agora você pode usar o Power View para visualizar dados do modelo. Verifique se as contas do Analysis Services e do Reporting Services no site do SharePoint têm permissões de leitura para a instância do Analysis Services onde você implantou seu modelo.  
  
Para criar uma fonte de dados de relatório do Reporting Services que aponta para seu modelo, consulte [Tipo de conexão de modelo de tabela (SSRS)](http://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx).  
  
  
  
