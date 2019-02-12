---
title: 'Tarefa 12: Adicionar transformação coluna derivada para adicionar colunas exigidas pelo MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c80f719bd756a0ad241ef270507e638b08c2081
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036508"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Tarefa 12: Adicionando a Transformação Coluna Derivada para adicionar as colunas necessárias para o MDS
  Nesta tarefa, você adiciona a Transformação Coluna Derivada ao fluxo de dados. Você adiciona duas colunas derivadas, **ImportType** e **BatchTag**, para os registros passados a essa transformação. Você deve adicionar essas colunas antes de carregar os dados nas tabelas de preparo no MDS. Esses duas colunas são necessárias para as tabelas de preparo no MDS. Ver [tabelas de preparo de membros folha](../master-data-services/leaf-member-staging-table-master-data-services.md) para obter mais detalhes.  
  
1.  Arrastar e soltar **transformação coluna derivada** de **comuns** seção os **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia.  
  
2.  Clique com botão direito **coluna derivada** transformar na **fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo de **adicionar colunas exigidas pelo MDS** e pressione **ENTER**.  
  
3.  Conectar-se **filtrar duplicatas** à **adicionar colunas exigidas pelo MDS** usando o conector azul. Você deve ver a **seleção de saída e entrada** caixa de diálogo.  
  
4.  No **seleção de saída e entrada** caixa de diálogo, selecione **registros exclusivos**e clique em **Okey**.  
  
     ![Caixa de diálogo de seleção de saída de entrada](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "caixa de diálogo de seleção de saída de entrada")  
  
5.  Clique em **SSIS** na barra de menus, clique em **variáveis**.  
  
6.  No **variáveis** janela, clique em **Adicionar variável** na barra de ferramentas.  
  
     ![Janela de variáveis do SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "janela variáveis do SSIS")  
  
7.  Tipo de **ImportType** para o **nome** e **2** para o **valor**. Você especifica o valor como 2 porque deseja adicionar novos membros a uma entidade no MDS. Para obter detalhes sobre esse parâmetro, consulte [tabela de preparo de membros folha](../master-data-services/leaf-member-staging-table-master-data-services.md).  
  
8.  Clique em **Adicionar variável** botão da barra de ferramentas novamente.  
  
9. Tipo de **BatchTag** para o **nome**, selecione **cadeia de caracteres** para o **tipo de dados**, e **EIMBatch** para o **Valor**. **BatchTag** é apenas um nome exclusivo para o lote que você enviará ao MDS.  
  
10. No **fluxo de dados** guia, clique duas vezes **adicionar colunas exigidas pelo MDS**.  
  
11. No **Editor de transformação coluna derivada** na caixa de **caixa de listagem no painel inferior**, tipo **ImportType** para o **nome da coluna derivada**.  
  
12. Expandir **variáveis e parâmetros** no painel superior esquerdo, arraste e solte **User:: importType** para o **expressão** coluna.  
  
     ![Derivado de Editor de transformação de coluna](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "derivado do Editor de transformação de coluna")  
  
13. Tipo de **BatchTag** na linha seguinte para o **nome da coluna derivada**.  
  
14. Arrastar e soltar **User:: batchtag** partir **variáveis e parâmetros** para o **expressão** coluna.  
  
15. Clique em **Okey** para fechar o **transformação coluna derivada** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 13: Adicionando o destino do OLE DB para gravar dados em tabela de preparo do MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
