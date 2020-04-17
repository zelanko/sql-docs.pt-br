---
title: Tipos de dados de integração de colagem e CLR | Microsoft Docs
description: Na integração SQL Server CLR, as APIs da seqüência de caracteres .NET Framework usam a propriedade CompareInfo do CultureInfo do segmento atual para executar comparações de seqüência.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
ms.openlocfilehash: 46e4d450db90e4bfc93187a48ca8adae472036c6
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488469"
---
# <a name="collation-and-clr-integration-data-types"></a>Tipos de dados de integração CLR e ordenação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  No [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]objeto **CompareInfo,** o objeto CompareInfo lida com colagens. As [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] APIs (String Application Programming Interfaces, interfaces de programação de aplicativos de string) usam a propriedade **CompareInfo** associada ao objeto **CultureInfo** do segmento atual para realizar comparações de strings. A configuração padrão do objeto **CultureInfo** é baseada na [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuração do local do Windows para o computador no qual [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado. Isso determina a semântica de comparação padrão, se não for especificado **o CultureInfo** explícito, para comparações de valores **do System.String.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não altera explicitamente a propriedade **CompareInfo** para o banco de dados ou a colagem do servidor. Se necessário, os usuários devem definir a propriedade **compareInfo** apropriada em suas rotinas.  
  
## <a name="parameter-collation"></a>Ordenação de parâmetros  
 Quando você cria uma rotina de tempo de execução de linguagem comum (CLR) e um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parâmetro de um método CLR vinculado à rotina é do tipo **SQLString,** cria uma instância do parâmetro com a colagem padrão do banco de dados contendo a rotina de chamada. Se um parâmetro não for um **SqlType** (por exemplo, **String** em vez de **SQLString),** as informações de colagem do banco de dados não estão associadas ao parâmetro.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
