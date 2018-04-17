---
title: ODBC e a CLI padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef863329a0f0c8a7c7b8aaef6f55717fbbc1f638
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e a CLI padrão
ODBC de acordo com as seguintes especificações e padrões que lidam com a Interface de nível de chamada (CLI). (Os recursos de ODBC são um subconjunto de cada um desses padrões.)  
  
-   A especificação de CAE Open Group "gerenciamento de dados: SQL Interface de nível de chamada (CLI)"  
  
-   ISO/IEC 9075-Interface de nível de chamada 3:1995 (E) (SQL/CLI)  
  
 Como resultado, esse alinhamento forem verdadeiras:  
  
-   Um aplicativo escrito às especificações ISO CLI do Open Group e funcionará com um ODBC 3. *x* driver ou um driver compatível com os padrões quando ele é compilado com o ODBC 3. *x* arquivos de cabeçalho e vinculado com o ODBC 3. *x* bibliotecas, e quando ele obtém acesso do driver por meio de ODBC 3. *x* Gerenciador de Driver.  
  
-   Um driver criado às especificações do Open Group e ISO CLI funcionará com um ODBC 3*. x* aplicativo ou um aplicativo compatível com os padrões quando ele é compilado com o ODBC 3*. x* arquivos de cabeçalho e vinculado com o ODBC 3*. x* bibliotecas, e quando o aplicativo obtém acesso do driver por meio de ODBC 3*. x* Gerenciador de Driver. (Para obter mais informações, consulte [compatível com os padrões de aplicativos e Drivers](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 O nível de conformidade de interface de núcleo abrange todos os recursos do CLI ISO e todos os recursos os CLI grupo aberto. Recursos opcionais do CLI grupo aberto aparecem em níveis mais altos de conformidade de interface. Como todos os ODBC 3. *x* drivers são necessários para oferecer suporte os recursos no nível de conformidade a principal interface, os seguintes condições forem verdadeiras:  
  
-   ODBC 3. *x* driver dará suporte a todos os recursos usados por um aplicativo compatível com os padrões.  
  
-   ODBC 3. *x* usando somente os recursos no ISO CLI e os recursos do CLI grupo aberto de aplicativo funcionará com qualquer driver compatível com os padrões.  
  
 Além das especificações de interface de nível de chamada contidas nos padrões ISO/IEC e abra CLI de grupo, o ODBC implementa os seguintes recursos. (Alguns desses recursos existiam em versões do ODBC antes de ODBC 3. *x*.)  
  
-   Buscas multilinha por uma única chamada de função  
  
-   Associando a uma matriz de parâmetros  
  
-   Suporte a indicadores incluindo busca pelo indicador indicadores de comprimento variável e, em massa de atualização e exclusão por operações de indicador em linhas não contíguas  
  
-   A associação  
  
-   Deslocamentos de associação  
  
-   Suporte a lotes de instruções SQL, em um procedimento armazenado ou como uma sequência de instruções SQL executadas por meio de **SQLExecute** ou **SQLExecDirect**  
  
-   Contagens de linha de cursor exato ou aproximado  
  
-   Posicionada exclusões e atualizações em lotes e operações de exclusão e atualização pela chamada de função (**SQLSetPos**)  
  
-   Funções de catálogo que extrair informações do esquema de informações sem a necessidade de exibições do esquema de informações de suporte  
  
-   Sequências de escape para procedimentos armazenados, funções escalares, literais de data e hora, literais de intervalo e junções externas  
  
-   Bibliotecas de conversão de página de código  
  
-   Relatórios de nível de conformidade ANSI e suporte SQL de um driver  
  
-   População automática sob demanda do descritor de parâmetro de implementação  
  
-   Diagnóstico aprimorado e matrizes de status de linha e de parâmetro  
  
-   Data e hora, intervalo, decimal/numeric e tipos de buffer de aplicativo inteiro de 64 bits  
  
-   Execução assíncrona  
  
-   Suporte de procedimento armazenado, incluindo sequências de escape, mecanismos de associação de parâmetro de saída e funções de catálogo  
  
-   Aprimoramentos de Conexão, incluindo suporte para atributos de conexão e a navegação de atributo
