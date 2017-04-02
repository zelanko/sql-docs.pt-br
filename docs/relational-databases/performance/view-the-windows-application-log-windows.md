---
title: "Exibir o log de aplicativos do Windows (Windows) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibindo logs"
  - "logs do aplicativo [SQL Server]"
  - "logs [SQL Server], aplicativo"
  - "monitorando o log de aplicativos do Windows NT [SQL Server]"
  - "logs de aplicativos do Windows NT [SQL Server]"
  - "exibindo logs"
  - "monitorando [SQL Server], eventos"
  - "logs [SQL Server], exibindo"
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Exibir o log de aplicativos do Windows (Windows)
  Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para usar o log de aplicativos do Windows, cada sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grava novos eventos nesse log. Ao contrário do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], não é criado um novo log de aplicativos cada vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada.  
  
### Para exibir o log de aplicativos do Windows  
  
1.  No menu **Iniciar**, aponte para **Todos os Programas**, **Ferramentas Administrativas** e clique em **Visualizador de Eventos**.  
  
2.  No Visualizador de Eventos, clique em **Aplicativo**.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os eventos são identificados pela entrada **MSSQLSERVER** (as instâncias nomeadas são identificadas com **MSSQL$***<instance_name>*) na coluna **Origem**. Os eventos do SQL Server Agent são identificados pela entrada SQLSERVERAGENT (para instâncias nomeadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são identificados com **SQLAgent$**\<*instance_name*>). Os eventos do serviço do Microsoft Search são identificados pela entrada **Microsoft Search**.  
  
4.  Para exibir o log de um computador diferente, clique com o botão direito do mouse em **Visualizador de Eventos**, clique em **Conectar-se a outro computador** e preencha a caixa de diálogo **Selecionar Computador**.  
  
5.  Opcionalmente, para exibir apenas eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no menu **Exibir** clique em **Filtro** e, na lista **Origem do evento**, selecione **MSSQLSERVER**. Para exibir apenas eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, selecione **SQLSERVERAGENT** na lista **Origem do evento**.  
  
6.  Para exibir mais informações sobre um evento, clique duas vezes no evento.  
  
## Consulte também  
 [Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  