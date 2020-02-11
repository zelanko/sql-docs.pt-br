---
title: Limitações da instrução de CREATE TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db5d2cb8decde9828acd3005551717ac9f6cef32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096591"
---
# <a name="create-table-statement-limitations"></a>Limitações da instrução CREATE TABLE
Quando o Microsoft Access, o Microsoft Excel ou o Paradoxdriver são usados, e o comprimento de um texto ou coluna binária não é especificado (ou é especificado como 0), o comprimento da coluna será definido como 255.  
  
 Quando o driver do dBASE é usado e o comprimento de um texto ou coluna binária não é especificado (ou é especificado como 0), o comprimento da coluna será definido como 254.  
  
 Há suporte para um máximo de 255 colunas.  
  
 Quando o driver do Microsoft Excel é usado em uma fonte de dados MicrosoftExcel 5,0, 7,0 ou 97, uma planilha não pode ser criada com o mesmo nome de uma planilha que foi previamente descartada. Quando o driver do Microsoft Excel é usado para acessar uma planilha da versão 5,0, 7,0 ou 97, uma instrução DROP TABLE limpa a planilha, mas não exclui o nome da planilha.  
  
 Quando o driver do Paradox for usado, as colunas não poderão ser adicionadas depois que um índice tiver sido definido em uma tabela. Se a primeira coluna da lista de argumentos de uma instrução CREATE TABLE criar um índice, uma segunda coluna não poderá ser incluída na lista de argumentos.
