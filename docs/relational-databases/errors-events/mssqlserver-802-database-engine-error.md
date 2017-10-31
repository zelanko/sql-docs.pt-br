---
title: "MSSQLSERVER_802 – erro do mecanismo de banco de dados | Microsoft Docs"
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
- 802 (Database Engine error)
ms.assetid: 5892ed24-4dcb-4bf9-a8a4-a7ca898832d5
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83a4a02b0977f3a1b9feec0ad720aef6728cb906
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver802---database-engine-error"></a>MSSQLSERVER_802 – erro do mecanismo de banco de dados
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|802|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NO_BUFS|  
|Texto da mensagem|Não há memória suficiente disponível no pool de buffers.|  
  
## <a name="explanation"></a>Explicação  
Isso ocorre quando o pool de buffers está cheio e não pode ficar maior.  
  
## <a name="user-action"></a>Ação do usuário  
Esta lista descreve etapas gerais que ajudarão a corrigir erros de memória:  
  
1.  Verifique se outros aplicativos ou serviços estão consumindo memória neste servidor. Reconfigure os aplicativos ou serviços menos críticos de maneira que eles consumam menos memória.  
  
2.  Comece a coletar contadores do monitor de desempenho para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: gerenciador de buffer**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: gerenciador de memória**.  
  
3.  Verifique os seguintes parâmetros de configuração da memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   **memória máxima do servidor**  
  
    -   **memória mínima do servidor**  
  
    -   **memória mínima por consulta**  
  
    Observe todas as configurações incomuns e corrija-as conforme suas necessidades. Considere os requisitos de memória aumentados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As configurações padrão estão listadas em "Definindo opções de configuração do servidor" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Observe o resultado do DBCC MEMORYSTATUS e a forma como ele se altera quando você vê essas mensagens de erro.  
  
5.  Verifique a carga de trabalho (o número de sessões simultâneas, consultas em execução atualmente).  
  
As seguintes ações podem disponibilizar mais memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se outros aplicativos além do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiverem consumindo recursos, tente parar esses aplicativos ou executá-los em um servidor separado.  
  
-   Se você tiver configurado a **memória máxima do servidor**, aumente a configuração.  
  
Execute os comandos DBCC a seguir para liberar diversos caches de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Se o problema persistir, será necessário aprofundar as investigações e possivelmente reduzir a carga de trabalho.  
  

