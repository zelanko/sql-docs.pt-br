---
title: Perguntas frequentes no PolyBase | Microsoft Docs
description: Compare o PolyBase com os servidores vinculados e compare o PolyBase em Clusters de Big Data com o PolyBase em instâncias autônomas. Descubra as novidades no PolyBase 2019.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.openlocfilehash: 5083228cc44b859faec866eca7d36aae9626e8fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760444"
---
# <a name="frequently-asked-questions"></a>Perguntas frequentes

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="polybase-vs-linked-servers"></a>PolyBase VS. servidores vinculados
A tabela a seguir destaca as diferenças entre o PolyBase e os recursos de servidor vinculado:

|PolyBase | Servidores vinculados|
|--------------------------|--------------------------|  
|Objeto no escopo do banco de dados|Objeto no escopo da instância|
|Usa drivers ODBC|Usa provedores OLE DB|
|Oferece suporte a operações somente leitura para todas as fontes de dados e a operação de inserção para HADOOP e fonte de dados de pool de dados somente|Oferece suporte a operações de leitura e gravação|
|Consultas à fonte de dados remota de uma única conexão podem ser expandidas |Consultas à fonte de dados remota de uma única conexão não podem ser expandidas|
|Há suporte para a propagação de predicados|Há suporte para a propagação de predicados|
|Nenhuma configuração separada é necessária para o grupo de disponibilidade|Configuração separada necessária para cada instância no grupo de disponibilidade|
|Somente autenticação básica|Autenticação básica e integrada|
|Adequado para consultas analíticas que processam um grande número de linhas|Adequado para consultas OLTP que retornam uma ou algumas linhas|
|Consultas que usam tabela externa não podem participar de transações distribuídas|Consultas distribuídas podem participar de transações distribuídas|

## <a name="whats-new-in-polybase-2019"></a>Quais são as novidades no PolyBase 2019? 

O PolyBase no [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] agora pode ler dados de uma maior variedade de fontes de dados. Os dados destas fontes de dados externas podem ser armazenados como tabelas externas no SQL Server. O PolyBase também oferece suporte a computação de propagação para essas fontes de dados externas, exceto tipos genéricos de ODBC.

### <a name="compatible-data-sources"></a>Fontes de dados compatíveis

- SQL Server
- Oracle
- Teradata
- MongoDB
- Tipos genéricos de ODBC compatíveis
  
> [!NOTE]
> O PolyBase pode permitir a conexão a fontes de dados externas usando drivers ODBC de terceiros. Esses drivers não são fornecidos com o PolyBase e podem não funcionar conforme o esperado. Para obter mais informações, veja nosso [guia](../../relational-databases/polybase/polybase-configure-odbc-generic.md) para configuração genérica do PolyBase ODBC.  

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>O PolyBase em clusters de Big Data VS. PolyBase em Instâncias autônomas

A tabela a seguir destaca os recursos do PolyBase disponíveis na instalação autônoma do [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] e no cluster de Big Data do [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]:

|Recurso |Cluster de Big Data|Instância autônoma|
|--------------------------|--------------------------|---------|   
|Criar fonte de dados externa para SQL Server, Oracle, Teradata e Mongo DB |X|X |
|Criar fonte de dados externa usando um Driver ODBC de terceiros compatível | | X|
|Criar fonte de dados externa para a fonte de dados do HADOOP | X| X|
|Criar fonte de dados externa para o Armazenamento de Blobs do Azure | X| X|
|Criar tabela externa em um pool de dados do SQL Server | X| |
|Criar tabela externa em um pool de armazenamento do SQL Server | X| |
|Expandir execução de consulta | X| X|

> [!NOTE]
>A tabela não descreve a funcionalidade disponível na última CTP do [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]. Para conhecer os recursos disponíveis, confira as notas sobre a versão. Para obter mais informações sobre conexões usando o conector genérico ODBC, acesse nosso [Guia de instruções para configurar os tipos genéricos de ODBC](polybase-configure-odbc-generic.md).