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
ms.openlocfilehash: 6d82bfd3c49576a35b24f5a04cdc2c03dceeb766
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081495"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Descoberta e classificação de dados no SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A [Descoberta e Classificação de Dados](../../../relational-databases/security/sql-data-discovery-and-classification.md) é um conjunto de serviços avançados para descobrir, classificar, rotular e relatar os dados confidenciais em seus bancos de dados. O SqlClient fornece uma API que expõe informações de Descoberta e Classificação de Dados somente leitura quando a fonte subjacente dá suporte ao recurso. Essas informações são acessadas por meio do SqlDataReader.

Este aplicativo de exemplo demonstra como acessar as propriedades de Classificação de Dados do SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Consulte também**  

 [Recursos do SQL Server e ADO.NET](sql-server-features-adonet.md)