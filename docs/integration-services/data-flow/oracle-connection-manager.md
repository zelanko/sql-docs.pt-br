---
description: Gerenciador de Conexões do Oracle
title: Gerenciador de Conexões do Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428ca450371e452081d548a64e26dba2bd29b3b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430738"
---
# <a name="oracle-connection-manager"></a>Gerenciador de Conexões do Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Um Gerenciador de Conexões do Oracle é usado para habilitar um pacote para extrair dados de Oracle Databases e carregar dados em Oracle Databases.

A propriedade **ConnectionManagerType** do Gerenciador de Conexões do Oracle está definida como **ORACLE**.

## <a name="configuring-the-oracle-connection-manager"></a>Configurando o Gerenciador de Conexões do Oracle

As alterações de configuração do Gerenciador de Conexões do Oracle serão resolvidas por Integration Services no runtime. Use a caixa de diálogo **Editor do Gerenciador de Conexões do Oracle** para adicionar uma conexão com uma fonte de dados do Oracle.

![Gerenciador de Conexões](media/oracle-connection-manager.png)

### <a name="options"></a>Opções

#### <a name="connection-manager-information"></a>Informações do gerenciador de conexões

Insira as informações sobre a conexão do Oracle.

**Nome**

Insira um nome para a conexão do Oracle. O nome padrão é Gerenciador de Conexões do Oracle. 

**Descrição** 

Insira uma descrição da conexão. Esta entrada é opcional.

**Nome do serviço TNS**

Insira o nome do banco de dados do Oracle com o qual você deseja trabalhar. O nome do serviço TNS poderia ser:

- o nome do descritor da conexão definido no arquivo tnsnames.ora localizado na pasta do administrador do cliente Oracle.

- Formato EzConnect: [//]host[:port][/service_name]

Para obter mais informações, consulte a documentação Oracle.

#### <a name="connection-manager-logging"></a>Registro em log do Gerenciador de Conexões

Selecione uma das opções a seguir:

- **Usar a autenticação do Windows**: selecione esta opção para usar autenticação do Windows.

- **Usar a autenticação do Oracle**: selecione esta opção para usar a autenticação do banco de dados do Oracle. Se você usar esta autenticação, insira suas credenciais do Oracle da seguinte forma:  
    **Nome de Usuário**: digite o nome de usuário usado para se conectar ao banco de dados do Oracle.  
    **Senha**: digite a senha do banco de dados Oracle para o usuário inserido no campo nome do usuário.

> [!NOTE]
>
>A Autenticação do Windows não é compatível com o Oracle Server 18c.

**Testar Conexão**

Clique em **Testar Conexão** para verificar se as informações fornecidas estão corretas. Você receberá a mensagem **Teste de conexão bem-sucedido**, se as informações inseridas puderem ser conectadas ao banco de dados do Oracle.

### <a name="custom-properties"></a>Propriedades personalizadas

Há as seguintes propriedades personalizadas do gerenciador de conexões no gerenciador de conexões do Oracle:

- **EnableDetailedTracing**: não usado.

- **OracleHome**: especifique o nome ou pasta de 32-bit do Oracle Home a ser usado pelo conector. (Opcional)

- **OracleHome64**: especifique o nome ou pasta do Oracle Home de 64 bits a ser usado pelo conector durante a execução no modo 64 bits. (Opcional)

As propriedades personalizadas não são listadas no Editor do Gerenciador de Conexões do Oracle. Para definir as propriedades **OracleHome** e **OracleHome64**:

1. Da área do Gerenciador de Conexões, clique com o botão direito do mouse no gerenciador de conexões do Oracle com o qual você está trabalhando e selecione **Propriedades**.

2. No painel **Propriedades**, defina a propriedade **OracleHome** ou **OracleHome64** com o caminho completo para o diretório base do Oracle.

## <a name="next-steps"></a>Próximas etapas

- Configurar a [Origem do Oracle](oracle-source.md).
- Configurar o [Destino Oracle](oracle-destination.md).
- Caso tenha dúvidas, visite a [TechCommunity](https://aka.ms/AA5u35j).
