---
title: Gerenciar um serviço Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 5972cee3-b1a9-4c56-aed6-bdddf84af283
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f73c92b4b426a9598d80da89d8f17365fc63212b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790468"
---
# <a name="manage-an-oracle-cdc-service"></a>Manage an Oracle CDC Service
  Você pode usar o Console de Configuração do Serviço CDC para gerenciar um Serviço CDC específico.  
  
 **Para selecionar o serviço CDC com o qual você deseja trabalhar**  
  
1.  No painel esquerdo no Console de Configuração do Serviço CDC, expanda **Serviços Locais de CDC**.  
  
2.  Selecione o serviço CDC com o qual você deseja trabalhar.  
  
     Você também pode clicar com o botão direito no serviço CDC com o qual você deseja trabalhar e selecionar a ação desejada. Consulte [O que pode fazer você com um Serviço ](manage-an-oracle-cdc-service.md#bkmk_whatcandowithcdcservice).  
  
 **OR**  
  
1.  Selecione **Serviços Locais de CDC** no painel esquerdo no Console de Configuração do Serviço de CDC.  
  
2.  Da seção do meio do Console de Configuração do Serviço CDC, selecione o serviço com o qual você deseja trabalhar.  
  
     Você também pode clicar com o botão direito no serviço CDC com o qual você deseja trabalhar e selecionar a ação desejada. Consulte [O que pode fazer você com um Serviço ](manage-an-oracle-cdc-service.md#bkmk_whatcandowithcdcservice).  
  
##  <a name="BKMK_WhatcandowithCDCService"></a> O que pode fazer você com um Serviço CDC  
 Você pode realizar as seguintes ações ao trabalhar com um serviço CDC.  
  
### <a name="delete-the-service"></a>Excluir o serviço  
 No painel **Ações** no lado direito do Console de Configuração do Serviço CDC, clique em **Excluir** para excluir o serviço.  
  
 Você também pode clicar com o botão direito do mouse no serviço CDC que deseja excluir e selecionar **Excluir**.  
  
 **Observação**: Se o serviço é executado ao excluir o serviço, o serviço é interrompido antes de serem excluídos.  
  
 Para excluir a definição de Serviço do Windows do Oracle CDC, o programa precisa de acesso de atualização ao banco de dados MSXDBCDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada. Quando você clicar em OK para excluir o serviço, o programa tentará excluir o registro do Serviço Oracle CDC no banco de dados MSXDBCDC. Se o programa não puder excluir o registro do Serviço Oracle CDC porque não tem as permissões corretas, ele solicitará que o usuário insira um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com permissões de atualização para o banco de dados MSXDBCDC.  
  
 Para obter informações sobre os dados que você deverá inserir na caixa de diálogo Conecte-se ao SQL Server, consulte [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md).  
  
### <a name="edit-the-cdc-service-properties"></a>Editar as propriedades de serviço CDC  
 No painel **Ações** no lado direito do Console de Configuração do Serviço CDC, clique em **Propriedades**.  
  
 Você também pode clicar com o botão direito do mouse no serviço CDC em que deseja editar as propriedades e selecionar **Propriedades**.  
  
## <a name="see-also"></a>Consulte Também  
 [Como gerenciar um serviço CDC local](how-to-manage-a-local-cdc-service.md)  
  
  
