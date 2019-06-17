---
title: Suporte ao conjunto de caracteres nacionais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ab17d9e60752b1aea747b03947d235b7d5f91605
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801808"
---
# <a name="national-character-set-support"></a>Suporte ao conjunto de caracteres nacionais
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O driver JDBC oferece suporte à API do JDBC 4.0, que inclui novos métodos da API de conversão do conjunto de caracteres nacional. Esse suporte inclui novos métodos setter, getter e updater para **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, e **NCLOB** tipos do JDBC.  
  
 A seguir encontra-se uma lista de novos métodos de getter, setter e updater para dar suporte à conversão do conjunto de caracteres nacionais:  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md).  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md).  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md).  
  
> [!NOTE]  
>  É preciso definir o classpath para incluir o arquivo sqljdbc4.jar a fim de usar esses métodos em um aplicativo.  
  
 Para enviar parâmetros String ao servidor no formato Unicode, os aplicativos devem usar os novos métodos de caracteres nacionais do JDBC 4.0 ou definir a propriedade de conexão **sendStringParametersAsUnicode** como "**true**" ao usar os métodos de caracteres não nacionais. O modo recomendado é usar os novos métodos de caracteres nacionais do JDBC 4.0 onde possível. Para obter mais informações sobre o **sendStringParametersAsUnicode** propriedade de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
