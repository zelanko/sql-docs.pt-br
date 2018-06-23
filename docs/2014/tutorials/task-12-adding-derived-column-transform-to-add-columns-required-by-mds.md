---
title: 'Tarefa 12: Adicionando transformação coluna derivada para adicionar colunas exigidas pelo MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b81dd18f0ba79167a66b5cdd09c2059fcd0e0a96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120248"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Tarefa 12: Adicionando a Transformação Coluna Derivada para adicionar as colunas necessárias pelo MDS
  Nesta tarefa, você adiciona a Transformação Coluna Derivada ao fluxo de dados. Você adiciona duas colunas derivadas, **ImportType** e **BatchTag**, para os registros passados a essa transformação. Você deve adicionar essas colunas antes de carregar os dados nas tabelas de preparo no MDS. Esses duas colunas são necessárias para as tabelas de preparo no MDS. Consulte [tabelas de preparo de membro folha](http://msdn.microsoft.com/library/ee633854.aspx) para obter mais detalhes.  
  
1.  Arraste e solte **transformação coluna derivada** de **comuns** seção o **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia.  
  
2.  Clique com botão direito **coluna derivada** transformar no **de fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo **adicionar colunas exigidas pelo MDS** e pressione **ENTER**.  
  
3.  Conecte-se **filtrar duplicatas** para **adicionar colunas exigidas pelo MDS** usando o conector azul. Você deve ver o **seleção de saída e entrada** caixa de diálogo.  
  
4.  No **seleção de saída e entrada** caixa de diálogo, selecione **registros exclusivos**e clique em **Okey**.  
  
     ![Caixa de diálogo de seleção de saída de entrada](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "caixa de diálogo de seleção de saída de entrada")  
  
5.  Clique em **SSIS** na barra de menus, clique em **variáveis**.  
  
6.  No **variáveis** janela, clique em **Adicionar variável** na barra de ferramentas.  
  
     ![Janela de variáveis do SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "janela variáveis do SSIS")  
  
7.  Tipo **ImportType** para o **nome** e **2** para o **valor**. Você especifica o valor como 2 porque deseja adicionar novos membros a uma entidade no MDS. Para obter detalhes sobre esse parâmetro, consulte [tabela de preparo de membro folha](http://msdn.microsoft.com/library/ee633854.aspx).  
  
8.  Clique em **Adicionar variável** botão da barra de ferramentas novamente.  
  
9. Tipo **BatchTag** para o **nome**, selecione **cadeia de caracteres** para o **tipo de dados**, e **EIMBatch** para o **Valor**. **BatchTag** é apenas um nome exclusivo para o lote que você envie ao MDS.  
  
10. No **de fluxo de dados** guia, clique duas vezes em **adicionar colunas exigidas pelo MDS**.  
  
11. No **Editor de transformação coluna derivada** na caixa de **caixa de lista no painel inferior**, tipo **ImportType** para o **nome de coluna derivada**.  
  
12. Expanda **variáveis e parâmetros** no painel superior esquerdo, arraste e solte **User:: importType** para o **expressão** coluna.  
  
     ![Derivado do Editor de transformação de coluna](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "derivado do Editor de transformação de coluna")  
  
13. Tipo **BatchTag** na próxima linha para o **nome de coluna derivada**.  
  
14. Arraste e solte **User:: batchtag** de **variáveis e parâmetros** para o **expressão** coluna.  
  
15. Clique em **Okey** para fechar o **transformação coluna derivada** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 13: Adicionando o destino OLE DB para gravar dados na tabela de preparo do MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  