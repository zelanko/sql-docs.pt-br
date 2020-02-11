---
title: MSSQLSERVER_8651 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8651 (Database Engine error)
ms.assetid: 4cc3498d-5449-4c4e-b1f9-3271831c725a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 429956528484a11b26caf6c39a666ef933515314
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62762369"
---
# <a name="mssqlserver_8651"></a>MSSQLSERVER_8651
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8651|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|MEMGRANT_ERR|  
|Texto da mensagem|Não foi possível executar a operação solicitada porque o mínimo de memória para consulta não está disponível. Diminua o valor configurado para a opção de configuração de servidor 'min memory per query'.|  
  
## <a name="explanation"></a>Explicação  
 Outros processos estão usando memória do servidor (exercendo pressão de memória no servidor).  
  
## <a name="user-action"></a>Ação do usuário  
 Diminua o valor configurado para a opção de configuração de servidor 'min memory per query' ou reduza a carga de consultas no servidor.  
  
 Esta lista descreve etapas gerais que ajudarão a corrigir erros de memória:  
  
1.  Verifique se outros aplicativos ou serviços estão consumindo memória neste servidor. Reconfigure os aplicativos ou serviços menos críticos de maneira que eles consumam menos memória.  
  
2.  Comece a coletar contadores do monitor de desempenho relativos a **SQL Server: Gerenciador de Buffer**, **SQL Server: Gerenciador de Memória**.  
  
3.  Verifique os seguintes parâmetros de configuração da memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   **memória máxima do servidor**  
  
    -   **memória mínima do servidor**  
  
    -   **memória mínima por consulta**  
  
     Observe se há configurações incomuns. Corrija-as conforme necessário. As configurações padrão estão listadas em "Definindo opções de configuração do servidor" nos Manuais Online do SQL Server.  
  
4.  Verifique a carga de trabalho (por exemplo, o número de sessões simultâneas e de consultas em execução).  
  
 As seguintes ações podem disponibilizar mais memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se outros aplicativos além do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiverem consumindo recursos, experimente interrompê-los ou considere a possibilidade de executá-los em um servidor à parte. Isso eliminará a pressão de memória externa.  
  
-   Se você tiver configurado a opção **memória máxima do servidor**, aumente sua configuração.  
  
 Execute os comandos DBCC a seguir para liberar diversos caches de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 Se o problema persistir, será necessário aprofundar as investigações e possivelmente reduzir a carga de trabalho.  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC FREESYSTEMCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-freesystemcache-transact-sql)   
 [DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-freesessioncache-transact-sql)   
 [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-freeproccache-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [SQL Server, objeto Gerenciador de buffer](../performance-monitor/sql-server-buffer-manager-object.md)   
 [SQL Server, objeto gerenciador de memória](../performance-monitor/sql-server-memory-manager-object.md)  
  
  
