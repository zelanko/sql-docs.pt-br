---
title: Remover colunas de uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61bca79fe550622ac5c5967a71a2705aa8891536
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286332"
---
# <a name="remove-columns-from-a-mining-structure"></a>Remover colunas de uma estrutura de mineração
  Você pode usar o Designer de Mineração de Dados para remover colunas de uma estrutura de mineração após a criação da estrutura. Alguns motivos para remover uma coluna da estrutura de mineração:  
  
-   A estrutura de mineração contém várias cópias de uma coluna e você deseja evitar o uso de dados duplicados em um modelo.  
  
-   Os dados devem ser protegidos, mas o detalhamento foi habilitado.  
  
-   Os dados não são usados na modelagem e não devem ser processados.  
  
 A exclusão de uma coluna da estrutura de mineração não altera a coluna na exibição da fonte de dados nem nos dados externos; apenas os metadados são excluídos. Entretanto, quando você altera as colunas usadas em uma estrutura de mineração, precisa reprocessar a estrutura e quaisquer modelos com base nela.  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>Para remover colunas de uma estrutura de mineração  
  
1.  Selecione a guia **Estrutura de Mineração** no Designer de Mineração de Dados.  
  
2.  Expanda a árvore da estrutura de mineração para que mostre todas as colunas.  
  
3.  Clique com o botão direito do mouse na coluna que você quer excluir e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objetos** , clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
  
