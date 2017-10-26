---
title: Assistente de origem | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9b7406edf9f7234db739730473772d77c42399ec
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="source-assistant"></a>Assistente de origem
  O componente Assistente de Origem ajuda a criar um componente de origem e um gerenciador de conexões. O componente está localizado na seção **Favoritos** da Caixa de Ferramentas do SSIS.  
  
> [!NOTE]  
>  O Assistente de Origem substitui o projeto de Conexões do Integration Services e o assistente correspondente.  
  
## <a name="add-a-source-with-source-assistant"></a>Adicionar uma fonte com o Assistente de fonte
Esta seção fornece as etapas para adicionar uma nova fonte usando o Assistente de origem e também lista as opções que estão disponíveis no **adicionar nova fonte** caixa de diálogo, o que você verá ao arrastar-soltar o Assistente de origem para o Designer SSIS.  

1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ao qual você deseja adicionar um componente de origem.  
  
2.  Arraste o componente **Assistente de Origem** da Caixa de Ferramentas do SSIS para a guia **Fluxo de Dados** . Você deveria ver a caixa de diálogo **Adicionar Nova Origem** . A próxima seção fornece detalhes sobre as opções disponíveis na caixa de diálogo.  
  
3.  Selecione o tipo do destino na lista **Tipos**.  
  
4.  Selecione um Gerenciador de conexão existente no **gerenciadores de Conexão** lista ou selecione  **\<Novo >** para criar uma nova conexão Gerenciador.  
  
5.  Se você selecionar um gerenciador de conexões existente, clique em **OK** para fechar a caixa de diálogo **Adicionar Novo Destino**. Você deve ver o destino e os gerenciadores de conexões adicionados ao fluxo de dados.  
  
6.  Se você clicar em  **\<Novo >** para criar uma nova conexão Gerenciador, você verá um **Gerenciador de Conexão** caixa de diálogo que permite que você especifique parâmetros para a conexão. Depois de concluir a criação do novo gerenciador de conexões, você verá o destino e o gerenciador de conexões no Designer SSIS.  

## <a name="add-new-source-dialog-box"></a>Adicionar caixa de diálogo nova origem
A tabela a seguir lista as opções disponíveis no **adicionar nova fonte** caixa de diálogo.  
  
|Opção|Description|  
|------------|-----------------|  
|Types|Selecione o tipo de origem ao qual você deseja conectar-se.|  
|Gerenciadores de conexões|Selecione um Gerenciador de conexão existente ou clique em  **\<Novo >** para criar uma nova conexão Gerenciador.|  
|Mostrar somente itens instalados|Especifique se apenas origens instaladas devem ser exibidas.|  
|OK|Clique para salvar suas alterações e abrir uma caixa de diálogo subsequente para configurar opções adicionais.| 
  

