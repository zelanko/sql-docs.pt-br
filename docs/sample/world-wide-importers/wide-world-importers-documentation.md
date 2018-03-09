---
title: "Documentação do Wide World Importers | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology: samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 17cabd9d-cb2f-436c-ad9c-ce02225808b7
caps.latest.revision: "3"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: a2510ee889f57f7ab51c0f45574a8fa6e86abb47
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="wide-world-importers-documentation"></a>Documentação do Wide World Importers
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Wide World Importers é o novo banco de dados de exemplo para o SQL Server 2016 e banco de dados do SQL Azure. Ele ilustra os principais recursos do SQL Server 2016 e banco de dados SQL Azure, para processamento de transações (OLTP), data warehouse e cargas de trabalho de análise (OLAP), bem como transações híbrida e cargas de trabalho de processamento (HTAP) de análise.

## <a name="about-this-sample"></a>Sobre este exemplo

Wide World Importers é um exemplo de banco de dados abrangente que ilustra o design de banco de dados e ilustra como os recursos do SQL Server podem ser aproveitados em um aplicativo.

Observe que o exemplo deve ser representativos de um banco de dados típica. Ele não inclui todos os recursos do SQL Server. O design do banco de dados segue um conjunto comum de padrões, mas há muitas maneiras que um pode criar um banco de dados.

**Versão mais recente**: [wide world-importadores liberação](http://go.microsoft.com/fwlink/?LinkID=800630)

**O código do exemplo de fonte**: [world-wide-importadores](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers).

**Comentários**: envie a [ sqlserversamples@microsoft.com ](mailto:sqlserversamples@microsoft.com).

A documentação para o exemplo é organizada da seguinte forma:

## <a name="overview"></a>Visão geral

Visão geral da empresa de exemplo Wide World Importers e os fluxos de trabalho resolvidos pelo exemplo.

## <a name="main-oltp-database-wideworldimporters"></a>WideWorldImporters de banco de dados OLTP principal

Instruções para a instalação e configuração do núcleo do banco de dados WideWorldImporters que é usado para OLTP (transação - processamento de transações OnLine) e análise operacional (HTAP - híbrida transacional/analítico processamento).

Descrição dos esquemas e tabelas no banco de dados de WideWorldImporters.  

Descreve como WideWorldImporters aproveita os principais recursos do SQL Server.

Exemplos de consultas para o banco de dados de WideWorldImporters.

## <a name="data-warehousing-and-analytics-database-wideworldimportersdw"></a>Data warehouse e WideWorldImportersDW de banco de dados de análise

Instruções para a instalação e configuração de OLAP WideWorldImportersDW de banco de dados.

Descrição dos esquemas e tabelas no banco de dados WideWorldImportersDW, que é o banco de dados de exemplo para o data warehouse e análise OLAP (processamento).

Fluxo de trabalho para o processo ETL (extrair, transformar e carregar) que migra os dados do banco de dados transacional WideWorldImporters no data warehouse WideWorldImportersDW.

Descreve como o WideWorldImportersDW aproveita os recursos do SQL Server para processamento da análise.

Exemplos de consultas de análise aproveitar o banco de dados WideWorldImportersDW.

## <a name="data-generation"></a>Geração de dados

Descreve como adicionais dados podem ser gerados o banco de dados de exemplo, por exemplo, inserindo vendas e compra dados até a data atual.
