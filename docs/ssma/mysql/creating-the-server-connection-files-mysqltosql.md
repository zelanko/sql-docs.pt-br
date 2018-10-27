---
title: Criar os arquivos de Conexão de servidor (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server connection file validation
- Server connection files
ms.assetid: df0e970c-da0b-4118-b359-c9dcbbad16d6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cd954964af9c2495311423620c95af621021a5b
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099238"
---
# <a name="creating-the-server-connection-files-mysqltosql"></a>Criar os arquivos de Conexão de servidor (MySQLToSQL)
Informações do servidor podem ser especificadas na seção de servidores do arquivo de script ou em um arquivo de conexão de servidor separado. O parâmetro de linha de comando para o arquivo de conexão de servidor é, `-c <serverconnectionfile>`. Se a mesma id de servidor estiver presente no arquivo de script e no arquivo de conexão do servidor, a definição de servidor no arquivo de script é considerada.  
  
**Exemplo:**  
  
```xml  
<!--Sample of server connection file commands -->  
  
<mysql name ="<source-server-unique-name>">  
  
   <standard-mode>  
  
      <server value ="<server-name>"/>  
  
      <user-id value ="<user-name>"/>  
  
      <password value ="<password>"/>  
  
      <port value ="<port>"/>  
  
   </standard-mode>  
  
</mysql>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
   <sql-server-authentication>  
  
      <server value="<server-name>"/>  
  
      <database value="<database-name>"/>  
  
      <user-id value="<user-name>"/>  
  
      <password value="<password>"/>  
  
      <encrypt value="<true/false>"/>  
  
      <trust-server-certificate value="<true/false>"/>  
  
   </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="<target-server-unique-name>">  
  
   <server value="<server-name>"/>  
  
   <database value="<database-name>"/>  
  
   <user-id value="<user-name>"/>  
  
   <password value="<password>"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>Validação do arquivo de Conexão de servidor  
O usuário pode validar com facilidade seu arquivo de conexão de servidor contra o arquivo de definição de esquema **'M2SSConsoleScriptServersSchema.xsd'** disponível na pasta "Esquemas".  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no operando o console [executar o Console do SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (MySQL)](http://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
