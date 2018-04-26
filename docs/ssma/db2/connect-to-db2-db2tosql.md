---
title: Conecte-se ao DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d6ba7b6cb1440a918160dbd9660930d4896a8d7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-db2-db2tosql"></a>Conecte-se ao DB2 (DB2ToSQL)
Use o **conectar ao DB2** caixa de diálogo para se conectar ao banco de dados DB2 que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar ao DB2**. Se você se conectou anteriormente, o comando é **reconectar-se ao DB2**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione o provedor de acesso de dados para a conexão ao banco de dados DB2. Provedores disponíveis são o provedor de cliente DB2 e o provedor OLE DB. O padrão é o provedor de cliente do DB2.  
  
**Modo**  
Selecione o modo padrão, TNSNAME ou cadeia de caracteres de Conexão.  
  
-   No modo padrão, digite ou selecione os valores para o provedor, nome do servidor, porta do servidor, DB2 SID, nome de usuário e senha.  
  
-   No modo TNSNAME, insira o identificador de conexão (alias TNS) do banco de dados DB2, nome de usuário e senha.  
  
-   No modo de cadeia de caracteres de Conexão, você deve fornecer uma cadeia de caracteres de conexão.  
  
    > [!IMPORTANT]  
    > Não é recomendável que você use o modo de cadeia de caracteres de Conexão porque o texto pode incluir as senhas e é enviado como texto não criptografado.  
  
O padrão é o modo padrão.  
  
**Nome do servidor**  
Insira o nome do servidor DB2. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando um número de porta diferente 1521 (padrão) para conexões ao DB2, insira o número da porta. Essa é uma opção de modo padrão.  
  
**Identificador de conexão**  
Insira o DB2 identificador de conexão. Este é o alias do banco de dados, conforme definido no arquivo tnsnames.ora local.  
  
Essa é uma opção de modo TNSNAME.  
  
**DB2 SID**  
Insira o SID para o banco de dados. O SID é um identificador que distingue o banco de dados do DB2 em um computador. O padrão de SID para um banco de dados é os oito primeiros caracteres do nome do banco de dados.  
  
Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Digite o nome de usuário SSMA usará para se conectar ao banco de dados DB2.  
  
**Senha**  
Digite a senha para o nome de usuário.  
  
**Cadeia de conexão**  
> [!IMPORTANT]  
> Não é recomendável que você use o modo de cadeia de caracteres de Conexão porque o texto pode incluir as senhas e é enviado como texto não criptografado.  
  
Se você usar o modo de cadeia de caracteres de Conexão, insira a cadeia de conexão completa para a conexão para o DB2.  
  
Cadeias de caracteres de Conexão consistem de pares de nome e valor de parâmetro.  
  
-   Para informações de cadeia de caracteres de conexão OLE DB, consulte [Microsoft OLE DB Provider for DB2](http://go.microsoft.com/fwlink/?LinkId=85640) artigo na biblioteca MSDN.  
  
Cadeias de caracteres de conexão do SSMA, sempre inclua o parâmetro de provedor. Além disso, certifique-se de incluir o parâmetro Port quando você se conectar ao DB2.  
  
