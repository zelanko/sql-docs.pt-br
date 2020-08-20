---
description: Excluir uma condição de Gerenciamento baseado em Políticas
title: Excluir uma condição de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, delete policy conditions
ms.assetid: e04148b8-f6dd-4c50-a5ef-c650b71dbf4d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3265e970fbad572e09527dedcb35397d811daefa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470311"
---
# <a name="delete-a-policy-based-management-condition"></a>Excluir uma condição de Gerenciamento baseado em Políticas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como excluir uma condição de Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para excluir uma condição, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-condition"></a>Para excluir uma condição  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a condição que você deseja excluir.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Condições** .  
  
5.  Clique com o botão direito do mouse na condição a ser excluída e selecione **Excluir**.  
  
6.  Na caixa de diálogo **Excluir Objeto** , verifique se a condição correta está selecionada e clique em **OK**.  

