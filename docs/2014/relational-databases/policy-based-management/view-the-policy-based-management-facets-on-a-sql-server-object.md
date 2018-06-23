---
title: Exibir as facetas de Gerenciamento Baseado em Políticas em um objeto do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e95abe9e853c0e90bed9d58765fae1640f9885f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007493"
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>Exibir as facetas de Gerenciamento Baseado em Políticas em um objeto do SQL Server
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
  
2.  Na caixa de diálogo **Exibir Facetas –***object_name*, na lista **Faceta**, selecione uma faceta para exibir suas propriedades. Para obter mais informações sobre as opções disponíveis nesta caixa de diálogo, consulte [View Facets Dialog Box](view-facets-dialog-box.md).  
  
3.  Quando terminar, clique em **OK**.  
  
  