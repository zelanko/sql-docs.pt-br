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
manager: jroth
ms.openlocfilehash: 155e1e810309ee4efa40badac55ca749a4329182
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702333"
---
# <a name="ado-fundamentals"></a>Conceitos básicos do ADO
ADO oferece aos desenvolvedores um modelo de objeto lógico eficientes para acessar de modo programático, editar e atualizar dados de uma ampla variedade de fontes de dados por meio de interfaces do sistema de banco de dados OLE. É o uso mais comum do ADO consultar uma tabela ou tabelas em um banco de dados relacional, recuperar e exibir os resultados em um aplicativo e talvez permitem aos usuários fazer e salvar as alterações dos dados. Outras tarefas incluem o seguinte:  
  
-   Consultando um banco de dados usando o SQL e exibindo os resultados.  
  
-   Acesso a informações em um armazenamento de arquivos pela Internet.  
  
-   Manipulação de mensagens e pastas em um sistema de email.  
  
-   Salvar dados de um banco de dados em um arquivo XML.  
  
-   Executar comandos descritos com XML e recuperar um fluxo XML.  
  
-   Salvando dados em um fluxo XML ou binário.  
  
-   Permitir que um usuário revisar e alterar dados nas tabelas de banco de dados.  
  
-   Criar e reutilizar parametrizadas comandos de banco de dados.  
  
-   Executando procedimentos armazenados.  
  
-   Criar dinamicamente uma estrutura flexível, que é chamada de um **Recordset**, para manter, navegar e manipular dados.  
  
-   Executando operações de banco de dados transacional.  
  
-   Filtrando e classificando cópias locais de informações do banco de dados com base em critérios de tempo de execução.  
  
-   Criando e manipulando resultados hierárquicos de bancos de dados.  
  
-   Campos de banco de dados de associação para componentes que reconhecem a dados.  
  
-   Criar remoto, desconectado **conjuntos de registros**.  
  
 ADO expõe uma grande variedade de opções e configurações para fornecer tal flexibilidade. Portanto, é importante adotar uma abordagem metódica para aprender a usar o ADO em um aplicativo, separando cada um dos seus objetivos em partes gerenciáveis.  
  
 Quatro operações principais envolvidas na maioria dos aplicativos que usam o ADO: obtenção de dados, examinando os dados, edição de dados e atualização de dados. Essas operações são examinadas em mais detalhes posteriormente nesta seção.  
  
 No entanto, antes de discutir esses detalhes, apresentaremos uma visão geral do modelo de objeto ADO e um aplicativo ADO simples, que é gravado no Microsoft® Visual Basic® e executa cada uma das quatro operações ADO primárias:  
  
-   [Objetos e coleções ADO](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData: Um aplicativo ADO simples](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [Provedores OLE DB](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [Erros](../../../ado/guide/data/errors-ado.md)
