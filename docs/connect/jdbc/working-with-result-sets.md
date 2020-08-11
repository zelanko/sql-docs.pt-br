---
title: Trabalhando com conjuntos de resultados
description: Saiba como trabalhar com os dados usando os conjuntos de resultados no JDBC Driver para SQL Server nesses aplicativos de exemplo.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82618ee27e1aa32716fe4b4d3817ff0128baebab
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921022"
---
# <a name="working-with-result-sets"></a>Trabalhando com conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com os dados contidos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um método de manipular os dados é usar um conjunto de resultados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de conjuntos de resultados por meio do objeto [SQLServerResultSet](reference/sqlserverresultset-class.md). Usando o objeto SQLServerResultSet, você pode recuperar os dados retornados por uma instrução SQL ou um procedimento armazenado, atualizar os dados conforme necessário e, em seguida, persisti-los de volta para o banco de dados.

Além disso, o objeto SQLServerResultSet fornece métodos para navegar pelas respectivas linhas de dados, obter ou definir os dados que ele contém e estabelecer diversos níveis de sensibilidade a alterações no banco de dados subjacente.

> [!NOTE]
> Para obter mais informações sobre como gerenciar conjuntos de resultados, inclusive sua sensibilidade a alterações, confira [Como gerenciar conjuntos de resultados com o JDBC Driver](managing-result-sets-with-the-jdbc-driver.md).

Os tópicos desta seção descrevem diversas maneiras de usar um conjunto de resultados para manipular os dados contidos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="in-this-section"></a>Nesta seção

| Tópico                                                                     | Descrição                                                                                                                                                                                          |
| ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Recuperando exemplo de dados do conjunto de resultados](retrieving-result-set-data-sample.md) | Descreve como usar um conjunto de resultados para recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibi-los.                                                         |
| [Modificando exemplo de dados de conjunto de resultados](modifying-result-set-data-sample.md)   | Descreve como usar um conjunto de resultados para inserir, recuperar e modificar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                      |
| [Exemplo de dados do conjunto de resultados de caching](caching-result-set-data-sample.md)       | Descreve como usar um conjunto de resultados para recuperar grandes volumes de dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como controlar a maneira como esses dados são armazenados em cache no cliente. |

## <a name="see-also"></a>Confira também

[Aplicativos de exemplo do JDBC Driver](sample-jdbc-driver-applications.md)
