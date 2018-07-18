---
title: Usando repositórios de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 863fee753776b0e86408d6ccd0d9d7e0cfc7f33b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979738"
---
# <a name="using-test-repositories-oracletosql"></a>Usando repositórios de teste (OracleToSQL)
O repositório de teste do SSMA armazenamentos casos de teste do testador do SSMA e resultados de teste para uso posterior. Os dados de repositório são salvos nas tabelas do SQL Server **TestCaseRepository** e **RunTestCaseResultRepository** no esquema **ssma_oracle_utilities** de **ssmatesterdb** banco de dados.  
  
Os seguintes botões estão disponíveis na caixa de diálogo repositório de casos de teste:  
  
-   Clique o **Refresh** botão para atualizar a lista de casos de teste ou resultados de teste.  
  
-   Clique o **feche** botão para fechar a caixa de diálogo repositório de casos de teste.  
  
## <a name="test-cases-repository"></a>Repositório de casos de teste  
Você pode exibir o repositório de casos de teste clicando **casos de teste...** dos **testador** menu. O SSMA, em seguida, exibe o **repositório de casos de teste** janela da caixa de diálogo com uma lista de casos de teste salvos no **casos de teste** página.  
  
A grade mostra as seguintes informações sobre cada caso de teste:  
  
-   Nome: O nome de caso de teste.  
  
-   Criado: A caso de teste data de criação.  
  
-   Modificado: O caso de teste Data da última modificação.  
  
-   Descrição: As caso de teste descrições.  
  
Os seguintes botões estão disponíveis na página de casos de teste:  
  
-   Clique o **adicionar** botão para executar o Assistente de caso de teste e criar um novo teste.  
  
-   Clique o **remover** botão para excluir o teste selecionado do repositório. Quando um caso de teste é excluído, todos os resultados de teste relacionados também são excluídos.  
  
-   Clique o **editar** botão para executar o Assistente de caso de teste e alterar o teste selecionado.  
  
-   Clique o **executados** para abrir o [executando casos de teste (OracleToSQL)](http://msdn.microsoft.com/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) caixa de diálogo e executar o teste selecionado.  
  
## <a name="test-results-repository"></a>Repositório de resultados de teste  
Você pode exibir o repositório de resultados de teste na **resultados de teste** página do **repositório de casos de teste** janela. Abra-o clicando em **resultados de teste...** dos **testador** menu.  
  
Você pode usar dois filtros na **resultados de teste** página:  
  
-   O filtro de nome do caso de teste: permite escolher os resultados do teste por nome do caso de teste. Esse filtro **todos os casos de teste** valor permite que a exibição dos resultados de teste para todos os casos de teste.  
  
-   O filtro de data de execução do caso de teste: filtros de resultados de teste por data de salvar. Esse filtro **todo o período** valor permite exibir os resultados de teste para qualquer data de salvar.  
  
As seguintes informações sobre resultados de teste são exibidas na grade.  
  
-   Nome: nome do caso de teste.  
  
-   Salvo: Teste a data do caso de salvar.  
  
-   Resultados: Um breve resumo da execução de teste (dica de ferramenta dessa célula exibe um resumo completo de execução de teste).  
  
Os seguintes botões estão disponíveis na página de resultados de teste:  
  
-   Clique o **modo de exibição** para abrir [exibindo relatórios de caso de teste &#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) do resultado do caso de teste atual.  
  
-   Clique o **excluir** botão para excluir o resultado do teste selecionado  
  
## <a name="see-also"></a>Consulte também  
[Executar casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
