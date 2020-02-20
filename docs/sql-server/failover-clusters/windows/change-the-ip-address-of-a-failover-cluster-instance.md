---
title: Alterar o endereço IP de uma instância de cluster de failover
description: Saiba como alterar o endereço IP de uma instância de cluster de failover do SQL Server usando o Gerenciador de Cluster de Failover.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f4960a10a44e3a84b42c0bf43872a38be05be292
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75230140"
---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>Alterar o endereço IP de uma instância do cluster de failover
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como alterar o recurso de endereço IP em uma FCI (instância de cluster de failover) AlwaysOn usando o snap-in Gerenciador de Cluster de Failover. O snap-in Gerenciador de Cluster de Failover é o aplicativo de gerenciamento de cluster do serviço WSFC (Windows Server Failover Clustering).  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Antes de começar, examine o seguinte tópico dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
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
  
  
