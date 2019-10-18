---
title: Definindo o membro desconhecido e as propriedades de processamento nulo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d9abb09c-9bfa-4e32-b530-8590e4383566
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d0d97b7fea9557e1ce462fcc540e51a1ee4b0228
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493926"
---
# <a name="defining-the-unknown-member-and-null-processing-properties"></a>Definindo o membro desconhecido e as propriedades de processamento nulo
  Quando o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] processa uma dimensão, todos os valores distintos das colunas subjacentes nas tabelas, ou nas exibições da fonte de dados, populam os atributos na dimensão. Se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encontrar um valor nulo durante o processamento, por padrão, ele converterá NULL em zero em colunas numéricas ou em uma cadeia de caracteres vazia para colunas de cadeia de caracteres. Você pode modificar as configurações padrão ou converter valores nulos em seu processo de extração, transformação e carregamento (se houver) do data warehouse relacional subjacente. Além disso, você pode fazer [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] converter o valor nulo em um valor designado Configurando três propriedades: as propriedades **UnknownMember** e **UnknownMemberName** para a dimensão e a propriedade **NullProcessing** para o atributo de chave da dimensão.  
  
 O assistente para dimensões e o assistente para Cubos habilitarão essas propriedades para você com base em se o atributo de chave de uma dimensão é anulável ou o atributo raiz de uma dimensão floco de neve é baseado em uma coluna anulável. Nesses casos, a propriedade **NullProcessing** do atributo de chave será definida como **UnknownMember** e a propriedade **UnknownMember** será definida como **Visible**.  
  
 No entanto, quando você cria dimensões floco de neve de forma incremental, como estamos fazendo com a dimensão produto neste tutorial, ou quando você define as dimensões usando o designer de dimensão e, em seguida, incorpora essas dimensões existentes em um cubo, o **UnknownMember** e as propriedades **NullProcessing** podem precisar ser definidas manualmente.  
  
 Nas tarefas deste tópico, você adicionará os atributos categoria de produto e subcategoria de produto à dimensão produto das tabelas de floco de neve que serão adicionadas à exibição da fonte de dados [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW. Em seguida, você habilitará a propriedade **UnknownMember** para a dimensão produto, especificará `Assembly Components` como o valor para a propriedade **UnknownMemberName** , relacionará os atributos `Subcategory` e `Category` ao atributo nome do produto e, em seguida, definirá personalizado tratamento de erro para o atributo de chave de membro que vincula as tabelas floco de neve.  
  
> [!NOTE]  
>  Se você tiver adicionado os atributos subcategoria e categoria quando definiu originalmente o cubo de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial usando o assistente para cubos, essas etapas teriam sido executadas automaticamente.  
  
## <a name="reviewing-error-handling-and-unknown-member-properties-in-the-product-dimension"></a>Examinando o tratamento de erros e propriedades de membros desconhecidos na dimensão Produto  
  
1.  Alterne para o designer de dimensão da dimensão **produto** , clique na guia **estrutura da dimensão** e selecione **produto** no painel **atributos** .  
  
     Isso permite que você exiba e modifique as propriedades da própria dimensão.  
  
2.  Na janela Propriedades, examine as propriedades **UnknownMember** e **UnknownMemberName** .  
  
     Observe que a propriedade **UnknownMember** não está habilitada, pois seu valor está definido como **None** , em vez de **Visible** ou **Hidden**, e que nenhum nome é especificado para a propriedade **UnknownMemberName** .  
  
3.  Na janela Propriedades, selecione **(personalizado)** na célula da propriedade **ErrorConfiguration** e expanda a coleção de propriedades **ErrorConfiguration** .  
  
     Definir a propriedade **ErrorConfiguration** como **(personalizado)** permite que você exiba as definições de configuração de erro padrão – ela não altera as configurações.  
  
4.  Examine as propriedades de configuração de erro de chave nula e chave, mas não faça nenhuma alteração.  
  
     Observe que, por padrão, quando chaves nulas são convertidas para o membro desconhecido e o erro de processamento associado a essa conversão é ignorado.  
  
     A imagem a seguir mostra as configurações de propriedade para a coleção de propriedades **ErrorConfiguration** .  
  
     ![Coleção de propriedades ErrorConfiguration](../../2014/tutorials/media/l4-productdimensionerrorconfig-1.gif "Coleção de propriedades ErrorConfiguration")  
  
5.  Clique na guia **navegador** , verifique se **linhas de modelo de produto** está selecionada na lista **hierarquia** e, em seguida, expanda `All Products`.  
  
     Observe os cinco membros do nível de linha de produto.  
  
6.  Expanda **componentes**e, em seguida, expanda o membro sem rótulo do nível de **nome do modelo** .  
  
     Esse nível contém os componentes do assembly que são usados ao criar outros componentes, começando com o produto de **corrida ajustável** , conforme mostrado na imagem a seguir.  
  
     ![Componentes de assembly usados para criar outros componentes](../../2014/tutorials/media/l4-productdimensionerrorconfig-2.gif "Componentes de assembly usados para criar outros componentes")  
  
## <a name="defining-attributes-from-snowflaked-tables-and-a-product-category-user-defined-hierarchy"></a>Definindo atributos de tabelas flocos de neve e uma hierarquia definida pelo usuário da categoria de produto  
  
1.  Abra o designer de exibição da fonte de dados para a exibição da fonte de dados [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW, selecione **vendas do revendedor** no painel **organizador de diagramas** e clique em **Adicionar/remover objetos** no menu **exibição da fonte de dados** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     A caixa de diálogo **Adicionar/remover tabelas** é aberta.  
  
2.  Na lista **objetos incluídos** , selecione **DimProduct (dbo)** e, em seguida, clique em **adicionar tabelas relacionadas**.  
  
     Ambos os **DimProductSubcategory (dbo)** e **FactProductInventory (dbo)** são adicionados. Remova **FactProductInventory (dbo)** para que apenas a tabela **DimProductSubcategory (dbo)** seja adicionada à lista de **objetos incluídos** .  
  
3.  Com a tabela **DimProductSubcategory (dbo)** selecionada por padrão como a tabela adicionada mais recentemente, clique em **adicionar tabelas relacionadas** novamente.  
  
     A tabela **DimProductCategory (dbo)** é adicionada à lista de **objetos incluídos** .  
  
4.  Clique em **OK**.  
  
5.  No menu **Formatar** da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aponte para **layout automático**e clique em **diagrama**.  
  
     Observe que as tabelas **DimProductSubcategory (dbo)** e **DimProductCategory (dbo)** estão vinculadas umas às outras e também à tabela **ResellerSales** por meio da tabela **Product** .  
  
6.  Alterne para o designer de dimensão da dimensão **produto** e clique na guia **estrutura da dimensão** .  
  
7.  Clique com o botão direito do mouse em qualquer lugar no painel **exibição da fonte de dados** e clique em **Mostrar todas as tabelas**.  
  
8.  No painel **exibição da fonte de dados** , localize a tabela **DimProductCategory** , clique com o botão direito do mouse em **ProductCategoryKey** nessa tabela e clique em **novo atributo da coluna**.  
  
9. No painel **atributos** , altere o nome desse novo atributo para `Category`.  
  
10. No janela Propriedades, clique no campo de propriedade **NameColumn** e, em seguida, clique no botão procurar ( **...** ) para abrir a caixa de diálogo **coluna de nome** .  
  
11. Selecione **EnglishProductCategoryName** na lista **coluna de origem** e clique em **OK**.  
  
12. No painel **exibição da fonte de dados** , localize a tabela **DimProductSubcategory** , clique com o botão direito do mouse em **ProductSubcategoryKey** nessa tabela e clique em **novo atributo da coluna**.  
  
13. No painel **atributos** , altere o nome desse novo atributo para `Subcategory`.  
  
14. No janela Propriedades, clique no campo de propriedade **NameColumn** e, em seguida, clique no botão procurar **(...)** para abrir a caixa de diálogo **coluna de nome** .  
  
15. Selecione **EnglishProductSubcategoryName** na lista **coluna de origem** e clique em **OK**.  
  
16. Crie uma nova hierarquia definida pelo usuário chamada **categorias de produto** com os seguintes níveis, em ordem de cima para baixo: `Category`, `Subcategory` e **nome do produto**.  
  
17. Especifique `All Products` **como o valor para a propriedade** itempropertyname da hierarquia definida pelo usuário categorias de produto.  
  
## <a name="browsing-the-user-defined-hierarchies-in-the-product-dimension"></a>Navegando pelas hierarquias definidas pelo usuário na dimensão Produto  
  
1.  Na barra de ferramentas da guia **estrutura da dimensão** do designer de **dimensão** da dimensão **produto** , clique em **processar**.  
  
2.  Clique em **Sim** para criar e implantar o projeto e, em seguida, clique em **executar** para processar a dimensão **produto** .  
  
3.  Quando o processamento tiver sido bem-sucedido, expanda **processar dimensão ' produto ' concluído com êxito** na caixa de diálogo **progresso do processo** , expanda **processar atributo de dimensão ' nome do produto ' concluído**e, em seguida, expanda **consultas SQL 1** .  
  
4.  Clique na consulta Selecionar DISTINCT e, em seguida, clique em **Exibir detalhes**.  
  
     Observe que uma cláusula WHERE foi adicionada à cláusula SELECT DISTINCT que remove os produtos que não têm valor na coluna ProductSubcategoryKey, conforme mostrado na imagem a seguir.  
  
     ![Selecione a cláusula DISTINCT mostrando a cláusula WHERE](../../2014/tutorials/media/l4-productnametraceline-1.gif "Selecione a cláusula DISTINCT mostrando a cláusula WHERE")  
  
5.  Clique em **fechar** três vezes para fechar todas as caixas de diálogo de processamento.  
  
6.  Clique na guia **navegador** do designer de dimensão da dimensão **produto** e, em seguida, clique em **reconectar**.  
  
7.  Verifique se **as linhas de modelo do produto** aparecem na lista **hierarquia** , expanda `All Products` e, em seguida, expanda **componentes**.  
  
8.  Selecione **categorias de produtos** na lista **hierarquia** , expanda `All Products` e, em seguida, expanda **componentes**.  
  
     Observe que nenhum dos componentes do assembly aparece.  
  
 Para modificar o comportamento mencionado na tarefa anterior, você habilitará a propriedade **UnknownMember** da dimensão Products, definirá um valor para a propriedade **UnknownMemberName** , definirá a propriedade **NullProcessing** para o `Subcategory` eAtributos de nome de modelo para **UnknownMember**, defina o atributo `Category` como um atributo relacionado do atributo `Subcategory` e, em seguida, defina o atributo de **linha de produto** como um atributo relacionado do atributo de **nome de modelo** . Essas etapas farão com que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use o valor de nome de membro desconhecido para cada produto que não tenha um valor para a coluna **SubcategoryKey** , como você verá na tarefa a seguir.  
  
## <a name="enabling-the-unknown-member-defining-attribute-relationships-and-specifying-custom-processing-properties-for-nulls"></a>Habilitando o membro desconhecido, definindo relações de atributo e especificando propriedades de processamento personalizadas para NULLs  
  
1.  Clique na guia **estrutura da dimensão** no designer de dimensão da dimensão **produto** e selecione **produto** no painel **atributos** .  
  
2.  Na janela **Propriedades** , altere a propriedade **UnknownMember** para **visível**e, em seguida, altere o valor da propriedade **UnknownMemberName** para `Assembly Components`.  
  
     Alterar a propriedade **UnknownMember** para **Visible** ou **Hidden** habilita a propriedade **UnknownMember** para a dimensão.  
  
3.  Clique na guia **relações de atributo** .  
  
4.  No diagrama, clique com o botão direito do mouse no atributo `Subcategory` e selecione **nova relação de atributo**.  
  
5.  Na caixa de diálogo **criar relação de atributo** , o **atributo de origem** é `Subcategory`. Defina o **atributo relacionado** como `Category`. Deixe o tipo de relação definido como **flexível**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  No painel **atributos** , selecione **subcategoria.**  
  
8.  No janela Propriedades, expanda a propriedade **KeyColumns** e expanda a propriedade **DimProductSubcategory. ProductSubcategoryKey (Integer)** .  
  
9. Altere a propriedade **NullProcessing** para **UnknownMember**.  
  
10. No painel **atributos** , selecione **nome do modelo**.  
  
11. No janela Propriedades, expanda a propriedade **KeyColumns** e expanda a propriedade **Product. ModelName (WCHAR)** .  
  
12. Altere a propriedade **NullProcessing** para **UnknownMember**.  
  
     Devido a essas alterações, quando [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encontra um valor nulo para o atributo `Subcategory` ou o atributo de **nome de modelo** durante o processamento, o valor de membro desconhecido será substituído como o valor de chave e as hierarquias definidas pelo usuário serão construídas devidamente.  
  
## <a name="browsing-the-product-dimension-again"></a>Pesquisando a dimensão Produto novamente  
  
1.  No menu **Compilar** , clique em **implantar Analysis Services tutorial**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **navegador** do designer de dimensão da dimensão **produto** e, em seguida, clique em **reconectar**.  
  
3.  Verifique se **categorias de produto** está selecionada na lista **hierarquia** e, em seguida, expanda `All Products`.  
  
     Observe que os componentes do assembly aparecem como um novo membro do nível de categoria.  
  
4.  Expanda o membro `Assembly Components` do nível de `Category` e, em seguida, expanda o membro `Assembly Components` do nível de `Subcategory`.  
  
     Observe que todos os componentes do assembly agora aparecem no nível do **nome do produto** , conforme mostrado na imagem a seguir.  
  
     ![Nível de nome do produto mostrando componentes de assembly](../../2014/tutorials/media/l4-assemblycomponents-1.gif "Nível de nome do produto mostrando componentes de assembly")  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 5: Definindo relações entre dimensões e grupos de medidas](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)  
  
  
