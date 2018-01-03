---
title: Objetos com suporte no Assistente para Gerar Scripts | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b775783cf11a74bbf5ddfd2641f8dc6b483a6ff
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos com suporte no Assistente para Gerar Scripts
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] O Assistente para Gerar e Publicar Scripts dá suporte a um subconjunto dos objetos compatíveis com o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos com suporte  
 A seguinte tabela lista os objetos que podem ser publicados e as versões com suporte do Assistente para Gerar e Publicar Scripts.  
  
||||||  
|-|-|-|-|-|  
|Função de aplicativo|Função de banco de dados|esquema|Agregação definida pelo usuário|Exibição*|  
|Assembly|Restrição DEFAULT|Procedimento armazenado*|Tipo de dados definido pelo usuário|Coleção de esquemas XML|  
|Restrição CHECK|Catálogo de texto completo|Sinônimo|Função definida pelo usuário||  
|Procedimento armazenado CLR (common language runtime)*|Índice|Table|Tabela definida pelo usuário||  
|Função CLR definida pelo usuário|Regra|Usuário**|Tipo definido pelo usuário||  
  
 *Publicado sem criptografia.  
  
 **Qualquer usuário que não seja do sistema existente no banco de dados será publicado como Funções.  
  
  
