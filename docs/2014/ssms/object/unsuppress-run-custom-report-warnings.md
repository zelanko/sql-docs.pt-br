---
title: Cancelar supressão da execução de avisos de relatório personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d303321941668d5115c3796022f70195b4a0d066
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122762"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Cancelar supressão da execução de avisos de relatório personalizado
  Há duas caixas de diálogo de aviso para relatórios personalizados. Este tópico descreve como cancelar a supressão da exibição dessas caixas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece antes da execução de um relatório personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais. Além disso, por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece quando você abre um relatório personalizado e, em seguida, clica em um link para abrir outro relatório personalizado. Essa caixa de diálogo exibe o caminho de preenchimento para o arquivo de relatório detalhado personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório personalizado principal  
  
1.  Conecte-se ao \< *servidor*>\\<*compartilhamento*>|\<*unidade*> \ Documents and Settings\\< UserProfile\>data\microsoft\microsoft SQL server\120\tools\shell\reports.XML.  
  
2.  Clique com botão direito `reports.xml`e, em seguida, clique em **editar**.  
  
3.  Alterar**\<SuppressWarning > true\</SuppressWarning > para \<SuppressWarning > false\</SuppressWarning >**.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório detalhado personalizado  
  
1.  Conecte-se ao \< *servidor*>\\<*compartilhamento*>|\<*unidade*> \ Documents and Settings\\< UserProfile\>data\microsoft\microsoft SQL server\120\tools\shell\reports.XML.  
  
2.  Clique com botão direito `reports.xml`e clique em **editar**.  
  
3.  Alterar  **\<SuppressDrillthroughWarning > true\</SuppressDrillthroughWarning > para \<SuppressDrillthroughWarning > false\</SuppressDrillthroughWarning >**.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Relatórios personalizados no Management Studio](custom-reports-in-management-studio.md)   
 [Adicionar um relatório personalizado ao Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usar relatórios personalizados com propriedades de nó do Pesquisador de Objetos](use-custom-reports-with-object-explorer-node-properties.md)  
  
  