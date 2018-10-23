---
title: Arquivos diversos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ecabdec464cb72cf5024feab83e547c95cafd9d6
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119793"
---
# <a name="miscellaneous-files"></a>arquivos diversos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Arquivos externos a qualquer projeto são chamados de *arquivos diversos*. Quando você tiver uma solução aberta, poderá abrir e modificar arquivos diversos relacionados ao projeto. Um arquivo é classificado como um arquivo diverso se a extensão do arquivo não for associada com o editor de códigos de projeto. Por exemplo, em um projeto de script do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , arquivos com a extensão .txt ou .mdx serão tratados como arquivos diversos. Em um projeto MDX, arquivos com a extensão .txt ou .sql serão tratados como arquivos diversos. Para associar uma extensão de arquivo a um editor de códigos, consulte [Como associar extensões de arquivo a um Editor de Códigos](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md).  
  
Poder adicionar arquivos diversos a seu projeto é útil por vários motivos. Você poderia ter um arquivo que necessariamente não fosse um script reconhecido, mas parte do desenvolvimento da solução. Exemplos comuns incluem notas ou instruções de desenvolvimento, arquivos de dados e trechos de código.  
  
Os arquivos diversos fornecem flexibilidade. Por exemplo, suponha que você tenha um projeto de script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com vários scripts para criação de tabelas e procedimentos armazenados em seu banco de dados. Você também tem vários arquivos de dados para as tabelas com extensão de arquivo .BCP e instruções de execução em um arquivo README.TXT. Você pode anexar os arquivos de dados e o README como arquivos diversos ao projeto e se beneficiar do controle de código-fonte e outros recursos do sistema de projeto.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Os menus e barras de ferramentas mudam de acordo com o formato do arquivo que você abre. Por exemplo, quando você abre um arquivo de texto, a barra de ferramentas do Editor de Texto é exibida. Se você abrir um arquivo de Esquema XML, a barra de ferramentas de Esquema XML será exibida. Enquanto editar seu Esquema XML, a barra de ferramentas do Editor de Texto estará indisponível. Quando você alterna entre um arquivo de projeto e um arquivo diverso, todos os comandos relacionados ao projeto e barras de ferramentas são substituídos por aqueles pertinentes ao arquivo diverso.  
  
## <a name="see-also"></a>Consulte Também  
[Arquivos que gerenciam soluções e projetos](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[Soluções &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Projetos &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
  
