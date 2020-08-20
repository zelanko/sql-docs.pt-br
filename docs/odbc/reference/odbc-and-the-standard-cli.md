---
description: ODBC e a CLI padrão
title: ODBC e a CLI Standard | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 844ca219bf912421cf859e0fc459b78d755fe159
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487379"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e a CLI padrão
O ODBC alinha-se com as especificações e os padrões a seguir que lidam com a CLI (interface de nível de chamada). (Os recursos do ODBC são um superconjunto de cada um desses padrões.)  
  
-   A especificação CAE do grupo aberto "Gerenciamento de Dados: interface de nível de chamada do SQL (CLI)"  
  
-   Interface de nível de chamada ISO/IEC 9075-3:1995 (E) (SQL/CLI)  
  
 Como resultado desse alinhamento, as seguintes opções são verdadeiras:  
  
-   Um aplicativo gravado nas especificações do grupo aberto e da CLI ISO funcionará com um driver ODBC *3. x* ou com um driver compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3. x* e vinculado com bibliotecas ODBC *3. x* e quando ele obtiver acesso ao driver por meio do Gerenciador de driver ODBC *3. x* .  
  
-   Um driver escrito nas especificações do grupo aberto e da CLI ISO funcionará com um aplicativo ODBC *3. x* ou com um aplicativo compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3. x* e vinculado com bibliotecas ODBC *3. x* e quando o aplicativo obtiver acesso ao driver por meio do Gerenciador de driver ODBC *3. x* . (Para obter mais informações, consulte [aplicativos e drivers em conformidade com os padrões](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 O nível de conformidade da interface principal abrange todos os recursos na CLI ISO e todos os recursos não-Optional na CLI do grupo aberto. Os recursos opcionais da CLI do Open Group aparecem em níveis de conformidade de interface mais altos. Como todos os drivers ODBC *3. x* são necessários para dar suporte aos recursos no nível de conformidade da interface principal, os seguintes itens são verdadeiros:  
  
-   Um driver ODBC *3. x* dará suporte a todos os recursos usados por um aplicativo compatível com os padrões.  
  
-   Um aplicativo ODBC *3. x* que usa apenas os recursos na CLI ISO e os recursos não-informativos da CLI do grupo aberto funcionará com qualquer driver compatível com padrões.  
  
 Além das especificações de interface de nível de chamada contidas nos padrões ISO/IEC e Open Group CLI, o ODBC implementa os seguintes recursos. (Alguns desses recursos existiam em versões do ODBC antes do ODBC *3. x*.)  
  
-   O LinhaMúltipla busca por uma única chamada de função  
  
-   Associação a uma matriz de parâmetros  
  
-   Suporte a indicadores, incluindo busca por indicador, indicadores de comprimento variável e atualização em massa e exclusão por operações de indicador em linhas descontínuas  
  
-   Associação de linha  
  
-   Deslocamentos de associação  
  
-   Suporte para lotes de instruções SQL, em um procedimento armazenado ou como uma sequência de instruções SQL executadas por meio de **SQLExecute** ou **SQLExecDirect**  
  
-   Contagens de linhas de cursor exatas ou aproximadas  
  
-   Operações de atualização e exclusão posicionadas e atualizações em lote e exclusões por chamada de função (**SQLSetPos**)  
  
-   Funções de catálogo que extraem informações do esquema de informações sem a necessidade de dar suporte a exibições de esquema de informações  
  
-   Sequências de escape para junções externas, funções escalares, literais DateTime, literais de intervalo e procedimentos armazenados  
  
-   Bibliotecas de tradução de página de código  
  
-   Relatórios de nível de conformidade ANSI de um driver e suporte a SQL  
  
-   População automática sob demanda do descritor de parâmetro de implementação  
  
-   Diagnóstico aprimorado e matrizes de status de linha e parâmetro  
  
-   DateTime, intervalo, numérico/decimal e tipos de buffer de aplicativo inteiros de 64 bits  
  
-   Execução assíncrona  
  
-   Suporte a procedimentos armazenados, incluindo sequências de escape, mecanismos de associação de parâmetro de saída e funções de catálogo  
  
-   Aprimoramentos de conexão, incluindo suporte para atributos de conexão e navegação de atributo
