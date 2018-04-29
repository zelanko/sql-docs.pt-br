---
title: Selecionar um pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bf8cf86fce968150d94ef1893ebe34a2fa92c0b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="select-a-package"></a>Selecionar um Pacote
  Use a caixa de diálogo **Selecionar um Pacote** para especificar o pacote do qual a tarefa Fila de Mensagens pode receber mensagens.  
  
## <a name="static-options"></a>Opções estáticas  
 **Local**  
 Especifique o local do pacote. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Defina o local como uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao selecionar esse valor, as opções dinâmicas **Servidor**, **Usar Autenticação do Windows**, **Usar Autenticação do SQL Server**, **Nome de usuário**e **Senha**são exibidas.|  
|Arquivo DTSX|Defina o local para um arquivo DTSX. Ao selecionar este valor,a opção dinâmica **Nome do arquivo**será exibida.|  
  
## <a name="location-dynamic-options"></a>Opções Dinâmicas de Local  
  
### <a name="location--sql-server"></a>Local = SQL Server  
 **Nome do pacote**  
 Selecione um pacote que esteja armazenado no servidor especificado.  
  
 **Servidor**  
 Forneça um nome de servidor ou selecione um servidor na lista.  
  
 **Usar Autenticação do Windows**  
 Clique para usar Autenticação do Windows.  
  
 **Usar Autenticação do SQL Server**  
 Clique para usar Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **User name**  
 Se usar Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça um nome de usuário a ser usado no logon no servidor.  
  
 **Senha**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça uma senha.  
  
### <a name="location--dtsx-file"></a>Local = arquivo DTSX  
 **Nome do arquivo**  
 Forneça o caminho de um pacote ou clique no botão Procurar **(...)** e localize o pacote.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa Fila de Mensagens](../../integration-services/control-flow/message-queue-task.md)  
  
  
