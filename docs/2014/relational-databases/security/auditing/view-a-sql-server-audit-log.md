---
title: Exibir um log de auditoria do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 80b20cf0c2de76f4b693560ff2ad4abd4b07f755
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117632"
---
# <a name="view-a-sql-server-audit-log"></a>Exibir um log auditoria do SQL Server
  Este tópico descreve como exibir um log de auditoria do SQL Server no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir um log de auditoria do SQL Server usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão `CONTROL SERVER`.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Para exibir um log de auditoria do SQL Server  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Expanda a pasta **Auditorias** .  
  
3.  Clique com o botão direito do mouse no log de auditoria que você deseja exibir e selecione **Exibir Logs de Auditoria**. Isso abrirá a caixa de diálogo *Visualizador de Arquivo de Log –***server_name*. Para obter mais informações, consulte [Log File Viewer F1 Help](../../logs/log-file-viewer-f1-help.md).  
  
4.  Quando terminar, clique em **Fechar**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda exibir o log de auditoria usando o Visualizador do Arquivo de Log. No entanto, se você estiver criando um sistema de monitoramento automatizado, as informações no arquivo de auditoria podem ser lidas diretamente usando a função [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql). Ler o arquivo diretamente retorna dados em um formato ligeiramente diferente (não processado). Consulte **sys.fn_get_audit_file** para obter mais informações  
  
## <a name="see-also"></a>Consulte também  
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](sql-server-audit-database-engine.md)   
 [Gravar eventos de auditoria do SQL Server no log de segurança](write-sql-server-audit-events-to-the-security-log.md)  
  
  
