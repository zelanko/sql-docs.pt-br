---
title: 'Tarefa 13: adicionando OLE DB destino para gravar dados na tabela de preparo do MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bb39e9d50d135adfedcf307cda2ad703e302eda5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061136"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>Tarefa 13: Adicionando o destino OLE DB para gravar dados na tabela de preparo do MDS
  Agora que você adicionou valores **importType** e **BatchTag** a todos os registros, você está pronto para enviá-los para o MDS para preparo. Nesta tarefa, você usa o destino OLE DB para gravar os dados em **STG. supplier_Leaf** tabela de preparo.  
  
1.  Arraste **OLE DB destino** de **outros destinos** seção na **caixa de ferramentas do SSIS** para a guia fluxo de **dados** e solte-o em **adicionar colunas exigidas pelo MDS**.  
  
2.  Clique com o botão direito do mouse **OLE DB destino** na guia **fluxo de dados** e clique em **renomear**. Digite **gravar dados do fornecedor na tabela de preparo do MDS** e pressione **Enter**.  
  
3.  Conecte as **colunas de adição exigidas pelo MDS** para **gravar dados de fornecedor na tabela de preparo do MDS** usando o conector azul.  
  
4.  Clique duas vezes em **gravar dados do fornecedor na tabela de preparo do MDS** na guia fluxo de **dados** .  
  
5.  Na caixa de diálogo **Editor de destino OLE DB** , verifique se **(local). MDS** (ou **localhost. MDS**) está selecionado para o campo **OLE DB Gerenciador de conexões** .  
  
6.  Selecione **STG. Supplier_Leaf** tabela na lista de **nome da tabela ou exibição**.  
  
     ![Editor de Destino de OLEDB](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "Editor de Destino de OLEDB")  
  
7.  Alterne para a página **mapeamentos** clicando em **mapeamento** no menu à esquerda.  
  
8.  Mapeie as colunas de **entrada** e de **destino** , conforme mostrado na tabela a seguir.  
  
     ![Editor de Destino OLEDB - Mapeamentos](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "Editor de Destino OLEDB - Mapeamentos")  
  
9. Confirme se você está usando colunas **_Output** para colunas de entrada, não as colunas **_Status** ou **_Source** . **_Output** colunas contêm os valores de saída da limpeza DQS.  
  
10. Clique em **OK** para fechar a caixa de diálogo **OLE DB editor de destino** .  
  
11. O fluxo de dados deve ter a aparência da imagem a seguir.  
  
     ![Fluxo de dados concluído](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "Fluxo de dados concluído")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 14: Adicionando a tarefa Executar SQL ao fluxo de controle para executar o procedimento armazenado para MDS](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
