---
title: Conectar componentes em um fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 90d3e9e50ef16e51e9669a92cfb53f5f734c83ef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827921"
---
# <a name="connect-components-in-a-data-flow"></a>Conectar componentes em um fluxo de dados
  Este procedimento descreve como conectar a saída dos componentes em um fluxo de dados para outros componentes dentro do mesmo fluxo de dados.  
  
### <a name="to-connect-components-in-a-data-flow"></a>Para conectar os componentes em um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados no qual você deseja conectar componentes.  
  
4.  Na superfície de design da guia **Fluxo de Dados** , selecione a transformação ou fonte que você quer conectar.  
  
5.  Arraste a seta de saída verde de uma transformação ou uma fonte para uma transformação ou para um destino. Alguns componentes de fluxo de dados têm saídas de erro, que você pode conectar da mesma maneira.  
  
    > [!NOTE]  
    >  Alguns componentes de fluxo de dados podem ter múltiplas saídas, sendo possível conectar cada saída para uma transformação ou destino diferentes.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar ou excluir um componente em um fluxo de dados](data-flow.md)   
 [Configurar uma saída de erro em um componente de fluxo de dados](../configure-an-error-output-in-a-data-flow-component.md)   
 [Fluxo de Dados](data-flow.md)  
  
  
