---
title: 'Tarefa 7: adicionando a transformação de limpeza DQS ao fluxo de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0978452104eb9a55d49dfa9f851ef7578489db26
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006480"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>Tarefa 7: Adicionando a Transformação de Limpeza DQS ao fluxo de dados
  Nesta tarefa, você adiciona a Transformação de Limpeza DQS ao fluxo de dados para limpar os dados do fornecedor de entrada usando o DQS. Consulte **[transformação de limpeza DQS](https://msdn.microsoft.com/library/ee677619.aspx)** para obter mais detalhes sobre a transformação.  
  
1.  Clique com o botão direito do mouse em **limpeza DQS** na guia **fluxo de dados** e clique em **renomear**. Digite **limpar dados do fornecedor**e pressione **Enter**.  
  
2.  Selecione **ler dados do fornecedor do arquivo do Excel**; Arraste o conector azul para **limpar os dados do fornecedor**. Os componentes estão conectados agora.  
  
     ![Ler dados do fornecedor-> limpar dados do fornecedor](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "Ler Dados de Fornecedor -> Limpar Dados de Fornecedor")  
  
3.  Clique duas vezes em **limpar dados do fornecedor**.  
  
4.  No **Editor de transformação de limpeza DQS**, clique em **novo** ao lado da **lista suspensa Gerenciador de conexões de qualidade de dados**.  
  
5.  Na caixa de diálogo **Gerenciador de conexões de limpeza DQS** , digite **(local)** ou **ponto** (.) para se conectar ao servidor local. Esta lição supõe que você tenha o DQS instalado em um servidor local.  
  
6.  Clique em **testar conexão** para testar a conexão com o servidor DQS.  
  
7.  Clique em **OK** para fechar a caixa de diálogo.  
  
8.  Selecione os **fornecedores** para a **base de dados de conhecimento de qualidade**.  
  
     ![Caixa de diálogo Editor de Transformação de Limpeza DQS - KB de Fornecedores](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "Caixa de diálogo Editor de Transformação de Limpeza DQS - KB de Fornecedores")  
  
9. Alterne para a guia **mapeamento** na parte superior.  
  
10. Nas **colunas de entrada disponíveis**, selecione **nome do fornecedor**, **ContactEmailAddress**, **linha de endereço**, **cidade**, **estado**, **país**e **CEP** marcando as caixas de seleção.  
  
     ![Editor de Transformação de Limpeza DQS - Mapeamentos](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "Editor de Transformação de Limpeza DQS - Mapeamentos")  
  
11. No painel inferior, mapeie essas colunas usando listas suspensas na coluna **domínio** :  
  
    |Coluna|Domínio|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Email de contato|  
    |Linha de Endereço|Linha de Endereço|  
    |City|City|  
    |Estado|Estado|  
    |País|País|  
    |Zip Code|Zip|  
  
12. Clique em **OK** para fechar a caixa de diálogo **Editor de transformação de limpeza DQS** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 8: Adicionando a Transformação Divisão Condicional para dividir a saída da limpeza](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
