---
title: Habilitar um Publicador remoto em um Distribuidor (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7b554dc39832a834ebe1bc2ac2d4bfefa21721a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721314"
---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>Habilitar um Publicador remoto em um Distribuidor (SQL Server Management Studio)
   Habilite um Publicador a usar um Distribuidor remoto na página **Publicadores**. Esta página está disponível no Assistente para Configurar Distribuição e na caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Configurar publicação e distribuição](configure-publishing-and-distribution.md) e [Exibir e modificar o distribuidor e as propriedades do publicador](view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>Para habilitar um Publicador no Assistente para Configurar Distribuição  
  
1.  Na página **Publicadores** do Assistente para Configurar Distribuição, clique em **Adicionar**.  
  
2.  Clique em **Adicionar Editor SQL Server**. Para obter informações sobre como habilitar um Oracle Publisher para usar um Distribuidor, consulte [Create a Publication from an Oracle Database](publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , especifique a informação de conexão para o Publicador que usará o Distribuidor remoto e, então, clique em **Conectar**.  
  
4.  Na página **Senha do Distribuidor** nas caixas de texto **Senha** e **Confirmar Senha** , especifique uma senha forte para a conta **distributor_admin** , que a replicação usa para conectar-se do Publicador para o Distribuidor para executar tarefas administrativas.  
  
5.  Para exibir e modificar as configurações para um Publicador, clique no botão de propriedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>Para habilitar um Publicador na caixa de diálogo Propriedades de Distribuidor  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**, clique em **Adicionar**.  
  
2.  Clique em **Adicionar Editor SQL Server**. Para obter informações sobre como habilitar um Oracle Publisher para usar um Distribuidor, consulte [Create a Publication from an Oracle Database](publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , especifique a informação de conexão para o Publicador que usará o Distribuidor remoto e, então, clique em **Conectar**.  
  
4.  Na página **Publicadores** nas caixas de texto **Senha** e **Confirmar Senha** , especifique uma senha forte para a conta **distributor_admin** , que a replicação usará para conectar-se do Publicador para o Distribuidor para executar tarefas administrativas.  
  
5.  Para exibir e modificar as configurações para um Publicador, clique no botão de propriedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md)   
 [Configurar a distribuição](configure-distribution.md)   
 [Proteger o Distribuidor](security/secure-the-distributor.md)  
  
  
