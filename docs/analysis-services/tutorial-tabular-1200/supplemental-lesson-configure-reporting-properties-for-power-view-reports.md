---
title: Configurar propriedades de relatório para relatórios do Power View | Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ee35ac833a1170a688bb9439ed4dd8f6b6d6716
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403368"
---
# <a name="supplemental-lesson---configure-reporting-properties-for-power-view-reports"></a>Complementares lição – configurar propriedades de relatório para relatórios do Power View
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição suplementar, você irá definir propriedades de relatório para o projeto de vendas pela Internet AW. Propriedades de relatório facilitam para os usuários selecionem e exibir dados de modelo no Power View. Você também definirá as propriedades para ocultarem determinadas colunas e tabelas, e criará novos dados para usar em gráficos.   
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Esta lição suplementar faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição suplementar, conclua todas as lições anteriores.  
Para concluir esta lição suplementar específica, você deverá ter o seguinte:  
  
-   O projeto de vendas pela Internet AW (concluído este tutorial) pronto para ser implantado ou já implantado em um servidor do Analysis Services.  
  
  
## <a name="model-properties-that-affect-reporting"></a>Propriedades do modelo que afetam o relatório  
Ao criar um modelo tabular, há determinadas propriedades que podem ser definidas nas tabelas e colunas individuais para aprimorar o experiência no Power View de relatórios dos usuários. Além disso, você pode criar dados de modelo adicionais para dar suporte à visualização de dados e outros recursos específicos para o cliente de relatório. Para o Modelo de Vendas pela Internet do Adventure Works de exemplo, aqui estão algumas das alterações que você fará:  
  
-   **Adicionar novos dados** -adicionando novos dados em uma coluna calculada usando uma fórmula DAX cria informações de data em um formato que é mais fácil de exibir em gráficos.  
  
-   **Ocultar tabelas e colunas que não são úteis para o usuário final** – A propriedade **Hidden** controla se as tabelas e colunas de tabela são exibidas no cliente de relatório. Os itens que estão ocultos ainda fazem parte do modelo e permanecem disponíveis para consultas e cálculos.  
  
-   **Habilite as tabelas em um único clique** -por padrão, nenhuma ação ocorrerá se um usuário clicar em uma tabela na lista de campos. Para alterar este comportamento de modo que um clique na tabela adicione a tabela ao relatório, você definirá o Conjunto de Campos Padrão em cada coluna que você deseja incluir na tabela. Esta propriedade é definida nas colunas da tabela que os usuários finais provavelmente desejarão usar.  
  
-   **Definir o agrupamento quando necessário** – A propriedade **Keep Unique Rows** determina se os valores na coluna devem ser agrupados por valores em um campo diferente, como um campo de identificador. Para colunas que contêm valores duplicados como nome do cliente (por exemplo, vários clientes chamados John Smith), é importante agrupar (Manter linhas exclusivas) na **identificador de linha** campo para fornecer a seus usuários finais com o resultados corretos.  
  
-   **Definir tipos e formatos de dados** – Por padrão, o Power View aplica regras com base no tipo de dados de coluna para determinar se o campo pode ser usado como uma medida. Como cada visualização de dados no Power View também tem regras sobre onde as medidas e medidas não podem ser colocadas, é importante definir o tipo de dados no modelo ou substituir o padrão, para obter o comportamento desejado para seu usuário.  
  
-   **Definir a classificação por coluna** propriedade - a **classificar por coluna** propriedade especifica se os valores na coluna devem ser classificados por valores em um campo diferente. Por exemplo, na coluna Calendário do Mês que contém o nome do mês, classifique pela coluna Número do Mês.  
  
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
  
Para obter informações detalhadas sobre o conjunto de campo padrão, consulte [configurar o conjunto de campos padrão para relatórios do Power View](../tabular-models/power-view-configure-default-field-set-for-reports.md).  
  
#### <a name="to-set-default-field-set-for-tables"></a>Para definir o Conjunto de Campos Padrão para tabelas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Na janela **Propriedades** , em **Propriedades de Relatório**, na propriedade **Conjunto de Campos Padrão** , clique em **Clique para editar** para abrir a caixa de diálogo **Conjunto de Campos Padrão** .  
  
