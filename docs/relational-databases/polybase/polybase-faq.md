---
title: Perguntas frequentes no PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 331ac177831b1e07cfab253c363a35f2bab42a6c
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072871"
---
# <a name="frequently-asked-questions"></a>Perguntas frequentes

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>O PolyBase em clusters de Big Data VS. PolyBase em Instâncias autônomas

|Recurso |Cluster de Big Data| Instância autônoma|
|--------------------------|--------------------------|---------|   
|Criar tabelas externas| X| X|
|Criar fonte de dados externa usando SQL Server, Oracle, Teradata e Mongo DB |X|X |
|Criar fonte de dados externa usando um Driver ODBC de terceiros compatível | | X|
|Grupos de expansão do PolyBase | X | |
|instâncias do pool de dados | X| |
|instâncias do pool de armazenamento| X| |

>[!NOTE]
>
>Para obter mais informações sobre conexões usando o conector genérico ODBC, acesse nosso [Guia de instruções para configurar os tipos genéricos de ODBC](polybase-configure-odbc-generic.md)

## <a name="whats-new-with-polybase-in-sql-server-2019"></a>O que há de novo no PolyBase no SQL Server 2019? 

O PolyBase no SQL Server 2019 agora pode ler dados de uma maior variedade de fontes de dados. Os dados destas fontes de dados externas podem ser armazenados como tabelas externas no SQL Server. O PolyBase também oferece suporte a computação de propagação para essas fontes de dados externas, exceto tipos genéricos de ODBC. 

### <a name="compatible-data-sources"></a>Fontes de dados compatíveis

- SQL Server
- Oracle
- Teradata
- MongoDB
- Tipos genéricos de ODBC **compatíveis**

  > [!NOTE]
  >
  >O PolyBase pode permitir a conexão a fontes de dados externas usando drivers ODBC de terceiros. Esses drivers não são fornecidos com o PolyBase e podem funcionar conforme o esperado. Para obter mais informações, veja nosso [guia](polybase-configure-odbc-generic.md) para configuração genérica do PolyBase ODBC.  

## <a name="polybase-vs-linked-servers"></a>PolyBase VS. servidores vinculados

|PolyBase | Servidores vinculados|
|--------------------------|--------------------------|  
|Objeto no escopo do banco de dados|Objeto no escopo da instância| 
|Usa drivers ODBC|Usa provedores OLE DB| 
| Dá suporte apenas a operações somente leitura. Será expandido no futuro| Dá suporte apenas a operações somente leitura. Será expandido no futuro| 
|As consultas podem ter suporte para expansão e propagação|As consultas têm suporte para thread único e propagação|
|Nenhuma configuração separada é necessária para o grupo de disponibilidade Always On|Configuração separada necessária para cada instância no grupo de disponibilidade Always On|
|Somente autenticação básica. Melhorias no SQL Server 2019|Autenticação básica e integrada|