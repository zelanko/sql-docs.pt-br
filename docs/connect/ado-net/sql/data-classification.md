---
title: Descoberta e classificação de dados no SqlClient
description: Descreve como verificar se um banco de dados do SQL Server dá suporte à classificação de dado e como acessar informações de classificação de dados por meio de um objeto SqlDataReader.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 27b9c232fe785d3c016848f3bb952236b8e7cd75
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110089"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Descoberta e classificação de dados no SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A [Descoberta e Classificação de Dados](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017) é um conjunto de serviços avançados para descobrir, classificar, rotular e relatar os dados confidenciais em seus bancos de dados. O SqlClient fornece uma API que expõe informações de Descoberta e Classificação de Dados somente leitura quando a fonte subjacente dá suporte ao recurso. Essas informações são acessadas por meio do SqlDataReader.

Este aplicativo de exemplo demonstra como acessar as propriedades de Classificação de Dados do SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Consulte também**  

 [Recursos do SQL Server e ADO.NET](sql-server-features-adonet.md)   