3.  Na caixa de diálogo **Conjunto de Campos Padrão** , na caixa de listagem **Campos na tabela** , pressione Ctrl e selecione os campos a seguir e clique em **Adicionar**.  
  
    **Data de nascimento**, **Customer Alternate ID**, **First Name**, **Sobrenome**.  
  
4.  Na janela **Campos padrão, na ordem** , use os botões Mover para Cima e Mover para Baixo para colocar na seguinte ordem:  
  
    **Customer Alternate ID**  
  
    **First Name**  
  
    **Last Name**  
  
    **Data de Nascimento**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Conjunto de Campos Padrão** da tabela **Customer** .  
  
6.  Realize estas mesmas etapas para a tabela **Geography** , selecionando os campos a seguir e colocando-os nesta ordem.  
  
    **City**, **State Province Code**e **Country Region Code**.  
  
7.  Por fim, realize estas mesmas etapas para a tabela **Product** , selecionando os campos a seguir e colocando-os nesta ordem.  
  
    **Product Alternate ID**, **nome do produto**.  
  
## <a name="table-behavior"></a>Comportamento de tabela  
Usando as propriedades do Comportamento da Tabela, você pode alterar o comportamento padrão para diferentes tipos de visualização e o comportamento de agrupamento para tabelas usadas nos relatórios do Power View. Isto permite uma melhor colocação padrão de identificação de informações como nomes, imagens ou títulos em layouts de peça, cartão e gráfico.  
  
Para obter informações detalhadas sobre as propriedades de comportamento da tabela, consulte [configurar propriedades de comportamento de tabela para relatórios do Power View](../tabular-models/power-view-configure-table-behavior-properties-for-reports.md).  
  
#### <a name="to-set-table-behavior"></a>Para definir o comportamento de tabela 
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Na janela **Propriedades** , na propriedade **Comportamento da Tabela** , clique em **Clique para editar**, para abrir a caixa de diálogo **Comportamento da Tabela** .  
  
3.  No **comportamento da tabela** na caixa de **identificador de linha** caixa de listagem suspensa, selecione o **ID do cliente** coluna.  
  
4.  Na caixa de listagem **Manter Linhas Exclusivas** , selecione **First Name** e **Last Name**.  
  
    As configurações dessa propriedade especificam que essas colunas fornecem valores que devem ser tratados como exclusivos mesmo se forem duplicados (por exemplo, nome e sobrenome do funcionário, quando dois ou mais funcionários têm o mesmo nome).  
  
5.  Na caixa de listagem suspensa **Rótulo Padrão** , selecione a coluna **Last Name** .  
  
    As configurações dessa propriedade especificam que esta coluna fornece um nome para exibição para representar os dados de linha.  
  
6.  Repita essas etapas para o **geografia** de tabela, selecionando a **Geography ID** coluna como o identificador de linha e o **Cidade** coluna no **manter linhas exclusivas**  caixa de listagem. Você não precisa definir um Rótulo Padrão para esta tabela.  
  
7.  Repita essas etapas para o **produto** de tabela, selecionando a **ID do produto** coluna como o identificador de linha e o **nome do produto** coluna no **manter exclusivo Linhas** caixa de listagem. Para **rótulo padrão**, selecione **Product Alternate ID**.  
  
## <a name="reporting-properties-for-columns"></a>Propriedades de relatório para colunas  
Há várias propriedades básicas de coluna e propriedades específicas de relatório nas colunas que você pode definir para melhorar a experiência de relatório do modelo. Por exemplo, pode não ser necessário que os usuários vejam todas as colunas em todas as tabelas. Assim como você ocultou as tabelas Product Category e Product Subcategory anteriormente, usando a propriedade Hidden de uma coluna, você pode ocultar colunas específicas de uma tabela que seriam mostradas. Outras propriedades, como Formato de Dados e Classificar por Coluna, também podem afetar o modo como os dados da coluna podem aparecer nos relatórios. Você definirá algumas dessas propriedades em colunas específicas agora. Outras colunas não exigem nenhuma ação e não são mostradas abaixo.  
  
Você somente definirá algumas propriedades de coluna diferentes aqui, mas há muitas outras. Para obter mais informações sobre propriedades de relatório de coluna, consulte [propriedades da coluna](../tabular-models/column-properties-ssas-tabular.md).  
  
