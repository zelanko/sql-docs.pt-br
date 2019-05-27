---
title: Recursos desativado por padrão (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59c27d5f34d6e5a3f33e0f153a9077995bd99650
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080018"
---
# <a name="features-off-by-default-analysis-services"></a>Recursos desativados por padrão (Analysis Services)
  Uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é considerada segura por padrão. Assim, os recursos que podem comprometer a segurança são desabilitados por padrão. Os recursos a seguir são instalados em um estado desabilitado e deverão ser habilitados especificamente se você quiser usá-los.  
  
## <a name="feature-list"></a>Lista de recursos  
 Para habilitar os recursos a seguir, conecte-se ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Clique com o botão direito do mouse no nome da instância e selecione **Facetas**. Como alternativa, você pode habilitar esses recursos por meio das propriedades do servidor, conforme descrito na próxima seção.  
  
-   Consultas de mineração de dados ad hoc (OpenRowset)  
  
-   Objetos vinculados (para)  
  
-   Objetos vinculados (de)  
  
-   Escutar apenas em conexões locais  
  
-   Funções definidas pelo usuário  
  
## <a name="server-properties"></a>Propriedades do servidor  
 Recursos adicionais que são desativados por padrão podem ser habilitados por meio das propriedades do servidor. Conectar-se a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Clique com o botão direito do mouse no nome da instância e selecione **Propriedades**. Clique em **Geral**e, em seguida, clique em **Mostrar avançado** para exibir uma lista de propriedades maior.  
  
-   Consultas de mineração de dados ad hoc (OpenRowset)  
  
-   Permitir modelos de mineração de sessão (Mineração de dados)  
  
-   Objetos vinculados (para)  
  
-   Objetos vinculados (de)  
  
-   Funções COM definidas pelo usuário  
  
-   Definição de Rastreamento do Registrador de Voo (modelos).  
  
-   Gravação de log de consulta  
  
-   Escutar apenas em conexões locais  
  
-   XML binário  
  
-   Compactação  
  
-   Afinidade do grupo. Para obter detalhes, consulte [Thread Pool Properties](../server-properties/thread-pool-properties.md) .  
  
  
