---
title: Tela 1 (Driver ODBC para SQL Server) do Assistente de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dc34a7239f931b09f36365ce2dfb595c0c6e9ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-1"></a>Tela 1 do Assistente de fonte de dados

Especifique o nome e descrição da fonte de dados e o nome do servidor que está executando o SQL Server ao qual se conectar a fonte de dados. 
    
## <a name="options"></a>Opções

### <a name="name"></a>Nome

O nome da fonte de dados usado por um aplicativo ODBC quando solicita uma conexão com a fonte de dados. Por exemplo, "Pessoal". O nome da fonte de dados é exibido na caixa de diálogo Administrador de Fonte de Dados ODBC.

### <a name="description"></a>Description

(Opcional) Uma descrição da fonte de dados. Por exemplo, "data de admissão, histórico de salário e análise atual de todos os funcionários".

### <a name="select-or-enter-a-server-name"></a>Selecione ou digite um nome de servidor

O nome de uma instância do SQL Server em sua rede. Você precisará especificar um servidor na próxima caixa de edição.

Na maioria dos casos, o driver ODBC pode se conectar usando a ordem dos protocolos padrão e o nome do servidor fornecido nesta caixa. Use o SQL Server Configuration Manager se desejar criar um alias para o servidor ou configurar bibliotecas de rede do cliente.

Você pode digitar "(local)" na caixa do servidor quando você estiver usando o mesmo computador que o SQL Server. O usuário, em seguida, pode se conectar à instância local do SQL Server, mesmo se estiver executando uma versão fora da rede do SQL Server. Podem executar várias instâncias do SQL Server no mesmo computador. Para especificar uma instância nomeada do SQL Server, o nome do servidor é especificado como _ServerName_\\_InstanceName_.

Para obter mais informações sobre nomes de servidor para diferentes tipos de redes, consulte a documentação de instalação do SQL Server nos Manuais Online do SQL Server.

### <a name="finish"></a>Concluir

Se as informações especificadas nesta tela são tudo o que é necessário para se conectar ao SQL Server, você pode clicar em **concluir**. Os padrões são usados para todos os atributos especificados em outras telas do assistente.

### <a name="next"></a>Próximo

Para prosseguir para a próxima tela do assistente, clique em **próximo**.

## <a name="next-steps"></a>Próximas etapas

[Tela 2 do Assistente de fonte de dados](../../../connect/odbc/windows/dsn-wizard-2.md)
