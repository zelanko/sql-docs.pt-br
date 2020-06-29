---
title: Acionar eventos no componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], raising events
ms.assetid: bb389073-e1d0-4794-8d29-c8b293b6a5e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 88cbe69d39ffd0d76ea0a14f185ce537595fa57d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426123"
---
# <a name="raising-events-in-the-script-component"></a>Gerando eventos no componente Script
  Os eventos fornecem um modo de relatar erros, avisos e outras informações, como o progresso ou status da tarefa, ao pacote que os contém. O pacote fornece manipuladores de eventos para gerenciar notificações de eventos. O componente Script pode gerar eventos chamando métodos na propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> da classe `ScriptMain`. Para obter mais informações sobre como pacotes [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] manipulam eventos, consulte [Manipuladores de Eventos do SSIS &#40;Integration Services&#41;](../../integration-services-ssis-event-handlers.md).  
  
 Os eventos podem ser registrados em qualquer provedor de log que esteja habilitado no pacote. Provedores de logs armazenam informações sobre eventos em um repositório de dados. O componente Script também pode usar o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> para registrar informações para um provedor de log sem gerar um evento. Para obter mais informações sobre como usar o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>, consulte a seção seguinte.  
  
 Para gerar um evento, a tarefa Script chama um dos métodos seguintes da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> expostos pela propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>:  
  
|Evento|DESCRIÇÃO|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>|Gera um evento personalizado definido pelo usuário no pacote.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>|Informa o pacote sobre uma condição de erro.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A>|Fornece informações ao usuário.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireProgress%2A>|Informa o pacote sobre o progresso do componente.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A>|Informa o pacote que o componente está em um estado que garante a notificação do usuário, mas não é uma condição de erro.|  
  
 Eis um exemplo simples de geração de um evento de erro:  
  
 `Dim myMetadata as IDTSComponentMetaData100`  
  
 `myMetaData = Me.ComponentMetaData`  
  
 `myMetaData.FireError(...)`  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services &#40;os manipuladores de eventos&#41; SSIS](../../integration-services-ssis-event-handlers.md)   
 [Adicionar um manipulador de eventos a um pacote](../../add-an-event-handler-to-a-package.md)  
  
  
