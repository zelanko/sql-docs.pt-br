---
title: Criando os arquivos de conexão do servidor (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b74cf86e6a68653a2047aebefc7ca86ab6868475
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933977"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>Criando os arquivos de conexão do servidor (AccessToSQL)
As informações do servidor podem ser especificadas na seção servidores do arquivo de script. As informações do servidor também podem ser especificadas em um arquivo de conexão de servidor separado. O parâmetro de linha de comando para o arquivo de conexão do servidor é `-c <serverconnectionfile>` . Se a mesma ID do servidor estiver presente nos arquivos de conexão do servidor e do script, a definição do servidor no arquivo de script será considerada.  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>Validação do arquivo de conexão do servidor  
O usuário pode facilmente validar seu arquivo de conexão de servidor com o arquivo de definição de esquema **' A2SSConsoleScriptServersSchema. xsd '** disponível na pasta ' schemas '.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na operação do console é [executar o console do SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Executando o console do SSMA (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
