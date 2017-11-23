---
title: "Funções de RevoScaleR para trabalhar com dados do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08d8d3e6a13066aa79c96ba161e1c9d8f230e60f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>Funções de RevoScaleR para trabalhar com dados do SQL Server

Este tópico fornece uma visão geral das funções principais fornecidas no RevoScaleR para trabalhar com dados do SQL Server.

Para obter uma lista completa de funções ScaleR e como usá-los, consulte o [Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) referência.

## <a name="create-sql-server-data-sources"></a>Criar fontes de dados do SQL Server

As funções a seguir permitem que você defina uma fonte de dados do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Um objeto de fonte de dados é um contêiner que especifica uma cadeia de conexão com o conjunto de dados que você deseja, definido como uma tabela, exibição ou consulta. Não há suporte para chamadas de procedimento armazenado.

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -definir uma [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] objeto de fonte de dados.

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -criar objetos de dados para outros bancos de dados ODBC. 

## <a name="perform-ddl-statements"></a>Executar instruções DDL

Você pode executar as instruções DDL de R, se você tiver as permissões necessárias na instância e banco de dados. As funções a seguir usam chamadas ODBC para executar as instruções DDL ou recuperar o esquema de banco de dados.

+ `rxSqlServerTableExists`e [rxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -soltar um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabela ou verificar a existência de uma tabela de banco de dados ou objeto

+ [rxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -executar um comando Data Definition Language (DDL) que define ou manipula os objetos de banco de dados. Essa função não pode retornar dados e é usada somente para recuperar ou modificar o esquema de objeto ou metadados.

## <a name="define-or-manage-compute-contexts"></a>Definir ou gerenciar contextos de computação

As funções a seguir permitem que você defina um novo contexto de computação, mude de contexto de computação ou identifique o contexto de computação atual.

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext) – criar um contexto de computação.

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) – gerar um contexto de computação do SQL Server que permite que funções **ScaleR** sejam executadas no SQL Server R Services. Esse contexto de computação tem suporte apenas para instâncias do SQL Server no Windows.

+ `rxGetComputeContext`e [rxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) - obter ou definir o contexto de computação ativa.

## <a name="move-data-and-transform-data"></a>Mover dados e transformar dados

Depois de criar um objeto de fonte de dados, você pode usar o objeto para carregar dados nele, transformar dados ou gravar novos dados para o destino especificado. Dependendo do tamanho dos dados de origem, você também poderá definir o tamanho do lote como parte da fonte de dados e mover dados em partes.

+ [métodos de rxOpen](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods) - Verifique se uma fonte de dados está disponível, abrir ou fechar uma fonte de dados, ler dados de uma fonte de, gravar dados no destino e fechar uma fonte de dados

+ [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -mover dados de uma fonte de dados no armazenamento de arquivo ou em um quadro de dados.

+ [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -transformar dados ao movê-lo entre fontes de dados.

As funções a seguir podem ser usadas para criar um repositório de dados local no formato XDF. Esse arquivo pode ser útil ao trabalhar com mais dados do que é possível transferir do banco de dados em um lote ou mais dados do que cabem na memória.

Por exemplo, se você mover regularmente grandes quantidades de dados de um banco de dados em uma estação de trabalho local, em vez de consulta o banco de dados repetidamente para cada operação de R, você pode usar o arquivo XDF como um tipo de cache para salvar os dados localmente e, em seguida, trabalhar com eles no seu espaço de trabalho de R.

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -criar um objeto de dados XDF

+ [rxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -lê dados de um arquivo XDF em um quadro de dados

Para obter mais informações sobre como trabalhar com essas funções, incluindo o uso de dados de fontes diferentes de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [como guias para análise de dados no Microsoft R](https://docs.microsoft.com/r-server/r/how-to-introduction).
