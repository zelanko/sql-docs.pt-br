---
title: Registro em log no componente Script | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a2472399574753d67a44b93437b1698c8b086
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-component"></a>Registrando o componente Script
  O registro de pacotes do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite que você salve informações detalhadas sobre o progresso da execução, resultados e problemas, por meio do registro de eventos predefinidos ou mensagens definidas pelo usuário para análise posterior. O componente Script pode usar o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método o **ScriptMain** classe para registrar dados definidos pelo usuário. Se o log estiver habilitado e o **ScriptComponentLogEntry** evento é selecionado para o logon de **detalhes** guia do **configurar Logs de SSIS** caixa de diálogo, uma única chamada para o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> método armazena as informações de evento em todos os provedores de log que foram configurados para a tarefa de fluxo de dados.  
  
 Este é um exemplo simples de registro em log:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Embora seja possível executar o registro em log diretamente do componente Script, talvez você queira implementar eventos em vez de registrá-los. Ao usar eventos, você pode habilitar o registro de mensagens de evento e também responder ao evento com manipuladores de eventos padrão ou definidos pelo usuário.  
  
 Para obter mais informações sobre registro em log, consulte [Integration Services &#40; SSIS &#41; Registro em log](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Registro em log](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

