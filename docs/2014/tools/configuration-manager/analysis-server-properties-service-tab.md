---
title: Propriedades do Analysis Server (guia Serviço) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 8dbe4bc5-6aa9-48ee-857e-0b4ea764b9cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4f083aafd2dc8718bb79798d43483c66b3520b0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666734"
---
# <a name="analysis-server-properties-service-tab"></a>Propriedades do Analysis Server (guia Serviço)
  Este serviço é o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Ele deve estar sendo executado para que o [!INCLUDE[ssAS](../../includes/ssas-md.md)] funcione corretamente. Os valores de propriedade em cinza claro não podem ser alterados com o uso deste aplicativo.  
  
## <a name="options"></a>Opções  
 **Caminho Binário**  
 Exibe o local dos arquivos de programas usados por este serviço.  
  
 **Controle de Erro**  
 1 indica `SERVICE_ERROR_NORMAL`. Se o serviço não for iniciado durante a inicialização do computador, o programa de inicialização registrará o erro em log e exibirá uma caixa de mensagem pop-up, mas continuará a operação de inicialização. Esse valor não pode ser alterado.  
  
 **Código de Saída**  
 Quando ocorre um erro, o número do erro é exibido nesta caixa. Use esse número para solucionar problemas de falhas procurando-o na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou forneça o número à sua equipe de suporte técnico.  
  
 **Nome do Host**  
 Exibe o nome do computador ou cluster que está executando o [!INCLUDE[ssAS](../../includes/ssas-md.md)].  
  
 **Nome**  
 Indica o nome para exibição do serviço.  
  
 **ID do Processo**  
 Exibe o número usado pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para manter o controle dos processos deste programa.  
  
 **Tipo de Serviço do SQL**  
 Exibe o tipo de serviço fornecido a processos de chamada. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala vários serviços.  
  
 **Modo Inicial**  
 Defina este serviço com as seguintes opções:  
  
-   Manual: Esse serviço não iniciar automaticamente quando o computador é iniciado. Você deve iniciá-lo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou outra ferramenta.  
  
-   Automático: Este serviço tenta ser iniciado quando o computador é iniciado.  
  
-   Desabilitado: Este serviço não pode ser iniciado.  
  
 **Estado**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado.  
  
  
