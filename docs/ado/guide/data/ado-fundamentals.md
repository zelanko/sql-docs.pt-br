---
title: Conceitos básicos do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 75f5030f8faa5aa5d8e8a0f6bcb6d72b186c8448
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926069"
---
# <a name="ado-fundamentals"></a>Conceitos básicos do ADO
O ADO fornece aos desenvolvedores um modelo de objeto lógico e poderoso para acessar, editar e atualizar dados programaticamente de uma ampla variedade de fontes de dados por meio de interfaces de sistema OLE DB. O uso mais comum do ADO é consultar uma tabela ou tabelas em um banco de dados relacional, recuperar e exibir os resultados em um aplicativo e, talvez, permitir que os usuários façam e salvem alterações nos dados. Outras tarefas incluem o seguinte:  
  
-   Consultando um banco de dados usando SQL e exibindo os resultados.  
  
-   Acessando informações em um armazenamento de arquivos pela Internet.  
  
-   Manipulação de mensagens e pastas em um sistema de email.  
  
-   Salvando dados de um banco de dado em um arquivo XML.  
  
-   Executando comandos descritos com XML e recuperando um fluxo XML.  
  
-   Salvando dados em um fluxo binário ou XML.  
  
-   Permitir que um usuário revise e altere dados em tabelas de banco de dado.  
  
-   Criando e reutilizando comandos de banco de dados com parâmetros.  
  
-   Executando procedimentos armazenados.  
  
-   Criar dinamicamente uma estrutura flexível, chamada de conjunto de **registros**, para manter, navegar e manipular dados.  
  
-   Executando operações de banco de dados transacionais.  
  
-   Filtrar e classificar cópias locais de informações do banco de dados com base em critérios de tempo de execução.  
  
-   Criando e manipulando resultados hierárquicos de bancos de dados.  
  
-   Associando campos de banco de dados a componentes com reconhecimento de dado.  
  
-   Criando **conjuntos de registros**remotos desconectados.  
  
 O ADO expõe uma ampla variedade de opções e configurações para fornecer essa flexibilidade. Portanto, é importante tomar uma abordagem unificada para aprender a usar o ADO em um aplicativo, dividindo cada um de seus objetivos em partes gerenciáveis.  
  
 Quatro operações principais estão envolvidas na maioria dos aplicativos que usam ADO: obtendo dados, examinando dados, editando dados e atualizando dados. Essas operações são examinadas mais detalhadamente mais adiante nesta seção.  
  
 No entanto, antes de discutirmos esses detalhes, apresentaremos uma visão geral do modelo de objeto do ADO e de um aplicativo ADO simples, que é escrito no Microsoft® Visual Basic® e executa cada uma das quatro operações principais do ADO:  
  
-   [Objetos e coleções ADO](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: um aplicativo ADO simples](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [Provedores de OLE DB](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [Errors](../../../ado/guide/data/errors-ado.md)
