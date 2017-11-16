---
title: "4-6-especificando relações de atributo na hierarquia definida pelo usuário | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d68e4caadf4e19582fb5ccd767535baee1001762
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="4-6-specifying-attribute-relationships-in-user-defined-hierarchy"></a>4-6-especificando relações de atributo na hierarquia definida pelo usuário
Como você já aprendeu neste tutorial, é possível organizar as hierarquias de atributo em níveis dentro das hierarquias de usuário para fornecer caminhos de navegação aos usuários em um cubo. Uma hierarquia de usuário pode representar uma hierarquia natural, como cidade, estado e país, ou um caminho de navegação, como nome do funcionário, cargo e nome do departamento. Para o usuário que navega pela hierarquia, esses dois tipos de hierarquias de usuário são os mesmos.  
  
Em uma hierarquia natural, ao definir relações de atributo entre os atributos que criam os níveis, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode usar a agregação de um atributo para obter resultados a partir de um atributo relacionado. Se não houver nenhuma relação definida entre atributos, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] agregará todos os atributos que não forem atributos de chave do atributo de chave. Portanto, se os dados subjacentes permitirem, você também poderá definir relações de atributo entre atributos. Definir as relações de atributo melhora a dimensão, a partição e o desempenho do processamento de consulta. Para obter mais informações, consulte [Definir relações de atributo](../analysis-services/multidimensional-models/attribute-relationships-define.md) e [Relações de atributo](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
Quando você definir relações de atributo, poderá especificar se a relação é flexível ou rígida. Se defini-la como rígida, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] reterá as agregações quando a dimensão for atualizada. Se uma relação definida como rígida for realmente alterada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] irá gerar um erro durante o processamento, a menos que a dimensão esteja totalmente processada. Ao especificar as relações apropriadas e as propriedades da relação, são produzidos aumento de consulta e desempenho de processamento. Para obter mais informações, consulte [Definir relações de atributo](../analysis-services/multidimensional-models/attribute-relationships-define.md)e [Propriedades da hierarquia de usuário](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md).  
  
Nas tarefas deste tópico, você definirá relações de atributo para os atributos nas hierarquias de usuários naturais no projeto Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Isso inclui a hierarquia **Geografia do Cliente** na dimensão **Cliente**, a hierarquia **Região de Vendas** na dimensão **Região de Vendas** , a hierarquia **Linhas de Modelo do Produto** na dimensão **Produto** e as hierarquias **Data Fiscal** e **Data do Calendário** na dimensão **Data** . Todas essas hierarquias de usuário são hierarquias naturais.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Definindo relações de atributo para atributos na hierarquia Geografia do Cliente  
  
1.  Mude para o Designer de Dimensão da dimensão Customer e clique na guia **Estrutura da Dimensão** .  
  
    No painel **Hierarquias** , observe os níveis na hierarquia definida pelo usuário **Geografia do Cliente** . Essa hierarquia é apenas um caminho que permite aos usuários realizarem uma busca detalhada, pois não há relação definida entre níveis ou atributos.  
  
2.  Clique na guia **Relações de Atributo** .  
  
    Observe as quatro relações que vinculam os atributos que não são de chave da tabela **Geography** ao atributo de chave da tabela **Geography** . O atributo **Geography** está relacionado ao atributo **Full Name** . O atributo **CEP** está indiretamente vinculado ao atributo **Nome Completo** por meio do atributo **Geografia** , pois o **CEP** está vinculado ao atributo **Geografia** e o atributo **Geografia** está vinculado ao atributo **Nome Completo** . Em seguida, vamos alterar as relações de atributo para que elas não usem o atributo **Geography** .  
  
3.  No diagrama, clique com o botão direito do mouse no atributo **Full Name** e selecione **Nova Relação de Atributo**.  
  
4.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Full Name**. Defina o **Atributo Relacionado** como **CEP**. Na lista **Tipo de relação** , deixe o tipo de relação definido como **Flexível** porque as relações entre os membros podem mudar com o passar do tempo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Um ícone de advertência aparece no diagrama porque a relação é redundante. A relação **Nome Completo** -> **Geografia**-> **CEP** já existia, e você acabou de criar a relação **Nome Completo** -> **CEP**. A relação **Geografia**-> **CEP** agora é redundante e, portanto, vamos removê-la.  
  
6.  No painel **Relações de Atributo** , clique com o botão direito do mouse em **Geografia**-> **CEP** e clique em **Excluir**.  
  
7.  Quando a caixa de diálogo **Excluir Objetos** for exibida, clique em **OK**.  
  
8.  No diagrama, clique com o botão direito do mouse no atributo **CEP** e selecione **Nova Relação de Atributo**.  
  
9. Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **CEP**. Defina o **Atributo Relacionado** como **Cidade**. Na lista **Tipo de relação** , deixe o tipo de relação definido como **Flexível**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Agora, a relação **Geografia**-> **Cidade** é redundante e, portanto, vamos excluí-la.  
  
11. No painel Relações de Atributo, clique com o botão direito do mouse em **Geografia**-> **Cidade** e clique em **Excluir**.  
  
12. Quando a caixa de diálogo **Excluir Objetos** for exibida, clique em **OK**.  
  
13. No diagrama, clique com o botão direito do mouse no atributo **Cidade** e selecione **Nova Relação de Atributo**.  
  
14. Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Cidade**. Defina o **Atributo Relacionado** como **Estado/Província**. Na lista **Tipo de relação** , deixe o tipo de relação definido como **Rígido** porque as relações entre cidade e estado não mudam com o passar do tempo.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Clique com o botão direito do mouse na seta entre **Geografia** e **Estado/Província** e clique em **Excluir**.  
  
