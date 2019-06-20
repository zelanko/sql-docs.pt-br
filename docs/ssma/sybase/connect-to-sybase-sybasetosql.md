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
manager: craigg
ms.openlocfilehash: 0805246d5b88138cfa97019d1e0cd524c82456c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63060999"
---
# <a name="connect-to-sybase-sybasetosql"></a>Conectar-se ao Sybase (SybaseToSQL)
Use o **conectar-se ao Sybase** caixa de diálogo para se conectar à instância do Sybase Adaptive Server Enterprise (ASE) que você deseja migrar.  
  
Para acessar essa caixa de diálogo sobre o **arquivo** menu, selecione **conectar-se ao Sybase**. Se você tiver se conectado anteriormente, o comando é **reconectar-se ao Sybase**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione qualquer uma do provedor instalado no computador para conexão com o servidor do Sybase.  
  
**Modo**  
Selecione qualquer um dos modos de conexão padrão ou avançado. No modo padrão, insira ou selecione valores para o nome do servidor, porta, nome de usuário e senha. No modo avançado, você deve fornecer uma cadeia de caracteres de conexão.  
  
**Nome do servidor**  
Insira ou selecione o nome ou endereço IP do servidor adaptável. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando uma porta não padrão para conexões com o ASE, insira o número da porta. O número da porta padrão é 5000. Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Insira o nome de usuário que é usado para se conectar ao ASE. Essa é uma opção de modo padrão.  
  
**Senha**  
Digite a senha para o nome de usuário. Essa é uma opção de modo padrão.  
  
**Cadeia de conexão**  
Insira a cadeia de conexão completa para a conexão para o ASE.  
  
Cadeias de caracteres de Conexão consistem em pares de nome e valor do parâmetro. Os nomes dos parâmetros variam de acordo com o provedor que está sendo usado.  
  
**Parâmetros de Conexão para vários provedores são da seguinte maneira:**  
  
1.  Parâmetros de Conexão para **provedor OLE DB**  
  
    |Configuração|Parâmetro Sybase 12,5|Parâmetro Sybase 15|  
    |-----------|-------------------------|-----------------------|  
    |Nome do servidor|Nome do servidor|Servidor|  
    |Port|Endereço da porta do servidor|Port|  
    |Nome de usuário|ID de usuário|ID de usuário|  
    |Senha|Senha|Senha|  
    |Provedor|Provedor|Provedor|  
  
    Para Sybase ASE 12.5, uma cadeia de caracteres de conexão de exemplo é o seguinte:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Para 15 de ASE do Sybase, um exemplo de cadeia de conexão é da seguinte maneira:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Parâmetros de Conexão para **provedor ODBC**  
  
    |Configuração|Parâmetro Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nome do driver|Driver|  
    |Nome do servidor|Servidor|  
    |Nome do Usuário|UID|  
    |Senha|pwd|  
    |Número da Porta|Port|  
  
    Para Sybase ASE 12,5 ou 15, um exemplo de cadeia de conexão é da seguinte maneira:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Parâmetros de Conexão para **provedor ADO.NET**  
  
    |Configuração|Parâmetro Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nome do servidor|Servidor|  
    |Nome do Usuário|UID|  
    |Senha|pwd|  
    |Número da Porta|Port|  
  
    Um exemplo da cadeia de Conexão de provedor do ADO.NET é como segue:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Para obter mais informações, consulte a documentação do ASE.  
  
Essa é uma opção de modo avançado.  
  
