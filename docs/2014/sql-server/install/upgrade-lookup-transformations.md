---
title: Atualizar transformação pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: mashamsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 652cec720eae440106a0c8e30bd9910140dcff0a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182616"
---
# <a name="upgrade-lookup-transformations"></a>Atualizar transformação Pesquisa
  Ao atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], considere a possibilidade de modificar pacotes para aproveitar os novos recursos da Transformação Pesquisa. A transformação dá suporte a tipos de cache e opções de saída de dados disponíveis no [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]. Para obter mais informações sobre os armazenamento em cache e dados saídas adicionais, consulte [transformação Lookup](../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
 No [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], os tipos de cache disponíveis são cache cheio, cache parcial e nenhum cache. No [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], você pode configurar uma transformação Pesquisa para usar um desses tipos de cache. Para obter mais informações sobre como implementar cache parcial ou nenhum cache, consulte [implementar uma pesquisa no modo de Cache parcial ou No Cache](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md). Para obter informações sobre como implementar cache cheio, consulte [implementar uma transformação pesquisa em modo de Cache cheio usando o Gerenciador de Conexão de Cache](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md) e [implementar uma transformação pesquisa em modo de Cache cheio usando o OLE Gerenciador de Conexão de banco de dados](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md).  
  
 No [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], a transformação Pesquisa teve uma entrada, uma saída e uma saída de erro. As linhas nas entradas que possuem entradas correspondentes no conjunto de dados de referência são manipuladas pela saída. Linhas na entrada que não possuem entradas correspondentes são tratadas como erros e podem ser redirecionadas para a saída de erro. No [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], a transformação Pesquisa tem duas saídas: uma saída de correspondência e outra sem-correspondência.  
  
 Por padrão, quando você executa uma transformação Pesquisa que foi criada no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] trata as linhas sem entradas correspondentes como erros e permite que você redirecione as linhas a uma saída de erro. Você tem a opção de configurar a transformação Pesquisa para tratar as linhas como não erro e redirecioná-las para a saída sem-correspondência.  
  
 Para obter mais informações, consulte [Editor de transformação pesquisa &#40;página geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transformação Pesquisa](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
