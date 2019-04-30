---
title: Conectar-se ao DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ab734e93743d3a3158feb16dba044b58e7f48f23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299159"
---
# <a name="connect-to-db2-db2tosql"></a>Conectar-se ao DB2 (DB2ToSQL)
Use o **conectar-se ao DB2** caixa de diálogo para se conectar ao banco de dados DB2 que você deseja migrar.  
  
Para acessar essa caixa de diálogo, nos **arquivo** menu, selecione **conectar ao DB2**. Se você tiver se conectado anteriormente, o comando é **reconectar-se ao DB2**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione o provedor de acesso de dados para sua conexão ao banco de dados DB2. Provedores disponíveis são o provedor de cliente DB2 e o provedor OLE DB. O padrão é o provedor de cliente do DB2.  
  
**Modo**  
Selecione o modo padrão, TNSNAME ou cadeia de caracteres de Conexão.  
  
-   No modo padrão, insira ou selecione valores para o provedor, nome do servidor, porta do servidor, DB2 SID, nome de usuário e senha.  
  
-   No modo TNSNAME, insira o identificador de conexão (alias TNS) do banco de dados DB2, nome de usuário e senha.  
  
-   No modo de cadeia de caracteres de Conexão, você deve fornecer uma cadeia de caracteres de conexão.  
  
    > [!IMPORTANT]  
    > Não recomendamos que você use o modo de cadeia de caracteres de Conexão porque o texto pode incluir senhas, e ele é enviado como texto não criptografado.  
  
O padrão é o modo padrão.  
  
**Nome do servidor**  
Insira o nome do servidor DB2. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando um número de porta diferente 1521 (padrão) para conexões com o DB2, insira o número da porta. Essa é uma opção de modo padrão.  
  
**Conectar-se o identificador**  
Insira o DB2 connect identificador. Esse é o alias do banco de dados, conforme definido no arquivo tnsnames. ora local.  
  
Essa é uma opção de modo TNSNAME.  
  
**DB2 SID**  
Insira o SID para o banco de dados. O SID é um identificador que distingue o banco de dados do DB2 em um computador. O padrão de SID para um banco de dados é os oito primeiros caracteres do nome do banco de dados.  
  
Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Insira o nome de usuário que usará o SSMA para se conectar ao banco de dados DB2.  
  
**Senha**  
Digite a senha para o nome de usuário.  
  
**Cadeia de conexão**  
> [!IMPORTANT]  
> Não recomendamos que você use o modo de cadeia de caracteres de Conexão porque o texto pode incluir senhas, e ele é enviado como texto não criptografado.  
  
Se você usar o modo de cadeia de caracteres de Conexão, insira a cadeia de conexão completa para a conexão para o DB2.  
  
Cadeias de caracteres de Conexão consistem em pares de nome e valor do parâmetro.  
  
-   Para informações de cadeia de caracteres de conexão OLE DB, consulte [Microsoft OLE DB Provider for DB2](https://go.microsoft.com/fwlink/?LinkId=85640) artigo na biblioteca MSDN.  
  
Para cadeias de caracteres de conexão do SSMA, sempre inclua o parâmetro de provedor. Além disso, certifique-se de que você inclua o parâmetro de porta ao conectar-se ao DB2.  
  
