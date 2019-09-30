---
title: Assistente de Destino | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f302227746b0479f096fbfc29e50c328b61f114
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292908"
---
# <a name="destination-assistant"></a>Assistente de Destino

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O componente Assistente de Destino ajuda a criar um componente de destino e um gerenciador de conexões. O componente está localizado na seção **Favoritos** da Caixa de Ferramentas do SSIS.  
  
> [!NOTE]  
>  O Assistente de Destino substitui o projeto de Conexões do Integration Services e o assistente correspondente.  

## <a name="add-a-destination-with-destination-assistant"></a>Adicionar um destino com o Assistente de Destino
Este tópico fornece etapas para adicionar um novo destino por meio do Assistente de Destino e também lista as opções que estão disponíveis na caixa de diálogo **Adicionar Novo Destino** que você verá ao arrastar-soltar o Assistente de Destino para o Designer SSIS.  

1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ao qual você deseja adicionar um componente de destino.  
  
2.  Arraste o componente **Assistente de Destino** da Caixa de Ferramentas do SSIS para a guia **Fluxo de Dados** . Você deve ver a caixa de diálogo **Adicionar Novo Destino** . A próxima seção fornece detalhes sobre as opções disponíveis na caixa de diálogo.  
  
3.  Selecione o tipo do destino na lista **Tipos**.  
  
4.  Selecione um gerenciador de conexões na lista **Gerenciadores de Conexões** ou selecione **\<Novo>** para criar um novo gerenciador de conexões.  
  
5.  Se você selecionar um gerenciador de conexões existente, clique em **OK** para fechar a caixa de diálogo **Adicionar Novo Destino**. Você deve ver o destino e os gerenciadores de conexões adicionados ao fluxo de dados.  
  
6.  Se você clicar em **\<Novo>** para criar um novo gerenciador de conexões, deverá ver uma caixa de diálogo **Gerenciador de Conexões** que permitirá especificar parâmetros para a conexão. Depois de concluir a criação do novo gerenciador de conexões, você verá o destino e o gerenciador de conexões no Designer SSIS. 
  
## <a name="add-new-destination-dialog-box"></a>Caixa de diálogo Adicionar Novo Destino
A tabela a seguir lista as opções disponíveis na caixa de diálogo **Adicionar Novo Destino**.  
  
|Opção|Descrição|  
|------------|-----------------|  
|Types|Selecione o tipo de destino ao qual você deseja conectar-se.|  
|Gerenciadores de conexões|Selecione um gerenciador de conexões existente ou clique em **\<Novo>** para criar um novo gerenciador de conexões.|  
|Mostrar somente itens instalados|Especifique se apenas destinos instalados devem ser exibidos.|  
|OK|Clique para salvar suas alterações e abrir uma caixa de diálogo subsequente para configurar opções adicionais.|  
