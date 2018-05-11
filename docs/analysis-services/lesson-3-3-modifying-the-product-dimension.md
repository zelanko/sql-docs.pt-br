---
title: Modificando a dimensão de produto | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 333e1f8a56ee64389f5219dbc77fd08600cf3dcd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-3-3---modifying-the-product-dimension"></a>Lição 3-3-modificando a dimensão produto
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Nas tarefas deste tópico, você usará um cálculo nomeado para fornecer nomes mais descritivos às linhas de produto, definir uma hierarquia na dimensão Produto e especificar o nome do membro (Todos) para a hierarquia. Você também agrupará atributos nas pastas de exibição.  
  
## <a name="adding-a-named-calculation"></a>Adicionando um cálculo nomeado  
Você pode adicionar um cálculo nomeado a uma tabela em uma exibição de fonte de dados. Na tarefa a seguir, você criará um cálculo nomeado que exibirá o nome completo da linha de produto.  
  
#### <a name="to-add-a-named-calculation"></a>Para adicionar um cálculo nomeado  
  
1.  Para abrir a exibição da fonte de dados **Adventure Works DW 2012** , clique duas vezes em **Adventure Works DW 2012** na pasta **Exibições da Fonte de Dados** no Gerenciador de Soluções.  
  
2.  Na parte inferior do painel de diagrama, clique com o botão direito do mouse no cabeçalho da tabela **Product** e clique em **Novo Cálculo Nomeado**.  
  
3.  Na caixa de diálogo **Criar Cálculo Nomeado** , digite **ProductLineName** na caixa **Nome da coluna** .  
  
4.  Na caixa **Expressão** , digite ou copie e cole a seguinte instrução **CASE** :  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
    Essa instrução **CASE** cria nomes amigáveis para cada linha de produto no cubo.  
  
5.  Clique em **OK** para criar o cálculo nomeado **ProductLineName** . Talvez você precise esperar um pouco.  
  
6.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>Modificando a propriedade NameColumn de um atributo  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>Para modificar a propriedade NameColumn de um atributo  
  
1.  Alterne para o Designer de Dimensão da dimensão Produto. Para fazer isso, clique duas vezes na dimensão **Produto** no nó **Dimensões** do Gerenciador de Soluções.  
  
2.  No painel **Atributos** da guia **Estrutura da Dimensão** , selecione **Linha de Produto**.  
  
3.  Na janela Propriedades no lado direito da tela, clique no campo de propriedade **NameColumn** na parte inferior da janela e clique no botão Procurar (**…**) para abrir a caixa de diálogo **Coluna de Nome** . (Talvez seja necessário clicar na guia **Propriedades** à direita da tela para abrir a janela Propriedades.)  
  
4.  Selecione **ProductLineName** na parte inferior da lista **Coluna de origem** e clique em **OK**.  
  
    O campo NameColumn agora contém o texto **Product.ProductLineName (WChar)**. Os membros da hierarquia do atributo **Product Line** agora exibirão o nome completo da linha de produto, em vez do nome abreviado.  
  
5.  No painel **Atributos** da guia **Estrutura da Dimensão** , selecione **Chave do Produto (Product Key)**.  
  
6.  Na janela Propriedades, clique no campo de propriedade **NameColumn** e clique no botão Procurar (**…**) para abrir a caixa de diálogo **Coluna de Nome** .  
  
7.  Selecione **EnglishProductName** na lista **Coluna de origem** e clique em **OK**.  
  
    O campo NameColumn agora contém o texto **Product.EnglishProductName (WChar)**.  
  
8.  Na janela Propriedades, role a tela para cima, clique no campo de propriedade **Name** e digite **Product Name**.  
  
## <a name="creating-a-hierarchy"></a>Criando uma hierarquia  
  
#### <a name="to-create-a-hierarchy"></a>Para criar uma hierarquia  
  
1.  Arraste o atributo **Product Line** do painel **Atributos** até o painel **Hierarquias** .  
  
2.  Arraste o atributo **Model Name** do painel **Atributos** até a célula **<new level>** do painel **Hierarquias** , sob o nível **Linha de Produto** .  
  
3.  Arraste o atributo **Product Name** do painel **Atributos** até a célula **<new level>** do painel **Hierarquias** , sob o nível **Nome do Modelo** . (Você renomeou Product Key para Product Name na seção anterior.)  
  
