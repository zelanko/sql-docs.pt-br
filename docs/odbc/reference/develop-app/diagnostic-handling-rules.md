---
title: Regras de tratamento de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f7f9d19a5a369e9da0efbc0d62f8e556b0597c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305837"
---
# <a name="diagnostic-handling-rules"></a>Regras de tratamento de diagnóstico
As regras a seguir regem o tratamento de diagnóstico em **SQLGetDiagRec** e **SQLGetDiagField**.  
  
 Para todos os componentes ODBC:  
  
-   Não é necessário substituir, alterar ou mascarar erros ou avisos recebidos de outro componente ODBC.  
  
-   Pode adicionar um registro de status adicional ao receber uma mensagem de diagnóstico de outro componente ODBC. O registro adicionado deve adicionar um valor de informações real à mensagem original.  
  
 Para o componente ODBC que faz a interface diretamente de uma fonte de dados:  
  
-   Deve prefixar seu identificador de fornecedor, seu identificador de componente e o identificador da fonte de dados para a mensagem de diagnóstico que ele recebe da fonte de dados.  
  
-   Deve preservar o código de erro nativo da fonte de dados.  
  
-   Deve preservar a mensagem de diagnóstico da fonte de dados.  
  
 Para qualquer componente ODBC que gera um erro ou aviso independente da fonte de dados:  
  
-   Deve fornecer o SQLSTATE correto para o erro ou aviso.  
  
-   Deve gerar o texto da mensagem de diagnóstico.  
  
-   É necessário prefixar seu identificador de fornecedor e seu identificador de componente para a mensagem de diagnóstico.  
  
-   Deve retornar um código de erro nativo, se houver um disponível e significativo.  
  
 Para o componente ODBC que faz interface com o Gerenciador de driver:  
  
-   Deve inicializar os argumentos de saída de **SQLGetDiagRec** e **SQLGetDiagField**.  
  
-   Deve formatar e retornar as informações de diagnóstico como argumentos de saída de **SQLGetDiagRec** e **SQLGetDiagField** quando essa função é chamada.  
  
 Para um componente ODBC diferente do Gerenciador de driver:  
  
-   Deve definir o SQLSTATE com base no erro nativo. Para drivers baseados em arquivo e drivers baseados em DBMS que não usam um gateway, o driver deve definir o SQLSTATE. Para drivers baseados em DBMS que usam um gateway, o driver ou um gateway que oferece suporte a ODBC pode definir o SQLSTATE.
