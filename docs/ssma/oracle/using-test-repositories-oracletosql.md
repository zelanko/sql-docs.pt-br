---
title: "Usando repositórios de teste (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 2f32eec1e117a2f27b9581456dd707adf6d21f56
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="using-test-repositories-oracletosql"></a>Uso de repositórios de teste (OracleToSQL)
Os repositórios de repositório de teste do SSMA SSMA Tester casos de teste e resultados de teste para uso posterior. Os dados de repositório são salvos nas tabelas do SQL Server **TestCaseRepository** e **RunTestCaseResultRepository** no esquema **ssma_oracle_utilities** de **ssmatesterdb** banco de dados.  
  
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
  
-   Clique o **executar** para abrir o [casos de teste em execução (OracleToSQL)](http://msdn.microsoft.com/en-us/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) caixa de diálogo e executar o teste selecionado.  
  
## <a name="test-results-repository"></a>Repositório de resultados de teste  
Você pode exibir o repositório de resultados de teste a **resultados de teste** página do **repositório de casos de teste** janela. Abra-o clicando em **resultados de teste...** do **Tester** menu.  
  
Você pode usar dois filtros na **resultados de teste** página:  
  
-   O filtro de nome de caso de teste: permite escolher os resultados do teste por nome do caso de teste. Esse filtro **todos os casos de teste** valor permite exibir os resultados de teste para todos os casos de teste.  
  
-   O filtro de data de execução do caso de teste: filtros de resultados de teste pela data de salvar. Esse filtro **todo o período** valor permite exibir resultados de teste para qualquer data de salvar.  
  
As seguintes informações sobre resultados de teste são exibidas na grade.  
  
-   Nome: nome do caso de teste.  
  
-   Salvo: Teste a data do caso de salvar.  
  
-   : Um breve resumo de resultados Da execução de teste (dica de ferramenta dessa célula exibe um resumo completo de execução de teste).  
  
Os botões a seguir estão disponíveis na página de resultados de teste:  
  
-   Clique o **exibição** para abrir [exibindo relatórios de caso de teste &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) de resultado de caso de teste atual.  
  
-   Clique o **excluir** botão para excluir o resultado do teste selecionado  
  
## <a name="see-also"></a>Consulte também  
[Executar casos de teste &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testando migrados objetos de banco de dados &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
