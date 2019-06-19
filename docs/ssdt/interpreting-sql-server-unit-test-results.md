---
title: Interpretar Resultados de Teste de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: fde3c95b-2f68-483d-a197-0f7161b72fa3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1c68ace0ccbd49b63404aaf52419a06dda297f8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65088709"
---
# <a name="interpreting-sql-server-unit-test-results"></a>Interpretando resultados do teste de unidade do SQL Server
Quando você executa um teste de unidade do SQL Server, os resultados do teste são gerados automaticamente, salvos em disco e resumidos na janela **Resultados de Teste**. Assim que você iniciar uma execução do teste, a janela **Resultados de Teste** aparecerá e exibirá o andamento da execução do teste. Essa exibição inclui os testes que estão em execução e os que foram concluídos.  
  
Para ver informações detalhadas de um resultado de teste, clique duas vezes na janela **Resultados de Teste** para exibir a página **Detalhes dos Resultados de Teste**. Para obter mais informações sobre um resultado de teste, clique duas vezes nele.  
  
Para obter mais informações sobre como alterar a exibição da janela **Resultados do Teste**, veja [Como adicionar ou remover colunas em Janelas de Teste (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182508(VS.100).aspx) ou [Como adicionar ou remover colunas em Janelas de Teste (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182508.aspx).  
  
## <a name="storing-test-results"></a>Armazenando resultados de teste  
Os resultados dos testes de unidade são armazenados automaticamente no disco rígido, em arquivos com a extensão .trx. Um arquivo .trx é um arquivo XML que contém os detalhes de uma execução de teste. Você pode carregar arquivos .trx de execuções de teste anteriores para analisar os resultados dessas execuções ou executar novamente os testes anteriores. Para obter mais informações, confira [Como executar um teste novamente (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182472(VS.100).aspx).  
  
> [!NOTE]  
> Você não pode executar testes de unidade remotamente.  
  
Se sua equipe estiver usando um projeto de equipe do Visual Studio Team Foundation Server para facilitar o gerenciamento do trabalho, você também poderá publicar os dados de teste em um banco de dados do SQL Server conhecido como repositório operacional.  
  
Para obter mais informações sobre como salvar resultados de teste, reutilizá-los e compartilhá-los com sua equipe, veja [Como salvar e abrir resultados de teste no Visual Studio 2010](https://msdn.microsoft.com/library/ms404662(VS.100).aspx) ou [Como salvar e abrir resultados de teste no Visual Studio 2012](https://msdn.microsoft.com/library/ms404662.aspx).  
  
## <a name="see-also"></a>Consulte Também  
[Executar testes de unidade do SQL Server](../ssdt/running-sql-server-unit-tests.md)  
  
