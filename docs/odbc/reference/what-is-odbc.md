---
title: "O que é ODBC? | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5aaa2a57f9439eb1588a30c362118af9b5355a8d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="what-is-odbc"></a>O que é ODBC?
Muitos erros de concepção sobre ODBC existem no mundo da computação. Para o usuário final, é um ícone no painel de controle do Microsoft® Windows®. Para o programador de aplicativo, é uma biblioteca que contém rotinas de acesso a dados. Para muitos outros, é a resposta para todos os problemas de acesso ao banco de dados nunca imaginado.  
  
 Primeiramente, o ODBC é uma especificação de um banco de dados API. Essa API é independente de qualquer um DBMS ou sistema operacional. Embora este guia usa C, a API de ODBC é independente de linguagem. A API de ODBC é baseada nas especificações do Open Group e ISO/IEC CLI. ODBC 3. *x* totalmente implementa ambos essas especificações, versões anteriores do ODBC baseadas em versões anteriores dessas especificações, mas não os implementou totalmente — e adiciona recursos normalmente necessários por desenvolvedores de baseada em telas aplicativos de banco de dados, como cursores roláveis.  
  
 As funções da API do ODBC são implementadas por desenvolvedores de drivers específicos de DBMS. Aplicativos chamam as funções destes drivers para acessar dados de maneira independente do DBMS. Um Gerenciador de Driver gerencia a comunicação entre aplicativos e drivers.  
  
 Embora a Microsoft fornece um Gerenciador de driver para computadores que executam o Microsoft Windows® 95 e posterior, escreveu vários drivers ODBC e chama funções ODBC de alguns de seus aplicativos, qualquer pessoa pode gravar aplicativos de ODBC e drivers. Na verdade, a maioria dos aplicativos de ODBC e drivers disponíveis hoje são gravados pela Microsoft. Além disso, aplicativos e drivers de ODBC existem a Macintosh® em uma variedade de plataformas UNIX.  
  
 Para ajudar os desenvolvedores de drivers e aplicativos, a Microsoft oferece um ODBC Software Development Kit (SDK) para computadores que executam o Windows 95 e posterior que fornece o Gerenciador de driver, instalador DLL, as ferramentas de teste e aplicativos de exemplo. Microsoft associou-se à Visigenic Software para esses SDKs para Macintosh e uma variedade de plataformas UNIX da porta.  
  
 É importante entender que o ODBC foi projetado para expõe os recursos de banco de dados, não suplemento-los. Assim, gravadores de aplicativo não devem esperar que usando o ODBC repentinamente transformará um banco de dados simple em um mecanismo de banco de dados relacional totalmente em destaque. Nem gravadores de driver devem implementar a funcionalidade não encontrada no banco de dados subjacente. Uma exceção a isso é que os desenvolvedores que escrevem drivers que acessem diretamente os dados de arquivo (como dados em um arquivo Xbase) são necessárias para gravar um mecanismo de banco de dados que oferece suporte a pelo menos mínimo de funcionalidade SQL. Outra exceção é que o componente ODBC do SDK do Windows, anteriormente incluída no Microsoft Data Access Components (MDAC) SDK, fornece uma biblioteca de cursor que simula cursores roláveis para drivers que implementam um determinado nível de funcionalidade.  
  
 Aplicativos que usam ODBC são responsáveis por qualquer funcionalidade do banco de dados. Por exemplo, o ODBC não é um mecanismo de junção heterogêneo, nem é um processador de transação distribuída. No entanto, porque ele é independente de DBMS, ele pode ser usado para criar essas ferramentas de banco de dados.

