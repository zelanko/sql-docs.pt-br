---
title: Registro em log no componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 68aa22052d1dc499fbee5c7ebfb04923eff8a097
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426253"
---
# <a name="logging-in-the-script-component"></a>Registrando o componente Script
  O registro de pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite que você salve informações detalhadas sobre o progresso da execução, resultados e problemas, por meio do registro de eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. O componente Script pode usar a classe <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método da `ScriptMain` para registrar dados definidos pelo usuário. Se o registro em log estiver habilitado e o evento **ScriptComponentLogEntry** estiver selecionado para o registro em log na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS**, uma única chamada ao método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> armazenará informações do evento em todos os provedores de logs configurados para a tarefa de fluxo de dados.  
  
 Este é um exemplo simples de registro em log:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Embora seja possível executar o registro em log diretamente do componente Script, talvez você queira implementar eventos em vez de registrá-los. Ao usar eventos, você pode habilitar o registro de mensagens de evento e também responder ao evento com manipuladores de eventos padrão ou definidos pelo usuário.  
  
 Para obter mais informações sobre registro em log, consulte [Log do SSIS &#40;Integration Services&#41;](../../performance/integration-services-ssis-logging.md).  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do SSIS &#40;Integration Services&#41;](../../performance/integration-services-ssis-logging.md)  
  
  
