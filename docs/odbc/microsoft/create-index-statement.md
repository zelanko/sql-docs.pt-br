---
title: CRIAR a instrução de índice | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61d1532e457748b432e5aa14a55e9e68b4486c9c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="create-index-statement"></a>CRIAR a instrução de índice
A sintaxe da instrução CREATE INDEX é:  
  
 CRIAÇÃO do índice [UNIQUE] *nome do índice* ON *nome de tabela* (*identificador de coluna* [ASC] [DESC] [, *identificador de coluna* [ASC][DESC]...]) COM \< *lista de opções de índice*>  
  
 onde \< *lista de opções de índice*> pode ser: primário &#124; não permitir nulos &#124; IGNORE NULL  
  
 Somente o driver do Microsoft Access usa as opções de índice não permitir nulos e IGNORE NULL. Os drivers de Paradox e dBASE aceitam a sintaxe, mas ignorar a presença de qualquer opção.  
  
 Quando o driver do Paradox é usado, a instrução CREATE INDEX cria Paradox arquivos de chave primários e secundária.  
  
 Não há suporte para essa instrução pelos drivers de texto ou do Microsoft Excel.
