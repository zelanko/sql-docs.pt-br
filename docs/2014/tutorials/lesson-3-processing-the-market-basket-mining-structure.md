---
title: 'Lição 3: processando a estrutura de mineração de cesta de mercado | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce2c2e6944d524a38edc331d2cd128ca7cf7d419
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62653840"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>Lição 3: Processando a estrutura de mineração do Market Basket
  Nesta lição, você usará a instrução [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) e o vAssocSeqLineItems e o vAssocSeqOrders do banco [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] de dados de exemplo para processar as estruturas de mineração e os modelos de mineração criados na [lição 1: criando a estrutura de mineração da cesta de compras](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md) e a [lição 2: adicionando modelos de mineração à estrutura de mineração da cesta de compras](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md).  
  
 Ao processar uma estrutura de mineração, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] lê os dados de origem e compila as estruturas que dão suporte a modelos de mineração. Quando você processa um modelo de mineração, os dados definidos pela estrutura de mineração são passados pelo algoritmo de Data Mining que você escolheu. O algoritmo procura tendências e padrões e, depois, armazena as informações no modelo de mineração. Portanto, o modelo de mineração na verdade não contém os dados de origem, e sim as informações que foram descobertas pelo algoritmo. Para obter mais informações sobre o processamento de modelos de mineração, consulte [requisitos e considerações de processamento &#40;&#41;de mineração de dados ](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Só será necessário reprocessar uma estrutura de mineração se houver alteração em uma coluna de estrutura ou nos dados de origem. Se você adicionar um modelo de mineração a uma estrutura de mineração que já foi processada, será possível usar a instrução `INSERT INTO MINING MODEL` para treinar o novo modelo de mineração nos dados existentes.  
  
 Como a estrutura de mineração da cesta básica contém uma tabela aninhada, você terá que definir as colunas de mineração a serem treinadas, utilizando a estrutura de tabelas aninhadas, e utilizar o comando `SHAPE` para definir as consultas que recebem dados de treinamento das tabelas de origem.  
  
## <a name="insert-into-statement"></a>Instrução INSERT INTO  
 Para treinar a estrutura de mineração de cesta de compras e seus modelos de mineração associados, use a instrução [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx) . O código na instrução pode ser dividido nas seguintes partes.  
  
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
  
 As linhas seguintes do código especificam as colunas definidas pela estrutura de mineração. É preciso listar cada coluna na estrutura de mineração, e cada coluna deve mapear para uma coluna contida nos dados da consulta de origem. Você pode utilizar `SKIP` para ignorar colunas que existem nos dados de origem, mas não existem na estrutura de mineração. Para obter mais informações sobre como usar `SKIP`o, consulte [inserir em &#40;DMX&#41;](/sql/dmx/insert-into-dmx).  
  
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
  
 Nesta lição, use `OPENQUERY` para definir os dados de origem. Para obter informações sobre outros métodos de definição de uma consulta nos dados de origem, consulte [&#60;&#62;de consulta de dados de origem ](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará a seguinte tarefa nesta lição:  
  
-   Processe a estrutura de mineração da cesta básica  
  
## <a name="processing-the-market-basket-mining-structure"></a>Processando a estrutura de mineração da cesta básica  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>Para processar a estrutura de mineração utilizando INSERT INTO  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
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
  
     Na instrução, `Products` se refere à tabela Produtos definida pela instrução SHAPE. 
  `SKIP` é usado para ignorar a coluna Modelo, que existe nos dados de origem como uma chave, mas não é usada pela estrutura de mineração.  
  
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
  
     A consulta de origem faz [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] referência à fonte de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] definida no projeto de exemplo. Ela usa esta fonte de dados para acessar as exibições vAssocSeqLineItems e vAssocSeqOrders. Essas exibições contêm os dados de origem que serão usados para treinar o modelo de mineração. Se você não criou este projeto ou esses modos de exibição, consulte o [tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
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
  
6.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
7.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Process Market Basket.dmx`.  
  
8.  Na barra de ferramentas, clique no botão **executar** .  
  
 Após a conclusão da execução da consulta, você pode visualizar os padrões e os conjuntos de itens que foram encontrados, exibir associações ou filtrar por conjunto de itens, probabilidade ou importância. Para exibir essas informações, no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no nome do modelo de dados e clique em **procurar**.  
  
 Na próxima lição, você criará várias previsões com base nos modelos de mineração que adicionou à estrutura da cesta básica.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Executando previsões de Market Basket](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
