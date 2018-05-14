---
title: Habilitar um Publicador remoto em um Distribuidor (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8f66807a51eb6e13f1f7663acb06ad40719529a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>Habilitar um Publicador remoto em um Distribuidor (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Habilite um Publicador a usar um Distribuidor remoto na página **Publicadores** . Esta página está disponível no Assistente para Configurar Distribuição e na caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md) e [Exibir e modificar o distribuidor e as propriedades do publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>Para habilitar um Publicador no Assistente para Configurar Distribuição  
  
1.  Na página **Publicadores** do Assistente para Configurar Distribuição, clique em **Adicionar**.  
  
2.  Clique em **Adicionar Editor SQL Server**. Para obter informações sobre como habilitar um Oracle Publisher para usar um Distribuidor, consulte [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , especifique a informação de conexão para o Publicador que usará o Distribuidor remoto e, então, clique em **Conectar**.  
  
4.  Na página **Senha do Distribuidor** nas caixas de texto **Senha** e **Confirmar Senha** , especifique uma senha forte para a conta **distributor_admin** , que a replicação usa para conectar-se do Publicador para o Distribuidor para executar tarefas administrativas.  
  
5.  Para exibir e modificar as configurações para um Publicador, clique no botão de propriedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>Para habilitar um Publicador na caixa de diálogo Propriedades de Distribuidor  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**, clique em **Adicionar**.  
  
2.  Clique em **Adicionar Editor SQL Server**. Para obter informações sobre como habilitar um Oracle Publisher para usar um Distribuidor, consulte [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , especifique a informação de conexão para o Publicador que usará o Distribuidor remoto e, então, clique em **Conectar**.  
  
4.  Na página **Publicadores** nas caixas de texto **Senha** e **Confirmar Senha** , especifique uma senha forte para a conta **distributor_admin** , que a replicação usará para conectar-se do Publicador para o Distribuidor para executar tarefas administrativas.  
  
5.  Para exibir e modificar as configurações para um Publicador, clique no botão de propriedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
