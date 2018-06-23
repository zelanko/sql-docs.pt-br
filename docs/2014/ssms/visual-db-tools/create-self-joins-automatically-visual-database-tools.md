---
title: Criar autojunções automaticamente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5f73848107ec08829a48da0b921729ce318f3d63
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006249"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>Criar autojunções automaticamente (Visual Database Tools)
  Se uma tabela tiver uma relação reflexiva no banco de dados, a autojunção poderá ocorrer automaticamente.  
  
### <a name="to-create-a-self-join-automatically"></a>Para criar uma autojunção automaticamente  
  
1.  Adicione ao [painel Diagrama](visual-database-tools.md) a tabela com a qual deseja trabalhar.  
  
2.  Adicione a mesma tabela novamente, de forma que seja exibida a mesma tabela duas vezes no painel Diagrama.  
  
     O [Designer de Consulta e Exibição](query-and-view-designer-tools-visual-database-tools.md) atribui um alias à segunda instância adicionando um número sequencial ao nome da tabela. Além disso, o Designer de Consulta e Exibição cria uma linha de junção entre os dois retângulos representando dois modos diferentes de participação da tabela na consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Consultar com junções &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  