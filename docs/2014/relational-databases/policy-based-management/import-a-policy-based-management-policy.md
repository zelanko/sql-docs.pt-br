---
title: Importar uma política do Gerenciamento Baseado em Políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1f0cecc9489f57512ab9715bdbffdef7d82ece53
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063890"
---
# <a name="import-a-policy-based-management-policy"></a>Importar política de Gerenciamento Baseado em Políticas
  Este tópico descreve como importar uma instância de Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para importar uma instância de política, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transporta políticas que podem ser usadas para monitorar uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]; no entanto, elas podem ser importadas do local de instalação padrão C:\Arquivos de Programas\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>Para importar uma instância de política  
  
1.  No painel **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor em que a instância de política recém-importada residirá.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique com o botão direito do mouse na pasta **Políticas** e selecione **Importar Política**.  
  
5.  Na caixa de diálogo **Importar** , digite o caminho e o nome do arquivo ou use o botão Procurar ( **...** ) para localizar o arquivo XML que contém a política e selecione o arquivo. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Importar** , consulte [Import Policies Dialog Box](import-policies-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  
  
  
