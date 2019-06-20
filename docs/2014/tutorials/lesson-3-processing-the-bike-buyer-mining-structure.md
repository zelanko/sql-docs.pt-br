---
title: 'Lição 3: Processando a estrutura de mineração de comprador de bicicleta | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e748c2cd-339d-4e82-82f1-be2d0fc41b61
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e3f85016b32884b9a6b809e28d20d9985f97cd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655791"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>Lição 3: Como processar a estrutura de mineração de Comprador de Bicicleta
  Nesta lição, você usará a inserção em instrução e a exibição vTargetMail do [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] banco de dados de exemplo para processar as estruturas de mineração e modelos de mineração que você criou na [lição 1: Criando a estrutura de mineração de comprador de bicicleta](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md) e [lição 2: Adicionando modelos de mineração à estrutura de mineração de comprador de bicicleta](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 Ao processar uma estrutura de mineração, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] lê os dados de origem e compila as estruturas que dão suporte a modelos de mineração. Ao processar um modelo de mineração, os dados definidos pela estrutura de mineração são passados pelo algoritmo de mineração de dados escolhido. O algoritmo procura tendências e padrões e, depois, armazena as informações no modelo de mineração. Portanto, o modelo de mineração na verdade não contém os dados de origem, e sim as informações que foram descobertas pelo algoritmo. Para obter mais informações sobre como processar modelos de mineração, consulte [considerações e requisitos de processamento de &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Você precisará reprocessar uma estrutura de mineração somente se você alterar uma coluna de estrutura ou alterar os dados de origem. Adicionando-se um modelo de mineração a uma estrutura de mineração que já foi processada, é possível usar a instrução INSERT INTO MINING MODEL para treinar o novo modelo de mineração.  
  
## <a name="train-structure-template"></a>Treinar modelo de estrutura  
 Para treinar a estrutura de mineração e modelos de mineração associados, use o [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrução. O código na instrução pode ser dividido nas seguintes partes:  
  
-   Identificando a estrutura de mineração  
  
-   Listando as colunas na estrutura de mineração  
  
-   Definindo os dados de treinamento  
  
 Segue um exemplo genérico da instrução INSERT INTO:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 A primeira linha do código identifica a estrutura de mineração a ser treinada:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 A linha seguinte do código especifica as colunas definidas pela estrutura de mineração. É preciso listar cada coluna na estrutura de mineração, e cada coluna deve mapear para uma coluna contida nos dados da consulta de origem.  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 A linha final do código define os dados que serão usados para treinar a estrutura de mineração:  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 Nesta lição, use `OPENQUERY` para definir os dados de origem. Para obter informações sobre outros métodos de definição da consulta de origem, consulte [ &#60;consulta de fonte de dados&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará a seguinte tarefa nesta lição:  
  
-   Processe a estrutura de mineração de Compradores de Bicicleta  
  
## <a name="processing-the-predictive-mining-structure"></a>Processando a estrutura de mineração preditiva  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Para processar a estrutura de mineração utilizando INSERT INTO  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução INSERT INTO no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    [<mining structure name>]   
    ```  
  
     por:  
  
    ```  
    Bike Buyer  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining structure columns>  
    ```  
  
     por:  
  
    ```  
    [Customer Key],  
    [Age],  
    [Bike Buyer],  
    [Commute Distance],  
    [Education],  
    [Gender],  
    [House Owner Flag],  
    [Marital Status],  
    [Number Cars Owned],  
    [Number Children At Home],  
    [Occupation],  
    [Region],  
    [Total Children],  
    [Yearly Income]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     por:  
  
    ```  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
     A instrução OPENQUERY referencia a fonte de dados [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] para acessar a exibição vTargetMail. A exibição contém os dados de origem que serão usados para treinar os modelos de mineração.  
  
     A instrução completa agora deve ser:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key],  
       [Age],  
       [Bike Buyer],  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]     
    )  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Process Bike Buyer Structure.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
 Na próxima lição, você explorará o conteúdo dos modelos de mineração adicionados à estrutura de mineração nesta lição.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Procurar os modelos de mineração de comprador de bicicleta](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  
