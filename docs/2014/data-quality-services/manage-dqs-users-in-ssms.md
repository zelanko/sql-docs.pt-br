---
title: Gerenciar usuários DQS no SSMS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d17883d39f4579f509eed894735c676f464feeeb
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032181"
---
# <a name="manage-dqs-users-in-ssms"></a>Gerenciar usuários de DQS em SSMS
  Este tópico descreve como criar usuários adicionais na instância do SQL Server usando o SQL Server Management Studio e como concedê-los funções DQS apropriadas do [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] no banco de dados DQS_MAIN.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Sua conta de usuário do Windows deve ser membro da função de servidor fixa apropriada (como securityadmin, serveradmin ou sysadmin) para criar um logon do SQL e conceder funções DQS adequadas.  
  
##  <a name="GrantRoles"></a> Criar um logon do SQL e conceder funções DQS  
  
1.  Inicie o Microsoft SQL Server Management Studio.  
  
2.  Em Microsoft SQL Server Management Studio, expanda sua instância do SQL Server e expanda **Segurança**.  
  
3.  Clique com o botão direito na pasta **Segurança** , aponte para **Novo**e clique em **Logon**.  
  
4.  Na caixa de diálogo **Logon – Novo** , especifique o nome de um usuário do Windows na caixa **Nome de Logon** , especifique o tipo de autenticação como **Autenticação do Windows**e clique em **Pesquisar** para validar o usuário.  
  
    > [!NOTE]  
    >  O DQS dá suporte somente à autenticação do Windows; a autenticação do SQL Server não tem suporte.  
  
5.  Depois que o usuário for validado, clique na página **Mapeamento de Usuário** no painel esquerdo.  
  
6.  No painel direito, marque a caixa de seleção sob a coluna **Mapa** do banco de dados **DQS_MAIN** e, depois, marque a caixa de texto **dqs_administrator**, **dqs_kb_editor**ou **dqs_kb_operator** no painel **Associação à função de banco de dados para: DQS_MAIN** , dependendo do nível de acesso necessário ao usuário.  
  
7.  Na caixa de diálogo **Logon – Novo** , clique em **OK** para aplicar as alterações.  
  
    > [!NOTE]  
    >  Se você conceder a função **dqs_administrator** a um usuário, aplique as alterações e verifique novamente as permissões de usuário, as outras duas caixas de seleção de funções DQS (**dq_kb_editor** e **dqs_kb_operator**) também são marcadas.  
  
  
