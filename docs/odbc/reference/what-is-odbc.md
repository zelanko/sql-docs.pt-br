---
title: O que é o ODBC? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea0aa81188e5e58d3a66032af38700ece2d4e5b4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286496"
---
# <a name="what-is-odbc"></a>O que é o ODBC?
Muitos equívocos sobre a ODBC existem no mundo da computação. Para o usuário final, é um ícone no Painel de Controle ® Windows ® Microsoft. Para o programador de aplicativos, é uma biblioteca contendo rotinas de acesso a dados. Para muitos outros, é a resposta para todos os problemas de acesso ao banco de dados jamais imaginados.  
  
 Em primeiro lugar, ODBC é uma especificação para uma API de banco de dados. Esta API é independente de qualquer DBMS ou sistema operacional; embora este manual use C, a API ODBC é independente de linguagem. A API ODBC é baseada nas especificações cli do Open Group e iso/IEC. ODBC 3. *x* implementa totalmente ambas as especificações - versões anteriores do ODBC eram baseadas em versões preliminares dessas especificações, mas não as implementavam totalmente - e adiciona recursos comumente necessários pelos desenvolvedores de aplicativos de banco de dados baseados em tela, como cursores roláveis.  
  
 As funções na API ODBC são implementadas por desenvolvedores de drivers específicos do DBMS. Os aplicativos chamam as funções nesses drivers para acessar dados de forma independente do DBMS. Um Gerenciador de Driver gerencia a comunicação entre aplicativos e drivers.  
  
 Embora a Microsoft forneça um gerenciador de driverpara computadores que executam o Microsoft Windows® 95 e posterior, tenha escrito vários drivers ODBC e chame funções ODBC de alguns de seus aplicativos, qualquer pessoa pode escrever aplicativos e drivers ODBC. Na verdade, a grande maioria dos aplicativos e drivers da ODBC disponíveis hoje são escritos por outras empresas além da Microsoft. Além disso, os drivers e aplicativos ODBC existem no Macintosh® e uma variedade de plataformas UNIX.  
  
 Para ajudar os desenvolvedores de aplicativos e drivers, a Microsoft oferece um ODBC Software Development Kit (SDK) para computadores que executam o Windows 95 e, posteriormente, que fornece ao gerenciador de driver, instalador DLL, ferramentas de teste e aplicativos de amostra. A Microsoft se uniu à Visigenic Software para portar esses SDKs para o Macintosh e uma variedade de plataformas UNIX.  
  
 É importante entender que o ODBC foi projetado para expor os recursos do banco de dados, não suplementá-los. Assim, os autores de aplicativos não devem esperar que o uso do ODBC de repente transforme um banco de dados simples em um mecanismo de banco de dados relacional totalmente caracterizado. Também não se espera que os roteiristas de driver implementem funcionalidades não encontradas no banco de dados subjacente. Uma exceção para isso é que os desenvolvedores que escrevem drivers que acessam diretamente dados de arquivos (como dados em um arquivo Xbase) são obrigados a escrever um mecanismo de banco de dados que suporte pelo menos a funcionalidade mínima do SQL. Outra exceção é que o componente ODBC do Windows SDK, anteriormente incluído no Microsoft Data Access Components (MDAC) SDK, fornece uma biblioteca de cursor que simula cursores roláveis para drivers que implementam um certo nível de funcionalidade.  
  
 Os aplicativos que usam ODBC são responsáveis por qualquer funcionalidade de banco de dados cruzado. Por exemplo, o ODBC não é um mecanismo de adesão heterogêneo, nem é um processador de transações distribuídas. No entanto, por ser independente do DBMS, ele pode ser usado para construir tais ferramentas de banco de dados.
