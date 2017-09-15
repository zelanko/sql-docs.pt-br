---
title: "CRIAR a instrução de índice | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f6e7525059640e7ffdadd79ec26a62229eabae9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-statement"></a>CRIAR a instrução de índice
A sintaxe da instrução CREATE INDEX é:  
  
 CRIAÇÃO do índice [UNIQUE] *nome do índice* ON *nome de tabela* (*identificador de coluna* [ASC] [DESC] [, *identificador de coluna* [ASC][DESC]...]) COM \< *lista de opções de índice*>  
  
 onde \< *lista de opções de índice*> pode ser: primário &#124; Não permitir nulos &#124; IGNORAR NULL  
  
 Somente o driver do Microsoft Access usa as opções de índice não permitir nulos e IGNORE NULL. Os drivers de Paradox e dBASE aceitam a sintaxe, mas ignorar a presença de qualquer opção.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria Paradox arquivos de chave primários e secundária.  
  
 Não há suporte para essa instrução pelos drivers de texto ou do Microsoft Excel.
