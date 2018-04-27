---
title: Propriedades do navegador do SQL Server (guia serviço) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98ace9b0-72d5-4b72-9b7b-11fbc490981a
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af140523d7521dd5731f8bc167d02391f6f68d1e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-browser-properties-service-tab"></a>Propriedades do Navegador do SQL Server (guia Serviço)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  O programa Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado como um serviço no servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta as solicitações de entrada de recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
 Use a guia **Serviço** na caixa de diálogo **Propriedades do Navegador do SQL Server** para exibir as opções a seguir. Todas as propriedades, exceto **Modo Inicial** , são somente leitura.  
  
## <a name="options"></a>Opções  
 **Caminho Binário**  
 Exibe o local dos arquivos de programas usados por este serviço.  
  
 **Controle de Erro**  
 1 indica `SERVICE_ERROR_NORMAL`. Se o serviço não for iniciado durante a inicialização do computador, o programa de inicialização registrará o erro em log e exibirá uma caixa de mensagem pop-up, mas continuará a operação de inicialização. Esse valor não pode ser alterado.  
  
 **Código de Saída**  
 Quando ocorre um erro, o número do erro é exibido nesta caixa. Use esse número para solucionar problemas de falhas procurando-o na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou forneça o número à sua equipe de suporte técnico.  
  
 **Nome do Host**  
 Exibe o nome do computador ou do cluster que está executando o serviço do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Nome**  
 Indica o nome para exibição do serviço.  
  
 **ID do Processo**  
 Exibe a identificação do processo do Windows.  
  
 **Tipo de Serviço**  
 Exibe o tipo de serviço fornecido a processos de chamada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala vários serviços.  
  
 **Modo Inicial**  
 Defina este serviço com as seguintes opções:  
  
-   Manual: este serviço não é iniciado automaticamente na inicialização do computador. Você deve iniciá-lo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou outra ferramenta.  
  
-   Automático: este serviço tenta ser iniciado na inicialização do computador.  
  
-   Desabilitado: este serviço não pode ser iniciado.  
  
 **Estado**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado. "**…**" indica que uma alteração no estado está pendente.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
