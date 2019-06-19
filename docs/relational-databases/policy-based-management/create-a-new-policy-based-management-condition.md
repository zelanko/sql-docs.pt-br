---
title: Criar uma nova condição de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policy conditions
ms.assetid: 8a612f7e-6c70-49db-a4de-48431e097cc5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3f6f17e97b485e7c6c4dc747886bd5304b8fa812
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63007627"
---
# <a name="create-a-new-policy-based-management-condition"></a>Criar uma nova condição de Gerenciamento baseado em Políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar uma condição de Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar uma condição, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-condition"></a>Para criar uma condição  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar uma condição de Gerenciamento Baseado em Políticas.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Facetas** .  
  
5.  Clique com o botão direito do mouse na faceta em que você deseja criar uma nova condição e selecione **Nova Condição**.  
  
6.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite o nome da nova condição.  
  
7.  Confirme a faceta correta na lista **Faceta** ou selecione uma faceta diferente.  
  
8.  Em **Expressão**, construa expressões de condição selecionando uma propriedade de faceta na caixa **Campo** , junto com o operador e o valor associados. Quando você adicionar várias expressões, as expressões podem ser unidas usando **E** ou **Ou**. Para obter mais informações sobre as opções disponíveis nesta caixa de diálogo, veja [Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página Geral](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md), [Caixa de diálogo Criar Nova Condição ou Abrir Condição, Página de Descrição](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md) e [Caixa de diálogo Edição Avançada &#40;Condição&#41;](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md).  
  
9. Quando terminar, clique em **OK**.  
  
  
