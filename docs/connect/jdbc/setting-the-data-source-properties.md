---
title: Propriedades da fonte de configuração de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13a305b676d43a13ae731bcc98dd3f517a5bf733
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850381"
---
# <a name="setting-the-data-source-properties"></a>Definindo as propriedades da fonte de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  As fontes de dados são o mecanismo preferencial de criação das conexões JDBC em um ambiente Java EE (Java Platform, Enterprise Edition). As fontes de dados fornecem conexões, conexões agrupadas e conexões distribuídas sem propriedades de conexão codificadas em Java. Todos os [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fontes de dados podem definir ou obter o valor de qualquer propriedade usando os métodos setter e getter, respectivamente.  
  
 Os produtos Java EE, como servidores de aplicativos e mecanismos de servlet/JSP, normalmente permitem configurar fontes de dados para o acesso do banco de dados. Qualquer propriedade listada no [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) tópico pode ser especificado sempre que a configuração permite que você insira uma propriedade como uma propriedade = par de valor.  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] fontes de dados, consulte o [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe. Para obter um exemplo de como usar a classe SQLServerDataSource para fazer uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados, consulte [exemplo de fonte de dados](../../connect/jdbc/data-source-sample.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
