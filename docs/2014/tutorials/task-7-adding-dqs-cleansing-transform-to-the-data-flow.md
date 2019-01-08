---
title: 'Tarefa 7: Adicionando a transformação ao fluxo de dados de limpeza DQS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eaa36e392046abca935a1b67c4ee459a8b15939e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376868"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>Tarefa 7: Adicionando a Transformação Limpeza DQS ao fluxo de dados
  Nesta tarefa, você adiciona a Transformação de Limpeza DQS ao fluxo de dados para limpar os dados do fornecedor de entrada usando o DQS. Ver **[transformação de limpeza DQS](https://msdn.microsoft.com/library/ee677619.aspx)** para obter mais detalhes sobre a transformação.  
  
1.  Clique com botão direito **limpeza DQS** na **fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo de **limpar dados do fornecedor**e pressione **ENTER**.  
  
2.  Selecione **ler dados do fornecedor de arquivo do Excel**; arraste o conector azul para **limpar dados do fornecedor**. Os componentes estão conectados agora.  
  
     ![Ler dados do fornecedor -> Limpar dados do fornecedor](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "ler dados do fornecedor -> Limpar dados do fornecedor")  
  
3.  Clique duas vezes em **limpar dados do fornecedor**.  
  
4.  No **Editor de transformação de limpeza DQS**, clique em **New** lado de **Gerenciador de Conexão de qualidade de dados na lista suspensa**.  
  
5.  No **Gerenciador de Conexão de limpeza DQS** caixa de diálogo, digite **(local)** ou **período** (.) para se conectar ao servidor local. Esta lição supõe que você tenha o DQS instalado em um servidor local.  
  
6.  Clique em **Testar Conexão** para testar a conexão ao servidor DQS.  
  
7.  Clique em **OK** para fechar a caixa de diálogo.  
  
8.  Selecione **fornecedores** para o **Base de dados de Conhecimento de qualidade de dados**.  
  
     ![Editor de transformação - KB de fornecedores de limpeza DQS](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "Editor de transformação - KB de fornecedores de limpeza DQS")  
  
9. Alterne para o **mapeamento** guia na parte superior.  
  
10. Partir **colunas de entrada disponíveis**, selecione **Supplier Name**, **ContactEmailAddress**, **Address Line**, **Cidade**, **Estado**, **país**, e **CEP** marcando as caixas de seleção.  
  
     ![Editor de transformação - mapeamentos de limpeza DQS](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "Editor de transformação - mapeamentos de limpeza DQS.")  
  
11. No painel inferior, mapeie essas colunas usando listas suspensas na **domínio** coluna:  
  
    |coluna|Domínio|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Email de contato|  
    |Linha de Endereço|Linha de Endereço|  
    |Cidade|Cidade|  
    |Estado|Estado|  
    |País|País|  
    |Zip Code|CEP|  
  
12. Clique em **Okey** para fechar o **Editor de transformação de limpeza DQS** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 8: Adicionando a transformação divisão condicional para dividir a saída de limpeza](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
