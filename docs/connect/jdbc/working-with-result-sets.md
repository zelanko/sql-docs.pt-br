---
title: Trabalhando com conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86c2d4fdcaee554f9e4ed04a2765e7a02779a94b
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786960"
---
# <a name="working-with-result-sets"></a>Trabalhando com conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com os dados contidos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um método de manipular os dados é usar um conjunto de resultados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de conjuntos de resultados por meio do objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md). Usando o objeto SQLServerResultSet, você pode recuperar os dados retornados por uma instrução SQL ou um procedimento armazenado, atualizar os dados conforme necessário e, em seguida, persisti-los de volta para o banco de dados.  
  
Além disso, o objeto SQLServerResultSet fornece métodos para navegar pelas respectivas linhas de dados, obter ou definir os dados que ele contém e estabelecer diversos níveis de sensibilidade a alterações no banco de dados subjacente.  
  
> [!NOTE]  
> Para obter mais informações sobre como gerenciar conjuntos de resultados, inclusive sua sensibilidade a alterações, consulte [Gerenciando conjuntos de resultados com o Driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
Os tópicos desta seção descrevem diversas maneiras de usar um conjunto de resultados para manipular os dados contidos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
| Tópico                                                                                        | Descrição                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Exemplo de recuperação de dados do conjunto de resultados](../../connect/jdbc/retrieving-result-set-data-sample.md) | Descreve como usar um conjunto de resultados para recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibi-los.                                                         |
| [Exemplo de modificação de dados do conjunto de resultados](../../connect/jdbc/modifying-result-set-data-sample.md)   | Descreve como usar um conjunto de resultados para inserir, recuperar e modificar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                      |
| [Exemplo de armazenamento de dados do conjunto de resultados em cache](../../connect/jdbc/caching-result-set-data-sample.md)       | Descreve como usar um conjunto de resultados para recuperar grandes volumes de dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como controlar a maneira como esses dados são armazenados em cache no cliente. |
  
## <a name="see-also"></a>Consulte Também

 [Aplicativos de exemplo do JDBC Driver](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  