---
title: Escolher como importar os dados (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.choosehowtoimpdata.f1
ms.assetid: 17dc6903-c239-46aa-a3b0-6e3156accacc
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9929f61537fdf635ffd130b75d9e2738be256aab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122055"
---
# <a name="choose-how-to-import-the-data-ssas"></a>Escolher como importar os dados (SSAS)
  Esta página do **Assistente de Importação de Tabela** permite escolher como importar dados da fonte de dados selecionada. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Selecionar em uma lista de tabelas e exibições para escolher os dados a serem importados**  
 Selecione esta opção se desejar importar dados selecionando em uma lista.  
  
> [!NOTE]  
>  Esta opção só está disponível quando a fonte de dados selecionada expõe as informações de esquema com suporte no **Assistente de Importação de Tabela** .  
  
 **Escrever uma consulta para especificar os dados a serem importados**  
 Selecione esta opção se quiser importar dados usando uma consulta SQL. A consulta SQL pode manipular os dados que são importados. Por exemplo, é possível unir dados de tabelas diferentes ou selecionar apenas linhas que atendam a certos critérios.  
  
  