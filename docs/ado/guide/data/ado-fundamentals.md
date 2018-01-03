---
title: "Conceitos básicos de ADO | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a6b693060ad00f8b18268c503a7d0a96f3e5e62a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="ado-fundamentals"></a>Conceitos básicos de ADO
ADO fornece aos desenvolvedores um modelo de objeto avançado, lógica para acessar programaticamente, editar e atualizar dados de uma ampla variedade de fontes de dados por meio de interfaces de OLE DB do sistema. É o uso mais comum do ADO consultar uma tabela ou tabelas em um banco de dados relacional, recuperar e exibir os resultados em um aplicativo e talvez permitem aos usuários fazer e salvar as alterações nos dados. Outras tarefas incluem o seguinte:  
  
-   Consultar um banco de dados usando o SQL e exibir os resultados.  
  
-   Acessar informações em um repositório de arquivo pela Internet.  
  
-   Manipulação de mensagens e pastas em um sistema de email.  
  
-   Salvando dados de um banco de dados em um arquivo XML.  
  
-   Executando comandos descritos com XML e recuperar um fluxo XML.  
  
-   Salvando dados em um fluxo XML ou binário.  
  
-   Permitir que um usuário revisar e alterar dados em tabelas de banco de dados.  
  
-   Criando e reutilizando parametrizadas comandos de banco de dados.  
  
-   Executando procedimentos armazenados.  
  
-   Criar dinamicamente uma estrutura flexível, que é chamada um **registros**, para manter, navegar e manipular dados.  
  
-   Executando operações de banco de dados transacional.  
  
-   Filtrando e classificando cópias locais de informações do banco de dados com base em critérios de tempo de execução.  
  
-   Criação e manipulação de resultados hierárquicos de bancos de dados.  
  
-   Campos de banco de dados de associação para componentes com reconhecimento de dados.  
  
-   Criando remoto, desconectado **conjuntos de registros**.  
  
 ADO expõe uma grande variedade de opções e configurações para fornecer essa flexibilidade. Portanto, é importante adotar uma abordagem metódica para aprender a usar o ADO em um aplicativo, separando cada uma das suas metas em partes gerenciáveis.  
  
 Quatro operações principais envolvidas na maioria dos aplicativos que usam ADO: Obtendo dados, examinando os dados, edição de dados e atualização de dados. Essas operações são examinadas em mais detalhes posteriormente nesta seção.  
  
 No entanto, antes de discutir esses detalhes, vamos apresentar uma visão geral do modelo de objeto ADO e um aplicativo ADO simples, que é gravado no Microsoft® Visual Basic® e executa cada uma das quatro operações ADO primárias:  
  
-   [Objetos e coleções ADO](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: um aplicativo ADO simples](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [Provedores OLE DB](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [Erros](../../../ado/guide/data/errors-ado.md)
