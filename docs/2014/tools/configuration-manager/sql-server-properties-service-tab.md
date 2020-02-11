---
title: Propriedades do SQL Server (guia Serviço) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e4ae0c6b-6fd8-4325-b54e-1758fc659958
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f79b52e62a8080c70865ae8ebe33d1a8a87faa04
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63237989"
---
# <a name="sql-server-properties-service-tab"></a>Propriedades do SQL Server (guia Serviço)
  Use a guia **Serviço**na caixa de diálogo **Propriedades de MSSQLSERVER** para exibir ou especificar as opções a seguir.  
  
## <a name="options"></a>Opções  
 **Caminho binário**  
 Lista o local dos arquivos de programas usados por este serviço.  
  
 **Controle de erro**  
 1 indica `SERVICE_ERROR_NORMAL`. Se o serviço não for iniciado durante a inicialização do computador, o programa de inicialização registrará o erro em log e exibirá uma caixa de mensagem pop-up, mas continuará a operação de inicialização. Esse valor não pode ser alterado.  
  
 **Código de saída**  
 Quando ocorre um erro, o número do erro é exibido nesta caixa. Use esse número para solucionar problemas de falhas procurando-o na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou forneça o número à sua equipe de suporte técnico.  
  
 **Nome do host**  
 Exibe o nome do computador ou cluster que está executando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o serviço.  
  
 **Nome**  
 Indica o nome para exibição do serviço.  
  
 **ID do Processo**  
 Exibe a identificação do processo do Windows.  
  
 **Tipo de serviço**  
 Exibe o tipo de serviço fornecido a processos de chamada. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala vários serviços.  
  
 **Modo de início**  
 Defina este serviço com as seguintes opções:  
  
-   Manual: este serviço não é iniciado automaticamente na inicialização do computador. Você deve iniciá-lo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou outra ferramenta.  
  
-   Automático: este serviço tenta ser iniciado na inicialização do computador.  
  
-   Desabilitado: este serviço não pode ser iniciado.  
  
 **Estado**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado. "**...**" indica que há uma alteração de estado pendente.  
  
  
