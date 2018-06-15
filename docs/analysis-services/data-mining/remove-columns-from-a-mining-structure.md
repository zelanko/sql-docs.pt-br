---
title: Remover colunas de uma estrutura de mineração | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd8691d8ec0cc1546e27e8195e7d0bbc20709f59
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015873"
---
# <a name="remove-columns-from-a-mining-structure"></a>Remover colunas de uma estrutura de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Tarefas de estrutura de mineração e instruções](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
