---
description: MSSQLSERVER_4846
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9654cb637d07bb8bbf658e0daecc4361c195b81d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471018"
---
# <a name="mssqlserver_4846"></a>MSSQLSERVER_4846
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|4846|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BULKPROV_MEMORY|  
|Texto da mensagem|Falha no provedor de dados em massa ao alocar memória.|  
  
## <a name="explanation"></a>Explicação  
Falha na alocação de memória.  
  
## <a name="user-action"></a>Ação do usuário  
Siga estas etapas gerais para solucionar os erros de memória:  
  
1.  Verifique se outros aplicativos ou serviços estão consumindo memória neste servidor. Reconfigure os aplicativos ou serviços menos críticos de maneira que eles consumam menos memória.  
  
2.  Comece a coletar contadores do monitor de desempenho para o **SQL Server: Gerenciador de Buffer**, **SQL Server: Gerenciador de Memória**.  
  
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
  
