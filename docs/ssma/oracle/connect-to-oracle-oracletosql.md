---
title: Conectar-se ao Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 42ab1e77dbdb7cee237a9ec22c49a725a64390c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68264479"
---
# <a name="connect-to-oracle-oracletosql"></a>Conectar-se ao Oracle (OracleToSQL)
Use a caixa de diálogo **conectar-se ao Oracle** para se conectar ao banco de dados Oracle que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se ao Oracle**. Se você tiver se conectado anteriormente, o comando será **reconectado ao Oracle**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione o provedor de acesso a dados para a sua conexão com o Oracle Database. Os provedores disponíveis são o provedor de cliente Oracle e o provedor de OLE DB. O padrão é provedor de cliente Oracle.  
  
**Modo**  
Selecione o modo padrão, TNSNAME ou cadeia de conexão.  
  
-   No modo padrão, você insere ou seleciona valores para o provedor, o nome do servidor, a porta do servidor, o SID do Oracle, o nome de usuário e a senha.  
  
-   No modo TNSNAME, insira o identificador de conexão (alias TNS) do banco de dados Oracle, nome de usuário e senha.  
  
-   Em modo de cadeia de conexão, você fornece uma cadeia de conexão.  
  
    > [!IMPORTANT]  
    > Não recomendamos que você use o modo de cadeia de conexão porque o texto pode incluir senhas e é enviado como texto não criptografado.  
  
O padrão é o modo padrão.  
  
**Nome do servidor**  
Insira o nome do servidor Oracle. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando um número de porta diferente de 1521 (padrão) para conexões com o Oracle, insira o número da porta. Essa é uma opção de modo padrão.  
  
**Identificador de conexão**  
Insira o identificador do Oracle Connect. Esse é o alias do banco de dados, conforme definido no arquivo arquivo tnsnames. Ora local.  
  
Essa é uma opção de modo TNSNAME.  
  
**SID do Oracle**  
Insira o SID do banco de dados. O SID é um identificador que distingue o banco de dados Oracle em um computador. O SID padrão de um banco de dados são os oito primeiros caracteres do nome do banco de dados.  
  
Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados Oracle.  
  
**Senha**  
Digite a senha para o nome de usuário.  
  
**Cadeia de conexão**  
> [!IMPORTANT]  
> Não recomendamos que você use o modo de cadeia de conexão porque o texto pode incluir senhas e é enviado como texto não criptografado.  
  
Se você usar o modo de cadeia de conexão, insira a cadeia de conexão completa para a conexão com o Oracle.  
  
Cadeias de conexão consistem em pares de nome e valor de parâmetro.  
  
-   Para OLE DB informações de cadeia de conexão, consulte o artigo [provedor Microsoft OLE DB para Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) na biblioteca MSDN.  
  
Para cadeias de conexão do SSMA, inclua sempre o parâmetro Provider. Além disso, certifique-se de incluir o parâmetro Port ao se conectar ao Oracle.  
  
