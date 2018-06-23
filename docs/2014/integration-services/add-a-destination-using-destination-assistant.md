---
title: Adicionar um destino usando o Assistente de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 88d942ea38004d6d4085b73a4f2967a9a2e68705
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120414"
---
# <a name="add-a-destination-using-destination-assistant"></a>Adicionar um destino por meio do Assistente de Destino
  Este tópico fornece etapas para adicionar um novo destino por meio do Assistente de Destino e também lista as opções que estão disponíveis na caixa de diálogo **Adicionar Novo Destino** que você verá ao arrastar-soltar o Assistente de Destino para o Designer SSIS.  
  
### <a name="to-use-destination-assistant-to-add-a-destination"></a>Para usar o Assistente de Destino para adicionar um destino  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ao qual você deseja adicionar um componente de destino.  
  
2.  Arraste o componente **Assistente de Destino** da Caixa de Ferramentas do SSIS para a guia **Fluxo de Dados** . Você deve ver a caixa de diálogo **Adicionar Novo Destino** . A próxima seção fornece detalhes sobre as opções disponíveis na caixa de diálogo.  
  
3.  Selecione o tipo do destino na lista **Tipos**.  
  
4.  Selecione um gerenciador de conexões na lista **Gerenciadores de Conexões** ou selecione **\<Novo>** para criar um novo gerenciador de conexões.  
  
5.  Se você selecionar um gerenciador de conexões existente, clique em **OK** para fechar a caixa de diálogo **Adicionar Novo Destino**. Você deve ver o destino e os gerenciadores de conexões adicionados ao fluxo de dados.  
  
6.  Se você clicar em **\<Novo>** para criar um novo gerenciador de conexões, deverá ver uma caixa de diálogo **Gerenciador de Conexões** que permitirá especificar parâmetros para a conexão. Depois de concluir a criação do novo gerenciador de conexões, você verá o destino e o gerenciador de conexões no Designer SSIS.  
  
  