---
title: MSSQLSERVER_8645 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8645 (Database Engine error)
ms.assetid: 63d6d6d7-3850-4061-8e96-b1fa665e3180
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7a039055daf8574d0c6b217c26d6f5572dd015c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62762561"
---
# <a name="mssqlserver_8645"></a>MSSQLSERVER_8645
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8645|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|MEMTIMEDOUT_ERR|  
|Texto da mensagem|O tempo limite expirou enquanto aguardava por recursos de memória para executar a consulta. Execute a consulta novamente.|  
  
## <a name="explanation"></a>Explicação  
 Tempo limite excedido ao aguardar recursos de memória para executar a consulta no pool de recursos 'default'.  
  
## <a name="user-action"></a>Ação do usuário  
 Se você não estiver usando o Administrador de Recursos, nós recomendamos que você verifique o estado de servidor geral e a carga ou verifique o pool de recursos ou as configurações do grupo de cargas de trabalho.  
  
 Esta lista descreve etapas gerais que ajudarão a corrigir erros de memória:  
  
1.  Verifique se outros aplicativos ou serviços estão consumindo memória neste servidor. Reconfigure os aplicativos ou serviços menos críticos de maneira que eles consumam menos memória.  
  
2.  Comece a coletar contadores do monitor de desempenho relativos a **SQL Server: Gerenciador de Buffer**, **SQL Server: Gerenciador de Memória**.  
  
3.  Verifique os seguintes parâmetros de configuração da memória do SQL Server:  
  
    -   **memória máxima do servidor**  
  
    -   **memória mínima do servidor**  
  
    -   **memória mínima por consulta**  
  
     Observe se há configurações incomuns. Corrija-as conforme necessário. Considere os requisitos de memória aumentados para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. As configurações padrão estão listadas em "Definindo opções de configuração do servidor" nos Manuais Online do SQL Server.  
  
4.  Observe o resultado do DBCC MEMORYSTATUS e a forma como ele se altera quando você vê essas mensagens de erro.  
  
5.  Verifique a carga de trabalho (por exemplo, o número de sessões simultâneas e de consultas em execução).  
  
 As seguintes ações podem disponibilizar mais memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se outros aplicativos além do SQL Server estiverem consumindo recursos, tente parar a execução desses aplicativos ou considere a possibilidade de executá-los em outro servidor. Isso eliminará a pressão de memória externa.  
  
-   Se você tiver configurado a opção **memória máxima do servidor**, aumente sua configuração.  
  
 Execute os comandos DBCC a seguir para liberar diversos caches de memória do SQL Server.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 Se o problema persistir, será necessário aprofundar as investigações e possivelmente reduzir a carga de trabalho.  
  
  
