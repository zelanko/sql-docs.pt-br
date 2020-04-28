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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286496"
---
# <a name="what-is-odbc"></a>O que é o ODBC?
Há muitas concepções erradas sobre o ODBC no mundo da computação. Para o usuário final, é um ícone no painel de controle do Microsoft® Windows®. Para o programador de aplicativos, é uma biblioteca que contém rotinas de acesso a dados. Para muitos outros, é a resposta a todos os problemas de acesso ao banco de dados jamais imaginados.  
  
 Primeiro, o ODBC é uma especificação para uma API de banco de dados. Essa API é independente de um DBMS ou sistema operacional; Embora este manual use C, a API ODBC é independente de linguagem. A API ODBC é baseada nas especificações da CLI de Open Group e ISO/IEC. ODBC 3. o *x* implementa totalmente essas duas especificações: as versões anteriores do ODBC eram baseadas em versões preliminares dessas especificações, mas não as implementamos totalmente e adiciona recursos comumente necessários aos desenvolvedores de aplicativos de banco de dados baseados em tela, como cursores roláveis.  
  
 As funções na API ODBC são implementadas por desenvolvedores de drivers específicos do DBMS. Os aplicativos chamam as funções nesses drivers para acessar dados de maneira independente de DBMS. Um Gerenciador de driver gerencia A comunicação entre aplicativos e drivers.  
  
 Embora a Microsoft forneça um Gerenciador de driver para computadores que executam o Microsoft Windows® 95 e posterior, o escreveu vários drivers ODBC e chama funções ODBC de alguns de seus aplicativos, qualquer pessoa pode escrever aplicativos e drivers ODBC. Na verdade, a grande maioria dos aplicativos e drivers ODBC disponíveis hoje é escrita por empresas que não sejam a Microsoft. Além disso, existem drivers e aplicativos ODBC no® do Macintosh e em uma variedade de plataformas UNIX.  
  
 Para ajudar os desenvolvedores de aplicativos e drivers, a Microsoft oferece um SDK (Software Development Kit) ODBC para computadores que executam o Windows 95 e posterior que fornece o Gerenciador de driver, DLL do instalador, ferramentas de teste e aplicativos de exemplo. A Microsoft se integra ao Visigenic software para portar esses SDKs para o Macintosh e uma variedade de plataformas UNIX.  
  
 É importante entender que o ODBC foi projetado para expor recursos de banco de dados, e não complementá-los. Portanto, os gravadores de aplicativo não devem esperar que o uso do ODBC transforme repentinamente um banco de dados simples em um mecanismo de banco de dados relacional totalmente em destaque. Nem os criadores de driver esperavam implementar a funcionalidade não encontrada no banco de dados subjacente. Uma exceção a isso é que os desenvolvedores que escrevem drivers que acessam diretamente dados de arquivo (como dados em um arquivo Xbase) são necessários para gravar um mecanismo de banco de dados que ofereça suporte ao mínimo de funcionalidade SQL mínima. Outra exceção é que o componente ODBC do SDK do Windows, anteriormente incluído no SDK do MDAC (Microsoft Data Access Components), fornece uma biblioteca de cursores que simula os cursores roláveis para drivers que implementam um determinado nível de funcionalidade.  
  
 Os aplicativos que usam o ODBC são responsáveis por qualquer funcionalidade entre bancos de dados. Por exemplo, o ODBC não é um mecanismo de junção heterogênea, nem é um processador de transações distribuídas. No entanto, como ele é independente de DBMS, ele pode ser usado para criar ferramentas entre bancos de dados.
