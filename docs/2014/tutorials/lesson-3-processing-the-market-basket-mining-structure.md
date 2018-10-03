---
title: 'Lição 3: Processando a estrutura de mineração da cesta de compras | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 979738186c9af128087049e71fa248d41fd27b50
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192246"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>Lição 3: Processando a estrutura de mineração do Market Basket
  Nesta lição, você aprenderá a usar o [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrução e vAssocSeqLineItems e vAssocSeqOrders do [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] modelos de banco de dados de exemplo para processar as estruturas de mineração e mineração que você criado em [lição 1: Criando a estrutura de mineração do Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md) e [lição 2: adicionando modelos de mineração à estrutura de mineração da cesta](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md).  
  
 Ao processar uma estrutura de mineração, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] lê os dados de origem e compila as estruturas que dão suporte a modelos de mineração. Quando você processa um modelo de mineração, os dados definidos pela estrutura de mineração são passados por meio do algoritmo de mineração de dados que você escolheu. O algoritmo procura tendências e padrões e, depois, armazena as informações no modelo de mineração. Portanto, o modelo de mineração na verdade não contém os dados de origem, e sim as informações que foram descobertas pelo algoritmo. Para obter mais informações sobre como processar modelos de mineração, consulte [considerações e requisitos de processamento de &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Só será necessário reprocessar uma estrutura de mineração se houver alteração em uma coluna de estrutura ou nos dados de origem. Se você adicionar um modelo de mineração a uma estrutura de mineração que já foi processada, será possível usar a instrução `INSERT INTO MINING MODEL` para treinar o novo modelo de mineração nos dados existentes.  
  
 Como a estrutura de mineração da cesta básica contém uma tabela aninhada, você terá que definir as colunas de mineração a serem treinadas, utilizando a estrutura de tabelas aninhadas, e utilizar o comando `SHAPE` para definir as consultas que recebem dados de treinamento das tabelas de origem.  
  
## <a name="insert-into-statement"></a>Instrução INSERT INTO  
 Para treinar a estrutura de mineração da cesta de compras e seus modelos de mineração associados, use o [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrução. O código na instrução pode ser dividido nas seguintes partes.  
  
-   Identificando a estrutura de mineração  
  
-   Listando as colunas na estrutura de mineração  
  
-   Definindo os dados de treinamento usando `SHAPE`  
  
 A seguir, um exemplo genérico da instrução `INSERT INTO`:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 A primeira linha do código identifica a estrutura de mineração a ser treinada:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 As linhas seguintes do código especificam as colunas definidas pela estrutura de mineração. É preciso listar cada coluna na estrutura de mineração, e cada coluna deve mapear para uma coluna contida nos dados da consulta de origem. Você pode utilizar `SKIP` para ignorar colunas que existem nos dados de origem, mas não existem na estrutura de mineração. Para obter mais informações sobre como usar `SKIP`, consulte [inserir em &#40;DMX&#41;](/sql/dmx/insert-into-dmx).  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 As linhas finais do código definem os dados que serão usados para treinar a estrutura de mineração. Como os dados de origem estão contidos dentro de duas tabelas, você usará `SHAPE` para relacionar as tabelas.  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 Nesta lição, use `OPENQUERY` para definir os dados de origem. Para obter informações sobre outros métodos de definição de consulta na fonte de dados, consulte [ &#60;consulta de fonte de dados&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará a seguinte tarefa nesta lição:  
  
-   Processe a estrutura de mineração da cesta básica  
  
## <a name="processing-the-market-basket-mining-structure"></a>Processando a estrutura de mineração da cesta básica  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Para processar a estrutura de mineração utilizando INSERT INTO  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução INSERT INTO no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    [<mining structure>]  
    ```  
  
     por:  
  
    ```  
    Market Basket  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     por:  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     Na instrução, `Products` se refere à tabela Produtos definida pela instrução SHAPE. `SKIP` é usado para ignorar a coluna Modelo, que existe nos dados de origem como uma chave, mas não é usada pela estrutura de mineração.  
  
5.  Substitua o seguinte:  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     por:  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     A consulta de fonte faz referência a [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] fonte de dados definida no [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] projeto de exemplo. Ela usa esta fonte de dados para acessar as exibições vAssocSeqLineItems e vAssocSeqOrders. Essas exibições contêm os dados de origem que serão usados para treinar o modelo de mineração. Se você não tiver criado esse projeto ou essas exibições, consulte [Tutorial básico de mineração de dados](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
     Dentro do comando `SHAPE`, você usará `OPENQUERY` para definir duas consultas. A primeira consulta define a tabela pai, e a segunda consulta define a tabela aninhada. As duas tabelas estão relacionadas usando a coluna OrderNumber que existe em ambas as tabelas.  
  
     A instrução completa agora deve ser:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Process Market Basket.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
 Após a conclusão da execução da consulta, você pode visualizar os padrões e os conjuntos de itens que foram encontrados, exibir associações ou filtrar por conjunto de itens, probabilidade ou importância. Para exibir essas informações no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique no nome do modelo de dados e, em seguida, clique em **procurar**.  
  
 Na próxima lição, você criará várias previsões com base nos modelos de mineração que adicionou à estrutura da cesta básica.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Executando previsões de Market Basket](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
