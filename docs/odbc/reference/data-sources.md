---
description: Fontes de dados
title: Fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b9f980ad9ccd1fa38b6fce863703ec706e21a76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386052"
---
# <a name="data-sources"></a>Fontes de dados
Uma *fonte de dados* é simplesmente a fonte dos dados. Ele pode ser um arquivo, um banco de dados específico em um DBMS, ou até mesmo um Live Data feed. Os dados podem estar localizados no mesmo computador que o programa ou em outro computador em algum lugar em uma rede. Por exemplo, uma fonte de dados pode ser um DBMS do Oracle em execução em um sistema operacional do SO/2®, acessado pelo Novell® NetWare; um DBMS do IBM DB2 acessado por meio de um gateway; uma coleção de arquivos Xbase em um diretório de servidor; ou um arquivo de banco de dados local do Microsoft® Access.  
  
 A finalidade de uma fonte de dados é reunir todas as informações técnicas necessárias para acessar os dados-o nome do driver, o endereço de rede, o software de rede, etc., em um único local e ocultá-lo do usuário. O usuário deve ser capaz de examinar uma lista que inclui folha de pagamento, inventário e pessoal, escolher folha de pagamento na lista e fazer com que o aplicativo se conecte aos dados da folha de pagamento, tudo isso sem saber onde residem ou como o aplicativo foi obtido.  
  
 O termo *fonte de dados* não deve ser confundido com termos semelhantes. Neste manual, o *DBMS* ou o *banco de dados* refere-se a um mecanismo ou programa de banco de dados. Uma distinção adicional é feita entre *bancos de dados da área de trabalho,* projetada para ser executada em computadores pessoais e, muitas vezes, sem suporte completo a transações e SQL, e bancos de dados de *servidor,* projetados para execução em uma situação de cliente/servidor e caracterizado por um mecanismo de banco de dados autônomo e suporte avançado a transações e SQL. O *banco* de dados também se refere a uma determinada coleção de data, como uma coleção de arquivos Xbase em um diretório ou em uma SQL Server. Geralmente é equivalente ao catálogo de termos *,* usado em outro lugar neste manual ou no *qualificador* de termo em versões anteriores do ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de fontes de dados](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usando fontes de dados](../../odbc/reference/using-data-sources.md)  
  
-   [Exemplo de fonte de dados](../../odbc/reference/data-source-example.md)
