---
title: "Alterar o endereço IP de uma instância do cluster de failover | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d30ca9ae2885d25bd0b62a17501ae7dfe94f26e9
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>Alterar o endereço IP de uma instância do cluster de failover
  Este tópico descreve como alterar o recurso de endereço IP em uma FCI (instância de cluster de failover) AlwaysOn usando o snap-in Gerenciador de Cluster de Failover. O snap-in Gerenciador de Cluster de Failover é o aplicativo de gerenciamento de cluster do serviço WSFC (Windows Server Failover Clustering).  
  
-   **Before you begin:**  [Security](#Security)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Antes de começar, examine o seguinte tópico dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] : [Antes de instalar o Clustering de Failover](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para manter ou atualizar uma FCI, você deve ser um administrador local com permissão para fazer logon como um serviço em todos os nós da FCI.  
  
##  <a name="WSFC"></a> Usando o snap-in Gerenciador de Cluster de Failover  
 **Para alterar o recurso de endereço IP para uma FCI**  
  
1.  Abra o snap-in Gerenciador de Cluster de Failover.  
  
2.  Expanda o nó **Serviços e aplicativos** , no painel esquerdo e clique na FCI.  
  
3.  No painel direito, na categoria **Nome do Servidor** , clique com o botão direito do mouse na Instância do SQL Server e selecione **Propriedades** para abrir a caixa de diálogo **Propriedades** .  
  
4.  Na guia **Geral** , altere o recurso de endereço IP.  
  
5.  Clique em **OK** para fechar a caixa de diálogo.  
  
6.  No painel direito, clique com o botão direito do mouse no Endereço IP1 SQL (nome da instância do cluster de failover) e selecione **Colocar Offline**. Você verá o Endereço IP1 SQL(nome da instância do cluster de failover), o Nome de Rede do SQL(nome da instância do cluster de failover) e o status do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mudarem de Online para Pendente Offline e, depois, para Offline.  
  
7.  No painel direito, clique com o botão direito do mouse em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]e selecione **Colocar Online**. Você verá o Endereço IP1 SQL(nome da instância do cluster de failover), o Nome de Rede do SQL(nome da instância do cluster de failover) e o status do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mudarem de Offline para Pendente Online e, depois, para Online.  
  
8.  Feche o snap-in Gerenciador de Cluster de Failover.  
  
  
