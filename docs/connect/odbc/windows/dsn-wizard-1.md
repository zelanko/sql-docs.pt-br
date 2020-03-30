---
title: Tela 1 do Assistente de Fonte de Dados (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6edf465f5b853008c9bdc8c420f6e862e360593
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67936601"
---
# <a name="data-source-wizard-screen-1"></a>Tela 1 do Assistente de Fonte de Dados

Especifique o nome e a descrição da fonte de dados e o nome do servidor que executa o SQL Server ao qual a fonte de dados se conectará. 
    
## <a name="options"></a>Opções

### <a name="name"></a>Nome

O nome da fonte de dados usado por um aplicativo ODBC quando solicita uma conexão com a fonte de dados. Por exemplo, "Pessoal". O nome da fonte de dados é exibido na caixa de diálogo Administrador de Fonte de Dados ODBC.

### <a name="description"></a>DESCRIÇÃO

(Opcional) Uma descrição da fonte de dados. Por exemplo, "data de admissão, histórico de salário e análise atual de todos os funcionários".

### <a name="select-or-enter-a-server-name"></a>Selecione ou digite um nome de servidor

O nome de uma instância do SQL Server na sua rede. Você precisará especificar um servidor na próxima caixa de edição.

Na maioria dos casos, o driver ODBC pode se conectar usando a ordem de protocolos padrão e o nome do servidor fornecido nesta caixa. Use o SQL Server Configuration Manager se você desejar criar um alias para o servidor ou configurar bibliotecas de rede de cliente.

Você poderá digitar "(local)" na caixa de servidor quando estiver usando o mesmo computador como SQL Server. Assim, o usuário pode se conectar à instância local do SQL Server, até mesmo ao executar uma versão do SQL Server que não está em rede. É possível executar várias instâncias do SQL Server no mesmo computador. Para especificar uma instância nomeada do SQL Server, o nome do servidor é especificado como _ServerName_\\_InstanceName_.

Para obter mais informações sobre nomes de servidor para diferentes tipos de rede, confira a documentação de instalação do SQL Server nos Manuais Online do SQL Server.

### <a name="finish"></a>Concluir

Se as informações especificadas nesta tela constituírem todos os dados necessários para conexão com o SQL Server, clique em **Concluir**. Os padrões são usados para todos os atributos especificados em outras telas do assistente.

### <a name="next"></a>Próximo

Para passar para a próxima tela do assistente, clique em **Próximo**.

## <a name="next-steps"></a>Próximas etapas

[Tela 2 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-2.md)
