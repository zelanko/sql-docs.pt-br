---
title: 'Reparo automático de página (grupos de disponibilidade: espelhamento de banco de dados) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic page repair
- Availability Groups [SQL Server], automatic page repair
- database mirroring [SQL Server], automatic page repair
- suspect pages [SQL Server]
ms.assetid: cf2e3650-5fac-4f34-b50e-d17765578a8e
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3977d1893d009b9a427a28d4f320d31c1e747d03
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="automatic-page-repair-availability-groups-database-mirroring"></a>Reparo automático de página (grupos de disponibilidade: espelhamento de banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O reparo automático de página tem suporte do espelhamento de banco de dados e de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Depois que certos tipos de erros corrompem uma página, tornando-a ilegível, um parceiro de espelhamento de banco de dados (entidade de segurança ou espelho) ou uma réplica de disponibilidade (primária ou secundária) tenta recuperar a página automaticamente. O parceiro/réplica que não puder ler a página solicitará uma cópia atualizada da página do seu parceiro ou de outra réplica. Se essa solicitação tiver êxito, a página ilegível será substituída pela cópia legível. Isso costuma resolver o erro.  
  
 Em geral, o espelhamento de banco de dados e [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tratam erros de E/S de formas equivalentes. As poucas diferenças são destacadas explicitamente aqui.  
  
> [!NOTE]  
>  O reparo automático de página difere do reparo de DBCC. Todos os dados são preservados por um reparo automático de página. Por outro lado, a correção de erros usando a opção DBCC REPAIR_ALLOW_DATA_LOSS pode exigir que algumas páginas e, portanto, dados, sejam excluídos.  
  
-   [Tipos de erro que causam uma tentativa de reparo automático de página](#ErrorTypes)  
  
-   [Tipos de página que não podem ser reparados automaticamente](#UnrepairablePageTypes)  
  
-   [Manipulando erros de E/S no banco de dados principal/primário](#PrimaryIOErrors)  
  
-   [Manipulando erros de E/S no banco de dados espelho/secundário](#SecondaryIOErrors)  
  
-   [Prática recomendada de desenvolvedor](#DevBP)  
  
-   [Como exibir tentativas de reparo automático de página](#ViewAPRattempts)  
  
##  <a name="ErrorTypes"></a> Error Types That Cause an Automatic Page-Repair Attempt  
 O reparo automático de página do espelhamento de banco de dados tenta reparar apenas páginas em um arquivo de dados no qual houve falha na operação de um dos erros listados na tabela a seguir.  
  
|Número do erro|Description|Instâncias que causam uma tentativa de reparo automático de página|  
|------------------|-----------------|---------------------------------------------------------|  
|823|Ação realizada apenas se o sistema operacional tiver executado uma CRC (verificação de redundância cíclica) que falhou nos dados.|ERROR_CRC. O valor do sistema operacional desse erro é 23.|  
|824|Erros lógicos.|Erros de dados lógicos, como gravação interrompida ou soma de verificação de página inválida.|  
|829|Uma página foi marcada como restauração pendente.|Todos.|  
  
 Para exibir erros 823 CRC e erros 824 recentes, veja a tabela [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) no banco de dados [msdb](../../relational-databases/databases/msdb-database.md) .  

  
##  <a name="UnrepairablePageTypes"></a> Page Types That Cannot Be Automatically Repaired  
 O reparo automático de página não pode reparar os seguintes tipos de página de controle:  
  
-   Página de cabeçalho do arquivo (ID da página 0).  
  
-   Página 9 (a página de inicialização do banco de dados).  
  
-   Páginas de alocação: páginas GAM (Global Allocation Map), páginas SGAM (Shared Global Allocation Map) e páginas PFS (Page Free Space).  
  
 
##  <a name="PrimaryIOErrors"></a> Handling I/O Errors on the Principal/Primary Database  
 No banco de dados principal/primário, haverá a tentativa de reparo automático de página apenas quando o estado do banco de dados for SYNCHRONIZED e o principal/primário ainda estiver enviando registros de log do banco de dados ao espelho/secundário. A sequência básica de ações em uma tentativa de reparo automático de página é a seguinte:  
  
1.  Quando ocorre um erro de leitura em uma página de dados no banco de dados principal/primário, o principal/primário insere uma linha na tabela [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) com o status de erro apropriado. Para o espelhamento de banco de dados, o principal solicita uma cópia da página do espelho. Para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], o primário transmite a solicitação a todos os secundários e obtém a página do primeiro a responder. A solicitação especifica a ID da página e o LSN que estão atualmente na parte final do log liberado. A página é marcada como *restauração pendente*. Isso a torna inacessível durante a tentativa de reparo automático de página. Ocorrerá falha com o erro 829 nas tentativas de acesso a essa página durante a tentativa de reparo (restauração pendente).  
  
2.  Após o recebimento da solicitação de página, o espelho/secundário espera o log ser refeito para o LSN especificado na solicitação. Depois, o espelho/secundário tenta acessar a página em sua cópia do banco de dados. Se a página puder ser acessada, o espelho/secundário enviará a cópia da página ao principal/primário. Caso contrário, o espelho/secundário retornará um erro ao principal/primário e ocorrerá uma falha na tentativa de reparo automático de página.  
  
3.  O principal/primário processa a resposta que contém a cópia atualizada da página.  
  
4.  Depois que a tentativa de reparo automático de página reparar uma página suspeita, a página será marcada na tabela **suspect_pages** como restaurada (**event_type** = 5).  
  
5.  Se o erro de E/S de página causar quaisquer [transações adiadas](../../relational-databases/backup-restore/deferred-transactions-sql-server.md), após a página ser reparada, o principal/primário tentará resolver essas transações.  
  
 
##  <a name="SecondaryIOErrors"></a> Handling I/O Errors on the Mirror/Secondary Database  
 Os erros de E/S em páginas de dados que ocorrem no banco de dados espelho/secundário costumam ser tratados da mesma forma pelo espelhamento de banco de dados e pelo [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
1.  Com o espelhamento de banco de dados, se o espelho encontrar um ou mais erros de E/S de página ao refazer um registro de log, a sessão de espelhamento entrará no estado SUSPENDED. Com o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], se uma réplica secundária encontrar um ou mais erros de E/S de página ao refazer um registro de log, o banco de dados secundário entrará no estado SUSPENDED. Nesse ponto, o espelho/secundário insere uma linha na tabela **suspect_pages** com o status de erro apropriado. O espelho/secundário solicita uma cópia da página do principal/primário.  
  
2.  O principal/primário tenta acessar a página em sua cópia do banco de dados. Se a página puder ser acessada, o principal/primário enviará a cópia da página ao espelho/secundário.  
  
3.  Se o espelho/secundário receber cópias de cada página solicitada, ele tentará retomar a sessão de espelhamento. Se uma tentativa de reparo automático de página reparar uma página suspeita, a página será marcada na tabela **suspect_pages** como restaurada (**event_type** = 4).  
  
     Se um espelho/secundário não receber uma página solicitada do principal/primário, ocorrerá falha na tentativa de reparo automático de página. Com o espelhamento de banco de dados, a sessão de espelhamento permanece suspensa. Com o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], o banco de dados secundário permanece suspenso. Se a sessão de espelhamento ou o banco de dados secundário for retomado de forma manual, as páginas corrompidas serão acionadas novamente durante a fase de sincronização.  
  
 
##  <a name="DevBP"></a> Developer Best Practice  
 Um reparo automático de página é um processo assíncrono executado em segundo plano. Portanto, ocorre falha na operação de banco de dados que solicita uma página ilegível e o código de erro é retornado para qualquer condição que causou a falha. Ao desenvolver um aplicativo para um banco de dados espelho ou um banco de dados de disponibilidade, você deve interceptar as exceções para operações com falha. Se o código de erro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for 823, 824 ou 829, você deverá tentar novamente a operação mais tarde.  
  

##  <a name="ViewAPRattempts"></a> How To: View Automatic Page-Repair Attempts  
 As exibições de gerenciamento dinâmico a seguir retornam linhas para as últimas tentativas de reparo automático de página em determinado banco de dados de disponibilidade ou banco de dados espelho, com um máximo de 100 linhas por banco de dados.  
  
-   **Grupos de Disponibilidade AlwaysOn:**  
  
     [sys.dm_hadr_auto_page_repair &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
  
     Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados de disponibilidade em uma réplica de disponibilidade hospedada para qualquer grupo de disponibilidade pela instância do servidor.  
  
-   **Espelhamento de banco de dados:**  
  
     [sys.dm_db_mirroring_auto_page_repair &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)  
  
     Retorna uma linha para cada tentativa de reparo automático de página em qualquer banco de dados espelho na instância de servidor.  
  
 
## <a name="see-also"></a>Consulte Também  
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  


