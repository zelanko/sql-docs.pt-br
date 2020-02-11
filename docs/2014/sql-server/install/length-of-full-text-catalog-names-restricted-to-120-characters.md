---
title: Comprimento de nomes de catálogo de texto completo restritos a 120 caracteres | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs names
ms.assetid: 50633373-83f6-4ed9-99b9-71f92479a14f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5cce05426fdff2aacf40612738ad80b07d9ec0e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094057"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>Comprimento dos nomes de catálogo de texto completo restrito a 120 caracteres
  O comprimento dos nomes de catálogo de texto completo está restrito a 120 caracteres em vez de 128 caracteres como nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="description"></a>DESCRIÇÃO  
 Essa alteração não afeta os nomes de catálogos existentes. Entretanto, scripts que criarem catálogos de texto completo com nomes de mais de 120 caracteres causarão um erro.  Os nomes de catálogo são usados para gerar nomes de arquivos lógicos que correspondam aos catálogos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique todos os scripts que criam catálogos de texto completo para assegurar que eles restrinjam os nomes de catálogo a 120 caracteres.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
