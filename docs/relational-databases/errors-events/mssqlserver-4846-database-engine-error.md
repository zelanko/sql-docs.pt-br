---
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0b9152072fde4c139602eecef4a182e3e2cd1300
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver4846"></a>MSSQLSERVER_4846
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|4846|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BULKPROV_MEMORY|  
|Texto da mensagem|Falha no provedor de dados em massa ao alocar memória.|  
  
## <a name="explanation"></a>Explicação  
Falha na alocação de memória.  
  
## <a name="user-action"></a>Ação do usuário  
Siga estas etapas gerais para solucionar os erros de memória:  
  
1.  Verifique se outros aplicativos ou serviços estão consumindo memória neste servidor. Reconfigure os aplicativos ou serviços menos críticos de maneira que eles consumam menos memória.  
  
2.  Comece a coletar contadores do monitor de desempenho relativos a **SQL Server: Gerenciador de Buffer**, **SQL Server: Gerenciador de Memória**.  
  
3.  Verifique os seguintes parâmetros de configuração da memória do SQL Server:  
  
    -   **memória máxima do servidor**  
  
    -   **memória mínima do servidor**  
  
    -   **memória mínima por consulta**  
  
    Observe todas as configurações incomuns. Corrija-as conforme necessário. Considere os requisitos de memória para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. As configurações padrão estão listadas em "Definindo opções de configuração do servidor" nos Manuais Online do SQL Server.  
  
4.  Observe o resultado do DBCC MEMORYSTATUS e a forma como ele se altera quando você vê essas mensagens de erro.  
  
5.  Verifique a carga de trabalho (por exemplo, o número de sessões simultâneas e de consultas em execução).  
  
As seguintes ações podem disponibilizar mais memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se outros aplicativos além do SQL Server estiverem consumindo recursos, tente parar a execução desses aplicativos ou considere a possibilidade de executá-los em outro servidor. Isso eliminará a pressão de memória externa.  
  
-   Se você tiver configurado a opção **memória máxima do servidor**, aumente sua configuração.  
  
Execute os comandos DBCC a seguir para liberar diversos caches de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Se o problema persistir, será necessário aprofundar as investigações e possivelmente reduzir a carga de trabalho.  
  

