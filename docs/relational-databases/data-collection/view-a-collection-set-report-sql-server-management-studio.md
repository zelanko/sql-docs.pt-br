---
title: "Exibir um relat&#243;rio de conjuntos de coleta (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.dc.reporthistory.calendar.f1"
helpviewer_keywords: 
  - "conjuntos de coleta [SQL Server], exibindo relatórios"
  - "relatórios [SQL Server], exibindo conjunto de coleta"
ms.assetid: c3b1e791-9aa1-4bba-9622-4954568e1820
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Exibir um relat&#243;rio de conjuntos de coleta (SQL Server Management Studio)
  Depois de configurar o data warehouse de gerenciamento, você pode exibir um relatório do conjunto de coleta no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os relatórios são fornecidos para os conjuntos de coleta de Dados do Sistema instalados durante a instalação. Os relatórios incluídos são:  
  
-   Resumo de Uso do Disco  
  
-   Histórico de Estatísticas de Consulta  
  
-   Histórico de Atividade do Servidor  
  
 Este procedimento exibe o relatório para o conjunto de coleta **Uso do Disco**. É possível seguir o mesmo procedimento geral para exibir os relatórios para os outros conjuntos de coleta de Dados do Sistema.  
  
### Para exibir um relatório de conjunto de coleta  
  
1.  As tabelas de um relatório são criadas apenas na primeira vez em que os dados coletados são carregados. Se você tentar exibir um relatório antes desse primeiro carregamento, ocorrerá um erro e nenhum relatório será exibido. Para carregar os dados do conjunto de coleta Uso do Disco, no Pesquisador de Objetos, expanda a pasta **Gerenciamento**, **Coleta de Dados** e **Conjuntos de Coleta de Dados do Sistema**, clique com o botão direito do mouse no conjunto de coleta **Uso do Disco** e clique em **Coletar e Carregar Agora**.  
  
2.  Para exibir o relatório, no Pesquisador de Objetos, expanda a pasta **Gerenciamento**, clique com o botão direito do mouse em **Coleta de Dados**, aponte para **Relatórios**, aponte para **Data Warehouse de Gerenciamento** e clique em **Resumo de Uso do Disco**.  
  
    > [!NOTE]  
    >  Alguns relatórios podem exibir um botão de calendário sob a linha de tempo de coleta de dados. Clique neste botão para acessar o **Calendário de Relatório de Coleta de Dados**.  
  
#### Calendário de relatórios da coleta de dados  
 Use essa caixa de diálogo para especificar a data e a hora de início e a duração dos dados que servirão de base para o relatório. Por exemplo, talvez você queira gerar um relatório sobre a atividade de utilização do disco de um servidor em um período de 12 horas específico da última quarta-feira.  
  
 **Data de início**  
 Digite uma data inicial para obter os dados do relatório ou selecione-a no calendário.  
  
 **Hora de início**  
 Digite uma hora inicial para obter os dados do relatório ou especifique-a clicando nas setas.  
  
 **Duration**  
 Especifique o intervalo de tempo que será incluído no relatório. O valor padrão é 240 minutos. Os valores disponíveis para seleção são 15 minutos, 60 minutos, 240 minutos (4 horas), 720 minutos (12 horas) e 1440 minutos (24 horas).  
  
## Consulte também  
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)   
 [Relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md)   
 [Configurar o Data Warehouse de Gerenciamento &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  