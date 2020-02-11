---
title: Senhas fortes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 97b13e8ccf7ef331320d15254dde3480331c4bb0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62470353"
---
# <a name="strong-passwords"></a>Senhas fortes
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
  
-   Começa com o caractere $ ou \@.  
  
 Se usados em uma cadeia de conexão OLE DB ou ODBC, um logon ou senha não deve conter os seguintes caracteres: [] {}() , ; ? * ! \@. Esses caracteres são usados para iniciar uma conexão ou valores de conexão separados.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Política de senha](password-policy.md)  
  
  
