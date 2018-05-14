---
title: Avaliar uma política do gerenciamento baseado em políticas de um objeto | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 686b6ebac2c21c3e12f594340a8542efae97baee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="evaluate-a-policy-based-management-policy-from-an-object"></a>Avaliar uma política do Gerenciamento Baseado em Políticas de um objeto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como avaliar uma política de uma instância de servidor, banco de dados ou objeto de banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para avaliar uma política em um objeto, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O modo de execução é definido como parte da política e não pode ser alterado na caixa de diálogo **Avaliar Políticas** .  
  
-   A caixa de diálogo **Avaliar Políticas** só mostra políticas apropriadas para o objeto de banco de dados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-from-an-object"></a>Para avaliar uma política em um objeto  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em uma instância de servidor, um banco de dados ou um objeto de banco de dados, aponte para **Políticas**e selecione **Avaliar**.  
  
2.  Na caixa de diálogo **Avaliar Políticas** , selecione uma ou mais políticas e clique em **Avaliar** para executar a política no modo de avaliação. Isso gera um relatório de conformidade para o conjunto de destino, mas não reconfigura o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nem impõe conformidade no futuro. Para destinos que não seguem as políticas selecionadas e têm propriedades que podem ser reconfiguradas pelo Gerenciamento de Política, é possível impor a conformidade com a política clicando em **Aplicar**. Para obter mais informações sobre as opções disponíveis contidas na caixa de diálogo **Avaliar Políticas** , consulte [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md)e [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)e [Results Detailed View Dialog Box](../../relational-databases/policy-based-management/results-detailed-view-dialog-box.md).  
  
3.  Quando terminar, clique em **Fechar**.  
  
  
