---
title: Propriedades do SQL Server Integration Services (guia Serviço) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 37f0acd9-c96f-48fd-9b53-2ca0097af242
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4cb1b821604d125bc81148a06fb613c8547a449
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68186713"
---
# <a name="sql-server-integration-services-properties-service-tab"></a>Propriedades do SQL Server Integration Services (guia Serviço)
  Use a guia **Serviço**na caixa de diálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] **do** para exibir ou especificar as opções a seguir.  
  
## <a name="options"></a>Opções  
 **Caminho binário**  
 Exibe o local dos arquivos de programas usados por este serviço.  
  
 **Controle de erro**  
 1 indica `SERVICE_ERROR_NORMAL`. Se o serviço não for iniciado durante a inicialização do computador, o programa de inicialização registrará o erro em log e exibirá uma caixa de mensagem pop-up, mas continuará a operação de inicialização. Esse valor não pode ser alterado.  
  
 **Código de saída**  
 O código de erro do Windows no [!INCLUDE[msCoName](../../includes/msconame-md.md)] que define todos os problemas encontrados na inicialização ou interrupção do serviço. Esta propriedade é definida como **ERROR_SERVICE_SPECIFIC_ERROR** (1066) quando o erro é exclusivo do serviço representado por essa classe, e as informações sobre o erro estão disponíveis na propriedade **ServiceSpecificExitCode** . O serviço define esse valor como NO_ERROR (0) quando está sendo executado, e novamente no término normal.  
  
 **Nome do host**  
 Exibe o nome do computador ou cluster que está executando o serviço [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Nome**  
 Indica o nome para exibição do serviço.  
  
 **ID do Processo**  
 Exibe a identificação do processo do Windows.  
  
 **Tipo de serviço do SQL**  
 Exibe o tipo de serviço fornecido a processos de chamada. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala vários serviços.  
  
 **Modo de início**  
 Defina este serviço com as seguintes opções:  
  
-   Manual: este serviço não é iniciado automaticamente na inicialização do computador. Você deve iniciá-lo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou outra ferramenta.  
  
-   Automático: este serviço tenta ser iniciado na inicialização do computador.  
  
-   Desabilitado: este serviço não pode ser iniciado.  
  
 **Estado**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado. "**...**" indica que há uma alteração de estado pendente.  
  
  
