---
title: Principais considerações de segurança do SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7b89745551ba3f4d82272387149bca21466e9813
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010390"
---
# <a name="core-sqlxml-security-considerations"></a>Principais considerações de segurança do SQLXML
  A seguir, encontram-se diretrizes de segurança para o uso do SQLXML para acessar dados.  
  
-   O provedor SQLXMLOLEDB expõe uma propriedade `StreamFlags` que permite definir sinalizadores para indicar qual funcionalidade do SQLXML deve ser habilitada ou desabilitada para cada instância específica. Você pode usar essa propriedade para personalizar o uso do SQLXML e ter certeza de que apenas os que você deseja estão habilitados. Para obter mais informações, consulte [provedor SQLXMLOLEDB &#40;SQLXML 4.0&#41;](../../../database-engine/dev-guide/sqlxmloledb-provider-sqlxml-4-0.md).  
  
-   Quando erros de SQLXML ocorrem e são retornados, eles podem conter informações sobre o esquema de banco de dados, como nomes de tabela, nomes de colunas ou informações sobre tipo. Você deve ter cuidado ao tratar esses erros, para que as informações sobre a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não sejam facilmente descobertas por usuários não autorizados.  
  
-   Quando usado para consultar ou enviar atualizações para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o SQLXML não define limites para a quantidade de dados que podem ser trocados e não faz nenhuma verificação em relação ao tamanho dos dados em uma carga do SQLXML antes de tentar processá-los. Quando você desenvolve seu aplicativo usando SQLXML, é sua responsabilidade assegurar que haja memória suficiente no sistema para processar os dados. Por exemplo, ao consultar dados do servidor, você deve verificar se há espaço suficiente na memória do cliente para armazená-los. Da mesma forma, se você está carregando dados para o servidor, deve verificar se há memória disponível para processá-los e se há espaço disponível em disco no servidor para armazenar os dados.  
  
-   O SQLXML gera dinamicamente consultas de [!INCLUDE[tsql](../../../includes/tsql-md.md)] e atualiza comandos e os envia ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para execução. Esse é o único modo no qual o SQLXML consulta e atualiza o servidor. Os resultados serão recebidos como um fluxo (de XML) ou como um conjunto de linhas.  
  
-   Ao receber resultados de consulta, o SQLXML não executa nenhuma ação com base no conteúdo dos dados que recebe. Nenhum processamento adicional é feito baseado no tipo ou no conteúdo dos dados. Os dados nunca são tratados como código com o qual as ações serão executadas.  
  
-   Ao executar modelos XML, o SQLXML converte as consultas XPath e DBObject contidas no modelo enviado em comandos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] que são, por sua vez, executados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses comandos só afetam os dados existentes. Os comandos gerados pelo SQLXML nunca alterarão a estrutura do banco de dados. Os usuários devem executar comandos explícitos para alterar a estrutura do banco de dados. Por exemplo, incluindo-os em um bloco `sql:query` de um modelo.  
  
-   Ao executar consultas DBObject e instruções XPath em arquivos de mapeamento, o SQLXML não alterará os dados no banco de dados.  
  
-   O SQLXML pode fazer alterações de formatação nos dados especificados com base nas diferenças entre os XML e os modelos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, o formato para especificar hora é diferente. O SQLXML tentará resolver essas diferenças. Como resultado, algumas informações de precisão podem ser perdidas.  
  
-   O SQLXML não define limites para o tempo que leva para processar os dados. O processamento continuará até que um erro ocorra ou o processamento seja concluído.  
  
-   O SQLXML não grava no sistema de arquivos. Se os usuários quiserem salvar os dados que recuperam do banco de dados, deverão usar seus códigos.  
  
-   O SQLXML permite que os usuários executem qualquer consulta SQL que queiram no banco de dados. Essa funcionalidade nunca deve ser exposta para uma fonte não segura ou não controlada, já que ela está abrindo o banco de dados SQL para qualquer usuário.  
  
-   Ao executar diagramas de atualização, o SQLXML converte os blocos `updg:sync` em comandos DELETE, UPDATE e INSERT na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses comandos só afetam os dados existentes. Os comandos gerados pelo SQLXML nunca alterarão o banco de dados. Os usuários devem executar comandos explícitos para alterar a estrutura do banco de dados. Por exemplo, incluindo-os em um bloco `sql:query` de um modelo.  
  
-   Ao executar diagramas de atualização, o SQLXML converte o diagrama em comandos DELETE, UPDATE e INSERT na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses comandos só afetam os dados existentes. Os comandos gerados pelo SQLXML nunca alterarão o banco de dados. Os usuários devem executar comandos explícitos para alterar a estrutura do banco de dados. Por exemplo, incluindo-os em um bloco `sql:query` de um modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do SQLXML 4.0](sqlxml-4-0-security-considerations.md)  
  
  