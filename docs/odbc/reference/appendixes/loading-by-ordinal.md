---
title: Carregamento por Ordinal | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ccecc541143e971d82a225e24e1c8caf6a03c32c
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793188"
---
# <a name="loading-by-ordinal"></a>Carregamento por ordinal
Em ODBC *2.x*, carregamento por ordinal pôde ser executado para melhorar o desempenho do processo de conexão. ODBC *2.x* driver exporta uma função fictícia com o ordinal 199; quando o Gerenciador de Driver detecta a ele, ele resolve os endereços das funções ODBC por ordinal, e não por nome. Ainda há suporte para essa funcionalidade para ODBC *2.x* drivers, mas não há suporte para ODBC *3.x* drivers.
