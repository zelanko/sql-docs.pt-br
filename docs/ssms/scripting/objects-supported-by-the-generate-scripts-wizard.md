---
title: Objetos com suporte no Assistente para Gerar Scripts
description: Confira quais tipos de objetos o Assistente para Gerar e Publicar Scripts pode ajudar você a publicar.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ba406c4418979f4cdc57363806c9561b3480959
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474267"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos com suporte no Assistente para Gerar Scripts
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  O Assistente para Gerar e Publicar Scripts oferece suporte a um subconjunto dos objetos com suporte no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos com suporte  
 A seguinte tabela lista os objetos que podem ser publicados e as versões com suporte do Assistente para Gerar e Publicar Scripts.  
  
:::row:::
    :::column:::
        Função de aplicativo
    :::column-end:::
    :::column:::
        Função de banco de dados
    :::column-end:::
    :::column:::
        Esquema
    :::column-end:::
    :::column:::
        Agregação definida pelo usuário
    :::column-end:::
    :::column:::
        Exibição*
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Assembly
    :::column-end:::
    :::column:::
        Restrição DEFAULT
    :::column-end:::
    :::column:::
        Procedimento armazenado*
    :::column-end:::
    :::column:::
        Tipo de dados definido pelo usuário
    :::column-end:::
    :::column:::
        Coleção de esquemas XML
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Restrição CHECK
    :::column-end:::
    :::column:::
        Catálogo de texto completo
    :::column-end:::
    :::column:::
        Sinônimo
    :::column-end:::
    :::column:::
        Função definida pelo usuário
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Procedimento armazenado CLR (common language runtime)*
    :::column-end:::
    :::column:::
        Índice
    :::column-end:::
    :::column:::
        Tabela
    :::column-end:::
    :::column:::
        Tabela definida pelo usuário
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Função CLR definida pelo usuário
    :::column-end:::
    :::column:::
        Regra
    :::column-end:::
    :::column:::
        Usuário**
    :::column-end:::
    :::column:::
        Tipo definido pelo usuário
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

 *Publicado sem criptografia.  
  
 **Qualquer usuário que não seja do sistema existente no banco de dados será publicado como Funções.  
  
  
