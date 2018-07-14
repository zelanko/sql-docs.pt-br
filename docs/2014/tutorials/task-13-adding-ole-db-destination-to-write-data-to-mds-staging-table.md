---
title: 'Tarefa 13: Adicionando um destino de OLE DB para gravar dados em tabela de preparo do MDS | Microsoft Docs'
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
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc0bd3ad05ec740299e0cb06def5a439fa87da9c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234276"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>Tarefa 13: Adicionando o destino OLE DB para gravar dados na tabela de preparo do MDS
  Agora que você adicionou **ImportType** e **BatchTag** valores para todos os registros, você está pronto para enviá-los pelo MDS para preparação. Nesta tarefa, você deve usar o destino OLE DB para gravar os dados na **supplier_leaf** tabela de preparo.  
  
1.  Arraste **destino OLE DB** de **outros destinos** seção o **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia e solte-o sob  **Adicionar colunas exigidas pelo MDS**.  
  
2.  Clique com botão direito **destino OLE DB** na **fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo de **gravar dados do fornecedor para a tabela de preparo do MDS** e pressione **ENTER**.  
  
3.  Conectar-se a **adicionar colunas exigidas pelo MDS** à **gravar dados do fornecedor para a tabela de preparo do MDS** usando o conector azul.  
  
4.  Clique duas vezes em **gravar dados do fornecedor para a tabela de preparo do MDS** na **fluxo de dados** guia.  
  
5.  No **Editor de destino do OLE DB** diálogo caixa, certifique-se de que **(local). MDS** (ou **localhost. MDS**) é selecionado para o **Gerenciador de Conexão do OLE DB** campo.  
  
6.  Selecione **STG. Supplier_Leaf** tabela da lista de **nome da tabela ou exibição**.  
  
     ![Editor de destino de OLEDB](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "Editor de destino de OLE DB")  
  
7.  Alterne para o **mapeamentos** página clicando **mapeamento** no menu à esquerda.  
  
8.  Mapa **entrada** e **destino** colunas, conforme mostrado na tabela a seguir.  
  
     ![Editor de destino OLEDB - mapeamentos](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "Editor de destino OLEDB - mapeamentos")  
  
9. Confirme que você está usando **_Output** colunas de entrada, não a **_Status** ou **_Source** colunas. **Saída** colunas contêm os valores de saída da limpeza DQS.  
  
10. Clique em **Okey** para fechar o **Editor de destino do OLE DB** caixa de diálogo.  
  
11. O fluxo de dados deve ter a aparência da imagem a seguir.  
  
     ![Concluir o fluxo de dados](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "concluir o fluxo de dados")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 14: Adicionando a tarefa Executar SQL ao fluxo de controle para executar o procedimento armazenado para MDS](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
