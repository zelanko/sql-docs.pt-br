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
manager: craigg
ms.openlocfilehash: ed653b16fe524f364ba89f13e00715b725080033
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62824385"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Cancelar supressão da execução de avisos de relatório personalizado
  Há duas caixas de diálogo de aviso para relatórios personalizados. Este tópico descreve como cancelar a supressão da exibição dessas caixas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece antes da execução de um relatório personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais. Além disso, por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece quando você abre um relatório personalizado e, em seguida, clica em um link para abrir outro relatório personalizado. Essa caixa de diálogo exibe o caminho de preenchimento para o arquivo de relatório detalhado personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório personalizado principal  
  
1.  Conectar- \<se à*unidade* de*compartilhamento*>|\< *do servidor*>\\<> \Documents\>and Settings\\<UserProfile \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Clique `reports.xml`com o botão direito do mouse em e clique em **Editar**.  
  
3.  Altere**\<SuppressWarning>true\</SuppressWarning> para \<SuppressWarning>false\</SuppressWarning>**.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório detalhado personalizado  
  
1.  Conectar- \<se à*unidade* de*compartilhamento*>|\< *do servidor*>\\<> \Documents\>and Settings\\<UserProfile \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Clique `reports.xml`com o botão direito do mouse e clique em **Editar**.  
  
3.  Altere ** \<SuppressDrillthroughWarning>true\</SuppressDrillthroughWarning>para \<SuppressDrillthroughWarning>false\</SuppressDrillthroughWarning>**.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Relatórios personalizados no Management Studio](custom-reports-in-management-studio.md)   
 [Adicionar um relatório personalizado a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usar relatórios personalizados com propriedades de nó do Pesquisador de Objetos](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
