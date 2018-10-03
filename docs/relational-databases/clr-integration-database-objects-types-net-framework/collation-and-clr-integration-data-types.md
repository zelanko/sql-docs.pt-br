---
title: Tipos de dados de integração de CLR e agrupamento | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f99bb2f8aac2278fd25713ce43e23e1a5f1d14a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678304"
---
# <a name="collation-and-clr-integration-data-types"></a>Tipos de dados de integração CLR e agrupamento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  No [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], o **CompareInfo** agrupamentos alças do objeto. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] aplicativo usar interfaces de programação (APIs) da cadeia de caracteres de **CompareInfo** propriedade associada a **CultureInfo** objeto do thread atual para executar comparações de cadeia de caracteres. A configuração padrão do **CultureInfo** objeto se baseia o [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuração de localidade do Windows para o computador no qual [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. Isso determina a semântica de comparação padrão, se não explícita **CultureInfo** for especificado, para comparações de **System. String** valores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não altera explicitamente o **CompareInfo** propriedade para o agrupamento de banco de dados ou servidor. Se necessário, os usuários devem definir apropriado **CompareInfo** propriedade em suas rotinas.  
  
## <a name="parameter-collation"></a>Agrupamento de parâmetros  
 Quando você cria uma rotina do common language runtime (CLR), e um parâmetro de um método CLR associado para a rotina é do tipo **SQLString**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma instância do parâmetro com o agrupamento padrão do banco de dados que contém a rotina de chamada. Se um parâmetro não é um **SqlType** (por exemplo, **cadeia de caracteres** vez **SQLString**), as informações de agrupamento do banco de dados não estão associadas com o parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
