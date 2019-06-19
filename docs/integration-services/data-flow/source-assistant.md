---
title: Assistente de Origem | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 93bbfcc8b76fe6fe1028b5b13395e0a88a6b359a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726359"
---
# <a name="source-assistant"></a>Assistente de origem

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O componente Assistente de Origem ajuda a criar um componente de origem e um gerenciador de conexões. O componente está localizado na seção **Favoritos** da Caixa de Ferramentas do SSIS.  
  
> [!NOTE]  
>  O Assistente de Origem substitui o projeto de Conexões do Integration Services e o assistente correspondente.  
  
## <a name="add-a-source-with-source-assistant"></a>Adicionar uma origem com o Assistente de Origem
Esta seção fornece etapas para adicionar uma nova origem por meio do Assistente de Origem e também lista as opções que estão disponíveis na caixa de diálogo **Adicionar Nova Origem** que você verá ao arrastar-soltar o Assistente de Origem para o Designer SSIS.  

1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ao qual você deseja adicionar um componente de origem.  
  
2.  Arraste o componente **Assistente de Origem** da Caixa de Ferramentas do SSIS para a guia **Fluxo de Dados** . Você deveria ver a caixa de diálogo **Adicionar Nova Origem** . A próxima seção fornece detalhes sobre as opções disponíveis na caixa de diálogo.  
  
3.  Selecione o tipo do destino na lista **Tipos**.  
  
4.  Selecione um gerenciador de conexões na lista **Gerenciadores de Conexões** ou selecione **\<Novo>** para criar um novo gerenciador de conexões.  
  
5.  Se você selecionar um gerenciador de conexões existente, clique em **OK** para fechar a caixa de diálogo **Adicionar Novo Destino**. Você deve ver o destino e os gerenciadores de conexões adicionados ao fluxo de dados.  
  
6.  Se você clicar em **\<Novo>** para criar um novo gerenciador de conexões, deverá ver uma caixa de diálogo **Gerenciador de Conexões** que permitirá especificar parâmetros para a conexão. Depois de concluir a criação do novo gerenciador de conexões, você verá o destino e o gerenciador de conexões no Designer SSIS.  

## <a name="add-new-source-dialog-box"></a>Caixa de diálogo Adicionar Nova Origem
A tabela a seguir lista as opções disponíveis na caixa de diálogo **Adicionar Nova Origem**.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Types|Selecione o tipo de origem ao qual você deseja conectar-se.|  
|Gerenciadores de conexões|Selecione um gerenciador de conexões existente ou clique em **\<Novo>** para criar um novo gerenciador de conexões.|  
|Mostrar somente itens instalados|Especifique se apenas origens instaladas devem ser exibidas.|  
|OK|Clique para salvar suas alterações e abrir uma caixa de diálogo subsequente para configurar opções adicionais.| 
  
