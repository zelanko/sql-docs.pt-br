---
title: Trabalhando com dados grandes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9163e9244b46e4eeb26cb0766186d7bfdb38fbf1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-large-data"></a>Trabalhando com dados grandes
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  O driver JDBC oferece suporte para buffer adaptável, que permite recuperar qualquer tipo de dados de valor grande sem a sobrecarga de cursores de servidor. Com buffer adaptável, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] recupera os resultados da execução de instrução da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] como o aplicativo precisa deles, e não tudo de uma vez. O driver também descarta os resultados assim que o aplicativo já não os pode acessar.  
  
 No [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] JDBC Driver versão 1.2, o modo de buffer era "**completo**" por padrão. Se seu aplicativo não definiu a propriedade de conexão "responseBuffering" como "**adaptável**" nas propriedades de conexão ou usando o [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método o [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto, o driver deu suportada a leitura do resultado inteiro do servidor ao mesmo tempo. Para obter o comportamento de buffer adaptável, o aplicativo teve que definir a propriedade de conexão "responseBuffering" como "**adaptável**" explicitamente.  
  
 O **adaptável** valor é o modo de buffer padrão e o driver JDBC armazena em buffer o mínimo possível de dados quando necessário. Para obter mais informações sobre como usar buffer adaptável, consulte [buffer adaptável usando](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Os tópicos nesta seção descrevem maneiras diferentes que você pode usar para recuperar dados de valor grande de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Lendo exemplo de dados grande](../../../connect/jdbc/reading-large-data-sample.md)|Descreve como usar uma instrução SQL para recuperar dados de valor grande.|  
|[Exemplo de leitura de dados grandes com procedimentos armazenados](../../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|Descreve como recuperar um valor grande do parâmetro OUT do CallableStatement.|  
|[Atualizando exemplo de dados grande](../../../connect/jdbc/updating-large-data-sample.md)|Descreve como atualizar dados de valor grande em um banco de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos de exemplo do JDBC Driver](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
