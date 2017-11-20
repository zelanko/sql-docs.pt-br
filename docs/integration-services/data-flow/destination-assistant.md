---
title: O Assistente de destino | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aebe1dfa1046bddfa86e48aecdd68930caf3285c
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="destination-assistant"></a>Assistente de Destino
  O componente Assistente de Destino ajuda a criar um componente de destino e um gerenciador de conexões. O componente está localizado na seção **Favoritos** da Caixa de Ferramentas do SSIS.  
  
> [!NOTE]  
>  O Assistente de Destino substitui o projeto de Conexões do Integration Services e o assistente correspondente.  

## <a name="add-a-destination-with-destination-assistant"></a>Adicionar um destino com o Assistente de destino
Este tópico fornece etapas para adicionar um novo destino por meio do Assistente de Destino e também lista as opções que estão disponíveis na caixa de diálogo **Adicionar Novo Destino** que você verá ao arrastar-soltar o Assistente de Destino para o Designer SSIS.  

1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ao qual você deseja adicionar um componente de destino.  
  
2.  Arraste o componente **Assistente de Destino** da Caixa de Ferramentas do SSIS para a guia **Fluxo de Dados** . Você deve ver a caixa de diálogo **Adicionar Novo Destino** . A próxima seção fornece detalhes sobre as opções disponíveis na caixa de diálogo.  
  
3.  Selecione o tipo do destino na lista **Tipos**.  
  
4.  Selecione um Gerenciador de conexão existente no **gerenciadores de Conexão** lista ou selecione  **\<Novo >** para criar uma nova conexão Gerenciador.  
  
5.  Se você selecionar um gerenciador de conexões existente, clique em **OK** para fechar a caixa de diálogo **Adicionar Novo Destino**. Você deve ver o destino e os gerenciadores de conexões adicionados ao fluxo de dados.  
  
6.  Se você clicar em  **\<Novo >** para criar uma nova conexão Gerenciador, você verá um **Gerenciador de Conexão** caixa de diálogo que permite que você especifique parâmetros para a conexão. Depois de concluir a criação do novo gerenciador de conexões, você verá o destino e o gerenciador de conexões no Designer SSIS. 
  
## <a name="add-new-destination-dialog-box"></a>Adicionar caixa de diálogo Novo destino
A tabela a seguir lista as opções disponíveis sobre o **adicionar novo destino** caixa de diálogo.  
  
|Opção|Description|  
|------------|-----------------|  
|Types|Selecione o tipo de destino ao qual você deseja conectar-se.|  
|Gerenciadores de conexões|Selecione um Gerenciador de conexão existente ou clique em  **\<Novo >** para criar uma nova conexão Gerenciador.|  
|Mostrar somente itens instalados|Especifique se apenas destinos instalados devem ser exibidos.|  
|OK|Clique para salvar suas alterações e abrir uma caixa de diálogo subsequente para configurar opções adicionais.|  

