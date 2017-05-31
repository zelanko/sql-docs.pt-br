---
title: "Propriedades do Publicador – Publicador, Bancos de Dados de Publicação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cc86424019df085038fffd9b076576eb9c717024
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="publisher-properties---publisher-publication-databases"></a>Propriedades do Publicador - Publicador, Bancos de Dados de Publicação
  A página **Bancos de dados de Publicação** da caixa de diálogo **Propriedades do Publicador** permite que um usuário da função de servidor fixa **sysadmin** habilite bancos de dados para replicação. Habilitar um banco de dados não publica esse banco de dados, mas permite que qualquer usuário na função de banco de dados fixa **db_owner** daquele banco de dados crie uma ou mais publicações no banco de dados.  
  
## <a name="options"></a>Opções  
 **Transacional.**  
 Marque essa caixa de seleção para permitir que usuários na função de banco de dados fixa **db_owner** criem publicações de instantâneo ou transacionais no banco de dados.  
  
 **Mesclagem**  
 Marque essa caixa de seleção para permitir que usuários na função de banco de dados fixa **db_owner** criem publicações de mesclagem no banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referência de propriedades &#40;Replicação&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
