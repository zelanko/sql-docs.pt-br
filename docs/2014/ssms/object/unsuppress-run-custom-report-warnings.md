---
title: Cancelar supressão da execução de avisos de relatório personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: stevestein
ms.author: sstein
ms.openlocfilehash: ae7f4d08ac613113d715728a5cb78ae37bd6f99b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058526"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Cancelar supressão da execução de avisos de relatório personalizado
  Há duas caixas de diálogo de aviso para relatórios personalizados. Este tópico descreve como cancelar a supressão da exibição dessas caixas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece antes da execução de um relatório personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais. Além disso, por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece quando você abre um relatório personalizado e, em seguida, clica em um link para abrir outro relatório personalizado. Essa caixa de diálogo exibe o caminho de preenchimento para o arquivo de relatório detalhado personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório personalizado principal  
  
1.  Conecte-se ao \<*Server*> \\ < *compartilhamento* >| \<*Drive*> \Documents and Settings \\<USERPROFILE \> \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Clique com o botão direito do mouse em `reports.xml` e clique em **Editar**.  
  
3.  Altere** \<SuppressWarning> true \</SuppressWarning> para \<SuppressWarning> false \</SuppressWarning> **.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório detalhado personalizado  
  
1.  Conecte-se ao \<*Server*> \\ < *compartilhamento* >| \<*Drive*> \Documents and Settings \\<USERPROFILE \> \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Clique com o botão direito do mouse `reports.xml` e clique em **Editar**.  
  
3.  Altere ** \<SuppressDrillthroughWarning> true \</SuppressDrillthroughWarning> para \<SuppressDrillthroughWarning> false \</SuppressDrillthroughWarning> **.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Relatórios personalizados no Management Studio](custom-reports-in-management-studio.md)   
 [Adicionar um relatório personalizado a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usar relatórios personalizados com propriedades de nó do Pesquisador de Objetos](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
