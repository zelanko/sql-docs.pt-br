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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081915"
---
# <a name="create-index-statement"></a>Instrução CREATE INDEX
A sintaxe da instrução CREATE INDEX é:  
  
 Criar índice [UNIQUE] *nome do índice* ON *nome da tabela* (*identificador de coluna* [ASC] [DESC] [, *identificador da coluna* [ASC][DESC]...]) COM o \< *lista de opções de índice*>  
  
 em que \< *lista de opções de índice*> pode ser: PRINCIPAL &#124; NÃO PERMITIR NULOS &#124; IGNORAR NULL  
  
 Somente o driver do Microsoft Access usa as opções de índice não permitir nulo e ignorar nulo. O dBASE e drivers do Paradox aceitam a sintaxe, mas ignorar a presença de uma das opções.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria arquivos de chave primários Paradox e arquivos secundários.  
  
 Essa instrução não é suportada pelos drivers da Microsoft Excel ou texto.
