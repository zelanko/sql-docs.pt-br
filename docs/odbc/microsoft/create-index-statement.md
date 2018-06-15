---
title: CRIAR a instrução de índice | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86d4cf1bb047cd475b86b9a58c37f3268c07c91d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900011"
---
# <a name="create-index-statement"></a>CRIAR a instrução de índice
A sintaxe da instrução CREATE INDEX é:  
  
 CRIAÇÃO do índice [UNIQUE] *nome do índice* ON *nome de tabela* (*identificador de coluna* [ASC] [DESC] [, *identificador de coluna* [ASC][DESC]...]) COM \< *lista de opções de índice*>  
  
 onde \< *lista de opções de índice*> pode ser: primário &#124; não permitir nulos &#124; IGNORE NULL  
  
 Somente o driver do Microsoft Access usa as opções de índice não permitir nulos e IGNORE NULL. Os drivers de Paradox e dBASE aceitam a sintaxe, mas ignorar a presença de qualquer opção.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria Paradox arquivos de chave primários e secundária.  
  
 Não há suporte para essa instrução pelos drivers de texto ou do Microsoft Excel.
