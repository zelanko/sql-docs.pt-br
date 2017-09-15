---
title: "Importar uma política do Gerenciamento Baseado em Políticas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: fc3420c4b87cc1d304e7a58b540d7f9210aac18a
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

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
  
###  <a name="Restrictions"></a> Limitações e restrições  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transporta políticas que podem ser usadas para monitorar uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no entanto, elas podem ser importadas do local de instalação padrão C:\Arquivos de Programas\Microsoft SQL Server\###\Tools\Policies\DatabaseEngine\1033 ou C:\Arquivos de Programas (x86)\Microsoft SQL Server\###\Tools\Policies\DatabaseEngine\1033 em instalações de 64 bits.
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>Para importar uma instância de política  
  
1.  No painel **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor em que a instância de política recém-importada residirá.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique com o botão direito do mouse na pasta **Políticas** e selecione **Importar Política**.  
  
5.  Na caixa de diálogo **Importar** , digite o caminho e o nome do arquivo ou use o botão Procurar (**...**) para localizar o arquivo XML que contém a política e selecione o arquivo. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Importar** , consulte [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  
  
  

