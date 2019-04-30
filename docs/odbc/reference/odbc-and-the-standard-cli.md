---
title: ODBC e a CLI padrão | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5485da176b9bd4aa7afca7afa088e6932d6f0d58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273299"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e a CLI padrão
ODBC alinha-se com as seguintes especificações e padrões que lidam com a Interface de nível de chamada (CLI). (Os recursos de ODBC são um subconjunto de cada um desses padrões.)  
  
-   A especificação do Open Group CAE "gerenciamento de dados: Interface de nível de chamada SQL (CLI)"  
  
-   ISO/IEC 9075-Interface de nível de chamada 3:1995 (E) (SQL/CLI)  
  
 Como resultado, esse alinhamento forem verdadeiras:  
  
-   Um aplicativo escrito para o Open Group e especificações ISO CLI funcionará com um ODBC 3. *x* driver ou um driver compatível com os padrões quando ele é compilado com o ODBC 3. *x* arquivos de cabeçalho e vinculado com o ODBC 3. *x* bibliotecas, e quando ele ganha acesso para o driver por meio de ODBC 3. *x* Gerenciador de Driver.  
  
-   Um driver escrito com as especificações do Open Group e a CLI de ISO funcionará com um ODBC 3 *. x* aplicativo ou um aplicativo compatível com os padrões quando ele é compilado com o ODBC 3 *. x* arquivos de cabeçalho e vinculado com o ODBC 3 *. x* bibliotecas, e quando o aplicativo obtém acesso ao driver por meio de ODBC 3 *. x* Gerenciador de Driver. (Para obter mais informações, consulte [compatível com os padrões de aplicativos e Drivers](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 O nível de conformidade de interface Core abrange todos os recursos na CLI do ISO e todos os recursos os na CLI do grupo aberto. Recursos opcionais da CLI do grupo aberto aparecem em níveis mais altos de conformidade de interface. Porque todos os ODBC 3. *x* drivers são necessários para dar suporte os recursos no nível de conformidade de interface de núcleo, as seguintes condições forem verdadeiras:  
  
-   ODBC 3. *x* driver dará suporte a todos os recursos usados por um aplicativo compatível com os padrões.  
  
-   ODBC 3. *x* aplicativo usando apenas os recursos na CLI do ISO e os recursos da CLI do grupo aberto funcionará com qualquer driver compatível com os padrões.  
  
 Além das especificações de interface de nível de chamada contidas nos padrões ISO/IEC e abrir CLI de grupo, o ODBC implementa os seguintes recursos. (Alguns desses recursos existiam em versões do ODBC anterior à ODBC 3. *x*.)  
  
-   Multilinha buscas por uma única chamada de função  
  
-   Associando a uma matriz de parâmetros  
  
-   Suporte a indicadores como buscar por indicador, indicadores de comprimento variável e em massa de atualização e exclusão por operações de indicador em linhas não adjacentes  
  
-   Associação por linha  
  
-   Deslocamentos de associação  
  
-   Suporte a lotes de instruções SQL, em um procedimento armazenado ou como uma sequência de instruções SQL executadas por meio **SQLExecute** ou **SQLExecDirect**  
  
-   As contagens de linhas de cursor exato ou aproximado  
  
-   Posicionado exclusões e atualizações em lote e operações de exclusão e atualização pela chamada de função (**SQLSetPos**)  
  
-   Funções de catálogo que extrair informações do esquema de informações sem a necessidade de dar suporte a modos de exibição de esquema de informações  
  
-   Sequências de escape para procedimentos armazenados, funções escalares, literais datetime, literais de intervalo e junções externas  
  
-   Bibliotecas de tradução de página de código  
  
-   Relatórios de nível de conformidade ANSI um driver e o suporte do SQL  
  
-   Sob demanda a população automática do descritor de parâmetro de implementação  
  
-   Diagnóstico aprimorado e matrizes de status de linha e de parâmetro  
  
-   Data e hora, intervalo, decimal/numeric e tipos de buffer de aplicativo inteiro de 64 bits  
  
-   Execução assíncrona  
  
-   Suporte de procedimento armazenado, incluindo sequências de escape, mecanismos de associação de parâmetro de saída e funções de catálogo  
  
-   Aprimoramentos de Conexão, incluindo suporte para atributos de conexão e navegação de atributo
