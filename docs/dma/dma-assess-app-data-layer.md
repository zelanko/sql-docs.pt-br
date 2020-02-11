---
title: Avaliar a camada de acesso a dados de um aplicativo com Assistente de Migração de Dados
description: Saiba como usar Assistente de Migração de Dados para avaliar a camada de acesso a dados de um aplicativo.
ms.date: 01/23/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 24763f190172da637d19df7ce36553b7341bd894
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76761980"
---
# <a name="assess-an-apps-data-access-layer-with-data-migration-assistant"></a>Avaliar a camada de acesso a dados de um aplicativo com Assistente de Migração de Dados

Os aplicativos normalmente se conectam e mantêm dados em um banco de dado. A camada de acesso a dados do aplicativo fornece acesso simplificado a esses dados. O Assistente de Migração de Dados (DMA) permitiu que os usuários avaliassem seus bancos de dados e objetos relacionados. A versão mais recente do DMA (v 5.0) apresenta suporte para análise de conectividade de banco de dados e consultas SQL inseridas no código do aplicativo.

Considere o segmento de código C# abaixo:

![Segmento de código C# de exemplo](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-segment.png)

Nesse caso, você pode ver que o aplicativo está usando uma consulta SQL para obter o nome de um funcionário.

![Detalhes do segmento de código C# de exemplo](../dma/media/dma-assess-app-data-layer/dma-sample-c-sharp-code-detail.png)

Como proprietário de um aplicativo, preciso ser capaz de identificar os vários bancos de dados aos quais o aplicativo pode se conectar e as consultas inseridas na camada de acesso a dados do aplicativo. Além disso, preciso identificar as alterações necessárias para modernizar o aplicativo para os serviços de dados do Azure.

## <a name="assess-an-app-with-data-access-migration-toolkit"></a>Avaliar um aplicativo com o kit de ferramentas de migração de acesso a dados

Para habilitar essa avaliação, introduzimos recentemente o Data Access Migration Toolkit (DAMT), uma extensão Visual Studio Code. A versão mais recente desta extensão (v 0,2) adiciona suporte para aplicativos .net e dialeto T-SQL.

1. Baixe e instale o VS Code [aqui](https://code.visualstudio.com/download).
2. Habilite a [extensão do kit de ferramentas de migração de acesso a dados](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit) do Marketplace de extensões.

   ![Página extensão do kit de migração de acesso a dados](../dma/media/dma-assess-app-data-layer/dma-damt-extension-page.png)

3. Abra o projeto de aplicativo no Visual Studio Code.

   ![Projeto de aplicativo no Visual Studio Code](../dma/media/dma-assess-app-data-layer/dma-app-project-in-vscode.png)

4. Inicie o console de extensão (Ctrl-Shft-P) e execute o comando **acesso a dados: analisar espaço de trabalho** .

   ![Console de extensão no Visual Studio Code](../dma/media/dma-assess-app-data-layer/dma-vscode-extension-console.png)

5. Selecione o dialeto SQL Server.

   ![SQL Server seleção de dialeto](../dma/media/dma-assess-app-data-layer/dma-sql-server-dialect.png)

   No final da análise, o comando produz um relatório de comandos e consultas de conectividade do SQL.

   ![Relatório de acesso a dados](../dma/media/dma-assess-app-data-layer/dma-data-access-report.png)

6. Examine o relatório de componentes de conectividade de dados e consultas SQL inseridas no código do aplicativo, que aparecem realçadas.

   ![Consultas SQL no código do aplicativo](../dma/media/dma-assess-app-data-layer/dma-sql-queries-in-app-code.png)

   Essas consultas podem ser analisadas por meio de DMA para obter compatibilidade e problemas de paridade de recursos com base na plataforma SQL de destino.

7. Para avaliar a camada de dados do aplicativo, exporte o relatório como arquivo JSON.

   ![exportação de arquivo. JSON](../dma/media/dma-assess-app-data-layer/dma-json-file-export.png)

   Nesse caso, o arquivo gerado é:

   ![Exibir conteúdo do arquivo JSON](../dma/media/dma-assess-app-data-layer/dma-json-file-contents.png)

   Assistente de Migração de Dados permite avaliar as consultas identificadas no aplicativo dentro do contexto de modernização do banco de dados para a plataforma do Azure Data.

8. Inicie o Assistente de Migração de Dados e, em seguida, crie um projeto de avaliação.

   ![Assistente de Migração de Dados novo projeto de avaliação](../dma/media/dma-assess-app-data-layer/dma-new-assessment-project.png)

9. Selecione a instância de SQL Server de origem.

   ![Assistente de Migração de Dados selecionar fonte de SQL Server](../dma/media/dma-assess-app-data-layer/dma-select-sql-source.png)

10. Selecione o banco de dados ao qual o aplicativo está se conectando.

    ![Data Access Migration selecionar banco de dados de aplicativo](../dma/media/dma-assess-app-data-layer/dma-select-app-database.png)

    Para facilitar a avaliação de acesso a dados, o DMA apresenta a capacidade de incluir arquivos JSON com consultas de aplicativo. Em seguida, incluiremos o arquivo JSON que criamos anteriormente com as consultas de aplicativo.

11. Selecione o banco de dados e navegue até o arquivo JSON exportado de Data Access Migration Toolkit para incluir as consultas do aplicativo para a avaliação.

    ![Assistente de Migração de Dados abrir arquivo JSON DMAT](../dma/media/dma-assess-app-data-layer/dma-open-damt-json-file.png)

12. Inicie a avaliação.

    ![Assistente de Migração de Dados Iniciar avaliação](../dma/media/dma-assess-app-data-layer/dma-start-assessment.png)

13. Examine o relatório de avaliação. O relatório gerado incluirá quaisquer problemas de compatibilidade ou de paridade de recursos detectados nas consultas de aplicativo, conforme mostrado abaixo.

    ![Relatório de avaliação de Assistente de Migração de Dados](../dma/media/dma-assess-app-data-layer/dma-assessment-report.png)

Agora, além de ter a perspectiva do banco de dados da migração, os usuários também têm uma exibição da perspectiva do aplicativo.

## <a name="see-also"></a>Confira também

* [Visão geral do Assistente de Migração de Dados](../dma/dma-overview.md)
* [Assistente de Migração de Dados: definições de configuração](../dma/dma-configurationsettings.md)
* [Assistente de Migração de Dados: práticas recomendadas](../dma/dma-bestpractices.md)
* [Kit de ferramentas de migração de acesso a dados](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)