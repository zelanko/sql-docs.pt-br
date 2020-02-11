---
title: Tipos de dados de integração de agrupamento e CLR | Microsoft Docs
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
ms.openlocfilehash: 51345c498277cc7013bbc05784022f65d77aef65
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081342"
---
# <a name="collation-and-clr-integration-data-types"></a>Tipos de dados de integração CLR e ordenação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  No [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], o objeto **CompareInfo** manipula agrupamentos. As [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] APIs (interfaces de programação de aplicativo) de cadeia de caracteres usam a propriedade **CompareInfo** associada ao objeto **CultureInfo** do thread atual para executar comparações de cadeia de caracteres. A configuração padrão do objeto **CultureInfo** baseia-se na configuração [!INCLUDE[msCoName](../../includes/msconame-md.md)] de localidade do Windows para o computador no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qual o está em execução. Isso determina a semântica de comparação padrão, se nenhum **CultureInfo** explícito for especificado, para comparações de valores **System. String** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Não altera explicitamente a propriedade **CompareInfo** para o agrupamento do banco de dados ou do servidor. Se necessário, os usuários devem definir a propriedade **CompareInfo** apropriada em suas rotinas.  
  
## <a name="parameter-collation"></a>Ordenação de parâmetros  
 Quando você cria uma rotina de Common Language Runtime (CLR) e um parâmetro de um método CLR associado à rotina é do tipo **SqlString**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o cria uma instância do parâmetro com o agrupamento padrão do banco de dados que contém a rotina de chamada. Se um parâmetro não for um **SqlType** (por exemplo, **cadeia de caracteres** em vez de **SqlString**), as informações de agrupamento do banco de dados não serão associadas ao parâmetro.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do SQL Server no .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
