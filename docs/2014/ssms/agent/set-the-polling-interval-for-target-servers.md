---
title: Definir o intervalo de sondagem para servidores de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- interval for polling [SQL Server]
- target servers [SQL Server], polling interval
- polling interval [SQL Server]
ms.assetid: 4ffbbefa-77fb-442e-a77c-cb8c6cab9f3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1578bbefc9ae17baae56799d943e5ae6186628ea
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818678"
---
# <a name="set-the-polling-interval-for-target-servers"></a>Definir o intervalo de sondagem para servidores de destino
  Este tópico descreve como definir a frequência com que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent atualiza as informações do servidor mestre para os servidores de destino. Um trabalho é uma série especificada de ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa. Um trabalho multisservidor é um trabalho executado por um servidor mestre em um ou mais servidores de destino.  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
-   **Para definir o intervalo de sondagem para servidores de destino usando:**  [SQL Server Management Studio](#SSMS), [Transact-SQL](#TSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Cada servidor de destino pode executar uma instância do mesmo trabalho ao mesmo tempo. Cada servidor de destino sonda o servidor mestre periodicamente, baixa uma cópia dos eventuais trabalhos novos a ele atribuídos e, em seguida, desconecta-se. O servidor de destino executa o trabalho localmente e, depois, reconecta-se ao servidor mestre para carregar o status do resultado do trabalho.  
  
> [!NOTE]  
>  Se o servidor mestre não estiver acessível quando o servidor de destino tentar carregar o status do trabalho, este será colocado em spool até que o servidor mestre esteja novamente acessível.  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) e [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
 **Para definir o intervalo de sondagem de servidores de destino**  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Gerenciar Servidores de Destino**.  
  
3.  Na guia **Status do Servidor de Destino** , clique em **Postar Instruções**.  
  
4.  Na lista **Tipo de instrução** , selecione **Definir intervalo de sondagem**.  
  
5.  Na caixa **Intervalo de sondagem** , insira o número de segundos, de 10 a 28.800, a decorrer entre uma sondagem e outra do servidor mestre pelo servidor de destino.  
  
6.  Em **Destinatários**, siga um destes procedimentos:  
  
    1.  Clique em **Todos os servidores de destino** se todos os servidores de destino compartilharem o mesmo intervalo de sondagem.  
  
    2.  Clique em **Estes servidores de destino** se nem todos os servidores de destino compartilharem o mesmo intervalo de sondagem, e selecione cada servidor de destino que usará o intervalo de sondagem que está sendo definido.  
  
##  <a name="TSQL"></a> Usando Transact-SQL  
 **Para definir o intervalo de sondagem de servidores de destino**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do Mecanismo de Banco de Dados e expanda-a.  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, use o [sp_post_msx_operation &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql) procedimento para definir o intervalo de sondagem para servidores de destino armazenado do sistema.  
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysdownloadlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysdownloadlist-transact-sql)  
  
  
