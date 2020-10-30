---
description: MSSQLSERVER_17112
title: MSSQLSERVER_17112
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17112 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 870f9b9f4d3fcc8186ed1d16faee861ed63e4135
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418653"
---
# <a name="mssqlserver_17112"></a>MSSQLSERVER_17112
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|17112|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|INIT_INVCOMMAND|
|Texto da mensagem|Foi fornecida uma opção de inicialização inválida por meio do Registro ou do prompt de comando. Corrija ou remova a opção.|
||

## <a name="explanation"></a>Explicação

Esse erro indica que uma [Opção de Inicialização do Serviço de Mecanismo de Banco de Dados](/sql/database-engine/configure-windows/database-engine-service-startup-options) inválida foi especificada. Quando uma opção de inicialização não é especificada corretamente, o SQL Server não consegue ser inicializado ou pode não ser executado conforme o esperado. O erro 17112 também é gerado.

Em alguns casos, a instância pode ser iniciada, mas ao examinar o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os parâmetros de inicialização não têm a aparência correta:

> \<Datetime> Parâmetros de inicialização do Registro do Servidor:  
\<Datetime> Servidor -d D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\DATA\master.mdf  
\<Datetime> Servidor -e D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\LOG\ERRORLOG  
\<Datetime> Servidor -l D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\DATA\mastlog.ldf  
\<Datetime> Servidor -T1118 -g512

Observe como os dois últimos parâmetros de inicialização estão na mesma linha.

Você também pode observar que, em alguns casos, a adição dos parâmetros de inicialização necessários não teve o efeito pretendido sobre o comportamento do servidor.

## <a name="possible-causes"></a>Possíveis causas

Você receberá esses problemas devido aos seguintes motivos:

- Usar parâmetros de inicialização que não estão presentes na lista válida de parâmetros de inicialização
- Especificar parâmetros de inicialização sem os delimitadores apropriados [;]
- Copiar e colar os parâmetros de inicialização de editores de texto que introduziram alguns caracteres especiais invisíveis, [por exemplo, um espaço antes do -T]
- Não usar a diferenciação de maiúsculas e minúsculas correta para o parâmetro de inicialização

## <a name="user-action"></a>Ação do usuário

Use a ferramenta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para fornecer e validar os parâmetros de inicialização especificados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verifique se cada um dos parâmetros de inicialização está delimitado corretamente e se nenhum caractere especial está presente.

## <a name="more-information"></a>Mais informações

Veja os seguintes tópicos para obter mais informações sobre este tópico:

- [Opções de inicialização do serviço Mecanismo de Banco de Dados](/sql/database-engine/configure-windows/database-engine-service-startup-options)
- [Serviços SCM – configurar opções de inicialização do servidor](/sql/database-engine/configure-windows/scm-services-configure-server-startup-options)
