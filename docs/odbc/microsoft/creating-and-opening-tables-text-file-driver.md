---
title: Criação e abertura de tabelas (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280916"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Criar e abrir tabelas (Driver de Arquivo de texto)
Quando o driver Texto é usado, uma nova tabela é criada usando o formato especificado em Odbcinst.ini. Se não especificado, as tabelas são criadas no formato CSVDELIMITED. Por padrão, as colunas INTEGER são padrão para 11 caracteres e as colunas FLOAT são padrão para 22 caracteres. As colunas DATE usam o formato YYYY-MM-DD. As colunas CHAR e LONGCHAR são a largura especificada na declaração CREATE.
