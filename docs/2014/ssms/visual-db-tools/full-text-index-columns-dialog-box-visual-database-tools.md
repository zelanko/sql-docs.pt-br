---
title: Caixa de diálogo Colunas de Índice de Texto Completo (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextcolumn
ms.assetid: a6f41c5c-d950-4d64-9e42-d062925917b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: d4d77bb77ab3cf0fecc2e254af53782f982923ae
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054587"
---
# <a name="full-text-index-columns-dialog-box-visual-database-tools"></a>Caixa de diálogo colunas de índice de texto completo (Visual Database Tools)
  Esta caixa de diálogo lista as colunas que participam do índice de texto completo para a tabela aberta no Designer de Tabela. Para acessar essa caixa de diálogo, clique com o botão direito do mouse na tabela no Designer de Tabela, escolha **Índice de Texto Completo** e, na caixa de diálogo **Índice de Texto Completo**, clique no índice com as colunas que você deseja exibir ou editar, clique no campo **Colunas** na grade à direita e clique nas reticências ( **…** ).  
  
## <a name="options"></a>Opções  
 **Coluna**  
 Mostra os nomes das colunas que fazem parte do índice de texto completo. Para adicionar uma coluna, clique na primeira célula vazia e escolha uma coluna da lista suspensa. Só estarão acessíveis as colunas com tipos de dados baseados em texto ou em imagens.  
  
 **Tipo de Dados**  
 Mostra o tipo de dados para cada coluna. Trata-se de uma propriedade somente leitura. Para alterar um tipo de dados, abra a tabela no Designer de Tabela, clique na coluna e edite o tipo de dados na guia **Propriedades da Coluna** .  
  
 **Digitado por Coluna**  
 Aplica-se somente a colunas com o tipo de dados `image`. Fornece uma lista suspensa na qual você pode escolher quais das outras colunas representam o tipo de dados dessa coluna. Se esta coluna não for do tipo de dados `image`, o valor será Nenhum.  
  
 Colunas com o tipo de dados `image` podem conter arquivos do Microsoft Office (arquivos .doc, .xls, e .ppt), arquivo de texto (arquivos .txt) e arquivos HTML (arquivos .htm); definir o tipo de dados dessa coluna para imagem permite que a procura de texto completo busque os conteúdos dos arquivos.  
  
 **Idioma**  
 Lista os idiomas disponíveis. Escolha o idioma da lista suspensa de idiomas que é apropriado para seus dados de coluna. Por exemplo, se você estiver usando um sistema operacional em inglês, mas quiser indexar uma coluna que contenha texto em alemão, escolha alemão na lista suspensa para melhorar o desempenho do índice.  
  
 **Semântica Estatística**  
 Especifique se habilitará a indexação semântica da coluna selecionada. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será desabilitada. Se você selecionar **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na caixa de combinação suspensa serão restringidos a esses para os quais o Modelo de Idioma Semântico dá suporte.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Índice de Texto Completo &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
