---
title: 'Lição 10 do tutorial de serviços de análise: criar partições | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: b7a4cfcb32023c20e05728a3faac3715278c1019
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43091324"
---
# <a name="create-partitions"></a>Criar partições

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você cria partições dividir a tabela FactInternetSales em partes lógicas menores que podem ser processadas (atualizadas) independentemente de outras partições. Por padrão, cada tabela incluída em seu modelo tem uma partição, o que inclui todas a colunas e linhas da tabela. Para a tabela FactInternetSales, desejamos dividir os dados por ano; uma partição para cada um dos cinco anos da tabela. Cada partição pode ser processada independentemente. Para obter mais informações, consulte [partições](../tabular-models/partitions-ssas-tabular.md). 
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 9: criar hierarquias](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Criar partições  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Para criar partições na tabela FactInternetSales  
  
1.  No Gerenciador de modelos tabulares, expanda **tabelas**e, em seguida, clique com botão direito **FactInternetSales** > **partições**.  
  
2.  No Gerenciador de partições, clique em **cópia**e, em seguida, altere o nome para **FactInternetSales2010**.
  
    Porque você deseja que a partição inclua somente as linhas dentro de um determinado período, para o ano de 2010, você deve modificar a expressão de consulta.
  
4.  Clique em **Design** para abrir o Editor de consultas e, em seguida, clique no **FactInternetSales2010** consulta.

5.  Na visualização, clique na seta para baixo a **OrderDate** título de coluna e clique **filtros de data/hora** > **entre**.

    ![as-lesson10-query-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  Na caixa de diálogo Filtrar linhas, no **Mostrar linhas nas quais: OrderDate**, deixe **é posterior ou igual a**e, em seguida, no campo Data, digite **1/1/2010**. Deixe o **e** operador selecionado, em seguida, selecione **está antes**, em seguida, no campo Data, digite **1/1/2011**e, em seguida, clique em **Okey**.

    ![como-lesson10-filtrar-linhas](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    Observe que no Editor de consulta, em etapas aplicadas, você vê outra etapa chamada linhas filtradas. Esse filtro é selecionar apenas as datas de pedido de 2010.

8.  Clique em **Importar**.

    No Gerenciador de partições, observe que a expressão de consulta agora tem uma cláusula adicional de linhas filtradas.

    ![as-lesson10-query](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    Essa instrução Especifica que essa partição deve incluir somente os dados nessas linhas onde OrderDate refere-se no ano civil de 2010, conforme especificado na cláusula linhas filtradas.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>Para criar uma partição para o ano 2011  
  
1.  Na lista de partições, clique no **FactInternetSales2010** partição que você criou e, em seguida, clique em **cópia**.  Altere o nome de partição para **FactInternetSales2011**. 

    Você não precisa usar o Editor de consultas para criar uma nova cláusula linhas filtradas. Como você criou uma cópia da consulta para o 2010, tudo o que você precisa fazer é fazer uma pequena alteração na consulta para 2011.
  
2.  Na **expressão de consulta**, em ordem para que essa partição inclua somente as linhas do ano 2011, substitua os anos na cláusula linhas filtradas com **2011** e **2012**, respectivamente, como:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>Para criar partições para 2012, 2013 e 2014.  
  
- Siga as etapas anteriores, criando partições para 2012, 2013 e 2014, alterando os anos na cláusula linhas filtradas para incluir apenas as linhas nesse ano. 
  

## <a name="delete-the-factinternetsales-partition"></a>Excluir a partição FactInternetSales

Agora que você tem partições para cada ano, você pode excluir a partição FactInternetSales; impedindo a sobreposição ao escolher o processo de todos os durante o processamento de partições.

#### <a name="to-delete-the-factinternetsales-partition"></a>Para excluir a partição FactInternetSales

-  Clique o **FactInternetSales** de partição e, em seguida, clique em **excluir**.



## <a name="process-partitions"></a>Processar partições  

No Gerenciador de partições, observe os **último processamento** coluna para cada uma das novas partições que você criou mostra essas partições nunca foram processadas. Quando você cria partições, você deve executar uma operação processar partições ou processar tabela para atualizar os dados nessas partições.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>Para processar as partições FactInternetSales  
  
1.  Clique em **Okey** para fechar o Gerenciador de partições.  
  
2.  Clique o **FactInternetSales** da tabela e, em seguida, clique no **modelo** menu > **processo** > **processar partições**.  
  
3.  Na caixa de diálogo processar partições, verifique se **modo** é definido como **processar padrão**.  
  
4.  Marque a caixa de seleção na coluna **Processar** para cada uma das cinco partições criadas e clique em **OK**.  

    ![como-lesson10-processo-partições](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    Se você for solicitado para credenciais de representação, insira o nome de usuário do Windows e a senha que você especificou na lição 2.  
  
    A caixa de diálogo **Processamento de Dados** será exibida, mostrando os detalhes do processo de cada partição. Observe que um número diferente de linhas para cada partição é transferido. Cada partição inclui somente as linhas do ano especificado na cláusula WHERE na instrução SQL. Quando o processamento for concluído, vá em frente e feche a caixa de diálogo Processamento de Dados.  
  
    ![como-lesson10-processo-concluído](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>O que vem a seguir?

Vá para a próxima lição: [lição 11: criar funções](../tutorial-tabular-1400/as-lesson-11-create-roles.md). 
