---
title: 'Tarefa 2: mapeando colunas do Excel para domínios do DQS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 646204e2c40c09ac0fac9259f5acc43c7f422894
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006652"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>Tarefa 2: Mapeando colunas do Excel para domínios do DQS
    
1.  Na página **Mapear** , selecione **Arquivo do Excel** em **Fonte de Dados**.  
  
2.  Clique em **procurar**, selecione **Suppliers.xlsx**e clique em **abrir**.  
  
3.  Selecione **IncomingSuppliers $** para a **planilha**.  
  
4.  Mapeie as colunas conforme mostrado na tabela e na captura de tela a seguir. Ao criar mapeamentos para o domínio de **estado** , clique no botão **Adicionar um mapeamento de coluna** na barra de ferramentas localizada logo acima da lista.  
  
    > [!TIP]  
    >  Você não está usando a coluna/domínio da **ID do fornecedor** para limpeza. Você usará o domínio da **ID do fornecedor** mais tarde na atividade de correspondência.  
  
    |Coluna do Excel|Domínio do DQS|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Email de contato|  
    |Linha de Endereço|Linha de Endereço|  
    |City|City|  
    |Estado|Estado|  
    |País (clique na barra de ferramentas **(adicionar um mapeamento de coluna)** para adicionar uma linha)|País|  
    |Zip Code|Zip|  
  
     ![Mapeamentos de colunas do Excel para Domínios](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Mapeamentos de colunas do Excel para Domínios")  
  
5.  Como você mapeou todos os domínios individuais dentro do domínio composto de **validação de endereço** , o domínio composto participa automaticamente do processo de limpeza. Clique no botão **Exibir/selecionar domínios compostos** para ver se o domínio composto de **validação de endereço** está selecionado automaticamente e clique em **OK**.  
  
     ![Caixa de diálogo Exibir/Selecionar Domínios Compostos](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "Caixa de diálogo Exibir/Selecionar Domínios Compostos")  
  
6.  Clique em **Avançar** para alternar para a página **limpar** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 3: Limpando dados em relação à base de dados de conhecimento de fornecedores](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
