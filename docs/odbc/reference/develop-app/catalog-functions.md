---
title: Funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 232d2e9b7e9eb695a40058075ea511392e464a32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064399"
---
# <a name="catalog-functions"></a>Funções de catálogo
Todos os bancos de dados têm uma estrutura que descreve como os data serão armazenados no banco de dado. Por exemplo, um banco de dados de ordem de venda simples pode ter a estrutura mostrada na ilustração a seguir, na qual as colunas de ID são usadas para vincular as tabelas.  
  
 ![Mostra a estrutura de um banco de dados simples](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Essa estrutura, juntamente com outras informações, como privilégios, é armazenada em um conjunto de tabelas do sistema chamado catálogo do banco de dados *,* que também é conhecido como um *dicionário de dado*.  
  
 Um aplicativo pode descobrir essa estrutura por meio de chamadas para as *funções de catálogo*. As funções de catálogo retornam informações em conjuntos de resultados e geralmente são implementadas por meio de instruções **Select** em relação às tabelas no catálogo. Por exemplo, um aplicativo pode solicitar um conjunto de resultados que contém informações sobre todas as tabelas no sistema ou todas as colunas de uma tabela específica.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funções de catálogo em ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
