---
title: Atualizar AZDATA_PASSWORD
description: Atualizar o `AZDATA_PASSWORD` manualmente
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/19/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1cc2a7778100be5c919c86a4c949d5aeb784d8e5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76265988"
---
# <a name="manually-update-azdata_password"></a>Atualizar o `AZDATA_PASSWORD` manualmente

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Se o cluster está ou não operando com a integração do Active Directory, o `AZDATA_PASSWORD` é definido durante a implantação. Ele fornece uma autenticação Básica para o controlador de cluster e a instância mestra. Este documento descreve como atualizar o `AZDATA_PASSWORD` manualmente.

## <a name="change-azdata_password-for-controller"></a>Alterar o `AZDATA_PASSWORD` para o controlador

Se o cluster estiver operando no modo não Active Directory, atualize a senha do Gateway do Apache Knox fazendo o seguinte:

1. Obtenha as credenciais do SQL Server do controlador executando os seguintes comandos:

   a. Execute este comando como um administrador do Kubernetes:

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. Decodifique o segredo em Base64:
   
   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. Em uma janela Comando separada, exponha a porta do servidor de banco de dados do controlador:

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```
 
1. Use a senha do administrador do sistema que você acabou de obter para se conectar ao servidor de banco de dados do controlador por meio de uma ferramenta de cliente SQL.

1. Gere uma nova senha complexa para `AZDATA_USERNAME` substituir o `AZDATA_PASSWORD` existente.

   Para simplificar o exemplo, as próximas etapas usam "newPassword" porque a senha gerada é "newPassword". 

1. Obtenha `hexsalt` na tabela de usuários:

   ```sql
   SELECT hexsalt FROM [auth].[users] WHERE username = '<username>'
   ```

   `hexsalt` retorna uma cadeia de caracteres hexa aleatória (por exemplo, `64FC59DF31244FFEE02F457BC0750226`).

1. Criptografe a nova senha complexa usando `hexsalt`:

   Para sua conveniência, fornecemos uma ferramenta predefinida `pbkdf2` para criptografar a senha. Baixe o aplicativo .NET Core apropriado para a plataforma para [`pbkdf2`](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/security/password-hashing/pbkdf2/prebuilt-binaries).

   O aplicativo é independente e não exige nenhum pré-requisito, como runtimes do .NET. Para criptografar a senha, execute:

   ```bash
   pbkdf2 <password> <hexsalt>
   J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=
   ```

1. Atualize a senha na tabela de usuários:

   ```SQL
   UPDATE [auth].[users] SET password = 'J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=' WHERE username = '<username>'
   ```

## <a name="change-azdata_password-in-the-sql-server-master-instance"></a>Alterar `AZDATA_PASSWORD` na instância mestra do SQL Server

1. Conecte-se ao ponto de extremidade do SQL mestre com qualquer usuário administrador.

1. Para alterar a senha das credenciais de logon que você definiu durante a implantação no parâmetro `AZDATA_USERNAME`, execute o seguinte comando T-SQL:

   ```sql
   ALTER LOGIN <AZDATA_USERNAME> WITH PASSWORD = 'newPassword'
   ```
