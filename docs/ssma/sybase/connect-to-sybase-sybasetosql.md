---
title: Conectar-se ao Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6cb2f4196737cceec2f60684de1b7409f5e383a0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083389"
---
# <a name="connect-to-sybase-sybasetosql"></a>Conectar-se ao Sybase (SybaseToSQL)
Use a caixa de diálogo **conectar-se ao Sybase** para se conectar à instância de ase (Sybase Adaptive Server Enterprise) que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se ao Sybase**. Se você tiver se conectado anteriormente, o comando será **reconectado ao Sybase**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione qualquer provedor instalado no computador para se conectar ao servidor Sybase.  
  
**Modo**  
Selecione o modo de conexão Standard ou avançado. No modo padrão, você insere ou seleciona valores para o nome do servidor, a porta, o nome de usuário e a senha. No modo avançado, você fornece uma cadeia de conexão.  
  
**Nome do servidor**  
Insira ou selecione o nome ou endereço IP do servidor adaptável. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando uma porta não padrão para conexões com o ASE, insira o número da porta. O número da porta padrão é 5000. Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Insira o nome de usuário que é usado para se conectar ao ASE. Essa é uma opção de modo padrão.  
  
**Senha**  
Digite a senha para o nome de usuário. Essa é uma opção de modo padrão.  
  
**Cadeia de conexão**  
Insira a cadeia de conexão completa para a conexão com o ASE.  
  
Cadeias de conexão consistem em pares de nome e valor de parâmetro. Os nomes dos parâmetros variam de acordo com o provedor que está sendo usado.  
  
**Os parâmetros de conexão para vários provedores são os seguintes:**  
  
1.  Parâmetros de conexão para o **provedor de OLE DB**  
  
    |Configuração|Parâmetro Sybase 12,5|Parâmetro Sybase 15|  
    |-----------|-------------------------|-----------------------|  
    |Nome do servidor|Nome do servidor|Server (Servidor)|  
    |Porta|Endereço de porta do servidor|Porta|  
    |Nome de usuário|Id de Usuário|Id de Usuário|  
    |Senha|Senha|Senha|  
    |Provedor|Provedor|Provedor|  
  
    Para Sybase ASE 12,5, um exemplo de cadeia de conexão é o seguinte:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Para Sybase ASE 15, um exemplo de cadeia de conexão é o seguinte:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Parâmetros de conexão para o **provedor ODBC**  
  
    |Configuração|Parâmetro Sybase 12.5/15|  
    |-----------|-----------------------------|  
    |Nome do driver|Driver|  
    |Nome do servidor|Server (Servidor)|  
    |Nome do Usuário|UID|  
    |Senha|Pwd|  
    |Número da porta|Porta|  
  
    Para Sybase ASE 12,5 ou 15, um exemplo de cadeia de conexão é o seguinte:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Parâmetros de conexão para o **provedor ADO.net**  
  
    |Configuração|Parâmetro Sybase 12.5/15|  
    |-----------|-----------------------------|  
    |Nome do servidor|Server (Servidor)|  
    |Nome do Usuário|UID|  
    |Senha|Pwd|  
    |Número da porta|Porta|  
  
    Um exemplo da cadeia de conexão para o provedor ADO.NET é o seguinte:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Para obter mais informações, consulte a documentação do ASE.  
  
Essa é uma opção de modo avançado.  
  
