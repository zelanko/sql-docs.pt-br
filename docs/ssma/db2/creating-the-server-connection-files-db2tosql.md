---
title: Criando os arquivos de conexão do servidor (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 685419f6-8606-462c-be12-8bace45bede6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4a1ee05cbf14f18a34b15161eec88df04be5539b
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86392774"
---
# <a name="creating-the-server-connection-files-db2tosql"></a>Criando os arquivos de conexão do servidor (DB2ToSQL)

As informações do servidor podem ser especificadas na seção servidores do arquivo de script ou em um arquivo de conexão de servidor separado. O parâmetro de linha de comando para o arquivo de conexão do servidor é, `-c <serverconnectionfile>` . Se a mesma ID do servidor estiver presente no arquivo de script e no arquivo de conexão do servidor, a definição do servidor no arquivo de script será considerada.

**Exemplo: 1**

```xml
<!-- Sample of server connection file commands -->
<db2 name="<source-server-unique-name>">
  <standard-mode>

    <connection-provider value="OleDB Provider" />

    <!-- Defines server manager to connect.
         Available manager attribute values
           • zOs - DB2 for z/OS
           • LUW - DB2 for Linux, Unix and Windows
           • DBi - DB2 for i -->
    <database-manager value="$Db2Manager$" />

    <server-name value="$Db2HostName$" />

    <port value="$Db2Port$" />

    <initial-catalog value="$Db2Instance$" />

    <user-id value="$Db2UserName$" />

    <password value="$Db2Password$"/>

  </standard-mode>
</db2>
```

```xml
<sql-server name="<target-server-unique-name>">
  <sql-server-authentication>

    <server value="<server-name>" />

    <database value="<database-name>" />
  
    <user-id value="<user-name>"/>
  
    <password value="<password>"/>

  </sql-server-authentication>
</sql-server>
```

## <a name="next-step"></a>Próxima etapa

A próxima etapa na operação do console é [executar o console do SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)

## <a name="see-also"></a>Consulte Também

- [Executar o console do SSMA](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)
