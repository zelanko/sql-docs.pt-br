---
title: Extensão de Servidores de Gerenciamento Central do SQL Server
description: Saiba como instalar e usar a extensão de Servidores de Gerenciamento Central do SQL Server. Uma extensão para agrupar servidores e aplicar ações ao grupo.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/06/2019
ms.openlocfilehash: ca200de903675da9fdfbd2549d3ee1b5bd192907
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91122981"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>Extensão de Servidores de Gerenciamento Central do SQL Server (versão prévia)

A extensão de Servidores de Gerenciamento Central permite que os usuários armazenam uma lista de instâncias do SQL Server que é organizada em um ou mais grupos. As ações executadas usando um grupo de CMS afetarão todos os servidores do grupo.

Atualmente, essa experiência está na versão prévia inicial. Informe problemas e solicite recursos [aqui](https://github.com/microsoft/azuredatastudio/issues).

![Extensão de CMS](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>Instalar a extensão de Servidores de Gerenciamento Central do SQL Server

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione uma extensão disponível para exibir os detalhes.
3. Selecione a extensão desejada (Servidores de Gerenciamento Central do SQL Server) e **Instale-a**.

### <a name="how-do-i-start-central-management-servers"></a>Como fazer para começar a usar os Servidores de Gerenciamento Central?

 Os Servidores de Gerenciamento Central podem ser exibidos clicando no ícone de Conexões (Ctrl/Cmd + G). Na primeira vez que você baixar a extensão, a exibição do CMS será minimizada e você poderá abri-la clicando em **Servidores de Gerenciamento Central**

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os Servidores de Gerenciamento Central do ponto de vista conceitual, [leia mais aqui](../../ssms/register-servers/create-a-central-management-server-and-server-group.md).