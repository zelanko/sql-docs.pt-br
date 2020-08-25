---
title: Compilar e publicar um projeto
description: Compilar e publicar com a extensão de Projetos de Banco de Dados do SQL Server
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 191b10fd32d7c49c3f4a4e81c109e52fb2a1a81c
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88171365"
---
# <a name="build-and-publish-a-project"></a>Compilar e publicar um projeto

O processo de compilação na extensão de Projetos de Banco de Dados SQL para Azure Data Studio permite a criação de *dacpac* em ambientes Windows, macOS e Linux. O projeto pode ser implantado em um ambiente local ou de nuvem com o processo de publicação.

## <a name="prerequisites"></a>Pré-requisitos
- Instale e configure a [extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension.md).


## <a name="build-a-database-project"></a>Compilar um Projeto de Banco de Dados

 Na viewlet **Projetos**, em **Explorer**, clique com o botão direito do mouse no nó raiz *.sqlproj* e selecione **Compilar**.

 O painel de saída será exibido automaticamente com a saída do processo de compilação.  Uma compilação bem-sucedida será concluída com a mensagem: 

 ``` ... exited with code: 0 ```

## <a name="publish-a-database-project"></a>Publicar um Projeto de Banco de Dados

Depois que um projeto é compilado com sucesso por meio do processo de compilação, o banco de dados pode ser publicado em uma instância do SQL Server. Para publicar um projeto de banco de dados, na viewlet **Projetos**, em **Explorer**, clique com o botão direito do mouse no nó raiz *.sqlproj* e selecione **Publicar**.

Na caixa de diálogo **Publicar banco de dados** exibida, especifique uma conexão com o servidor e o nome do banco de dados a ser criado.

## <a name="next-steps"></a>Próximas etapas

- [Extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension.md)
- [Compilar projetos de banco de dados SQL por meio da linha de comando](sql-database-project-extension-build-from-command-line.md)
