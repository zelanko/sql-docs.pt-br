---
title: A atualização fará com que a pesquisa de texto completo use os separadores de palavras e os filtros em nível de instância, e não globais, por padrão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c81892d6b83cef87a27a836d9691779a841104a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095057"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>Atualização fará com que a Pesquisa de Texto Completo use separadores de palavras e filtros em nível de instância, e não globais, por padrão
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite os registro em nível de instância de novos separadores de palavras e filtros.  
  
## <a name="component"></a>Componente  
 Pesquisa de Texto Completo  
  
## <a name="description"></a>DESCRIÇÃO  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite o registro de novos separadores de palavras e filtros em nível de instância. Esse registro em nível de instância fornece isolamento funcional e de segurança entre instâncias.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Depois de atualizar para o `sp_fulltext_service` para definir a propriedade de serviço e `load_os_resources`, o que permitirá que os componentes sejam carregados. Você deve executar o seguinte:  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
