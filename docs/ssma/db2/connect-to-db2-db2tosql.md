---
description: Conectar-se ao DB2 (DB2ToSQL)
title: Conectar-se ao DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cef31b2968ea0241b3c999e0dbd781d70974b360
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426968"
---
# <a name="connect-to-db2-db2tosql"></a>Conectar-se ao DB2 (DB2ToSQL)
Use a caixa de diálogo **conectar-se ao DB2** para se conectar ao banco de dados DB2 que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se ao DB2**. Se você tiver se conectado anteriormente, o comando será **reconectado ao DB2**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione o provedor de acesso a dados para sua conexão com o banco de dado DB2. Os provedores disponíveis são o provedor de cliente do DB2 e o provedor de OLE DB. O padrão é o provedor de cliente do DB2.  
  
**Modo**  
Selecione o modo padrão, TNSNAME ou cadeia de conexão.  
  
-   No modo padrão, você insere ou seleciona valores para o provedor, o nome do servidor, a porta do servidor, o SID do DB2, o nome de usuário e a senha.  
  
-   No modo TNSNAME, você insere o identificador de conexão (alias TNS) do banco de dados DB2, nome de usuário e senha.  
  
-   Em modo de cadeia de conexão, você fornece uma cadeia de conexão.  
  
    > [!IMPORTANT]  
    > Não recomendamos que você use o modo de cadeia de conexão porque o texto pode incluir senhas e é enviado como texto não criptografado.  
  
O padrão é o modo padrão.  
  
**Nome do servidor**  
Insira o nome do servidor DB2. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando um número de porta diferente de 1521 (padrão) para conexões com o DB2, insira o número da porta. Essa é uma opção de modo padrão.  
  
**Identificador de conexão**  
Insira o identificador do DB2 Connect. Esse é o alias do banco de dados, conforme definido no arquivo arquivo tnsnames. Ora local.  
  
Essa é uma opção de modo TNSNAME.  
  
**SID DO DB2**  
Insira o SID do banco de dados. O SID é um identificador que distingue o banco de dados DB2 em um computador. O SID padrão de um banco de dados são os oito primeiros caracteres do nome do banco de dados.  
  
Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados DB2.  
  
**Senha**  
Digite a senha para o nome de usuário.  
  
**Cadeia de conexão**  
> [!IMPORTANT]  
> Não recomendamos que você use o modo de cadeia de conexão porque o texto pode incluir senhas e é enviado como texto não criptografado.  
  
Se você usar o modo de cadeia de conexão, insira a cadeia de conexão completa para a conexão com o DB2.  
  
Cadeias de conexão consistem em pares de nome e valor de parâmetro.  
  
-   Para OLE DB informações de cadeia de conexão, consulte o artigo [provedor Microsoft OLE DB para DB2](https://go.microsoft.com/fwlink/?LinkId=85640) na biblioteca MSDN.  
  
Para cadeias de conexão do SSMA, inclua sempre o parâmetro Provider. Além disso, certifique-se de incluir o parâmetro Port quando você se conectar ao DB2.  
  
