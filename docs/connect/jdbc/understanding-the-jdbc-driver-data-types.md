---
title: Noções básicas sobre os tipos de dados do Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 399037b5f888c767edf28c40c0658d31e8703ddc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-jdbc-driver-data-types"></a>Entendendo os tipos de dados do JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece suporte ao uso de tipos de dados básicos e avançados do JDBC dentro de um aplicativo Java que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como seu banco de dados.  
  
 O sistema de tipos do JDBC atua como mediador da conversão entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados e tipos de linguagem Java e objetos. Os tipos JDBC são modelados nos tipos SQL-92 e SQL-99. O driver JDBC segue a especificação de JDBC e é criado para fornecer o equilíbrio certo entre previsibilidade e flexibilidade.  
  
 Os tópicos nesta seção descrevem como usar os tipos de dados básicos e avançados e como tipos de dados podem ser convertidos em outros tipos de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Usando tipos de dados básicos](../../connect/jdbc/using-basic-data-types.md)|Descreva os tipos de dados básicos do JDBC. Inclui exemplos de como trabalhar com os tipos de dados usando conjuntos de resultados, consultas parametrizadas e procedimentos armazenados.|  
|[Configurando como os valores de java.sql.Time são enviados ao servidor](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)|Descreve como o JDBC Driver gera datas.|  
|[Usando tipos de dados avançados](../../connect/jdbc/using-advanced-data-types.md)|Descreva os tipos de dados avançados do JDBC.|  
|[Noções básicas sobre diferenças de tipo de dados](../../connect/jdbc/understanding-data-type-differences.md)|Descreve diferenças entre os vários tipos de dados do JDBC Driver.|  
|[Noções básicas sobre conversões de tipo de dados](../../connect/jdbc/understanding-data-type-conversions.md)|Descreve como a conversão de tipo de dados é tratada ao usar os métodos getter e setter.|  
|[Suporte ao conjunto de caracteres nacionais](../../connect/jdbc/national-character-set-support.md)|Descreve o suporte a tipos de conjunto de caracteres nacionais.|  
|[Dando suporte a dados XML](../../connect/jdbc/supporting-xml-data.md)|Descreve a interface SQLXML. Também descreve como ler e escrever dados XML de e para o banco de dados relacional com o **SQLXML** tipo de dados Java.|  
|[Wrappers e interfaces](../../connect/jdbc/wrappers-and-interfaces.md)|Aborda as interfaces que têm o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos específicos e constantes que permitem que um servidor de aplicativos criar um proxy da classe, também discute oferece suporte para a interface do Java.SQL.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
