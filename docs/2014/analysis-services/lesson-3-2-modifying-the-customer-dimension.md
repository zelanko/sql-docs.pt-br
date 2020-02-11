---
title: Modificando a dimensão do cliente | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2530d42c70b506fe927d35fd4e6f862e22e1ea1a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078924"
---
# <a name="modifying-the-customer-dimension"></a>Modificando a dimensão Cliente
  Há várias formas de aumentar a facilidade de uso e melhorar a funcionalidade das dimensões em um cubo. Nas tarefas deste tópico, você modificará a dimensão Customer.  
  
## <a name="renaming-attributes"></a>Renomeando atributos  
 Você pode alterar nomes de atributo na guia **Estrutura da Dimensão** do Designer de Dimensão.  
  
#### <a name="to-rename-an-attribute"></a>Para renomear um atributo  
  
1.  Mude para o **Designer de Dimensão** da dimensão Cliente no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para fazer isso, clique duas vezes na dimensão **Cliente** no nó **Dimensões** do Gerenciador de Soluções.  
  
2.  No painel **Atributos** , clique com o botão direito do mouse em **Nome do País/Região em Inglês**e clique em **Renomear**. Altere o nome do atributo para `Country-Region`.  
  
3.  Altere os nomes dos seguintes atributos da mesma maneira:  
  
    -   Atributo de **educação em inglês** – alterar para`Education`  
  
    -   Atributo de **ocupação em inglês** – alterar para`Occupation`  
  
    -   Atributo de **nome da província do estado** – alterar para`State-Province`  
  
4.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="creating-a-hierarchy"></a>Criando uma hierarquia  
 Você pode criar uma nova hierarquia arrastando um atributo do painel **Atributos** até o painel **Hierarquias** .  
  
#### <a name="to-create-a-hierarchy"></a>Para criar uma hierarquia  
  
1.  Arraste o `Country-Region` atributo do painel **atributos** até o painel **hierarquias** .  
  
2.  Arraste o `State-Province` atributo do painel **atributos** para o ** \<novo nível>** célula no painel **hierarquias** , sob o `Country-Region` nível.  
  
3.  Arraste o atributo **cidade** do painel **atributos** para o ** \<novo nível>** célula no painel **hierarquias** , sob o `State-Province` nível.  
  
4.  No painel **hierarquias** da guia **estrutura da dimensão** , clique com o botão direito do mouse na barra de título da hierarquia **hierarquia** , selecione **renomear**e digite `Customer Geography`.  
  
     O nome da hierarquia agora `Customer Geography`é.  
  
