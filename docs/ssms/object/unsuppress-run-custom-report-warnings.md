---
title: Cancelar supressão da execução de avisos de relatório personalizado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef82982f5a18595c28fd8fb20a1ba28c43936f9d
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="unsuppress-run-custom-report-warnings"></a>Cancelar supressão da execução de avisos de relatório personalizado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Há duas caixas de diálogo de aviso para relatórios personalizados. Este tópico descreve como cancelar a supressão da exibição dessas caixas no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
Por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece antes da execução de um relatório personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais. Além disso, por padrão, a caixa de diálogo **Executar Relatórios Personalizados** aparece quando você abre um relatório personalizado e, em seguida, clica em um link para abrir outro relatório personalizado. Essa caixa de diálogo exibe o caminho de preenchimento para o arquivo de relatório detalhado personalizado. Se você marcar a caixa de seleção **Não mostrar este aviso novamente** , a caixa de diálogo não aparecerá mais.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório personalizado principal  
  
1.  Conecte-se a \<*Server*>\\<*Share*>|\<*Drive*>\Documents and Settings\\<UserProfile>\Application Data\Microsoft\Microsoft SQL Server\130\Tools\Shell\reports.xml.  
  
2.  Clique com o botão direito do mouse em **reports.xml**e clique em **Editar**.  
  
3.  Mude**<SuppressWarning>true\<\/SuppressWarning> para <SuppressWarning>false\<\/SuppressWarning>**.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Para cancelar a supressão da caixa de diálogo de aviso do relatório detalhado personalizado  
  
1.  Conecte-se a \<*Server*>\\<*Share*>|\<*Drive*>\Documents and Settings\\<UserProfile>\Application Data\Microsoft\Microsoft SQL Server\130\Tools\Shell\reports.xml.  
  
2.  Clique com o botão direito do mouse em **reports.xml**e clique em **Editar**.  
  
3.  Mude **<SuppressDrillthroughWarning>true\<\/SuppressDrillthroughWarning> para <SuppressDrillthroughWarning>false\<\/SuppressDrillthroughWarning>**.  
  
4.  Reinicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
[adicionar um relatório personalizado ao Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[Usar relatórios personalizados com propriedades de nó do Pesquisador de Objetos](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
