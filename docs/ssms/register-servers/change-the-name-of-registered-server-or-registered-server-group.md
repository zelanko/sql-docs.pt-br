---
title: Alterar o nome de um servidor registrado ou de um grupo de servidores registrados | Microsoft Docs
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-registration
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7aabe8faf813462c6e674c395b4e0f2c49d7d656
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>Alterar o nome de um servidor registrado ou de um grupo de servidores registrados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Este tópico descreve como exibir ou alterar o nome de um servidor registrado ou grupo de servidores no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O nome pode ser alterado a qualquer momento. Alterar o nome de um servidor nos Servidores Registrados altera apenas como o nome é exibido. Para conectar-se a um servidor diferente, você deve editar as propriedades de conexão do servidor registrado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
No menu, procure **Exibir\\Servidores Registrados** para abrir o painel **Servidores Registrados**.  
#### <a name="to-change-the-name-of-a-server"></a>Para alterar o nome de um servidor  
  
1.  Em **Servidores Registrados**, expanda **Mecanismo de Banco de Dados** e **Grupos do Servidores Locais**.  

2.  Clique com o botão direito do mouse em um servidor e selecione **Propriedades** para abrir a janela de diálogo **Editar Propriedades de Registro do Servidor** .
  
3.  Na caixa de texto **Nome do servidor registrado** , digite o novo nome para o registro do servidor e clique em **Salvar**.  
  
#### <a name="to-change-the-name-of-a-server-group"></a>Para alterar o nome de um grupo de servidores  
  
1.  Em **Servidores Registrados**, expanda **Mecanismo de Banco de Dados** e **Grupos do Servidores Locais**.  

2.  Clique com o botão direito do mouse em um grupo de servidores e selecione **Propriedades** para abrir a janela de diálogo **Editar Propriedades do Grupo de Servidores** . 
  
3.  Na caixa de texto **Nome do grupo** , digite o novo nome para o grupo de servidores e clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Alterar um registro do servidor &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  
