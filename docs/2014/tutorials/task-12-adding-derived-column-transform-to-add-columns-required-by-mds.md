---
title: 'Tarefa 12: adicionando a transformação de coluna derivada para adicionar colunas exigidas pelo MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18789f5bc1d97e1531588d50e2430829f95912b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65485246"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Tarefa 12: Adicionando a Transformação Coluna Derivada para adicionar as colunas necessárias pelo MDS
  Nesta tarefa, você adiciona a Transformação Coluna Derivada ao fluxo de dados. Você adiciona duas colunas derivadas, **importType** e **BatchTag**, aos registros passados para essa transformação. Você deve adicionar essas colunas antes de carregar os dados nas tabelas de preparo no MDS. Esses duas colunas são necessárias para as tabelas de preparo no MDS. Consulte [tabelas de preparo de membro folha](../master-data-services/leaf-member-staging-table-master-data-services.md) para obter mais detalhes.  
  
1.  Arraste e solte a **coluna derivada Transform** de uma seção **comum** na **caixa de ferramentas do SSIS** para a guia fluxo de **dados** .  
  
2.  Clique com o botão direito do mouse em transformação de **coluna derivada** na guia **fluxo de dados** e clique em **renomear**. Digite **adicionar colunas exigidas pelo MDS** e pressione **Enter**.  
  
3.  Conecte as **duplicatas do filtro** para **adicionar colunas exigidas pelo MDS** usando o conector azul. Você deverá ver a caixa de diálogo **seleção de saída de entrada** .  
  
4.  Na caixa de diálogo **seleção de saída de entrada** , selecione **registros exclusivos**e clique em **OK**.  
  
     ![Caixa de diálogo Seleção de Saída e Entrada](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "Caixa de diálogo Seleção de Saída e Entrada")  
  
5.  Clique em **SSIS** na barra de menus e clique em **variáveis**.  
  
6.  Na janela **variáveis** , clique no botão **Adicionar variável** na barra de ferramentas.  
  
     ![Janela Variáveis do SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "Janela Variáveis do SSIS")  
  
7.  Digite **importType** para o **nome** e **2** para o **valor**. Você especifica o valor como 2 porque deseja adicionar novos membros a uma entidade no MDS. Para obter detalhes sobre esse parâmetro, consulte [tabela de preparo de membros folha](../master-data-services/leaf-member-staging-table-master-data-services.md).  
  
8.  Clique no botão Adicionar barra de ferramentas **variável** novamente.  
  
9. Digite **BatchTag** para o **nome**, selecione **cadeia de caracteres** para o **tipo de dados**e **EIMBatch** para o **valor**. **BatchTag** é apenas um nome exclusivo para o lote que você enviará para o MDS.  
  
10. Na guia **fluxo de dados** , clique duas vezes em **adicionar colunas exigidas pelo MDS**.  
  
11. Na caixa de diálogo **Editor de transformação coluna derivada** , na **caixa de listagem no painel inferior**, digite **importType** para o **nome da coluna derivada**.  
  
12. Expanda **variáveis e parâmetros** no painel superior esquerdo, arraste e solte **User:: importType** para a coluna **expression** .  
  
     ![Editor de Transformação Colunas Derivadas](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "Editor de Transformação Colunas Derivadas")  
  
13. Digite **BatchTag** na próxima linha para o **nome da coluna derivada**.  
  
14. Arrastar e soltar **usuário:: BatchTag** de **variáveis e parâmetros** para a coluna de **expressão** .  
  
15. Clique em **OK** para fechar a caixa de diálogo **transformação coluna derivada** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 13: Adicionando o destino OLE DB para gravar dados na tabela de preparo do MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
