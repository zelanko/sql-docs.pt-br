---
title: Consultas do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 27c45ab4dc51b86241d198da160b5ae5cf5ccf56
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158366"
---
# <a name="integration-services-ssis-queries"></a>Consultas do SSIS (Integration Services)
  A tarefa Executar SQL, a origem OLE DB, o destino OLE DB e a transformação Pesquisa podem usar consultas de SQL. Na tarefa Executar SQL, as instruções SQL podem criar, atualizar e excluir objetos de banco de dados e dados; executar procedimentos armazenados e executar instruções SELECT. Na origem OLE DB e na transformação Pesquisa, as instruções SQL são normalmente instruções SELECT ou EXEC. Esta última normalmente executa procedimentos que retornam conjuntos de resultados.  
  
 Uma consulta pode ser analisada para estabelecer se é válida. Ao analisar uma consulta que usa uma conexão com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a consulta é analisada, executada e o resultado de execução (sucesso ou falha) é atribuído ao resultado da análise. Se a consulta usar uma conexão com dados que seja diferente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a instrução só será analisada.  
  
 A instrução SQL pode ser definida sendo digitada diretamente no designer ou especificando uma conexão de arquivo ou uma variável que contenha a instrução.  
  
## <a name="direct-input-sql"></a>SQL de entrada direta  
 O Construtor de Consultas está disponível na interface do usuário para a tarefa Executar SQL, a origem OLE DB, o destino OLE DB e a transformação Pesquisa. O Construtor de Consultas oferece as seguintes vantagens:  
  
-   Possibilidade de trabalhar visualmente com comandos SQL.  
  
     O Construtor de Consultas inclui painéis gráficos que compõem a consulta visualmente e um painel de texto que exibe o texto SQL de sua consulta. Você pode trabalhar nos painéis gráfico ou de texto. O Construtor de Consultas sempre sincroniza as exibições de forma que o texto da consulta e a representação gráfica sempre sejam correspondentes.  
  
-   Possibilidade de unir tabelas relacionadas.  
  
     Se você adicionar mais de uma tabela a sua consulta, o Construtor de Consultas determinará automaticamente como as tabelas estão relacionadas e construirá o comando de junção apropriado.  
  
-   Consulta ou atualização de bancos de dados.  
  
     Você pode usar o Construtor de Consultas para retornar dados usando instruções Transact-SQL SELECT ou para criar consultas que atualizem, adicionem ou excluam registros de um banco de dados.  
  
-   Exibição e edição imediatas de resultados.  
  
     Você pode executar sua consulta e trabalhar com um conjunto de registros em uma grade que permite rolagem e edição de registros no banco de dados.  
  
 Embora o Construtor de Consultas seja visualmente limitado para criação de consultas SELECT, você pode digitar o SQL para outros tipos de instruções como DELETE e UPDATE no painel de texto. O painel gráfico é atualizado automaticamente para refletir a instrução SQL digitada.  
  
 Você também pode fornecer entrada direta digitando a consulta na caixa de diálogo de componente de tarefa ou fluxo de dados ou na janela Propriedades.  
  
 Para obter mais informações, consulte [Query Builder](../../2014/integration-services/query-builder.md).  
  
## <a name="sql-in-files"></a>SQL em arquivos  
 A instrução SQL da tarefa Executar SQL também pode residir em um arquivo separado. Por exemplo, você pode escrever consultas usando ferramentas como o Editor de Consultas no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], salvar a consulta em um arquivo e depois ler a consulta no arquivo ao executar um pacote. O arquivo pode conter apenas as instruções SQL para execução e comentários. Para usar uma instrução SQL armazenada em um arquivo, forneça uma conexão de arquivo que especifique o nome do arquivo e o local. Para obter mais informações, consulte [File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL em variáveis  
 Se a origem da instrução SQL na tarefa Executar SQL for uma variável, forneça o nome da variável que contém a consulta. A propriedade Value da variável contém o texto de consulta. Você define a propriedade ValueType da variável como um tipo de dados String e digita ou copia a instrução SQL na propriedade Value. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md).  
  
  
