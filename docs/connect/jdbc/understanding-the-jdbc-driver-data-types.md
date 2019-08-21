---
title: Noções básicas sobre os tipos de dados do driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8daea8b477be13dd7b267a17ddf5f960868f579
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027270"
---
# <a name="understanding-the-jdbc-driver-data-types"></a>Noções básicas sobre os tipos de dados do JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte ao uso de tipos de dados básicos e avançados do JDBC em um aplicativo Java que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como seu banco de dados.  
  
O sistema de tipos do JDBC atua como mediador da conversão entre tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tipos e objetos da linguagem Java. Os tipos JDBC são modelados nos tipos SQL-92 e SQL-99. O driver JDBC segue a especificação de JDBC e é criado para fornecer o equilíbrio certo entre previsibilidade e flexibilidade.  
  
Os tópicos nesta seção descrevem como usar os tipos de dados básicos e avançados e como tipos de dados podem ser convertidos em outros tipos de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
| Tópico                                                                                                                                            | Descrição                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Como usar tipos de dados básicos](../../connect/jdbc/using-basic-data-types.md)                                                                           | Descreva os tipos de dados básicos do JDBC. Inclui exemplos de como trabalhar com os tipos de dados usando conjuntos de resultados, consultas parametrizadas e procedimentos armazenados.                                                                                                        |
| [Configurando como os valores de java.sql.Time são enviados ao servidor](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md) | Descreve como o JDBC Driver gera datas.                                                                                                                                                                                                                       |
| [Como usar tipos de dados avançados](../../connect/jdbc/using-advanced-data-types.md)                                                                     | Descreva os tipos de dados avançados do JDBC.                                                                                                                                                                                                                              |
| [Entendendo diferenças de tipo de dados](../../connect/jdbc/understanding-data-type-differences.md)                                                 | Descreve diferenças entre os vários tipos de dados do JDBC Driver.                                                                                                                                                                                                    |
| [Entendendo conversões de tipo de dados](../../connect/jdbc/understanding-data-type-conversions.md)                                                 | Descreve como a conversão de tipo de dados é tratada ao usar os métodos getter e setter.                                                                                                                                                                                  |
| [Suporte ao conjunto de caracteres nacionais](../../connect/jdbc/national-character-set-support.md)                                                           | Descreve o suporte a tipos de conjunto de caracteres nacionais.                                                                                                                                                                                                          |
| [Suporte a dados XML](../../connect/jdbc/supporting-xml-data.md)                                                                                 | Descreve a interface SQLXML. Também descreve como ler e escrever dados XML de e para o banco de dados relacional com o tipo de dados **SQLXML** Java.                                                                                                             |
| [Wrappers e interfaces](../../connect/jdbc/wrappers-and-interfaces.md)                                                                         | Aborda as interfaces que têm os métodos e as constantes específicos do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] que permitem a um servidor de aplicativos criar um proxy da classe. Além disso, descreve suportes à interface `java.sql.Wrapper`. |
  
## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
