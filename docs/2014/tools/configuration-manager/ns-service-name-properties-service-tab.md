---
title: NS$&lt;nome do serviço&gt; propriedades (guia serviço) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57c6b791-1663-4a01-9de2-cf1bdd8adb2c
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c02ad64dfada49434900795f49802e75cf8d2945
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012609"
---
# <a name="nsltservice-namegt-properties-service-tab"></a>Propriedades do NS$&lt;nome do serviço&gt; (guia Serviço)
  Este é o serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNS](../../includes/ssns-md.md)] . Os valores de propriedade em cinza claro não podem ser alterados com o uso deste aplicativo.  
  
## <a name="options"></a>Opções  
 **Caminho Binário**  
 Exibe o local dos arquivos de programas usados por este serviço.  
  
 **Controle de Erro**  
 1 indica `SERVICE_ERROR_NORMAL`. Se o serviço não for iniciado durante a inicialização do computador, o programa de inicialização registrará o erro em log e exibirá uma caixa de mensagem pop-up, mas continuará a operação de inicialização. Esse valor não pode ser alterado.  
  
 **Código de Saída**  
 Quando ocorre um erro, o número do erro é exibido nesta caixa. Use esse número para solucionar problemas de falhas procurando-o na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou forneça o número à sua equipe de suporte técnico.  
  
 **Nome do Host**  
 Exibe o nome do computador ou cluster que está executando a pesquisa de texto completo.  
  
 **Nome**  
 Indica o nome para exibição do serviço.  
  
 **ID do Processo**  
 Exibe a identificação do processo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Tipo de Serviço do SQL**  
 Tipo de serviço fornecido a processos de chamada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala vários serviços.  
  
 **Modo Inicial**  
 Defina este serviço com as seguintes opções:  
  
-   Manual: este serviço não é iniciado automaticamente na inicialização do computador. Você deve iniciá-lo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou outra ferramenta.  
  
-   Automático: este serviço tenta ser iniciado na inicialização do computador.  
  
-   Desabilitado: este serviço não pode ser iniciado.  
  
 **Estado**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado.  
  
  