4.  No painel **Hierarquias** da guia **Estrutura da Dimensão** , clique com o botão direito do mouse na barra de título da hierarquia **Hierarquia** , clique em **Renomear**e digite **Linhas de Modelo do Produto**.  
  
    Agora, o nome da hierarquia é **Linhas de Modelo do Produto**.  
  
5.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="specifying-folder-names-and-all-member-names"></a>Especificando nomes de pastas e de todos os membros  
  
#### <a name="to-specify-the-folder-and-member-names"></a>Para especificar os nomes de pasta e membro  
  
1.  No painel **Atributos** , selecione os seguintes atributos pressionando e mantendo a tecla CTRL pressionada enquanto clica em cada um deles:  
  
    -   **Classe**  
  
    -   **Color**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **Tamanho**  
  
    -   **Size Range**  
  
    -   **Estilo**  
  
    -   **Weight**  
  
2.  No campo de propriedade **AttributeHierarchyDisplayFolder** da janela Propriedades, digite **Estoque**.  
  
    Você acaba de agrupar esses atributos em uma única pasta de exibição.  
  
3.  No painel **Atributos** , selecione os seguintes atributos:  
  
    -   **Preço do Revendedor**  
  
    -   **Preço da Lista**  
  
    -   **Custo Padrão**  
  
4.  Na célula da propriedade **AttributeHierarchyDisplayFolder** da janela Propriedades, digite **Financeiro**.  
  
    Você acaba de agrupar esses atributos em uma segunda pasta de exibição.  
  
5.  No painel **Atributos** , selecione os seguintes atributos:  
  
    -   **Data de Término**  
  
    -   **Data de Início**  
  
    -   **Status**  
  
6.  Na célula da propriedade **AttributeHierarchyDisplayFolder** da janela Propriedades, digite **Histórico**.  
  
    Você acaba de agrupar esses atributos em uma terceira pasta de exibição.  
  
7.  Selecione a hierarquia **Linhas de Modelo do Produto** no painel **Hierarquias** . Depois, altere a propriedade **AllMemberName** na janela Propriedades para **Todos os Produtos**.  
  
8.  Clique em uma área aberta do painel **Hierarquias** e altere a propriedade **AttributeAllMemberName** na parte superior da janela Propriedades para **Todos os Produtos**.  
  
    Clicar em uma área aberta permite que você modifique propriedades da própria dimensão Produto. Você também pode clicar em **Produto** na parte superior da lista de atributos no painel **Atributos** .  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-attribute-relationships"></a>Definindo relações de atributo  
Se os dados subjacentes permitirem, você também deve definir relações de atributo entre atributos. Definir relações de atributo acelera o processamento de dimensões, partições e consultas. Para obter mais informações, consulte [Definir relações de atributo](../analysis-services/multidimensional-models/attribute-relationships-define.md) e [Relações de atributo](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relações de atributo  
  
1.  No **Designer de Dimensão** da dimensão Produto, clique na guia **Relações de Atributo** .  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Nome do Modelo** e clique em **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo**, o **Atributo de Origem** é **Model Name**. Defina o **Atributo Relacionado** como **Linha de Produto**.  
  
    Na lista **Tipo de relação** , deixe o tipo de relação definido como **Flexível** porque as relações entre os membros podem mudar com o passar do tempo. Por exemplo, um modelo de produto pode ser movido para uma linha de produto diferente.  
  
4.  Clique em **OK**.  
  
5.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="reviewing-product-dimension-changes"></a>Revisando as alterações na dimensão Produto  
  
#### <a name="to-review-the-product-dimension-changes"></a>Para revisar as alterações na dimensão Produto  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Depois de receber a mensagem **Implantação Concluída com Êxito** , clique na guia **Navegador** do **Designer de Dimensão** da dimensão **Produto** e clique no botão Reconectar na barra de ferramentas do designer.  
  
3.  Verifique se a opção **Linhas de Modelo do Produto** está selecionada na lista **Hierarquia** e expanda **Todos os Produtos**.  
  
    Observe que o nome do membro **Todos** é exibido como **Todos os Produtos**. Isso acontece porque você alterou a propriedade **AllMemberName** da hierarquia para **Todos os Produtos** anteriormente nesta lição. Além disso, os membros do nível **Linha de Produto** agora têm nomes amigáveis, em vez de abreviações de apenas uma letra.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Modificando a dimensão de data](../analysis-services/lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>Consulte também  
[Definir cálculos nomeados em uma exibição da fonte de dados & #40; Analysis Services & #41;](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
[Criar hierarquias definidas pelo usuário](../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
[Configurar o nível &#40;All&#41; para hierarquias de atributo](../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
