---
title: "Selecionar um Pacote | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.selectapackage.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Selecionar um Pacote"
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Selecionar um Pacote
  Use a caixa de diálogo **Selecionar um Pacote** para especificar o pacote do qual a tarefa Fila de Mensagens pode receber mensagens.  
  
## Opções estáticas  
 **Local**  
 Especifique o local do pacote. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Defina o local como uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao selecionar esse valor, as opções dinâmicas **Servidor**, **Usar Autenticação do Windows**, **Usar Autenticação do SQL Server**, **Nome de usuário**e **Senha**são exibidas.|  
|Arquivo DTSX|Defina o local para um arquivo DTSX. Ao selecionar este valor,a opção dinâmica **Nome do arquivo**será exibida.|  
  
## Opções Dinâmicas de Local  
  
### Local = SQL Server  
 **Nome do pacote**  
 Selecione um pacote que esteja armazenado no servidor especificado.  
  
 **Servidor**  
 Forneça um nome de servidor ou selecione um servidor na lista.  
  
 **Usar Autenticação do Windows**  
 Clique para usar Autenticação do Windows.  
  
 **Usar Autenticação do SQL Server**  
 Clique para usar Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome de usuário**  
 Se usar Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça um nome de usuário a ser usado no logon no servidor.  
  
 **Senha**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], forneça uma senha.  
  
### Local = arquivo DTSX  
 **Nome do arquivo**  
 Forneça o caminho de um pacote ou clique no botão Procurar **(...)** e localize o pacote.  
  
## Consulte também  
 [Tarefa Fila de Mensagens](../../integration-services/control-flow/message-queue-task.md)  
  
  