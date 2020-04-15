---
title: Arquitetura do Motorista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffe2023f028357468700b9bd995d22129ba06817
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294216"
---
# <a name="driver-architecture"></a>Arquitetura do driver
A arquitetura do driver se enquadra em duas categorias, dependendo de qual software processa instruções SQL:  
  
-   **Drivers baseados em arquivos** O motorista acessa os dados físicos diretamente. Neste caso, o motorista atua como motorista e fonte de dados; ou seja, processa chamadas ODBC e declarações SQL. Por exemplo, drivers dBASE são drivers baseados em arquivos porque o dBASE não fornece um mecanismo de banco de dados autônomo que o motorista pode usar. É importante notar que os desenvolvedores de drivers baseados em arquivos devem escrever seus próprios mecanismos de banco de dados.  
  
-   **Drivers baseados em DBMS** O motorista acessa os dados físicos através de um mecanismo de banco de dados separado. Neste caso, o driver processa apenas chamadas ODBC; ele passa instruções SQL para o mecanismo de banco de dados para processamento. Por exemplo, os drivers Oracle são drivers baseados em DBMS porque a Oracle tem um mecanismo de banco de dados autônomo que o driver usa. Onde o mecanismo do banco de dados reside é imaterial. Ele pode residir na mesma máquina que o driver ou em uma máquina diferente na rede; ele pode até ser acessado através de um gateway.  
  
 A arquitetura do driver é geralmente interessante apenas para escritores de driver; ou seja, a arquitetura do driver geralmente não faz diferença para o aplicativo. No entanto, a arquitetura pode afetar se um aplicativo pode usar SQL específico do DBMS. Por exemplo, o Microsoft Access fornece um mecanismo de banco de dados autônomo. Se um driver do Microsoft Access for baseado em DBMS - ele acessa os dados através deste mecanismo - o aplicativo pode passar instruções Microsoft Access-SQL para o mecanismo para processamento.  
  
 No entanto, se o driver for baseado em arquivos - ou seja, ele contém um mecanismo proprietário que acessa diretamente o arquivo Microsoft® Access .mdb - qualquer tentativa de passar instruções SQL específicas do Microsoft Access para o motor provavelmente resultará em erros de sintaxe. A razão é que o motor proprietário provavelmente implementará apenas o ODBC SQL.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Drivers baseados em arquivo](../../odbc/reference/file-based-drivers.md)  
  
-   [Drivers baseados em DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Exemplo de rede](../../odbc/reference/network-example.md)  
  
-   [Outras arquiteturas do driver](../../odbc/reference/other-driver-architectures.md)