17. Quando a caixa de diálogo **Excluir Objetos** for exibida, clique em **OK**.  
  
18. No diagrama, clique com o botão direito do mouse no atributo **Estado/Província** e selecione **Nova Relação de Atributo**.  
  
19. Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Estado/Província**. Defina o **Atributo Relacionado** como **País/Região**. Na lista **Tipo de relação** , defina o tipo de relação definido como **Rígido** porque as relações entre estado-província e País/Região não mudam com o passar do tempo.  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. No painel Relações de Atributo, clique com o botão direito do mouse em **Geografia**-> **País/Região** e clique em **Excluir**.  
  
22. Quando a caixa de diálogo **Excluir Objetos** for exibida, clique em **OK**.  
  
23. Clique na guia **Estrutura da Dimensão** .  
  
    Observe que, quando a última relação de atributo entre **Geography** e outros atributos é excluída, a própria **Geography** é excluída. Isso ocorre porque o atributo não é mais usado.  
  
24. No menu Arquivo, clique em **Salvar Tudo**.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Definindo relações de atributo para atributos na hierarquia Região de Vendas  
  
1.  Abra o Designer de Dimensão na dimensão **Região de Vendas** e clique na guia **Relações de Atributo** .  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Sales Territory Country** e selecione **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **País da Região de Vendas**. Defina o **Atributo Relacionado** como **Grupo de Região de Vendas**. Na lista **Tipo de relação** , deixe o tipo de relação definido como **Flexível**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    **Grupo de Região de Vendas** agora está vinculado a **País da Região de Vendas**e **País da Região de Vendas** agora está vinculado a **Região de Vendas**. A propriedade **RelationshipType** de cada uma dessas relações é definida como **Flexível** , pois, com o passar do tempo, tanto os agrupamentos de regiões dentro de um país quanto os agrupamentos de países dentro dos grupos podem mudar.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Definindo relações de atributo para atributos na hierarquia Linhas de Modelo do Produto  
  
1.  Abra o Designer de Dimensão na dimensão **Produto** e clique na guia **Relações de Atributo** .  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Model Name** e selecione **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Model Name**. Defina o **Atributo Relacionado** como **Linha de Produto**. Na lista **Tipo de relação** , deixe o tipo de relação definido como **Flexível**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Definindo relações de atributo para atributos na hierarquia Data Fiscal  
  
1.  Mude para o Designer de Dimensão da dimensão **Data** e clique na guia **Relações de Atributo** .  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Nome do Mês** e selecione **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Nome do Mês**. Defina o **Atributo Relacionado** como **Trimestre Fiscal**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  No diagrama, clique com o botão direito do mouse no atributo **Fiscal Quarter** e selecione **Nova Relação de Atributo**.  
  
6.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Fiscal Quarter**. Defina o **Atributo Relacionado** como **Fiscal Semester**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  No diagrama, clique com o botão direito do mouse no atributo **Fiscal Semester** e selecione **Nova Relação de Atributo**.  
  
9. Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Fiscal Semester**. Defina o **Atributo Relacionado** como **Fiscal Year**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Definindo relações de atributo para atributos na hierarquia Data do Calendário  
  
1.  No diagrama, clique com o botão direito do mouse no atributo **Nome do Mês** e selecione **Nova Relação de Atributo**.  
  
2.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Nome do Mês**. Defina o **Atributo Relacionado** como **Trimestre do Calendário**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  No diagrama, clique com o botão direito do mouse no atributo **Trimestre Calendário** e selecione **Nova Relação de Atributo**.  
  
5.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Trimestre Calendário**. Defina o **Atributo Relacionado** como **Semestre do Calendário**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  No diagrama, clique com o botão direito do mouse no atributo **Calendar Semester** e selecione **Nova Relação de Atributo**.  
  
8.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Semestre do Calendário**. Defina o **Atributo Relacionado** como **Ano Civil**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Definindo relações de atributo para atributos na hierarquia Geografia  
  
1.  Abra o Designer de Dimensão na dimensão Geografia e clique na guia **Relações de Atributo** .  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **CEP** e selecione **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **CEP**. Defina o **Atributo Relacionado** como **Cidade**. Na lista **Tipo de relação** , defina o tipo de relação como **Flexível**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  No diagrama, clique com o botão direito do mouse no atributo **Cidade** e selecione **Nova Relação de Atributo**.  
  
6.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Cidade**. Defina o **Atributo Relacionado** como **Estado/Província**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  No diagrama, clique com o botão direito do mouse no atributo **Estado/Província** e selecione **Nova Relação de Atributo**.  
  
9. Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Estado/Província**. Defina o **Atributo Relacionado** como **País/Região**. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. No diagrama, clique com o botão direito do mouse no atributo **Geography Key** e selecione **Propriedades**.  
  
12. Defina a propriedade **AttributeHierarchyOptimizedState** como **NotOptimized**, a propriedade **AttributeHierarchyOrdered** como **False**e a propriedade **AttributeHierarchyVisible** como **False**.  
  
13. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
14. No menu **Compilar** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique em **Implantar Tutorial do Analysis Services**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Definindo o membro desconhecido e as propriedades de processamento nulo](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>Consulte também  
[Definir relações de atributo](../analysis-services/multidimensional-models/attribute-relationships-define.md)  
[Propriedades da hierarquia de usuário](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
  

