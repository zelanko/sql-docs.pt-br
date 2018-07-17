---
title: Senhas fortes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlraba
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a3bd36744f5604729d782822296dd6568b90a847
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36942622"
---
# <a name="strong-passwords"></a>Senhas fortes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  As senhas podem ser o link mais fraco em uma implantação de segurança de servidor. Você sempre deveria tomar muito cuidado ao selecionar uma senha. Uma senha segura tem as seguintes características:  
  
-   Tem pelo menos 8 caracteres de extensão.  
  
-   Combina letras, números e símbolos.  
  
-   Não se encontra em um dicionário.  
  
-   Não é o nome de um comando.  
  
-   Não é o nome de uma pessoa.  
  
-   Não é o nome de um usuário.  
  
-   Não é o nome de um computador.  
  
-   É alterada com frequência.  
  
-   É significativamente diferente das senhas anteriores.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as senhas podem conter até 128 caracteres, incluindo, símbolos e dígitos. Como os logons, nomes de usuários, funções e senhas são frequentemente usados nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , determinados símbolos devem ser colocados entre aspas (") ou chaves ([ ]). Use esses delimitadores nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] quando o logon, o usuário, a função ou a senha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver as seguintes características:  
  
-   Contém ou começa com um caractere de espaço.  
  
-   Começa com o $ ou @.  
  
 Se usados em uma cadeia de conexão OLE DB ou ODBC, um logon ou senha não deve conter os seguintes caracteres: [] {}() , ; ? * ! @. Esses caracteres são usados para iniciar uma conexão ou valores de conexão separados.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Política de senha](../../relational-databases/security/password-policy.md)  
  
  
