---
title: MSSQLSERVER_701 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 701 (Database Engine error)
ms.assetid: 3b975000-63a1-43c2-a40f-89d0a8a36bef
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 530d1c42d83d2390d67906f601d0a255b0db1a78
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver701"></a>MSSQLSERVER_701
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|701|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NOSYSMEM|  
|Texto da mensagem|Não há memória de sistema suficiente para executar essa consulta.|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhou ao alocar memória suficiente para executar a consulta. Isso pode ser causado por várias razões, incluindo as configurações do sistema operacional, disponibilidade de memória física ou limites de memória na carga de trabalho atual. Na maioria dos casos, a transação que falhou não é a causa do erro.  
  
As consultas de diagnósticos, como instruções DBCC, podem falhar porque o servidor não tem memória suficiente.  
  
Tempo limite excedido ao aguardar recursos de memória para executar a consulta no pool de recursos 'default'.  
  
## <a name="user-action"></a>Ação do usuário  
Se você não estiver usando o Administrador de Recursos, nós recomendamos que você verifique o estado de servidor geral e a carga ou verifique o pool de recursos ou as configurações do grupo de cargas de trabalho.  
  
Esta lista descreve etapas gerais que ajudarão a corrigir erros de memória:  
  
1.  Verifique se outros aplicativos ou serviços estão consumindo memória neste servidor. Reconfigure os aplicativos ou serviços menos críticos de maneira que eles consumam menos memória.  
  
2.  Comece a coletar contadores do monitor de desempenho relativos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Gerenciador de Buffer**, **SQL Server: Gerenciador de Memória**.  
  
3.  Verifique os seguintes parâmetros de configuração da memória do SQL Server:  
  
    -   **memória máxima do servidor**  
  
    -   **memória mínima do servidor**  
  
    -   **memória mínima por consulta**  
  
    Observe se há configurações incomuns. Corrija-as conforme necessário. Considere mais requisitos de memória. As configurações padrão estão listadas em "Definindo opções de configuração do servidor" nos Manuais Online do SQL Server.  
  
4.  Observe o resultado do DBCC MEMORYSTATUS e a forma como ele se altera quando você vê essas mensagens de erro.  
  
5.  Verifique a carga de trabalho (por exemplo, o número de sessões simultâneas e de consultas em execução).  
  
As seguintes ações podem disponibilizar mais memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se outros aplicativos além do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiverem consumindo recursos, experimente interrompê-los ou considere a possibilidade de executá-los em um servidor à parte. Isso eliminará a pressão de memória externa.  
  
-   Se você tiver configurado a opção **memória máxima do servidor**, aumente sua configuração.  
  
Execute os comandos DBCC a seguir para liberar diversos caches de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Se o problema persistir, será necessário aprofundar as investigações e possivelmente reduzir a carga de trabalho.  
  
