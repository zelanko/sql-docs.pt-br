---
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
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306507"
---
# <a name="data-sources"></a>Fontes de dados
Uma *fonte de dados* é simplesmente a fonte dos dados. Pode ser um arquivo, um banco de dados específico em um DBMS, ou até mesmo um feed de dados ao vivo. Os dados podem estar localizados no mesmo computador do programa, ou em outro computador em algum lugar em uma rede. Por exemplo, uma fonte de dados pode ser um Oracle DBMS em execução em um sistema operacional OS/2®, acessado pela Novell® Netware; um IBM DB2 DBMS acessado através de um gateway; uma coleção de arquivos Xbase em um diretório de servidor; ou um arquivo local de banco de dados microsoft® access.  
  
 O objetivo de uma fonte de dados é reunir todas as informações técnicas necessárias para acessar os dados - o nome do driver, endereço de rede, software de rede e assim por diante - em um único lugar e escondê-los do usuário. O usuário deve ser capaz de olhar para uma lista que inclui Folha de Pagamento, Inventário e Pessoal, escolher Folha de Pagamento da lista e fazer com que o aplicativo se conecte aos dados da folha de pagamento, tudo sem saber onde os dados da folha de pagamento residem ou como o aplicativo chegou a ele.  
  
 O termo *fonte de dados* não deve ser confundido com termos semelhantes. Neste manual, *DBMS* ou *banco de dados* refere-se a um programa de banco de dados ou mecanismo. Uma distinção adicional é feita entre *bancos de dados de desktop, projetados* para serem executados em computadores pessoais e muitas vezes sem suporte total a SQL e transações, e *bancos de dados de servidor, projetados* para serem executados em uma situação de cliente/servidor e caracterizados por um mecanismo de banco de dados autônomo e sql rico e suporte a transações. *O banco* de dados também se refere a uma coleta particular de dados, como uma coleção de arquivos Xbase em um diretório ou um banco de dados no SQL Server. É geralmente equivalente ao *termo catálogo,* usado em outros lugares neste manual, ou o termo *qualificador* em versões anteriores do ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de fontes de dados](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usando fontes de dados](../../odbc/reference/using-data-sources.md)  
  
-   [Exemplo de fonte de dados](../../odbc/reference/data-source-example.md)
