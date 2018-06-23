---
title: Atualização fará com que a pesquisa de texto completo use separadores de palavras de nível de instância, e não globais e filtros por padrão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d1e4bfcaf022207afd7822740af104d6b9dbff2e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009691"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>Atualização fará com que a Pesquisa de Texto Completo use separadores de palavras e filtros em nível de instância, e não globais, por padrão
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite os registro em nível de instância de novos separadores de palavras e filtros.  
  
## <a name="component"></a>Componente  
 Pesquisa de Texto Completo  
  
## <a name="description"></a>Description  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite o registro de novos separadores de palavras e filtros em nível de instância. Esse registro em nível de instância fornece isolamento funcional e de segurança entre instâncias.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Depois de atualizar para o `sp_fulltext_service` para definir a propriedade de serviço e `load_os_resources`, o que permitirá que os componentes sejam carregados. Você deve executar o seguinte:  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  