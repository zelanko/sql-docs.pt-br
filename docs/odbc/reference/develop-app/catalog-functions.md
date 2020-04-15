---
title: Funções do Catálogo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb28ec6f4ea299dae8737fc707fd53e4d102442d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305197"
---
# <a name="catalog-functions"></a>Funções de catálogo
Todos os bancos de dados possuem uma estrutura que descreve como os dados serão armazenados no banco de dados. Por exemplo, um banco de dados de pedidos de vendasimples simples pode ter a estrutura mostrada na ilustração a seguir, na qual as colunas de ID são usadas para vincular as tabelas.  
  
 ![Mostra a estrutura de um banco de dados simples](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Essa estrutura, juntamente com outras informações como privilégios, é armazenada em um conjunto de tabelas de sistema chamada catálogo do banco de *dados,* que também é conhecido como dicionário de *dados.*  
  
 Um aplicativo pode descobrir essa estrutura através de chamadas para as funções do *catálogo.* As funções do catálogo retornam informações em conjuntos de resultados e geralmente são implementadas através de instruções **SELECT** contra as tabelas do catálogo. Por exemplo, um aplicativo pode solicitar um conjunto de resultados que contém informações sobre todas as tabelas no sistema ou todas as colunas de uma tabela específica.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funções de catálogo em ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
