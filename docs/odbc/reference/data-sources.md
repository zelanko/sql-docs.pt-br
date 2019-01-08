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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb02dd54ea57af668e56fe910ca92830fb09c418
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514689"
---
# <a name="data-sources"></a>Fontes de dados
Um *fonte de dados* é simplesmente a origem dos dados. Ele pode ser um arquivo, um determinado banco de dados em um DBMS, ou até mesmo um feed de dados ao vivo. Os dados podem ser localizados no mesmo computador que o programa, ou em outro computador em algum lugar em uma rede. Por exemplo, uma fonte de dados pode ser um DBMS Oracle em execução em um sistema de operacional OS/2®, acessado por® do Novell Netware; um DBMS de DB2 da IBM acessados por meio de um gateway. uma coleção de arquivos do Xbase em um diretório de servidor; ou um arquivo de banco de dados local do Microsoft® Access.  
  
 A finalidade de uma fonte de dados é reunir todas as informações técnicas necessárias para acessar os dados, o nome do driver, endereço de rede, software de rede e assim por diante - o em um único lugar e ocultá-lo do usuário. O usuário deve ser capaz de examinar uma lista que inclui a folha de pagamento, inventário e pessoal, escolha a folha de pagamento na lista e ter o aplicativo se conectar aos dados da folha de pagamento, tudo sem saber onde residem os dados de folha de pagamento ou como o aplicativo obteve a ele.  
  
 O termo *fonte de dados* não devem ser confundidas com termos semelhantes. Neste manual *DBMS* ou *banco de dados* refere-se a um programa de banco de dados ou o mecanismo. Outra distinção é feita entre *bancos de dados da área de trabalho* projetado para ser executado em computadores pessoais e geralmente deficiente em SQL completo e suporte a transações, e *bancos de dados do servidor,* projetado para ser executado em um cliente / situação do servidor e caracterizados por um mecanismo de banco de dados autônomo e SQL Avançado e suporte a transações. *Banco de dados* também se refere a uma determinada coleção de dados, como uma coleção de arquivos do Xbase em um diretório ou um banco de dados no SQL Server. É geralmente equivalente ao termo *catálogo,* usado em outro local deste manual ou o termo *qualificador* em versões anteriores do ODBC.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de fontes de dados](../../odbc/reference/types-of-data-sources.md)  
  
-   [Usando fontes de dados](../../odbc/reference/using-data-sources.md)  
  
-   [Exemplo de fonte de dados](../../odbc/reference/data-source-example.md)
