---
title: Abrir o Visualizador do Arquivo de Log | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer, opening
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9e76c7eb85306f63e9be230c76159efbab25444a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68083980"
---
# <a name="open-log-file-viewer"></a>Abrir o Visualizador do Arquivo de Log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  É possível usar o Visualizador do Arquivo de Log no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para acessar informações sobre erros e eventos capturados nos seguintes logs:  
  
-   Coleta de Auditoria  
  
-   Coleta de dados  
  
-   Database Mail  
  
-   Histórico de Trabalhos  
  
-   SQL Server  
  
-   SQL Server Agent  
  
-   Eventos do Windows (esses eventos também podem ser acessados no Visualizador de Eventos do Windows.)  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode usar Servidores Registrados para exibir arquivos de log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instâncias locais ou remotas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usando Servidores Registrados, você poderá exibir os arquivos de log quando as instâncias forem online ou offline. Para obter mais informações sobre o acesso online, veja o procedimento “Para exibir arquivos de log online de Servidores Registrados”, mais adiante neste tópico. Para obter mais informações sobre como acessar arquivos de log offline do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
 Você pode abrir o Visualizador do Arquivo de Log de várias maneiras, dependendo das informações que você deseja exibir.  
  
##  <a name="BeforeYouBegin"></a> Permissões  
 Para acessar arquivos de log de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão online, é necessária associação na função de servidor fixa securityadmin.  
  
 Para acessar arquivos de log de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão offline, é necessário ter acesso de leitura no namespace do WMI **Root\Microsoft\SqlServer\ComputerManagement10** e na pasta em que os arquivos de log estão armazenados. Para obter mais informações, veja a seção Segurança do tópico [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
### <a name="security"></a>Segurança  
 Exige associação à função de servidor fixa securityadmin.  
  
### <a name="view-log-files"></a>Exibir Arquivos de Log  
  
##### <a name="to-view-logs-that-are-related-to-general-sql-server-activity"></a>Para exibir logs relacionados a atividades gerais do SQL Server  
  
1.  No Pesquisador de Objetos, expanda **Gerenciamento**.  
  
2.  Execute um destes procedimentos:  
  
    -   Clique com o botão direito do mouse em **Logs do SQL Server**, aponte para **Exibir**e clique em **Log do SQL Server** ou em **Log do SQL Server e do Windows**.  
  
    -   Expanda **Logs do SQL Server**, clique com o botão direito do mouse em qualquer arquivo de log e clique em **Exibir Log do SQL Server**. Você também pode clicar duas vezes em qualquer arquivo de log.  
  
     Os logs incluem **Database Mail**, **SQL Server**, **SQL Server Agent**e **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-jobs"></a>Para exibir logs relacionados a trabalhos  
  
-   No Pesquisador de Objetos, expanda **SQL Server Agent**, clique com o botão direito do mouse em **Trabalhos**e clique em **Exibir Histórico**.  
  
     Os logs incluem **Database Mail**, **Histórico de Trabalhos**e **SQL Server Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-maintenance-plans"></a>Para exibir logs relacionados a planos de manutenção  
  
-   No Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Planos de Manutenção**e clique em **Exibir Histórico**.  
  
     Os logs incluem **Database Mail**, **Histórico do Trabalho**, **Planos de Manutenção**, **Planos de Manutenção Remotos**e **SQL Server Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-data-collection"></a>Para exibir logs relacionados à Coleção de Dados  
  
-   No Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Coleção de Dados**e clique em **Exibir Logs**.  
  
     Os logs incluem **Coleta de Dados**, **Histórico de Trabalhos**e **SQL Server Agent**.  
  
##### <a name="to-view-logs-that-are-related-to-database-mail"></a>Para exibir logs relacionados ao Database Mail  
  
-   No Pesquisador de Objetos, expanda **Gerenciamento**, clique com o botão direito do mouse em **Database Mail**e clique em **Exibir Log do Database Mail**.  
  
     Os logs incluem **Database Mail, Histórico de Trabalhos**, **Planos de Manutenção**, **Planos de Manutenção Remotos**, **SQL Server**, **SQL Server Agent**e **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>Para exibir logs relacionados a coletas de auditorias  
  
-   No Pesquisador de Objetos, expanda **Segurança**e **Auditorias**, clique com o botão direito do mouse em uma auditoria e clique em **Exibir Logs de Auditoria**.  
  
     Os logs incluem **Coleta de Auditoria** e **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>Para exibir logs relacionados a coletas de auditorias  
  
-   No Pesquisador de Objetos, expanda **Segurança**e **Auditorias**, clique com o botão direito do mouse em uma auditoria e clique em **Exibir Logs de Auditoria**.  
  
     Os logs incluem **Coleta de Auditoria** e **Windows NT**.  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer.md)   
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
