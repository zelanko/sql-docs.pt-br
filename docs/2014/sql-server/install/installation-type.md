---
title: Tipo de instalação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0420c555-7a3b-42b9-8651-0b4f5bcb0008
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8b153d75c308a59a20ce5097b191f37fa92ed94c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115357"
---
# <a name="installation-type"></a>Tipo de Instalação
  Use a página Tipo de Instalação do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar se deseja instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou adicionar recursos a uma instância existente.  
  
## <a name="options"></a>Opções  
 Selecione o botão de opção que especifica sua opção:  
  
-   Executar uma nova instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Adicionar recursos a uma instância existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
     Se você selecionar a opção para adicionar recursos a uma instância existente, use a lista suspensa para selecionar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser atualizada.  
  
 Você somente pode adicionar os recursos com suporte do SysPrep —[!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]— a imagem preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Outros recursos aos quais o SysPrep não oferece suporte só poderão ser adicionados depois que a instância preparada for concluída.  
  
 **Observação** Você não poderá adicionar recursos a uma instância de cluster de failover depois que ela for instalada. Para adicionar recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um cluster de failover existente, você deve executar uma nova instalação para instalar uma instância separada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  