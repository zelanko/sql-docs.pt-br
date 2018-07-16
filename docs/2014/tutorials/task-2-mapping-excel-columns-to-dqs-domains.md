---
title: 'Tarefa 2: Mapeando colunas do Excel para domínios do DQS | Microsoft Docs'
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
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 89be07ed1cdd07fc8cd923d9672147b87a165d71
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202026"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>Tarefa 2: Mapeando colunas do Excel para domínios do DQS
    
1.  Na página **Mapear** , selecione **Arquivo do Excel** em **Fonte de Dados**.  
  
2.  Clique em **navegue**, selecione **Suppliers**e clique em **abrir**.  
  
3.  Selecione **IncomingSuppliers$** para o **planilha**.  
  
4.  Mapeie as colunas conforme mostrado na tabela e na captura de tela a seguir. Ao criar mapeamentos para o **estado** domínio, clique em **adicionar um mapeamento de coluna** na barra de ferramentas localizada imediatamente acima da lista.  
  
    > [!TIP]  
    >  Você não estiver usando **Supplier ID** coluna/domínio para limpeza. Você usará o **Supplier ID** domínio posteriormente na atividade de correspondência.  
  
    |Coluna do Excel|Domínio do DQS|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Email de contato|  
    |Linha de Endereço|Linha de Endereço|  
    |Cidade|Cidade|  
    |Estado|Estado|  
    |País (clique em **+ (Adicionar um mapeamento de coluna)** barra de ferramentas para adicionar uma linha)|País|  
    |Zip Code|CEP|  
  
     ![Mapeamentos de colunas do Excel para domínios](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "mapeamentos de colunas do Excel para domínios")  
  
5.  Como você mapeou todos os domínios individuais dentro de **Address Validation** domínio composto, o domínio composto participa automaticamente o processo de limpeza. Clique em **exibir/Selecionar domínios compostos** botão para ver que o **validação de endereço** domínio composto é selecionada automaticamente e, em seguida, clique em **Okey**.  
  
     ![Caixa de diálogo Exibir/Selecionar domínios compostos](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "caixa de diálogo Exibir/Selecionar domínios compostos")  
  
6.  Clique em **próxima** para alternar para o **limpar** página.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3: Limpando dados em relação à base de dados de conhecimento de fornecedores](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
