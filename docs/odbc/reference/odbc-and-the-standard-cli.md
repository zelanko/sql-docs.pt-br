---
title: ODBC e a CLI Padrão | Microsoft Docs
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
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305137"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e a CLI padrão
O ODBC está alinhado com as seguintes especificações e padrões que lidam com a Interface de Nível de Chamada (CLI). (As características do ODBC são um superconjunto de cada um desses padrões.)  
  
-   A especificação do CAE do Grupo Aberto "Gerenciamento de dados: Interface de Nível de Chamada SQL (CLI)"  
  
-   Interface de nível de chamada ISO/IEC 9075-3:1995 (E) (SQL/CLI)  
  
 Como resultado desse alinhamento, os seguintes são verdadeiros:  
  
-   Um aplicativo escrito para as especificações do Open Group e ISO CLI funcionará com um driver ODBC *3.x* ou um driver compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3.x* e vinculado com bibliotecas ODBC *3.x,* e quando ele ganhar acesso ao driver através do Gerenciador de Driver ODBC *3.x.*  
  
-   Um driver escrito nas especificações do Open Group e iso CLI funcionará com um aplicativo ODBC *3.x* ou um aplicativo compatível com padrões quando for compilado com os arquivos de cabeçalho ODBC *3.x* e vinculado com bibliotecas ODBC *3.x,* e quando o aplicativo obtém acesso ao driver através do Gerenciador de Driver ODBC *3.x.* (Para obter mais informações, consulte [Aplicativos e drivers compatíveis com normas](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 O nível de conformidade da interface Core abrange todos os recursos da CLI ISO e todos os recursos não opcionais no CLI do Grupo Aberto. Os recursos opcionais do CLI do Grupo Aberto aparecem em níveis mais altos de conformidade de interface. Como todos os drivers ODBC *3.x* são necessários para suportar os recursos no nível de conformidade da interface Core, os seguintes são verdadeiros:  
  
-   Um driver ODBC *3.x* suportará todos os recursos usados por um aplicativo compatível com padrões.  
  
-   Um aplicativo ODBC *3.x* usando apenas os recursos da ISO CLI e os recursos não opcionais da CLI do Grupo Aberto funcionará com qualquer driver compatível com padrões.  
  
 Além das especificações de interface de nível de chamada contidas nos padrões ISO/IEC e Open Group CLI, a ODBC implementa os seguintes recursos. (Alguns desses recursos existiam em versões do ODBC antes do ODBC *3.x*.)  
  
-   Multirow busca por uma única chamada de função  
  
-   Vinculando-se a uma matriz de parâmetros  
  
-   Suporte de marcadores, incluindo busca por marcador, marcadores de comprimento variável e atualização em massa e exclusão por operações de marcadores em linhas desconexas  
  
-   Vinculação em termos de linha  
  
-   Compensações de vinculação  
  
-   Suporte para lotes de instruções SQL, seja em um procedimento armazenado ou como uma seqüência de instruções SQL executadas através **de SQLExecute** ou **SQLExecDirect**  
  
-   Contagem exata ou aproximada da linha do cursor  
  
-   Operações posicionadas e exclusão de operações e atualizações e exclusões em lote por chamada de função **(SQLSetPos)**  
  
-   Funções de catálogo que extraem informações do esquema de informações sem a necessidade de suportar visualizações de esquemas de informações  
  
-   Sequências de fuga para adesões externas, funções escalares, literais de data-hora, literais de intervalo e procedimentos armazenados  
  
-   Bibliotecas de tradução de páginas de código  
  
-   Relatórios do nível de conformidade ANSI de um driver e suporte a SQL  
  
-   População automática sob demanda do descritor de parâmetros de implementação  
  
-   Diagnósticos aprimorados e matrizes de status de linha e parâmetros  
  
-   Data, intervalo, numérico/decimal e buffer de aplicativo inteiro de 64 bits  
  
-   Execução assíncrona  
  
-   Suporte ao procedimento armazenado, incluindo seqüências de fuga, mecanismos de vinculação de parâmetros de saída e funções de catálogo  
  
-   Aprimoramentos de conexão, incluindo suporte para atributos de conexão e navegação de atributos
