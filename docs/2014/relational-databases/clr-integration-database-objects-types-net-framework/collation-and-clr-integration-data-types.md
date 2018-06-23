---
title: Tipos de dados de integração de CLR e agrupamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 71b0c61678bff1be69cbb761dd00067150a30b0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120811"
---
# <a name="collation-and-clr-integration-data-types"></a>Tipos de dados de integração CLR e agrupamento
  No [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], o objeto `CompareInfo` trata os agrupamentos. As APIs de cadeia de caracteres do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usam a propriedade `CompareInfo` associada com o objeto `CultureInfo` do thread atual para executar comparações de cadeias de caracteres. A configuração padrão da `CultureInfo` objeto se baseia o [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuração de localidade do Windows para o computador no qual [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. Isso determina a semântica de comparação padrão, se nenhum `CultureInfo` explícito for especificado, para comparações de valores de `System.String`. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não altera explicitamente a propriedade `CompareInfo` para o agrupamento do servidor ou banco de dados. Se necessário, os usuários devem definir a propriedade `CompareInfo` apropriada em suas rotinas.  
  
## <a name="parameter-collation"></a>Agrupamento de parâmetros  
 Quando você cria uma rotina CLR (Common Language Runtime) e um parâmetro de um método CLR associado à rotina é do tipo `SQLString`, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma instância do parâmetro com o agrupamento padrão do banco de dados que contém a rotina que fez a chamada. Se um parâmetro não for um `SqlType` (por exemplo, `String` em vez de `SQLString`), as informações de agrupamento do banco de dados não são associadas com o parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  