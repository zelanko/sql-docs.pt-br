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
manager: craigg
ms.openlocfilehash: e4978471f25c1bf38d841e11f560a6bd99dac53e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783698"
---
# <a name="import-a-policy-based-management-policy"></a>Importar política de Gerenciamento Baseado em Políticas
  Este tópico descreve como importar uma instância de Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para importar uma instância de política, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transporta políticas que podem ser usadas para monitorar uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]; no entanto, elas podem ser importadas do local de instalação padrão C:\Arquivos de Programas\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>Para importar uma instância de política  
  
1.  No painel **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor em que a instância de política recém-importada residirá.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique com o botão direito do mouse na pasta **Políticas** e selecione **Importar Política**.  
  
5.  Na caixa de diálogo **Importar** , digite o caminho e o nome do arquivo ou use o botão Procurar (**...**) para localizar o arquivo XML que contém a política e selecione o arquivo. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Importar** , consulte [Import Policies Dialog Box](import-policies-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  
  
  
