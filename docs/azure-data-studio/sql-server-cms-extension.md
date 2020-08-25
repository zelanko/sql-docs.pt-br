---
title: Extensão de Servidores de Gerenciamento Central do SQL Server
description: Saiba como instalar e usar a extensão dos Servidores de Gerenciamento Central do SQL Server (versão prévia), uma extensão para agrupar servidores e aplicar ações ao grupo.
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/06/2019
ms.openlocfilehash: 3024a9c61fb51063b50f8fde769e7bdbb5608fbf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766045"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>Extensão de Servidores de Gerenciamento Central do SQL Server (versão prévia)

A extensão de Servidores de Gerenciamento Central permite que os usuários armazenam uma lista de instâncias do SQL Server que é organizada em um ou mais grupos. As ações executadas usando um grupo de CMS afetarão todos os servidores do grupo.

Atualmente, essa experiência está na versão prévia inicial. Informe problemas e solicite recursos [aqui](https://github.com/microsoft/azuredatastudio/issues).

![Extensão de CMS](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>Instalar a extensão de Servidores de Gerenciamento Central do SQL Server

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione uma extensão disponível para exibir os detalhes.
1. Selecione a extensão desejada (Servidores de Gerenciamento Central do SQL Server) e **Instale-a**.

### <a name="how-do-i-start-central-management-servers"></a>Como fazer para começar a usar os Servidores de Gerenciamento Central?
 Os Servidores de Gerenciamento Central podem ser exibidos clicando no ícone de Conexões (Ctrl/Cmd + G). Na primeira vez que você baixar a extensão, a exibição do CMS será minimizada e você poderá abri-la clicando em **Servidores de Gerenciamento Central**

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre os Servidores de Gerenciamento Central do ponto de vista conceitual, [leia mais aqui](../ssms/register-servers/create-a-central-management-server-and-server-group.md).