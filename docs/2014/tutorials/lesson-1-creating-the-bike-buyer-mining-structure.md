---
title: 'Lição 1: Criando a estrutura de mineração de comprador de bicicleta | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a73ac60b-660f-458a-bd2f-993fbeba7226
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8a4c42548e00ec27831639c7d7a147be3fcca1a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325316"
---
# <a name="lesson-1-creating-the-bike-buyer-mining-structure"></a>Lição 1: Criando a estrutura de mineração de Comprador de Bicicleta
  Nesta lição, você criará uma estrutura de mineração que permite prever se um cliente potencial da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] irá adquirir uma bicicleta. Se você estiver familiarizado com estruturas de mineração e seus papéis na mineração de dados, consulte [estruturas de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 A estrutura de mineração de comprador de bicicleta que você criará nesta lição oferece suporte à adição de modelos de mineração com base nas [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)[algoritmo de árvores de decisão Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md). Em lições posteriores, você usará os modelos de mineração de clustering para explorar as várias maneiras nas quais os clientes podem ser agrupados e usará os modelos de mineração da árvore de decisão para prever se um cliente potencial comprará ou não uma bicicleta.  
  
## <a name="create-mining-structure-statement"></a>Instrução CREATE MINING STRUCTURE  
 Para criar uma estrutura de mineração, use o [criar estrutura de MINERAÇÃO &#40;DMX&#41; ](/sql/dmx/create-mining-structure-dmx) instrução. O código na instrução pode ser dividido nas seguintes partes:  
  
-   Nomeando a estrutura.  
  
-   Definindo a coluna de chave.  
  
-   Definindo as colunas de mineração.  
  
-   Definindo um conjunto de dados de teste opcional.  
  
 A seguir, veja um exemplo genérico da instrução CREATE MINING STRUCTURE:  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
(  
    <key column>,  
    <mining structure columns>  
)   
WITH HOLDOUT (<holdout specifier>)  
```  
  
 A primeira linha do código define o nome da estrutura:  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
```  
  
 Para obter informações sobre como nomear um objeto em extensões DMX (Data Mining), consulte [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 A próxima linha do código define a coluna de chave da estrutura de mineração, que identifica exclusivamente uma entidade nos dados de origem:  
  
```  
<key column>,  
```  
  
 Na estrutura de mineração que você criará, o identificador do cliente, `CustomerKey`, define uma entidade nos dados de origem.  
  
 A próxima linha do código define as colunas de mineração que serão usadas pelos modelos de mineração associados à estrutura de mineração.  
  
```  
<mining structure columns>  
```  
  
 Você pode usar a função DISCRETIZE dentro \<colunas da estrutura de mineração > para diferenciar as colunas contínuas usando a sintaxe a seguir:  
  
 `DISCRETIZE(<method>,<number of buckets>)`  
  
 Para obter mais informações sobre como diferenciar colunas, consulte [métodos de discretização &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md). Para obter mais informações sobre os tipos de colunas de estrutura que você pode definir de mineração, consulte [colunas de estrutura de mineração](../../2014/analysis-services/data-mining/mining-structure-columns.md).  
  
 A última linha do código define uma partição opcional na estrutura de mineração:  
  
```  
WITH HOLDOUT (<holdout specifier>)  
```  
  
 Você especifica parte dos dados a serem usados no teste dos modelos de mineração relacionados com a estrutura, e os demais dados serão usados para treinamento dos modelos. Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria um conjunto de dados de teste que contém 30% de todos os dados dos casos. Você adicionará a especificação de que o conjunto de dados de teste deve conter 30% dos casos até o máximo de 1000 casos. Se 30% dos casos for inferior a 1000, o conjunto de dados de teste terá uma quantidade menor.  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Criar uma nova consulta em branco.  
  
-   Alterar a consulta para criar a estrutura de mineração.  
  
-   Executar a consulta.  
  
## <a name="creating-the-query"></a>Criando a consulta  
 A primeira etapa é se conectar a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e criar uma nova consulta DMX no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Para criar uma nova consulta DMX no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  No **conectar ao servidor** caixa de diálogo, para **tipo de servidor**, selecione **Analysis Services**. Na **nome do servidor**, digite `LocalHost`, ou digite o nome da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você deseja se conectar para esta lição. Clique em **Conectar**.  
  
3.  No **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX** para abrir o **Editor de consultas**e uma nova consulta em branco.  
  
## <a name="altering-the-query"></a>Alterando a consulta  
 A próxima etapa é modificar a instrução CREATE MINING STRUCTURE descrita acima para criar a estrutura de mineração de Comprador de Bicicleta.  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>Para personalizar a instrução CREATE MINING STRUCTURE.  
  
1.  No Editor de Consultas, copie o exemplo genérico da instrução CREATE MINING STRUCTURE na consulta em branco.  
  
2.  Substitua o seguinte:  
  
    ```  
    [<mining structure>]   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
3.  Substitua o seguinte:  
  
    ```  
    <key column>   
    ```  
  
     por:  
  
    ```  
    CustomerKey LONG KEY  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining structure columns>   
    ```  
  
     por:  
  
    ```  
    [Age] LONG DISCRETIZED(Automatic,10),  
    [Bike Buyer] LONG DISCRETE,  
    [Commute Distance] TEXT DISCRETE,  
    [Education] TEXT DISCRETE,  
    [Gender] TEXT DISCRETE,  
    [House Owner Flag] TEXT DISCRETE,  
    [Marital Status] TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Number Children At Home] LONG DISCRETE,  
    [Occupation] TEXT DISCRETE,  
    [Region] TEXT DISCRETE,  
    [Total Children]LONG DISCRETE,  
    [Yearly Income] DOUBLE CONTINUOUS  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    WITH HOLDOUT (holdout specifier>)  
    ```  
  
     por:  
  
    ```  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
    ```  
  
     A instrução completa da estrutura de mineração agora deve ser:  
  
    ```  
    CREATE MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key] LONG KEY,  
       [Age]LONG DISCRETIZED(Automatic,10),  
       [Bike Buyer] LONG DISCRETE,  
       [Commute Distance] TEXT DISCRETE,  
       [Education] TEXT DISCRETE,  
       [Gender] TEXT DISCRETE,  
       [House Owner Flag] TEXT DISCRETE,  
       [Marital Status] TEXT DISCRETE,  
       [Number Cars Owned]LONG DISCRETE,  
       [Number Children At Home]LONG DISCRETE,  
       [Occupation] TEXT DISCRETE,  
       [Region] TEXT DISCRETE,  
       [Total Children]LONG DISCRETE,  
       [Yearly Income] DOUBLE CONTINUOUS  
    )  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
  
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Bike Buyer Structure.dmx`.  
  
## <a name="executing-the-query"></a>Executando a consulta  
 A última etapa é executar a consulta. Depois que uma consulta é criada e salva, ela precisa ser executada. Ou seja, a instrução precisa ser executada para criar a estrutura de mineração no servidor. Para obter mais informações sobre como executar consultas no Editor de consultas, consulte [Editor de consultas do mecanismo de banco de dados &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Para executar a consulta.  
  
1.  No Editor de consultas, na barra de ferramentas, clique em **Execute**.  
  
     O status da consulta é exibido na **mensagens** guia na parte inferior do Editor de consultas após a instrução termina a execução. As mensagens devem exibir:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Uma estrutura nova nomeada **comprador de bicicleta** agora existe no servidor.  
  
 Na próxima lição, você adicionará modelos de mineração à estrutura que acaba de criar.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Adicionando modelos de mineração à estrutura de mineração de Comprador de Bicicleta](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
  
  