#### <a name="to-set-properties-for-columns"></a>Para definir propriedades para colunas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
2.  Clique no **ID do cliente** coluna para exibir as propriedades de coluna na **propriedades** janela.  
  
3.  Na janela **Propriedades** , defina a propriedade **Hidden** como True. O **Customer ID** coluna, em seguida, torna-se acinzentada no designer de modelo.  
  
4.  Repita estas etapas, definindo a coluna e as propriedades de relatório a seguir para cada tabela especificada. Deixe todas as outras propriedades em suas configurações padrão.  
  
    Observação: Para todas as colunas de data, certifique-se **tipo de dados** é **data**.  
  
    **Cliente**  
  
    |coluna|Propriedade|Valor|  
    |----------|------------|---------|  
    |ID da geografia|Hidden|True|  
    |Birth Date|Formato de Dados|Data Abreviada|  
  
    **Data**  
  
    > [!NOTE]  
    > Porque a tabela Date foi selecionada como os modelos de tabela de datas usando a marca como configuração da tabela de data, na lição 7: Marcar como tabela de data e a coluna de data na tabela de data como a coluna a ser usado como o identificador exclusivo, a propriedade do identificador de linha para a coluna Date serão automaticamente definido como True e não podem ser alterado. Ao usar as funções de inteligência de tempo em fórmulas DAX, você deverá especificar uma tabela de data. Neste modelo, você criou várias medidas usando funções de inteligência de tempo para calcular dados de vendas para vários períodos como trimestres anterior e atual, e também para usar em KPIs. Para obter mais informações sobre como especificar uma tabela de datas, consulte [especificar marcar como tabela de data para uso com inteligência de tempo](../tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md).  
  
    |coluna|Propriedade|Valor|  
    |----------|------------|---------|  
    |data|Formato de Dados|Data Abreviada|  
    |Day Number of Week|Hidden|True|  
    |Day Name|Sort By Column|Day Number of Week|  
    |Day Of Week|Hidden|True|  
    |Day of Month|Hidden|True|  
    |Day of Year|Hidden|True|  
    |Month Name|Sort By Column|Month|  
    |Month|Hidden|True|  
    |Month Calendar|Hidden|True|  
    |Fiscal Quarter|Hidden|True|  
    |Fiscal Year|Hidden|True|  
    |Fiscal Semester|Hidden|True|  
  
    **Geography**  
  
    |coluna|Propriedade|Valor|  
    |----------|------------|---------|  
    |ID da geografia|Hidden|True|  
    |ID do território de vendas|Hidden|True|  
  
    **Product**  
  
    |coluna|Propriedade|Valor|  
    |----------|------------|---------|  
    |ID do produto|Hidden|True|  
    |Product Alternate ID|Rótulo Padrão|True|  
    |Identificação da subcategoria de produto|Hidden|True|  
    |Product Start Date|Formato de Dados|Data Abreviada|  
    |Product End Date|Formato de Dados|Data Abreviada|  
  
    **Internet Sales**  
  
    |coluna|Propriedade|Valor|  
    |----------|------------|---------|  
    |ID do produto|Hidden|True|  
    |ID do cliente|Hidden|True|  
    |ID de promoção|Hidden|True|  
    |ID de moeda|Hidden|True|  
    |ID do território de vendas|Hidden|True|  
    |Order Quantity|Tipo de Dados<br /><br />Formato de Dados<br /><br />Casas Decimais|Número Decimal<br /><br />Número Decimal<br /><br />0|  
    |Data do Pedido|Formato de Dados|Data Abreviada|  
    |Due Date|Formato de Dados|Data Abreviada|  
    |Ship Date|Formato de Dados|Data Abreviada|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Reimplantar o modelo de tabela de vendas pela Internet da Adventure Works  
Como você alterou o modelo, deverá reimplantá-lo.  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Para reimplantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
-   No SSDT, clique o **construir** menu e clique **implantar a modelo de vendas do Adventure Works Internet**.  
  
    A caixa de diálogo **Implantar** será exibida com o status de implantação dos metadados, bem como cada tabela incluída no modelo.  
  
## <a name="next-steps"></a>Próximas etapas  
Agora você pode usar o Excel para visualizar dados do modelo. Verifique se as contas do Analysis Services e do Reporting Services no site do SharePoint têm permissões de leitura para a instância do Analysis Services onde você implantou seu modelo.  
  
  
  
  
