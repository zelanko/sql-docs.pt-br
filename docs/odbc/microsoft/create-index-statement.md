---
description: Instrução CREATE INDEX
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
ms.openlocfilehash: 7a3f5a13624cdb137e8c86cf2c27044c6705298f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483629"
---
# <a name="create-index-statement"></a>Instrução CREATE INDEX
A sintaxe da instrução CREATE INDEX é:  
  
 CRIAR índice de índice [exclusivo] *-nome* no *nome da tabela* (*identificador de coluna* [asc] [desc] [, *identificador de coluna* [asc] [desc]...]) POR \<*index option list*>  
  
 onde \<*index option list*> pode ser: primário &#124; não permitir nulo &#124; ignorar nulo  
  
 Somente o driver do Microsoft Access usa as opções de não permitir nulo e ignorar índice nulo. Os drivers do dBASE e do Paradox aceitam a sintaxe, mas ignoram a presença de qualquer uma das opções.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria arquivos de chave primária do Paradox e arquivos secundários.  
  
 Não há suporte para essa instrução nos drivers de texto ou do Microsoft Excel.
