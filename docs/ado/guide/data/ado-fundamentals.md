---
description: Conceitos básicos do ADO
title: Conceitos básicos do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
author: rothja
ms.author: jroth
ms.openlocfilehash: 02574be8fc8333e357e31fe1e1425d6e237871a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453768"
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
  
-   [Erros](../../../ado/guide/data/errors-ado.md)
