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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad15ad436b0f34f00acbd75e371e998183f22d2f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081915"
---
# <a name="create-index-statement"></a>Instrução CREATE INDEX
A sintaxe da instrução CREATE INDEX é:  
  
 CRIAR índice de índice [exclusivo] *-nome* no *nome da tabela* (*identificador de coluna* [asc] [desc] [, *identificador de coluna* [asc] [desc]...]) Com \< *lista de opções de índice*>  
  
 onde \<a *lista de opções de índice*> pode ser: Primary &#124; não permitir nulo &#124; ignorar nulo  
  
 Somente o driver do Microsoft Access usa as opções de não permitir nulo e ignorar índice nulo. Os drivers do dBASE e do Paradox aceitam a sintaxe, mas ignoram a presença de qualquer uma das opções.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria arquivos de chave primária do Paradox e arquivos secundários.  
  
 Não há suporte para essa instrução nos drivers de texto ou do Microsoft Excel.
