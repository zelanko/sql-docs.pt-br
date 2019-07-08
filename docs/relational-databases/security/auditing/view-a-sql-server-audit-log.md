---
title: Exibir um log de auditoria do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 78de1b6e053134a6bf1ab4f19b7ea6791d17a71c
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581144"
---
# <a name="view-a-sql-server-audit-log"></a>Exibir um log auditoria do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como exibir um log de auditoria do SQL Server no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir um log de auditoria do SQL Server usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão **CONTROL SERVER** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Para exibir um log de auditoria do SQL Server  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Expanda a pasta **Auditorias** .  
  
3.  Clique com o botão direito do mouse no log de auditoria que você deseja exibir e selecione **Exibir Logs de Auditoria**. Isso abre a caixa de diálogo **Visualizador de Arquivo de Log -** _server\_name_. Para obter mais informações, consulte [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
4.  Quando terminar, clique em **Fechar**.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda exibir o log de auditoria usando o Visualizador do Arquivo de Log. No entanto, se você estiver criando um sistema de monitoramento automatizado, as informações no arquivo de auditoria podem ser lidas diretamente usando a função [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). Ler o arquivo diretamente retorna dados em um formato ligeiramente diferente (não processado). Veja **sys.fn_get_audit_file** para obter mais informações.  
  
## <a name="see-also"></a>Consulte Também  
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Gravar eventos de auditoria do SQL Server no log de segurança](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
