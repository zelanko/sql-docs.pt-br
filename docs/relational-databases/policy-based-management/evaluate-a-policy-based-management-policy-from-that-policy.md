---
title: Avaliar uma política do gerenciamento baseado em políticas dessa política
description: Saiba como avaliar uma política usando essa política no SQL Server com o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: 0b3214bd-d0ab-45ab-9281-3d95507abe54
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 28b605b52600fe9855fb9e96f9f2dbc99bbc6a20
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760529"
---
# <a name="evaluate-a-policy-based-management-policy-from-that-policy"></a>Avaliar uma política do Gerenciamento Baseado em Políticas dessa política
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como avaliar uma política usando essa política no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para avaliar uma política, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy"></a>Para avaliar uma política  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a política que você deseja avaliar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Políticas** .  
  
5.  Clique com o botão direito do mouse na política a ser avaliada e selecione **Avaliar**.  
  
6.  Na caixa de diálogo **Avaliar Resultados**  , você pode ver os resultados da avaliação de política. Para destinos que não obedecem à política e têm propriedades que podem ser reconfiguradas pelo Gerenciamento de Política, é possível impor a conformidade com a política clicando em **Aplicar**. Para obter mais informações sobre as opções disponíveis contidas na caixa de diálogo **Avaliar Políticas** , consulte [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md) e [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md).  
  
7.  Quando terminar, clique em **Fechar**.  

