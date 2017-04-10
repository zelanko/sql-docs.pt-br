---
title: "Salvar resultados de rastreamento em uma tabela (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "salvando rastreamentos"
  - "rastreamentos [SQL Server], salvando"
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Salvar resultados de rastreamento em uma tabela (SQL Server Profiler)
  Este tópico descreve como salvar resultados de rastreamento em uma tabela do banco de dados, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### Para salvar resultados de rastreamento em uma tabela  
  
1.  No menu **Arquivo**, clique em **Novo Rastreamento** e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa de diálogo **Nome do rastreamento**, digite um nome para o rastreamento e clique em **Salvar em tabela**.  
  
3.  Na caixa de diálogo **Conectar ao Servidor**, conecte-se ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conterá a tabela de rastreamento.  
  
4.  Na caixa de diálogo **Tabela de Destino**, selecione um banco de dados na lista **Banco de Dados**.  
  
5.  Na lista **Proprietário**, selecione o proprietário do rastreamento.  
  
6.  Na lista **Tabela**, digite ou selecione o nome da tabela a conter os resultados do rastreamento. Clique em **OK.**  
  
7.  Na caixa de diálogo **Propriedades do Rastreamento**, marque a caixa de seleção **Definir máximo de linhas (em milhares)** para especificar o número máximo de linhas a serem salvas.  
  
## Consulte também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  