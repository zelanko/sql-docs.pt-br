---
title: Usando repositórios de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 939342a85ed657faa645c593018cbf39042031c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625823"
---
# <a name="using-test-repositories-sybasetosql"></a>Uso de repositórios de teste (SybaseToSQL)
O repositório de teste do SSMA armazenamentos casos de teste do testador do SSMA e resultados de teste para uso posterior. Os dados de repositório são salvos nas tabelas do SQL Server **TestCaseRepository** e **RunTestCaseResultRepository** no esquema **ssma_sybase_utilities** de **ssmatesterdb_syb** banco de dados.  
  
Os seguintes botões estão disponíveis na caixa de diálogo repositório de casos de teste:  
  
-   Clique o **Refresh** botão para atualizar a lista de casos de teste ou resultados de teste.  
  
-   Clique o **feche** botão para fechar a caixa de diálogo repositório de casos de teste.  
  
## <a name="test-cases-repository"></a>Repositório de casos de teste  
Você pode exibir o repositório de casos de teste clicando **casos de teste...**  do **testador** menu. O SSMA, em seguida, exibe o **repositório de casos de teste** janela da caixa de diálogo com uma lista de casos de teste salvos no **casos de teste** página.  
  
A grade mostra as seguintes informações sobre cada caso de teste:  
  
-   Nome: O nome do caso de teste.  
  
-   Criado: A data de criação do caso de teste.  
  
-   Modificação: O caso de teste Data da última modificação.  
  
-   Descrição: As descrições de caso de teste.  
  
Os seguintes botões estão disponíveis na página de casos de teste:  
  
-   Clique o **adicionar** botão para executar o Assistente de caso de teste e criar um novo teste.  
  
-   Clique o **remover** botão para excluir o teste selecionado do repositório. Quando um caso de teste é excluído, todos os resultados de teste relacionados também são excluídos.  
  
-   Clique o **editar** botão para executar o Assistente de caso de teste e alterar o teste selecionado.  
  
-   Clique no **executados** para abrir o [executando casos de teste &#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) caixa de diálogo e executar o teste selecionado.  
  
## <a name="test-results-repository"></a>Repositório de resultados de teste  
Você pode exibir o repositório de resultados de teste na **resultados de teste** página do **repositório de casos de teste** janela. Abra-o clicando em **resultados de teste...**  do **testador** menu.  
  
Você pode usar dois filtros na **resultados de teste** página:  
  
-   O filtro de nome de caso de teste: Permite escolher os resultados do teste por nome do caso de teste. Esse filtro **todos os casos de teste** valor permite que a exibição dos resultados de teste para todos os casos de teste.  
  
-   O filtro de data de execução do caso de teste: Filtros de resultados do teste por data de salvar. Esse filtro **todo o período** valor permite exibir os resultados de teste para qualquer data de salvar.  
  
As seguintes informações sobre resultados de teste são exibidas na grade.  
  
-   Nome: Nome do caso de teste.  
  
-   Introdução: Data do caso de teste de execução.  
  
-   Resultado: Um breve resumo da execução de teste (dica de ferramenta dessa célula exibe um resumo completo de execução de teste).  
  
Os seguintes botões estão disponíveis na página de resultados de teste:  
  
-   Clique o **modo de exibição** para abrir [exibindo relatórios de caso de teste &#40;SybaseToSQL&#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) do resultado do caso de teste atual.  
  
-   Clique o **excluir** botão para excluir o resultado do teste selecionado  
  
## <a name="see-also"></a>Consulte também  
[Executar casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testar objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
