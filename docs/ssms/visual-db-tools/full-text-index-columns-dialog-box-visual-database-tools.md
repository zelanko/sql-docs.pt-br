---
title: "Caixa de diálogo Colunas de Índice de Texto Completo (Ferramentas de Banco de Dados Visual) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.fulltextcolumn
ms.assetid: a6f41c5c-d950-4d64-9e42-d062925917b6
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b88b6ec8c86c16709b9fd22f1ef93f0c32b4f10c
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="full-text-index-columns-dialog-box-visual-database-tools"></a>Caixa de diálogo colunas de índice de texto completo (Visual Database Tools)
Esta caixa de diálogo lista as colunas que participam do índice de texto completo para a tabela aberta no Designer de Tabela. Para acessar essa caixa de diálogo, clique com o botão direito do mouse na tabela no Designer de Tabela, escolha **Índice de Texto Completo**e, na caixa de diálogo **Índice de Texto Completo** , clique no índice com as colunas que você deseja exibir ou editar, clique no campo **Colunas** na grade à direita e clique nas reticências (**…**).  
  
## <a name="options"></a>Opções  
**Coluna**  
Mostra os nomes das colunas que fazem parte do índice de texto completo. Para adicionar uma coluna, clique na primeira célula vazia e escolha uma coluna da lista suspensa. Só estarão acessíveis as colunas com tipos de dados baseados em texto ou em imagens.  
  
**Tipo de Dados**  
Mostra o tipo de dados para cada coluna. Trata-se de uma propriedade somente leitura. Para alterar um tipo de dados, abra a tabela no Designer de Tabela, clique na coluna e edite o tipo de dados na guia **Propriedades da Coluna** .  
  
**Digitado por Coluna**  
Aplica-se somente a colunas com o tipo de dados **image**. Fornece uma lista suspensa na qual você pode escolher quais das outras colunas representam o tipo de dados dessa coluna. Se esta coluna não for do tipo de dados **image** , o valor será Nenhum.  
  
Colunas com o tipo de dados **image** podem conter arquivos do Microsoft Office (arquivos .doc, .xls e .ppt), arquivo de texto (arquivos .txt) e arquivos HTML (arquivos .htm); definir o tipo de dados dessa coluna para imagem permite que a pesquisa de texto completo busque o conteúdo dos arquivos.  
  
**Idioma**  
Lista os idiomas disponíveis. Escolha o idioma da lista suspensa de idiomas que é apropriado para seus dados de coluna. Por exemplo, se você estiver usando um sistema operacional em inglês, mas quiser indexar uma coluna que contenha texto em alemão, escolha alemão na lista suspensa para melhorar o desempenho do índice.  
  
**Semântica Estatística**  
Especifique se habilitará a indexação semântica da coluna selecionada. Para obter mais informações, consulte [Espaço reservado Pesquisa semântica](http://msdn.microsoft.com/en-us/cd8faa9d-07db-420d-93f4-a2ea7c974b97).  
  
Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será desabilitada. Se você selecionar **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na caixa de combinação suspensa serão restringidos a esses para os quais o Modelo de Idioma Semântico dá suporte.  
  
## <a name="see-also"></a>Consulte também  
[Caixa de diálogo Índice de Texto Completo &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/full-text-index-dialog-box-visual-database-tools.md)  
  

