---
title: Opções (SQL Server AlwaysOn, página painel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 553f76520f9bb292d795fbbd5e13833391d6bdab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115502"
---
# <a name="options-sql-server-alwayson-dashboard-page"></a>Opções (SQL Server AlwaysOn, página Painel)
  Use a página **Painel do SQL Server AlwaysOn** da caixa de diálogo [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**Opções** para configurar o Painel do AlwaysOn.  
  
 **Para acessar essa página:**  
  
 No menu **Ferramentas** , clique em **Opções**, expanda a pasta **SQL Server AlwaysOn** e clique em **Painel**.  
  
## <a name="on-this-page"></a>Nessa página  
 **Ativar atualização automática.**  
 Clique para habilitar a atualização automática. As opções são:  
  
-   O campo **Intervalo de atualização (em segundos)** exibe o número de segundos nos quais o painel será atualizado. O valor padrão é 30. Quando a atualização automática estiver habilitada, você poderá editar esse campo para alterar o intervalo de atualização.  
  
-   O **Número de tentativas de conexão** exibe o número de vezes que o painel tentará se conectar a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda uma réplica de disponibilidade para um grupo de disponibilidade que o Painel está monitorando. O valor padrão é 65535. Quando a atualização automática estiver habilitada, você poderá editar esse campo para alterar o número de tentativas de conexão.  
  
 **Habilite sua política de AlwaysOn definida pelo usuário.**  
 Se você tiver definido sua própria política de AlwaysOn, clique nessa opção para habilitar sua política.  
  
## <a name="see-also"></a>Consulte também  
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  