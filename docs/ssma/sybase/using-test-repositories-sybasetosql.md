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
ms.openlocfilehash: a94bd053dac04c4d595e4f2077c02d1d79858e56
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020838"
---
# <a name="using-test-repositories-sybasetosql"></a>Uso de repositórios de teste (SybaseToSQL)
O repositório de teste do SSMA armazena casos de teste e resultados de teste do SSMA Tester para uso posterior. Os dados do repositório são salvos nas tabelas de SQL Server **TestCaseRepository** e **RunTestCaseResultRepository** no esquema **ssma_sybase_utilities** do banco de dados **ssmatesterdb_syb** .  
  
Os botões a seguir estão disponíveis na caixa de diálogo repositório de casos de teste:  
  
-   Clique no botão **Atualizar** para atualizar os casos de teste ou resultados de teste lista.  
  
-   Clique no botão **fechar** para fechar o repositório da caixa de diálogo casos de teste.  
  
## <a name="test-cases-repository"></a>Repositório de casos de teste  
Você pode exibir o repositório de casos de teste clicando em **casos de teste...** no menu **testador** . Em seguida, o SSMA exibe a janela de caixa de diálogo **repositório de casos de** teste com uma lista de casos de teste salvos na página **casos de teste** .  
  
A grade mostra as seguintes informações sobre cada caso de teste:  
  
-   Nome: o nome do caso de teste.  
  
-   Criado: a data de criação do caso de teste.  
  
-   Modificado: a data da última modificação do caso de teste.  
  
-   Descrição: as descrições do caso de teste.  
  
Os botões a seguir estão disponíveis na página casos de teste:  
  
-   Clique no botão **Adicionar** para executar o assistente de caso de teste e criar um novo teste.  
  
-   Clique no botão **remover** para excluir o teste selecionado do repositório. Quando um caso de teste é excluído, todos os Resultados de Teste relacionados também são excluídos.  
  
-   Clique no botão **Editar** para executar o assistente de caso de teste e alterar o teste selecionado.  
  
-   Clique no botão **executar** para abrir os [casos de teste em execução &#40;](../../ssma/sybase/running-test-cases-sybasetosql.md) caixa de diálogo SybaseToSQL&#41;e execute o teste selecionado.  
  
## <a name="test-results-repository"></a>Repositório de Resultados de Teste  
Você pode exibir o repositório Resultados de Teste na página **resultados de teste** do **repositório da janela casos de teste** . Abra-o clicando em **resultados de teste...** no menu do **testador** .  
  
Você pode usar dois filtros na página **resultados de teste** :  
  
-   O filtro de nome de caso de teste: permite escolher resultados de teste por nome de caso de teste. O valor de **todos os** casos de teste do filtro permite exibir resultados de teste para todos os caso de teste.  
  
-   O filtro de data de execução do caso de teste: filtra os resultados do teste pela data de salvamento. O valor de **todos os períodos** do filtro permite exibir resultados de teste para qualquer data de salvamento.  
  
As informações a seguir sobre os resultados de teste são exibidas na grade.  
  
-   Nome: nome do caso de teste.  
  
-   Iniciado: data da execução do caso de teste.  
  
-   Resultado: um breve resumo da execução de teste (a dica de ferramenta dessa célula exibe um resumo completo da execução do teste).  
  
Os botões a seguir estão disponíveis na página resultado do teste:  
  
-   Clique no botão **Exibir** para abrir a [exibição de relatórios de caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) do resultado do caso de teste atual.  
  
-   Clique no botão **excluir** para excluir o resultado do teste selecionado  
  
## <a name="see-also"></a>Consulte Também  
[Executando casos de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testando objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
