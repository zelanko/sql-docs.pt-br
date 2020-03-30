---
title: Como usar instruções com o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ddd61d15e3c363766c7e49b8e9045b60a7be164
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025791"
---
# <a name="using-statements-with-the-jdbc-driver"></a>Como usar instruções com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pode ser usado para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de diversas formas. O driver JDBC pode ser usado para executar instruções SQL no banco de dados ou pode ser usado para chamar procedimentos armazenados no banco de dados, usando parâmetros de entrada e saída. O driver JDBC também dá suporte ao uso de sequências de escape de SQL, contagens de atualização, chaves automaticamente geradas e realização de atualizações dentro de uma operação de lote.  
  
O driver JDBC fornece três classes para recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) – usado para executar instruções SQL sem parâmetros.  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) – (herdado de SQLServerStatement), usado para executar instruções SQL compiladas que podem conter parâmetros IN.  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) – (herdado de SQLServerPreparedStatement), usado para executar procedimentos armazenados que podem conter parâmetros IN, parâmetros OUT ou ambos.  
  
 Os tópicos nesta seção discutem como você pode usar cada uma das três classes de instrução para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  

| Tópico                                                                                                    | DESCRIÇÃO                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Como usar instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)                             | Descreve como usar instruções SQL com o driver JDBC para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    |
| [Como usar instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md) | Descreve como usar procedimentos armazenados com o driver JDBC para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Como usar vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md)                           | Descreve como usar o driver JDBC para recuperar dados de vários conjuntos de resultados.                                                                       |
| [Como usar sequências de escape do SQL](../../connect/jdbc/using-sql-escape-sequences.md)                           | Descreve como usar sequências de escape de SQL, como literais e funções de data e hora.                                                               |
| [Como usar chaves geradas automaticamente](../../connect/jdbc/using-auto-generated-keys.md)                             | Descreve como usar chaves automaticamente geradas.                                                                                                     |
| [Executando operações em lote](../../connect/jdbc/performing-batch-operations.md)                         | Descreve como usar o driver JDBC para realizar operações em lote.                                                                                      |
| [Tratando instruções complexas](../../connect/jdbc/handling-complex-statements.md)                         | Descreve como usar o driver JDBC para executar instruções complexas que realizam uma variedade de tarefas e podem retornar tipos diferentes de dados.               |
  
## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
