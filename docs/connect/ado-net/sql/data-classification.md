---
title: Descoberta e classificação de dados no SqlClient
description: Descreve como verificar se um banco de dados do SQL Server dá suporte à classificação de dado e como acessar informações de classificação de dados por meio de um objeto SqlDataReader.
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 32c4968c4e734abf7bcb4addfde69bbdc5294d1c
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123865"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Descoberta e classificação de dados no SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A [Descoberta e Classificação de Dados](../../../relational-databases/security/sql-data-discovery-and-classification.md) é um conjunto de serviços avançados para descobrir, classificar, rotular e relatar os dados confidenciais em seus bancos de dados. O SqlClient fornece uma API que expõe informações de Descoberta e Classificação de Dados somente leitura quando a fonte subjacente dá suporte ao recurso. Essas informações são acessadas por meio do SqlDataReader.

O Microsoft.Data.SqlClient v2.1.0 apresenta o suporte para informações de `Sensitivity Rank` da classificação de dados. `Sensitivity Rank` é um identificador baseado em um conjunto de valores predefinidos que determinam a classificação de sensibilidade. Ele pode ser usado por outros serviços, como a Proteção Avançada contra Ameaças, para detectar anomalias com base em sua classificação. As seguintes APIs de classificação de dados agora estão disponíveis no namespace Microsoft.Data.SqlClient.DataClassification:

```csharp
// New in Microsoft.Data.SqlClient v2.1.0
public enum SensitivityRank
{
    NOT_DEFINED = -1,
    NONE = 0,
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30,
    CRITICAL = 40
}

public sealed class SensitivityClassification
{
  // Returns the sensitivity rank for the query associated with the active 'SqlDataReader'.
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the labels collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<Label> Labels;

  // Returns the information types collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<InformationType> InformationTypes;

  // Returns the column sensitivity for this 'SensitivityClassification' Object
  public ReadOnlyCollection<ColumnSensitivity> ColumnSensitivities;
}

public sealed class SensitivityProperty
{
  // Returns the sensitivity rank for this 'SensitivityProperty' Object
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the label for this 'SensitivityProperty' Object
  public Label Label;

  // Returns the information type for this 'SensitivityProperty' Object
  public InformationType InformationType;
}

public sealed class Label
{
  // Gets the name for this 'Label' object
  public string Name;

  // Gets the ID for this 'Label' object
  public string Id;
}

public sealed class InformationType
{
  // Gets the name for this 'InformationType' object
  public string Name;

  // Gets the ID for this 'InformationType' object
  public string Id;
}

public sealed class ColumnSensitivity
{
  // Returns the list of sensitivity properties as received from Server for this 'ColumnSensitivity' information      
  public ReadOnlyCollection<SensitivityProperty> SensitivityProperties;
}
```

> [!NOTE]
> O Microsoft.Data.SqlClient lerá informações de `Sensitivity Rank` somente se o SQL Server der suporte à Classificação de dados com classificação. Para servidores com uma versão antiga da Classificação de dados sem classificação, o valor de classificação para consultas é "NÃO DEFINIDO".

Este aplicativo de exemplo demonstra como acessar as propriedades de Classificação de Dados do SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]


**Consulte também**  

 - [Recursos do SQL Server e ADO.NET](sql-server-features-adonet.md)
 - [sys.sensitivity_classifications (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)
 - [ADICIONAR CLASSIFICAÇAÕ DE SENSIBILIDADE](../../../t-sql/statements/add-sensitivity-classification-transact-sql.md)