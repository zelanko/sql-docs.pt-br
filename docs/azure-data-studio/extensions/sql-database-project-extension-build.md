---
title: Compilar e publicar um projeto
description: Compilar e publicar com a extensão de Projetos de Banco de Dados do SQL Server
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/25/2020
ms.openlocfilehash: 4320873affdab74a31d1e666a84bc744b1c00385
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123006"
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
