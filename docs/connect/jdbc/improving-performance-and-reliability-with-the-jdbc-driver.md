---
title: Melhorando o desempenho e a confiabilidade com o JDBC Driver
description: Conheça várias técnicas para melhorar o desempenho do aplicativo e a confiabilidade ao usar o Microsoft JDBC Driver para SQL Server.
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc04a90569974acbc99dcb66680d66289db1c0d1
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565374"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>Melhorando o desempenho e a confiabilidade com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Um aspecto de desenvolvimento de aplicativos que é comum a todos os aplicativos é a necessidade frequente de melhorar o desempenho e a confiabilidade. Há várias técnicas para fazer isso com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
Os tópicos nesta seção descrevem várias técnicas para melhorar o desempenho do aplicativo e a confiabilidade ao usar o driver JDBC.  

## <a name="in-this-section"></a>Nesta seção

|Tópico|Descrição|  
|-----------|-----------------|  
|[Fechando os objetos quando não estão em uso](../../connect/jdbc/closing-objects-when-not-in-use.md)|Descreve a importância de fechar objetos do driver JDBC quando eles não forem mais necessários.|  
|[Gerenciando o tamanho da transação](../../connect/jdbc/managing-transaction-size.md)|Descreve técnicas para melhorar o desempenho de transação.|  
|[Trabalhando com instruções e conjuntos de resultados](../../connect/jdbc/working-with-statements-and-result-sets.md)|Descreve técnicas para aprimorar o desempenho ao usar os objetos Statement ou ResultSet.|  
|[Como usar o buffer adaptável](../../connect/jdbc/using-adaptive-buffering.md)|Descreve um recurso de buffer adaptável, que foi desenvolvido para recuperar qualquer tipo de dados de valor grande sem a sobrecarga de cursores de servidor.|  
|[Colunas esparsas](../../connect/jdbc/sparse-columns.md)|Aborda o suporte do JDBC Driver para colunas esparsas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Metadados de instrução em cache preparados para o JDBC Driver](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Discute as técnicas para aprimorar o desempenho com consultas de instrução preparadas.|
|[Como usar a API de cópia em massa para a operação de inserção em lote](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|Descreve como habilitar a API de cópia em massa para operações de inserção em lote e seus benefícios.|
|[Não enviar parâmetros de cadeia de caracteres como Unicode](../../connect/jdbc/setting-the-connection-properties.md)|Ao trabalharem com dados **CHAR**, **VARCHAR** e **LONGVARCHAR**, os usuários podem definir a propriedade de conexão **sendStringParametersAsUnicode** como `false` para obter um ganho de desempenho ideal.|

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
