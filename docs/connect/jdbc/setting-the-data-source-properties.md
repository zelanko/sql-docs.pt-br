---
title: Propriedades da fonte de definição de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6804e8bb0f68ed88934e5bc86d61556b9bbbd499
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778068"
---
# <a name="setting-the-data-source-properties"></a>Definindo as propriedades da fonte de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

As fontes de dados são o mecanismo preferencial de criação das conexões JDBC em um ambiente Java EE (Java Platform, Enterprise Edition). As fontes de dados fornecem conexões, conexões agrupadas e conexões distribuídas sem propriedades de conexão codificadas em Java. Todas as fontes de dados do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] podem definir ou obter o valor de qualquer propriedade usando os métodos setter e getter, respectivamente.

Os produtos Java EE, como servidores de aplicativos e mecanismos de servlet/JSP, normalmente permitem configurar fontes de dados para o acesso do banco de dados. Qualquer propriedade listada no tópico [Definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md) pode ser especificada sempre que a configuração permitir a inserção de uma propriedade como um par propriedade=valor.

Para obter mais informações sobre as fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja a classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). Para obter um exemplo de como usar a classe SQLServerDataSource para fazer uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, consulte [exemplo de código-fonte de dados](../../connect/jdbc/data-source-sample.md).

## <a name="see-also"></a>Consulte Também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
