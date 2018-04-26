---
title: Conecte-se para Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8aad8b895c7a66dd31f537f6129598b05a8933a4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-sybase-sybasetosql"></a>Conecte-se para Sybase (SybaseToSQL)
Use o **conectar-se ao Sybase** caixa de diálogo para se conectar à instância do Sybase Adaptive Server Enterprise (ASE) que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar-se ao Sybase**. Se você se conectou anteriormente, o comando é **reconectar para Sybase**.  
  
## <a name="options"></a>Opções  
**Provedor**  
Selecione qualquer uma do provedor instalado no computador para se conectar ao servidor Sybase.  
  
**Modo**  
Selecione qualquer um dos modos de conexão padrão ou avançado. No modo padrão, digite ou selecione os valores para o nome do servidor, porta, nome de usuário e senha. No modo avançado, você deve fornecer uma cadeia de caracteres de conexão.  
  
**Nome do servidor**  
Insira ou selecione o nome ou endereço IP do servidor adaptável. O nome do servidor padrão é o mesmo que o nome do computador. Essa é uma opção de modo padrão.  
  
**Porta do servidor**  
Se você estiver usando uma porta não padrão para conexões com ASE, insira o número da porta. O número da porta padrão é 5000. Essa é uma opção de modo padrão.  
  
**Nome de usuário**  
Digite o nome de usuário que é usado para se conectar ao ASE. Essa é uma opção de modo padrão.  
  
**Senha**  
Digite a senha para o nome de usuário. Essa é uma opção de modo padrão.  
  
**Cadeia de conexão**  
Insira a cadeia de conexão completa para a conexão para ASE.  
  
Cadeias de caracteres de Conexão consistem de pares de nome e valor de parâmetro. Os nomes dos parâmetros variam de acordo com o provedor que está sendo usado.  
  
**Parâmetros de Conexão para vários provedores são da seguinte maneira:**  
  
1.  Parâmetros de Conexão para **provedor OLE DB**  
  
    |Configuração|Parâmetro Sybase 12,5|Parâmetro Sybase 15|  
    |-----------|-------------------------|-----------------------|  
    |Nome do servidor|Nome do servidor|Servidor|  
    |Porta|Endereço de porta do servidor|Porta|  
    |Nome de usuário|ID de usuário|ID de usuário|  
    |Senha|Senha|Senha|  
    |Provedor|Provedor|Provedor|  
  
    Para Sybase ASE 12,5, uma cadeia de caracteres de conexão de exemplo é o seguinte:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Para Sybase ASE 15, uma cadeia de caracteres de conexão de exemplo é o seguinte:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Parâmetros de Conexão para **provedor ODBC**  
  
    |Configuração|Parâmetro Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nome do driver|Driver|  
    |Nome do servidor|Servidor|  
    |Nome do Usuário|UID|  
    |Senha|Pwd|  
    |Número da Porta|Porta|  
  
    Para Sybase ASE 12,5 ou 15, uma cadeia de caracteres de conexão de exemplo é o seguinte:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Parâmetros de Conexão para **provedor ADO.NET**  
  
    |Configuração|Parâmetro Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nome do servidor|Servidor|  
    |Nome do Usuário|UID|  
    |Senha|Pwd|  
    |Número da Porta|Porta|  
  
    Um exemplo da cadeia de caracteres de Conexão para o provedor ADO.NET é como segue:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Para obter mais informações, consulte a documentação do ASE.  
  
Essa é uma opção de modo avançado.  
  
