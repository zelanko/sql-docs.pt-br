---
title: Habilitar / desabilitar a caixa de diálogo de write-back (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 498d1af6f96791b9ee3912c09a3667e139f30ff0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081293"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>Habilitar / desabilitar a caixa de diálogo de write-back (Analysis Services - dados multidimensionais)
  A caixa de diálogo **Habilitar/Desabilitar Write-back** habilita ou desabilita write-back para um grupo de medidas em um cubo. Habilitar write-back em um grupo de medidas define uma partição de write-back e cria uma tabela de write-back para esse grupo de medidas. Desabilitar write-back em um grupo de medidas remove a partição de write-back, mas não exclui a tabela de write-back, de modo a evitar perda de dados inesperada. A caixa de diálogo **Habilitar/Desabilitar Write-back** é exibida da seguintes maneiras:  
  
-   Clicando em **Configurações de Write-back** no painel **Grupos de Medidas** na guia **Partições** no Designer de Cubo.  
  
-   Clicando com o botão direito do mouse na grade **Partições** no painel **Grupos de Medidas** na guia **Partições** no Designer de Cubo e selecionando **Configurações de Write-back** no menu de contexto.  
  
## <a name="options"></a>Opções  
 **Nome da tabela**  
 Digite o nome da tabela de write-back a ser criada para a partição selecionada. A tabela write-back armazena as alterações feitas no grupo de medidas por um aplicativo cliente.  
  
> [!NOTE]  
>  Essa opção estará desabilitada se write-back não estiver habilitado.  
  
 **Fonte de dados**  
 Selecione a fonte de dados para conter a tabela de write-back.  
  
> [!NOTE]  
>  Essa opção estará desabilitada se write-back não estiver habilitado.  
  
 **Nova**  
 Clique para exibir a caixa de diálogo **Gerenciador de Conexões** e definir uma nova fonte de dados para conter a tabela de write-back.  
  
> [!NOTE]  
>  Essa opção estará desabilitada se write-back não estiver habilitado.  
  
  
