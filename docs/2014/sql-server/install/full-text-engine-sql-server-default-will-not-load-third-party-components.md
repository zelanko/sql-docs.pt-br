---
title: O mecanismo de texto completo da Microsoft para SQL Server não carregará componentes de terceiros não assinados por padrão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fe7f1359b55f2a488a58c37b9f3045a31dbc0778
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095161"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>O Mecanismo de Texto Completo da Microsoft para o SQL Server não carregará, por padrão, componentes de terceiros não assinados
  Por padrão, o Mecanismo de Texto Completo da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não carrega componentes que não são assinados pela [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="component"></a>Componente  
 Pesquisa de Texto Completo  
  
## <a name="description"></a>Descrição  
 Por padrão, um filtro de terceiros, como um filtro de PDF, que está instalado atualmente no servidor não será carregado pelo Mecanismo de Texto Completo da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depois da atualização.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Para carregar um filtro de terceiros, você deve definir *load_os_resource* e desative *verify_signature* nessa instância.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
