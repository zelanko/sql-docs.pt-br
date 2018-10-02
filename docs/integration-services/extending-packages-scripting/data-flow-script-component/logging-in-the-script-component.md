---
title: Registro em log no componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a45bb6728637d087063d4e90c51734396e98c06
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785904"
---
# <a name="logging-in-the-script-component"></a>Registrando o componente Script
  O registro de pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite que você salve informações detalhadas sobre o progresso da execução, resultados e problemas, por meio do registro de eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. O componente Script pode usar o método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> da classe **ScriptMain** para registrar dados definidos pelo usuário. Se o registro em log estiver habilitado e o evento **ScriptComponentLogEntry** estiver selecionado para o registro em log na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS**, uma única chamada ao método <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> armazenará informações do evento em todos os provedores de logs configurados para a tarefa de fluxo de dados.  
  
 Este é um exemplo simples de registro em log:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Embora seja possível executar o registro em log diretamente do componente Script, talvez você queira implementar eventos em vez de registrá-los. Ao usar eventos, você pode habilitar o registro de mensagens de evento e também responder ao evento com manipuladores de eventos padrão ou definidos pelo usuário.  
  
 Para obter mais informações sobre registro em log, consulte [Log do SSIS &#40;Integration Services&#41;](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do SSIS &#40;Integration Services&#41;](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
