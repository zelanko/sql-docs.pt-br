---
title: Copiar tabelas de diagramas de um banco de dados para outro | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- copying tables
- duplicating tables
ms.assetid: 155a4f09-9321-4887-a7d4-aa2ce6b51277
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4a64ef158777c4f5b5bfc091feb59a70b013973d
ms.contentlocale: pt-br
ms.lasthandoff: 08/18/2017

---
# <a name="copy-tables-from-one-database-diagrams-to-another-visual-database-tools"></a>Copiar tabelas de diagramas de um banco de dados para outro (Visual Database Tools)
Você pode copiar uma tabela de um diagrama de banco de dados para outro no mesmo banco de dados.  
  
Copiando uma tabela de um diagrama de banco de dados para outro diagrama adiciona uma referência à tabela no segundo diagrama. A tabela não é duplicada no seu banco de dados. Por exemplo, se você copiar a tabela `authors` de um diagrama de banco de dados para outro, cada diagrama referencia a mesma tabela `authors` no banco de dados.  
  
### <a name="to-copy-a-table-from-another-database-diagram"></a>Para copiar uma tabela de outro diagrama de banco de dados  
  
1.  Verifique se você está conectado ao banco de dados da tabela a ser copiada.  
  
2.  Abra os diagramas de origem e de destino do banco de dados e dentro do diagrama de origem, selecione a tabela que você deseja copiar no diagrama de destino.  
  
3.  Clique no botão **Copiar** na barra de ferramentas. Essa ação coloca a definição da tabela selecionada na Área de Transferência.  
  
4.  Alterne para o diagrama de destino. Esse diagrama deve estar no mesmo banco de dados do diagrama de origem.  
  
5.  Clique no botão **Colar** na barra de ferramentas. O conteúdo da Área de Transferência aparece no novo local e permanece realçado até que você clique em outro lugar. Se existir relações entre as tabelas selecionadas e outras tabelas no diagrama de destino, linhas de relação serão desenhadas automaticamente.  
  
Quando você edita a tabela em qualquer diagrama, suas alterações são refletidas em ambos os diagramas. Da mesma forma, quando você salva a tabela em qualquer diagrama, a tabela não é mais considerada "modificada" em qualquer diagrama.  
  
## <a name="see-also"></a>Consulte também  
[Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Adicionar tabelas a diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  

