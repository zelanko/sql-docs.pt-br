---
title: Tela 1 (Driver ODBC para SQL Server) do Assistente de fonte de dados | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: e8c961487aaff7e6aa57ea8add571ccbc2945dee
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797793"
---
# <a name="data-source-wizard-screen-1"></a>Tela 1 do Assistente de Fonte de Dados

Especifique o nome e a descrição da fonte de dados e o nome do servidor que executa o SQL Server ao qual a fonte de dados se conectará. 
    
## <a name="options"></a>Opções

### <a name="name"></a>Nome

O nome da fonte de dados usado por um aplicativo ODBC quando solicita uma conexão com a fonte de dados. Por exemplo, "Pessoal". O nome da fonte de dados é exibido na caixa de diálogo Administrador de Fonte de Dados ODBC.

### <a name="description"></a>Descrição

(Opcional) Uma descrição da fonte de dados. Por exemplo, "data de admissão, histórico de salário e análise atual de todos os funcionários".

### <a name="select-or-enter-a-server-name"></a>Selecione ou digite um nome de servidor

O nome de uma instância do SQL Server em sua rede. Você precisará especificar um servidor na próxima caixa de edição.

Na maioria dos casos, o driver ODBC pode se conectar usando a ordem de protocolos padrão e o nome do servidor fornecido nesta caixa. Use o SQL Server Configuration Manager se você desejar criar um alias para o servidor ou configurar bibliotecas de rede de cliente.

Você poderá digitar "(local)" na caixa de servidor quando estiver usando o mesmo computador como SQL Server. Assim, o usuário pode se conectar à instância local do SQL Server, até mesmo ao executar uma versão do SQL Server que não está em rede. É possível executar várias instâncias do SQL Server no mesmo computador. Para especificar uma instância nomeada do SQL Server, o nome do servidor é especificado como _ServerName_\\_InstanceName_.

Para obter mais informações sobre nomes de servidor para diferentes tipos de rede, confira a documentação de instalação do SQL Server nos Manuais Online do SQL Server.

### <a name="finish"></a>Concluir

Se as informações especificadas nesta tela constituírem todos os dados necessários para conexão com o SQL Server, clique em **Concluir**. Os padrões são usados para todos os atributos especificados em outras telas do assistente.

### <a name="next"></a>Próximo

Para prosseguir para a próxima tela do assistente, clique em **próxima**.

## <a name="next-steps"></a>Próximas etapas

[Tela 2 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-2.md)
