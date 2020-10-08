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
ms.openlocfilehash: b53e71c4c302145af14c1f2e37f30fe0e3c8f8e2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725717"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Descoberta e classificação de dados no SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A [Descoberta e Classificação de Dados](../../../relational-databases/security/sql-data-discovery-and-classification.md?view=sql-server-2017) é um conjunto de serviços avançados para descobrir, classificar, rotular e relatar os dados confidenciais em seus bancos de dados. O SqlClient fornece uma API que expõe informações de Descoberta e Classificação de Dados somente leitura quando a fonte subjacente dá suporte ao recurso. Essas informações são acessadas por meio do SqlDataReader.

Este aplicativo de exemplo demonstra como acessar as propriedades de Classificação de Dados do SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Consulte também**  

 [Recursos do SQL Server e ADO.NET](sql-server-features-adonet.md)