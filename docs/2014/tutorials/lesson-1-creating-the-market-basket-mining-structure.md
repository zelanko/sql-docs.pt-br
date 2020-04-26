---
title: 'Lição 1: criando a estrutura de mineração de cesta de mercado | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a817c8d1-aff4-42b4-b194-ad9cc1c60f35
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6a6e123e525512a72d70bcc8ca2eba549d1347e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62676263"
---
# <a name="lesson-1-creating-the-market-basket-mining-structure"></a>Lição 1: Criando a estrutura de mineração do Market Basket 
  Nesta lição, você criará uma estrutura de mineração que permite prever quais produtos [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] um cliente tende a adquirir ao mesmo tempo. Se você não estiver familiarizado com as estruturas de mineração e sua função no Data Mining, consulte [estruturas de mineração &#40;Analysis Services-&#41;de mineração de dados ](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 A estrutura de mineração de associação que você criará nesta lição oferece suporte à adição de modelos de mineração com base no [algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md). Em lições posteriores, você usará os modelos de mineração para prever o tipo de produtos que um cliente tente a comprar ao mesmo tempo, que é chamado de análise de cesta básica. Por exemplo, você pode achar que os clientes tendem a comprar mountain bikes, pneus de bicicleta e capacetes ao mesmo tempo.  
  
 Nesta lição, a estrutura de mineração é definida usando as tabelas aninhadas. As tabelas aninhadas são usadas porque o domínio de dados que será definido pela estrutura está em duas tabelas de origem diferentes. Para obter mais informações sobre tabelas aninhadas, consulte [tabelas aninhadas &#40;Analysis Services&#41;de mineração de dados ](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
## <a name="create-mining-structure-statement"></a>Instrução CREATE MINING STRUCTURE  
 Para criar uma estrutura de mineração contendo uma tabela aninhada, use a instrução [criar estrutura de mineração &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx) . O código na instrução pode ser dividido nas seguintes partes:  
  
-   Nomeando a estrutura  
  
-   Definindo a coluna de chave  
  
-   Definindo as colunas de mineração  
  
-   Definindo as colunas de tabelas aninhadas  
  
 A seguir, veja um exemplo genérico da instrução CREATE MINING STRUCTURE:  
  
```  
CREATE MINING STRUCTURE [<Mining Structure Name>]  
(  
   <key column>,  
   <mining structure columns>,  
   <table columns>  
   (  <nested key column>,  
      <nested mining structure columns> )  
)  
  
```  
  
 A primeira linha do código define o nome da estrutura:  
  
```  
CREATE MINING STRUCTURE [Mining Structure Name]  
```  
  
 Para obter informações sobre como nomear um objeto no DMX, consulte [identificadores &#40;&#41;DMX ](/sql/dmx/identifiers-dmx).  
  
 A próxima linha do código define a coluna de chave da estrutura de mineração, que identifica exclusivamente uma entidade nos dados de origem:  
  
```  
<key column>  
```  
  
 A próxima linha do código define as colunas de mineração que serão usadas pelos modelos de mineração associados à estrutura de mineração.  
  
```  
<mining structure columns>  
```  
  
 As próximas linhas do código definem as colunas de tabela aninhadas:  
  
```  
<table columns>  
(  <nested key column>,  
   <nested mining structure columns> )  
```  
  
 Para obter informações sobre os tipos de colunas de estrutura de mineração que você pode definir, consulte [colunas da estrutura de mineração](../../2014/analysis-services/data-mining/mining-structure-columns.md).  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] cria um conjunto de dados de validação de 30 por cento para cada estrutura de mineração; no entanto, ao usar DMX para criar uma estrutura de mineração, você deverá adicionar manualmente o conjunto de dados de validação, se desejado.  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Criar uma nova consulta em branco  
  
-   Alterar a consulta para criar a estrutura de mineração  
  
-   Executar a consulta  
  
## <a name="creating-the-query"></a>Criando a consulta  
 A primeira etapa é se conectar a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e criar uma nova consulta DMX no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Para criar uma nova consulta DMX no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Na caixa de diálogo **conectar ao servidor** , para **tipo de servidor**, selecione **Analysis Services**. Em **nome do servidor**, `LocalHost`digite ou o nome da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] à qual você deseja se conectar para esta lição. Clique em **Conectar**.  
  
3.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
## <a name="altering-the-query"></a>Alterando a consulta  
 A próxima etapa é modificar a instrução CREATE MINING STRUCTURE descrita acima para criar a estrutura de mineração de Cesta Básica.  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>Para personalizar a instrução CREATE MINING STRUCTURE.  
  
1.  No editor de consultas, copie o exemplo genérico da instrução criar estrutura de mineração para a consulta em branco.  
  
2.  Substitua o seguinte:  
  
    ```  
    [mining structure name]   
    ```  
  
     por:  
  
    ```  
    [Market Basket]  
    ```  
  
3.  Substitua o seguinte:  
  
    ```  
    <key column>  
    ```  
  
     por:  
  
    ```  
    OrderNumber TEXT KEY  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <table columns>  
    (  <nested key column>,  
       <nested mining structure columns> )  
    ```  
  
     por:  
  
    ```  
    [Products] TABLE (  
        [Model] TEXT KEY  
    )  
    ```  
  
     A linguagem TEXT KEY especifica que a coluna Modelo é a coluna de chave para a tabela aninhada.  
  
     A instrução completa da estrutura de mineração agora deve ser:  
  
    ```  
    CREATE MINING STRUCTURE [Market Basket] (  
        OrderNumber TEXT KEY,  
        [Products] TABLE (  
            [Model] TEXT KEY  
        )  
    )  
    ```  
  
5.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
6.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Market Basket Structure.dmx`.  
  
## <a name="executing-the-query"></a>Executando a consulta  
 A última etapa é executar a consulta. Depois que você cria e salva a consulta, ela deve ser executada (isto é, a instrução deve ser executada) para criar a estrutura de mineração no servidor. Para obter mais informações sobre a execução de consultas no editor de consultas, consulte [mecanismo de banco de dados editor de consultas &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Para executar a consulta.  
  
-   No editor de consultas, na barra de ferramentas, clique em **executar**.  
  
     O status da consulta é exibido na guia **mensagens** na parte inferior do editor de consultas após a conclusão da execução da instrução. As mensagens devem exibir:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Uma nova estrutura denominada **cesta de mercado** agora existe no servidor.  
  
 Na próxima lição, você adicionará dois modelos de mineração à estrutura de mineração Cesta Básica recém-criada.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Adicionando modelos de mineração à estrutura de mineração do Market Basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
  
  
