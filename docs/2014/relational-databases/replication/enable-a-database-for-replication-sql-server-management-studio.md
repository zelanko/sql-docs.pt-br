---
title: Habilitar um banco de dados para replicação (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 307d52e24187e35c1c30f609facd13bfad569216
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010743"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Habilitar um banco de dados para replicação (SQL Server Management Studio)
  Um banco de dados está implicitamente habilitado para replicação quando um membro da função do servidor fixa **sysadmin** cria uma publicação no Assistente para Novas Publicações. Um membro da função de servidor fixa **sysadmin** também pode habilitar um banco de dados explicitamente para replicação, assim, um membro da função de banco de dados fixa **db_owner** pode criar uma ou mais publicações naquele banco de dados. Para habilitar um banco de dados explicitamente, use a página bancos de dados de **publicação** da caixa de diálogo ** \<Publisher> Propriedades do Publicador** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Create a Publication](publish/create-a-publication.md).  
  
### <a name="to-enable-a-database-for-replication"></a>Para habilitar um banco de dados para replicação  
  
1.  Na página **bancos de dados de publicação** da caixa de diálogo ** \<Publisher> Propriedades do Publicador** , marque a caixa de seleção **transacional** e/ou **mesclagem** para cada banco de dados que você deseja replicar. Selecione **Transacional** para habilitar o banco de dados para replicação de instantâneo.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