5.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="adding-a-named-calculation"></a>Adicionando um cálculo nomeado  
 É possível adicionar um cálculo nomeado, que é uma expressão SQL representada como uma coluna calculada, a uma tabela em uma exibição da fonte de dados. A expressão se parece e se comporta como uma coluna na tabela. Cálculos nomeados permitem que você estenda o esquema relacional de tabelas existentes em uma exibição da fonte de dados sem modificar a tabela na fonte de dados subjacente. Para obter mais informações, consulte [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>Para adicionar um cálculo nomeado  
  
1.  Abra a exibição da fonte de dados do ** [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** clicando duas vezes nela na pasta **exibições da fonte de dados** em Gerenciador de soluções.  
  
2.  No painel **Tabelas** à esquerda, clique com o botão direito do mouse em **Cliente**e clique em **Novo Cálculo Nomeado**.  
  
3.  Na caixa de diálogo **criar cálculo nomeado** , digite `FullName` a caixa **nome da coluna** e digite ou copie e cole a seguinte `CASE` instrução na caixa **expressão** :  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
     A `CASE` instrução concatena as colunas **FirstName**, **MiddleName**e **LastName** em uma única coluna que será usada na dimensão Customer como o nome exibido para o atributo **Customer** .  
  
4.  Clique em **OK**e expanda **Cliente** no painel **Tabelas** .  
  
     O `FullName` cálculo nomeado aparece na lista de colunas na tabela Customer, com um ícone que indica que se trata de um cálculo nomeado.  
  
5.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
6.  No painel **Tabelas** , clique com o botão direito do mouse em **Cliente**e selecione **Explorar Dados**.  
  
7.  Examine a última coluna na exibição **Explorar Tabela Cliente** .  
  
     Observe que a `FullName` coluna aparece na exibição da fonte de dados, concatenando corretamente os dados de várias colunas da fonte de dados subjacente e sem modificar a fonte de dados original.  
  
8.  Feche a guia **Explorar Tabela Cliente** .  
  
## <a name="using-the-named-calculation-for-member-names"></a>Usando o cálculo nomeado para nomes de membros  
 Depois de criar um cálculo nomeado na exibição da fonte de dados, você pode usá-lo como propriedade para um atributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Para usar o cálculo nomeado para nomes de membros  
  
1.  Alterne para o Designer de Dimensão da dimensão Cliente.  
  
2.  No painel **Atributos** da guia **Estrutura da Dimensão** , clique no atributo **Chave de Cliente** .  
  
3.  Abra a janela Propriedades e clique no botão **Ocultar Automaticamente** na barra de título de forma que ela permaneça aberta.  
  
4.  No campo propriedade de **nome** , digite `Full Name`.  
  
5.  Clique no campo de propriedade **NameColumn** na parte inferior e, em seguida, clique no botão procurar (**...**) para abrir a caixa de diálogo **coluna de nome** .  
  
6.  Selecione `FullName` na parte inferior da lista **coluna de origem** e clique em **OK**.  
  
7.  Na guia estrutura de dimensões, arraste o `Full Name` atributo do painel **atributos** para o ** \<novo nível>** célula no painel **hierarquias** , sob o nível **cidade** .  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-display-folders"></a>Definindo pastas de exibição  
 Você pode usar pastas de exibição para agrupar hierarquias de usuário e atributo em estruturas de pastas, a fim de aumentar a facilidade de uso.  
  
#### <a name="to-define-display-folders"></a>Para definir pastas de exibição  
  
1.  Abra a guia **Estrutura da Dimensão** da dimensão Cliente.  
  
2.  No painel **Atributos** , selecione os seguintes atributos pressionando e mantendo a tecla CTRL pressionada enquanto clica em cada um deles:  
  
    -   **City**  
  
    -   `Country-Region`  
  
    -   **CEP**  
  
    -   `State-Province`  
  
3.  No janela Propriedades, clique no campo de propriedade **AttributeHierarchyDisplayFolder** na parte superior (talvez seja necessário apontar para ele para ver o nome completo) e, em seguida, `Location`digite.  
  
4.  No painel **hierarquias** , clique `Customer Geography`em e, na janela Propriedades à direita, selecione `Location` como o valor da propriedade **DisplayFolder** .  
  
5.  No painel **Atributos** , selecione os seguintes atributos pressionando e mantendo a tecla CTRL pressionada enquanto clica em cada um deles:  
  
    -   **Distância do Trabalho**  
  
    -   `Education`  
  
    -   **Sexo**  
  
    -   **Sinalizador de proprietário da casa**  
  
    -   **Estado Civil**  
  
    -   **Número de carros**  
  
    -   **Número de filhos em casa**  
  
    -   `Occupation`  
  
    -   **Total de Filhos**  
  
    -   **Renda Anual**  
  
6.  No janela Propriedades, clique no campo de propriedade **AttributeHierarchyDisplayFolder** na parte superior e, em seguida `Demographic`, digite.  
  
7.  No painel **Atributos** , selecione os seguintes atributos pressionando e mantendo a tecla CTRL pressionada enquanto clica em cada um deles:  
  
    -   **Endereço de email**  
  
    -   **Telemóvel**  
  
8.  Na janela Propriedades, clique no campo de propriedade **AttributeHierarchyDisplayFolder** e digite `Contacts`.  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-composite-keycolumns"></a>Definindo KeyColumns compostos  
 A propriedade **KeyColumns** contém a coluna ou as colunas que representam a chave do atributo. Nesta lição, você criará uma chave composta para a **cidade** e `State-Province` os atributos. As chaves compostas podem ser úteis quando você precisa identificar com exclusividade um atributo. Por exemplo, quando você define relações de atributo posteriormente neste tutorial, um atributo **City** deve identificar exclusivamente um `State-Province` atributo. Porém, pode haver várias cidades com o mesmo nome em estados diferentes. Por isso, você criará uma chave composta formada pelas colunas **StateProvinceName** e **City** para o atributo **Cidade** . Para obter mais informações, consulte [Modificar a propriedade KeyColumn de um atributo](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>Para definir KeyColumns compostos para o atributo Cidade  
  
1.  Abra a guia **Estrutura da Dimensão** da dimensão Cliente.  
  
2.  No painel **Atributos** , clique no atributo **Cidade** .  
  
3.  Na janela **Propriedades** , clique no campo **KeyColumns** próximo ao final e clique no botão Procurar (**...**).  
  
4.  Na caixa de diálogo **Colunas de Chave** , na lista **Colunas Disponíveis** , selecione a coluna **StateProvinceName**e clique no botão **>** .  
  
     As colunas **City** e **StateProvinceName** agora são exibidas na lista **Colunas de Chave** .  
  
5.  Clique em **OK**.  
  
6.  Para definir a propriedade **NameColumn** do atributo **Cidade** , clique no campo **NameColumn** na janela Propriedades e clique no botão Procurar (**...**).  
  
7.  Na caixa de diálogo **Coluna de Nome** , na lista **Coluna de origem** , selecione **Cidade**e clique em **OK**.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>Para definir KeyColumns compostos para o atributo State-Province  
  
1.  Verifique se a guia **Estrutura da Dimensão** da dimensão Customer está aberta.  
  
2.  No painel **atributos** , clique no `State-Province` atributo.  
  
3.  Na janela **Propriedades** , clique no campo **KeyColumns** e no botão Procurar (**...**).  
  
4.  Na caixa de diálogo **Colunas de Chave** , na lista **Colunas Disponíveis** , selecione a coluna **EnglishCountryRegionName**e clique no botão **>** .  
  
     As colunas **EnglishCountryRegionName** e **StateProvinceName** agora são exibidas na lista **Colunas de Chave** .  
  
5.  Clique em **OK**.  
  
6.  Para definir a propriedade **NameColumn** do `State-Province` atributo, clique no campo **NameColumn** na janela Propriedades e, em seguida, clique no botão procurar (**...**).  
  
7.  Na caixa de diálogo **Coluna de Nome** , na lista **Coluna de origem** , selecione **StateProvinceName**e clique em **OK**.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-attribute-relationships"></a>Definindo relações de atributo  
 Se os dados subjacentes permitirem, você também deve definir relações de atributo entre atributos. Definir relações de atributo acelera o processamento de dimensões, partições e consultas. Para obter mais informações, consulte [Definir relações de atributo](multidimensional-models/attribute-relationships-define.md) e [Relações de atributo](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relações de atributo  
  
1.  No **Designer de dimensão** da dimensão cliente, clique na guia **relações de atributo** . Talvez seja necessário aguardar.  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **Cidade** e clique em **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Cidade**. Defina o **atributo relacionado** como `State-Province`.  
  
4.  Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
     O tipo de relação é **Rígida** porque as relações entre os membros não mudarão com o passar do tempo. Por exemplo, não seria comum uma cidade se tornar parte de um estado ou província diferente.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  No diagrama, clique com o botão direito `State-Province` do mouse no atributo e selecione **nova relação de atributo**.  
  
7.  Na caixa de diálogo **criar relação de atributo** , o atributo de `State-Province` **origem** é. Defina o **atributo relacionado** como `Country-Region`.  
  
8.  Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
9. Clique em **OK**.  
  
10. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>Implantando alterações, processando objetos e exibindo alterações  
 Depois de alterar atributos e hierarquias, você deve implantar as alterações e processar novamente os objetos relacionados para poder exibir as alterações.  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>Para implantar alterações, processar objetos e exibir alterações  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Depois de receber a mensagem **Implantação Concluída com Êxito** , clique na guia **Navegador** do Designer de Dimensão da dimensão Customer e clique no botão Reconectar à esquerda da barra de ferramentas do designer.  
  
3.  Verifique se `Customer Geography` está selecionado na lista **hierarquia** e, no painel navegador, expanda **tudo**, **Austrália**, **novo Sul Gales**e, em seguida, clique em **COFF Harbour**.  
  
     O navegador exibe os clientes nesta cidade.  
  
4.  Mude para o **Designer de Cubo** do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para fazer isso, clique duas vezes no cubo **Analysis Services tutorial** no nó **cubos** de **Gerenciador de soluções**.  
  
5.  Clique na guia **Navegador** e no ícone Reconectar da barra de ferramentas do designer.  
  
6.  No painel **Grupo de Medidas** , expanda **Cliente**.  
  
     Observe que em vez de um longa lista de atributos, somente as pastas de exibição e os atributos que não têm valores de pasta de exibição aparecem sob Cliente.  
  
7.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando a dimensão Produto](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de propriedades de atributo de dimensão](multidimensional-models/dimension-attribute-properties-reference.md)   
 [Remover um atributo de uma dimensão](multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)   
 [Renomear um atributo](multidimensional-models/attribute-properties-rename-an-attribute.md)   
 [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
