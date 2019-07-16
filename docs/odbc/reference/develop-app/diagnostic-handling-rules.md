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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 269e021d3fd4610c2fccda46bcd8ca160982543c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039922"
---
# <a name="diagnostic-handling-rules"></a>Regras de tratamento de diagnóstico
As seguintes regras regem o tratamento de diagnóstico na **SQLGetDiagRec** e **SQLGetDiagField**.  
  
 Para todos os componentes ODBC:  
  
-   Não substituir, alter ou mascarar erros ou avisos recebidos de outro componente do ODBC.  
  
-   Pode adicionar um registro de status adicionais quando recebem uma mensagem de diagnóstico de outro componente do ODBC. O registro adicionado deve adicionar o valor das informações reais à mensagem original.  
  
 Para o ODBC componente interfaces que diretamente de uma fonte de dados:  
  
-   Necessário prefixar o identificador da fonte de dados para a mensagem de diagnóstico que ele recebe da fonte de dados, seu identificador de componente e seu identificador de fornecedor.  
  
-   Deve preservar o código de erro nativo da fonte de dados.  
  
-   Deve preservar a mensagem de diagnóstico da fonte de dados.  
  
 Para qualquer componente do ODBC que gera um erro ou aviso independente da fonte de dados:  
  
-   Deve fornecer o SQLSTATE correto para o erro ou aviso.  
  
-   Deve gerar o texto da mensagem de diagnóstico.  
  
-   Necessário prefixar seu identificador de fornecedor e seu identificador de componente para a mensagem de diagnóstico.  
  
-   Deve retornar um código de erro nativo, caso haja algum disponível e significativo.  
  
 Para o componente ODBC que interage com o Gerenciador de Driver:  
  
-   Os argumentos de saída deve ser inicializada **SQLGetDiagRec** e **SQLGetDiagField**.  
  
-   Formate e retornar as informações de diagnóstico como argumentos de saída **SQLGetDiagRec** e **SQLGetDiagField** quando essa função é chamada.  
  
 Para um componente ODBC que não seja o Gerenciador de Driver:  
  
-   Configure o SQLSTATE com base no erro nativo. Para drivers baseados em arquivo e drivers baseados em DBMS que não usam um gateway, o driver deve definir o SQLSTATE. Para drivers baseados em DBMS que usam um gateway, o driver ou um gateway que oferece suporte ao ODBC pode definir o SQLSTATE.
