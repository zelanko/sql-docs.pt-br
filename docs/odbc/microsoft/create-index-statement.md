---
title: DECLARAÇÃO DE ÍNDICE DE CRIAÇÃO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280966"
---
# <a name="create-index-statement"></a>Instrução CREATE INDEX
A sintaxe da declaração CREATE INDEX é:  
  
 CRIAR [EXCLUSIVO] *INDEX-name* ON *nome de tabela* *(identificador de coluna* [ASC][DESC][, *identificador de coluna* [ASC][DESC]...]] LISTA \<DE *OPÇÕES DE ÍNDICE* COM>  
  
 onde \<> *da lista de opções de índice* pode ser: PRIMARY &#124; DISALLOW NULL &#124; IGNORE NULL NULL  
  
 Apenas o driver microsoft access usa as opções de índice DISALLOW NULL e IGNORE NULL. Os drivers dBASE e Paradox aceitam a sintaxe, mas ignoram a presença de qualquer opção.  
  
 Quando o driver Paradox é usado, a declaração CREATE INDEX cria arquivos-chave primários do Paradox e arquivos secundários.  
  
 Esta declaração não é suportada pelos drivers Microsoft Excel ou Text.
