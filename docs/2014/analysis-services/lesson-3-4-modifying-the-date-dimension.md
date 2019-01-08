---
title: Modificando a dimensão data | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 4689d780-4bf6-4cf8-8fde-eb3f15dd668a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77d37fff5b22e15656ef2eb76f33ada44572ba4c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526113"
---
# <a name="modifying-the-date-dimension"></a>Modificando a dimensão de data
  Na tarefa deste tópico, você criará uma hierarquia definida pelo usuário e alterará os nomes de membro exibidos nos atributos Date, Month, Calendar Quarter e Calendar Semester. Você também definirá as chaves compostas para atributos, controlará a ordem de classificação dos membros de dimensão e definirá relações de atributo.  
  
## <a name="adding-a-named-calculation"></a>Adicionando um cálculo nomeado  
 É possível adicionar um cálculo nomeado, que é uma expressão SQL representada como uma coluna calculada, a uma tabela em uma exibição da fonte de dados. A expressão se parece e se comporta como uma coluna na tabela. Os cálculos nomeados permitem que você estenda o esquema relacional de tabelas existentes em uma exibição de fonte de dados sem modificar a tabela na fonte de dados subjacente. Para obter mais informações, consulte [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>Para adicionar um cálculo nomeado  
  
1.  Para abrir a exibição de fonte de dados do **Adventure Works DW 2012** , clique duas vezes nela na pasta **Exibições da Fonte de Dados** do Gerenciador de Soluções.  
  
2.  Próximo à parte inferior do **tabelas** painel, clique com botão direito `Date`e, em seguida, clique em **novo cálculo nomeado**.  
  
3.  No **criar cálculo nomeado** caixa de diálogo, digite `SimpleDate` no **nome da coluna** caixa e, em seguida, digite ou copie e cole o seguinte `DATENAME` instrução no **expressão**  caixa:  
  
    ```  
    DATENAME(mm, FullDateAlternateKey) + ' ' +  
    DATENAME(dd, FullDateAlternateKey) + ', ' +  
    DATENAME(yy, FullDateAlternateKey)  
    ```  
  
     A instrução `DATENAME` extrai os valores de ano, mês e dia da coluna FullDateAlternateKey. Essa nova coluna poderá ser usada como o nome exibido para o atributo FullDateAlternateKey.  
  
4.  Clique em **Okey**e, em seguida, expanda `Date` no **tabelas** painel.  
  
     O `SimpleDate` cálculo nomeado aparece na lista de colunas na tabela de data, com um ícone que indica que ele é um cálculo nomeado.  
  
5.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
6.  No **tabelas** painel, clique com botão direito `Date`e, em seguida, clique em **explorar dados**.  
  
7.  Role a tela para a direita para examinar a última coluna da exibição **Explorar Tabela Date** .  
  
     Observe que o `SimpleDate` coluna aparece na exibição da fonte de dados, concatenando corretamente os dados de várias colunas da fonte de dados subjacente, sem modificar a fonte de dados original.  
  
8.  Feche a exibição **Explorar Tabela Date** .  
  
## <a name="using-the-named-calculation-for-member-names"></a>Usando o cálculo nomeado para nomes de membros  
 Após criar um cálculo nomeado na exibição da fonte de dados, você pode usá-lo como propriedade de um atributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Para usar o cálculo nomeado para nomes de membros  
  
1.  Abra o **Designer de Dimensão** da dimensão Date no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para fazer isso, clique duas vezes o `Date` da dimensão na **dimensões** nó do **Gerenciador de soluções**.  
  
2.  No painel **Atributos** da guia **Estrutura da Dimensão** , clique no atributo **Date Key** .  
  
3.  Se a janela Propriedades não estiver aberta, abra-a e clique no botão **Ocultar Automaticamente** na barra de título para que ela permaneça aberta.  
  
4.  Clique o **NameColumn** propriedade de campo na parte inferior da janela e, em seguida, clique no botão Procurar (**...** ) para abrir o **nome da coluna** caixa de diálogo.  
  
5.  Selecione `SimpleDate` na parte inferior a **coluna de origem** e, em seguida, clique **Okey**.  
  
6.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="creating-a-hierarchy"></a>Criando uma hierarquia  
 Você pode criar uma nova hierarquia arrastando um atributo do painel **Atributos** até o painel **Hierarquias** .  
  
#### <a name="to-create-a-hierarchy"></a>Para criar uma hierarquia  
  
1.  No **estrutura da dimensão** guia do Designer de dimensão para o `Date` da dimensão, arraste o **ano civil** de atributos do **atributos** painel para o **Hierarquias** painel.  
  
2.  Arraste o **semestre do calendário** de atributos da **atributos** painel no  **\<novo nível >** célula o **hierarquias**painel, sob o **ano civil** nível.  
  
3.  Arraste o **trimestre do calendário** de atributos da **atributos** painel no  **\<novo nível >** célula o **hierarquias**painel, sob o **semestre do calendário** nível.  
  
4.  Arraste o **English Month Name** de atributos da **atributos** painel no  **\<novo nível >** célula o **hierarquias**painel, sob o **trimestre do calendário** nível.  
  
5.  Arraste o **Date Key** de atributos da **atributos** painel no  **\<novo nível >** célula a **hierarquias** painel , sob o **English Month Name** nível.  
  
6.  No **hierarquias** painel, a barra de título do botão direito do mouse a **hierarquia** hierarquia, clique em **Renomear**e, em seguida, digite `Calendar Date`.  
  
7.  Usando o menu de contexto do botão direito do mouse no `Calendar Date` hierarquia, renomear o **English Month Name** nível a `Calendar Month`e, em seguida, renomeie o **Date Key** nível para `Date`.  
  
8.  Exclua o atributo **Full Date Alternate Key** do painel **Atributos** , pois você não precisará mais dele. Clique em **OK** na janela de confirmação **Excluir Objetos** .  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-attribute-relationships"></a>Definindo relações de atributo  
 Se os dados subjacentes permitirem, você também deve definir relações de atributo entre atributos. Definir relações de atributo acelera o processamento de dimensões, partições e consultas.  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relações de atributo  
  
1.  No **Designer de dimensão** para o `Date` da dimensão, clique no **relações de atributo** guia.  
  
2.  No diagrama, clique com o botão direito do mouse no atributo **English Month Name** e clique em **Nova Relação de Atributo**.  
  
3.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **English Month Name**. Defina o **Atributo Relacionado** como **Trimestre do Calendário**.  
  
4.  Na lista **Tipo de relação**, defina o tipo de relação como **Rígida**.  
  
     O tipo de relação é **Rígida** porque as relações entre os membros não mudarão com o passar do tempo.  
  
5.  Clique em **OK**.  
  
6.  No diagrama, clique com o botão direito do mouse no atributo **Calendar Quarter** e clique em **Nova Relação de Atributo**.  
  
7.  Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Trimestre Calendário**. Defina o **Atributo Relacionado** como **Semestre do Calendário**.  
  
8.  Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
9. Clique em **OK**.  
  
10. No diagrama, clique com o botão direito do mouse no atributo **Calendar Semester** e clique em **Nova Relação de Atributo**.  
  
11. Na caixa de diálogo **Criar Relação de Atributo** , o **Atributo de Origem** é **Semestre do Calendário**. Defina o **Atributo Relacionado** como **Ano Civil**.  
  
12. Na lista **Tipo de relação** , defina o tipo de relação como **Rígida**.  
  
13. Clique em **OK**.  
  
14. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="providing-unique-dimension-member-names"></a>Fornecendo nomes de membro de dimensão exclusivos  
 Nesta tarefa, você criará colunas de nomes amigáveis que serão usadas pelos atributos **EnglishMonthName**, **CalendarQuarter**e **CalendarSemester** .  
  
#### <a name="to-provide-unique-dimension-member-names"></a>Para fornecer nomes de membro de dimensão exclusivos  
  
1.  Para mudar para a exibição de fonte de dados do **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** , clique duas vezes nela na pasta **Exibições da Fonte de Dados** do Gerenciador de Soluções.  
  
2.  No **tabelas** painel, clique com botão direito `Date`e, em seguida, clique em **novo cálculo nomeado**.  
  
3.  No **criar cálculo nomeado** caixa de diálogo, digite `MonthName` no **nome da coluna** caixa e, em seguida, digite ou copie e cole a seguinte instrução no **expressão** caixa:  
  
    ```  
    EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)  
    ```  
  
     A instrução concatena o mês e o ano para cada mês na tabela em uma nova coluna.  
  
4.  Clique em **OK**.  
  
5.  No **tabelas** painel, clique com botão direito `Date`e, em seguida, clique em **novo cálculo nomeado**.  
  
6.  No **criar cálculo nomeado** caixa de diálogo, digite `CalendarQuarterDesc` no **nome da coluna** caixa e, em seguida, digite ou copie e cole o seguinte script SQL no **expressão** caixa:  
  
    ```  
    'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY ' +  
    CONVERT(CHAR (4), CalendarYear)  
    ```  
  
     Esse script de SQL concatena o trimestre e o ano para cada trimestre na tabela em uma nova coluna.  
  
7.  Clique em **OK**.  
  
8.  No **tabelas** painel, clique com botão direito `Date`e, em seguida, clique em **novo cálculo nomeado**.  
  
9. No **criar cálculo nomeado** caixa de diálogo, digite `CalendarSemesterDesc` no **nome da coluna** caixa e, em seguida, digite ou copie e cole o seguinte script SQL no **expressão** caixa:  
  
    ```  
    CASE  
    WHEN CalendarSemester = 1 THEN 'H1' + ' ' + 'CY' + ' '   
           + CONVERT(CHAR(4), CalendarYear)  
    ELSE  
    'H2' + ' ' + 'CY' + ' ' + CONVERT(CHAR(4), CalendarYear)  
    END  
    ```  
  
     Esse script de SQL concatena o semestre e o ano para cada semestre na tabela em uma nova coluna.  
  
10. Clique em **OK.**  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="defining-composite-keycolumns-and-setting-the-name-column"></a>Definindo o composto KeyColumns e configurando a Coluna de Nome  
 A propriedade **KeyColumns** contém a coluna ou as colunas que representam a chave do atributo. Nesta tarefa, você definirá a composição **KeyColumns**.  
  
#### <a name="to-define-composite-keycolumns-for-the-english-month-name-attribute"></a>Para definir o composto KeyColumns para o atributo Nome do Mês em Inglês  
  
1.  Abra a guia **Estrutura da Dimensão** da dimensão Date.  
  
2.  No painel **Atributos** , clique no atributo **English Month Name** .  
  
3.  Na janela **Propriedades** , clique no campo **KeyColumns** e clique no botão Procurar (**...**).  
  
4.  Na caixa de diálogo **Colunas de Chaves** , na lista **Colunas Disponíveis** , selecione a coluna **CalendarYear**e clique no botão **>** .  
  
5.  Agora, as colunas **EnglishMonthName** e **CalendarYear** são exibidas na lista **Colunas de Chave** .  
  
6.  Clique em **OK**.  
  
7.  Para definir a propriedade **NameColumn** do atributo **EnglishMonthName** , clique no campo **NameColumn** na janela Propriedades e clique no botão Procurar (**...**).  
  
8.  No **nome da coluna** na caixa de **coluna de origem** lista, selecione `MonthName`e, em seguida, clique em **Okey**.  
  
9. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-quarter-attribute"></a>Para definir o composto KeyColumns para o atributo Calendar Quarter  
  
1.  No painel **Atributos** , clique no atributo **Calendar Quarter** .  
  
2.  Na janela **Propriedades** , clique no campo **KeyColumns** e clique no botão Procurar (**...**).  
  
3.  Na caixa de diálogo **Colunas de Chaves**, na lista **Colunas Disponíveis**, selecione a coluna **CalendarYear** e clique no botão **>**.  
  
     Agora, as colunas **CalendarQuarter** e **CalendarYear** são exibidas na lista **Colunas de Chave** .  
  
4.  Clique em **OK**.  
  
5.  Para definir a propriedade **NameColumn** do atributo **Calendar Quarter** , clique no campo **NameColumn** na janela Propriedades e clique no botão Procurar (**...**).  
  
6.  No **nome da coluna** na caixa de **coluna de origem** lista, selecione `CalendarQuarterDesc`e, em seguida, clique em **Okey**.  
  
7.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-semester-attribute"></a>Para definir o composto KeyColumns para o atributo Calendar Semester  
  
1.  No painel **Atributos** , clique no atributo **Calendar Semester** .  
  
2.  Na janela **Propriedades** , clique no campo **KeyColumns** e clique no botão Procurar (**...**).  
  
3.  Na caixa de diálogo **Colunas de Chave** , na lista **Colunas Disponíveis** , selecione a coluna **CalendarYear**e clique no botão **>** .  
  
     Agora, as colunas **CalendarSemester** e **CalendarYear** são exibidas na lista **Colunas de Chave** .  
  
4.  Clique em **OK**.  
  
5.  Para definir a propriedade **NameColumn** do atributo **Calendar Semester** , clique no campo **NameColumn** na janela Propriedades e clique no botão Procurar (**...**).  
  
6.  No **nome da coluna** na caixa de **coluna de origem** lista, selecione `CalendarSemesterDesc`e, em seguida, clique em **Okey**.  
  
7.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="deploying-and-viewing-the-changes"></a>Implantando e exibindo as alterações  
 Depois de alterar atributos e hierarquias, você deve implantar as alterações e processar novamente os objetos relacionados para poder exibir as alterações.  
  
#### <a name="to-deploy-and-view-the-changes"></a>Para implantar e exibir as alterações  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Depois de receber a **implantação concluída com êxito** , clique no **navegador** guia da **Designer de dimensão** para o `Date` dimensão, e em seguida, clique no botão reconectar na barra de ferramentas do designer.  
  
3.  Selecione **Calendar Quarter** na lista **Hierarquia** . Examine os membros da hierarquia de atributo **Calendar Quarter** .  
  
     Observe que os nomes dos membros da hierarquia de atributo **Calendar Quarter** são mais claros e fáceis de serem usados porque você criou um cálculo nomeado para ser usado como o nome. Agora, existem membros na hierarquia de atributo **Calendar Quarter** para cada trimestre do ano. Os membros não são classificados em ordem cronológica. Em vez disso, eles são classificados por trimestre e, depois, por ano. Na próxima tarefa deste tópico, você modificará esse comportamento para classificar os membros da hierarquia de atributo por ano e, depois, por trimestre.  
  
4.  Examine os membros das hierarquias de atributo **English Month Name** e **Calendar Semester** .  
  
     Observe que os membros dessas hierarquias também não são classificados em ordem cronológica. Em vez disso, eles são classificados por mês ou semestre, respectivamente, e, então, por ano. Na próxima tarefa deste tópico, você modificará esse comportamento com o objetivo de alterar essa ordem de classificação.  
  
## <a name="changing-the-sort-order-by-modifying-composite-key-member-order"></a>Alterando a ordem de classificação modificando ordem de membro de chave composta  
 Nesta tarefa, você poderá alterar a ordem de classificação alterando a ordem das chaves que criam a chave composta.  
  
#### <a name="to-modify-the-composite-key-member-order"></a>Para modificar a ordem de membro de chave composta  
  
1.  Abra o **estrutura da dimensão** guia do Designer de dimensão para o `Date` da dimensão e, em seguida, selecione **semestre do calendário** no **atributos** painel.  
  
2.  Na janela Propriedades, examine o valor da propriedade **OrderBy** . Ela está definida como **Chave**.  
  
     Os membros da hierarquia de atributo **Calendar Semester** são classificados por seus valores chave. Em uma chave composta, a ordem das chaves de membro baseia-se primeiro no valor da primeira chave de membro e, depois, no valor da segunda chave de membro. Em outras palavras, os membros da hierarquia de atributo **Calendar Semester** são classificados primeiro por semestre e depois por ano.  
  
3.  Na janela Propriedades, clique no botão Procurar (**...**) para alterar o valor da propriedade **KeyColumns** .  
  
4.  Na lista **Colunas de Chave** da caixa de diálogo **Colunas de Chave** , verifique se a opção **CalendarSemester** está selecionada e clique na seta para baixo para inverter a ordem dos membros dessa chave composta. Clique em **OK**.  
  
     Agora, os membros da hierarquia de atributo são classificados primeiro por ano e, depois, por semestre.  
  
5.  Selecione **Calendar Quarter** no painel **Atributos** e clique no botão Procurar (**...**) da propriedade **KeyColumns** na janela Propriedades.  
  
6.  Na lista **Colunas de Chave** da caixa de diálogo **Colunas de Chave** , verifique se o atributo **CalendarQuarter** está selecionado e clique na seta para baixo para inverter a ordem dos membros desta chave composta. Clique em **OK**.  
  
     Agora, os membros da hierarquia de atributo são classificados primeiro por ano e, depois, por trimestre.  
  
7.  Selecione **English Month Name** no painel **Atributos** e clique no botão Procurar (**...**) da propriedade **KeyColumns** na janela Propriedades.  
  
8.  Na lista **Colunas de Chave** da caixa de diálogo **Colunas de Chave** , verifique se o atributo **EnglishMonthName** está selecionado e clique na seta para baixo para inverter a ordem dos membros dessa chave composta. Clique em **OK**.  
  
     Agora, os membros da hierarquia de atributo são classificados primeiro por ano e, depois, por mês.  
  
9. No menu **Compilar** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **Implantar Tutorial do Analysis Services**. Quando a implantação for concluída com êxito, clique no **Browser** guia no Designer de dimensão para o `Date` dimensão.  
  
10. Na barra de ferramentas da guia **Navegador** , clique no botão Reconectar.  
  
11. Examine os membros das hierarquias de atributo **Calendar Quarter** e **Calendar Semester** .  
  
     Observe que agora os membros dessas hierarquias são classificados em ordem cronológica, por ano e, depois, por trimestre ou semestre, respectivamente.  
  
12. Examine os membros da hierarquia de atributo **English Month Name** .  
  
     Observe que agora os membros da hierarquia são classificados primeiro por ano e, depois, por mês (em ordem alfabética). Isso ocorre porque o tipo de dados da coluna EnglishCalendarMonth na exibição da fonte de dados é uma coluna da cadeia de caracteres que se baseia no tipo de dados nvarchar no banco de dados relacional subjacente. Para obter informações sobre como habilitar os meses a serem classificados em ordem cronológica em cada ano, consulte [Classificando membros de atributo com base em um atributo secundário](lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Navegando no cubo implantado](lesson-3-5-browsing-the-deployed-cube.md)  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
