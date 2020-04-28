---
title: Instrução CREATE INDEX | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280966"
---
# <a name="create-index-statement"></a>Instrução CREATE INDEX
A sintaxe da instrução CREATE INDEX é:  
  
 CRIAR índice de índice [exclusivo] *-nome* no *nome da tabela* (*identificador de coluna* [asc] [desc] [, *identificador de coluna* [asc] [desc]...]) Com \< *lista de opções de índice*>  
  
 onde \<a *lista de opções de índice*> pode ser: Primary &#124; não permitir nulo &#124; ignorar nulo  
  
 Somente o driver do Microsoft Access usa as opções de não permitir nulo e ignorar índice nulo. Os drivers do dBASE e do Paradox aceitam a sintaxe, mas ignoram a presença de qualquer uma das opções.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria arquivos de chave primária do Paradox e arquivos secundários.  
  
 Não há suporte para essa instrução nos drivers de texto ou do Microsoft Excel.
