---
title: Exibir as facetas de Gerenciamento Baseado em Políticas em um objeto do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 82acf976fef80f62059b5a433bb74e3fbbadec80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021433"
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>Exibir as facetas de Gerenciamento Baseado em Políticas em um objeto do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir todas as facetas do Gerenciamento Baseado em Políticas aplicadas a um objeto do SQL Server específico no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir todas as facetas em um objeto, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>Para exibir todas as facetas em um objeto  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um objeto de instância, banco de dados ou objeto de banco de dados e clique em **Facetas**.  
  
2.  Na caixa de diálogo **Exibir Facetas -** _nome_do_objeto_, na lista **Faceta**, selecione uma faceta para exibir suas propriedades. Para obter mais informações sobre as opções disponíveis nesta caixa de diálogo, consulte [View Facets Dialog Box](../../relational-databases/policy-based-management/view-facets-dialog-box.md).  
  
3.  Quando terminar, clique em **OK**.  
  
  
