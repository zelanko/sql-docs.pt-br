---
title: Usando repositórios de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef959c05f397a898d9c1e72adddd6b895eabf87d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="using-test-repositories-sybasetosql"></a>Uso de repositórios de teste (SybaseToSQL)
Os repositórios de repositório de teste do SSMA SSMA Tester casos de teste e resultados de teste para uso posterior. Os dados de repositório são salvos nas tabelas do SQL Server **TestCaseRepository** e **RunTestCaseResultRepository** no esquema **ssma_sybase_utilities** de **ssmatesterdb_syb** banco de dados.  
  
Os botões a seguir estão disponíveis na caixa de diálogo repositório de casos de teste:  
  
-   Clique o **atualização** botão para atualizar a lista de casos de teste ou resultados de teste.  
  
-   Clique o **fechar** para fechar a caixa de diálogo repositório de casos de teste.  
  
## <a name="test-cases-repository"></a>Repositório de casos de teste  
Você pode exibir o repositório de casos de teste clicando **casos de teste...** do **Tester** menu. O SSMA, em seguida, exibe o **repositório de casos de teste** janela da caixa de diálogo com uma lista de casos de teste salvos no **casos de teste** página.  
  
A grade mostra as seguintes informações sobre cada caso de teste:  
  
-   Nome: O nome de caso de teste.  
  
-   Criado: A caso de teste data de criação.  
  
-   Modificado: O caso de teste Data da última modificação.  
  
-   Descrição: As caso de teste descrições.  
  
Os botões a seguir estão disponíveis na página de casos de teste:  
  
-   Clique o **adicionar** para executar o Assistente de caso de teste e criar um novo teste.  
  
-   Clique o **remover** botão para excluir o teste selecionado do repositório. Quando um caso de teste é excluído, todos os resultados de teste relacionadas também serão excluídos.  
  
-   Clique o **editar** para executar o Assistente de caso de teste e alterar o teste selecionado.  
  
-   Clique o **executar** para abrir o [casos de teste em execução &#40; SybaseToSQL &#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) caixa de diálogo e executar o teste selecionado.  
  
## <a name="test-results-repository"></a>Repositório de resultados de teste  
Você pode exibir o repositório de resultados de teste a **resultados de teste** página do **repositório de casos de teste** janela. Abra-o clicando em **resultados de teste...** do **Tester** menu.  
  
Você pode usar dois filtros na **resultados de teste** página:  
  
-   O filtro de nome de caso de teste: permite escolher os resultados do teste por nome do caso de teste. Esse filtro **todos os casos de teste** valor permite exibir os resultados de teste para todos os casos de teste.  
  
-   O filtro de data de execução do caso de teste: filtros de resultados de teste pela data de salvar. Esse filtro **todo o período** valor permite exibir resultados de teste para qualquer data de salvar.  
  
As seguintes informações sobre resultados de teste são exibidas na grade.  
  
-   Nome: nome do caso de teste.  
  
-   Introdução: Data do caso de execução de teste.  
  
-   Resultado: Um breve resumo de execução de teste (dica de ferramenta dessa célula exibe um resumo completo de execução de teste).  
  
Os botões a seguir estão disponíveis na página de resultados de teste:  
  
-   Clique o **exibição** para abrir [exibindo relatórios de caso de teste &#40; SybaseToSQL &#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) do resultado do caso de teste atual.  
  
-   Clique o **excluir** botão para excluir o resultado do teste selecionado  
  
## <a name="see-also"></a>Consulte Também  
[Executar casos de teste &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testando migrados objetos de banco de dados &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
