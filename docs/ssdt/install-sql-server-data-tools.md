---
title: Instalar o SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.package.stub
ms.assetid: 6f8616cb-9119-42c3-a9b1-936e088763e7
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2df3214ce5ae02e4feb076f77e66b153c4d2abdb
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088018"
---
# <a name="install-sql-server-data-tools"></a>Instalar o SQL Server Data Tools
Este tópico descreve como instalar o SQL Server Data Tools. Atualizações do SQL Server Data Tools estão disponíveis na página de download do SQL Server Data Tools ([Instalar o SQL Server Data Tools mais recente](http://go.microsoft.com/fwlink/?LinkID=616714)).  
  
Se você estiver usando o Visual Studio 2012 ou o Visual Studio 2013, instale as últimas atualizações do SQL Server Data Tools para obter os recursos mais recentes.  
  
## <a name="sql-server-data-tools-for-visual-studio-2013"></a>SQL Server Data Tools para Visual Studio 2013  
O SQL Server Data Tools é fornecido no Visual Studio 2013 Express para Web, Visual Studio 2013 Express para Desktop, Visual Studio Community 2013 e todos os SKUs pagos, incluindo o Professional SKU e mais recentes. Depois de instalar o Visual Studio 2013, vá para Ferramentas -> Extensões e atualizações -> Atualizações para saber se há uma atualização para ser instalada.  
  
## <a name="sql-server-data-tools-for-visual-studio-2012"></a>SQL Server Data Tools para Visual Studio 2012  
O SQL Server Data Tools é fornecido no SKU Professional, ou posterior, no Visual Studio 2012. Após a instalação do Visual Studio 2012 e da atualização do SQL Server Data Tools de novembro de 2012, ou posterior, o SQL Server Data Tools poderá informar quando houver uma atualização para instalação. Para saber mais, confira [Caixa de diálogo Verificar Atualizações](../ssdt/check-for-updates-dialog-box.md).  
  
Se o Visual Studio 2012 não estiver instalado, o SQL Server Data Tools instalará o Visual Studio 2012 Integrated Shell e instalará o SQL Server Data Tools.  
  
## <a name="administrative-installation-point"></a>Ponto de instalação administrativa  
Se for necessário instalar o SQL Server Data Tools em vários computadores ou em computadores sem acesso à Internet, crie um layout de instalação administrativa em um compartilhamento de rede ou um meio físico e faça a instalação a partir desse ponto de instalação.  
  
Para criar um layout de instalação, baixe SSDTSetup.EXE e execute-o com a opção `/layout`*local* para criar um layout no *local*. Em seguida, os usuários podem executar o SSDTSetup.Exe no *local*.  
  
Baixe o SSDTSetup.exe acessando [Instalar o SQL Server Data Tools mais recente](http://go.microsoft.com/fwlink/?LinkID=616714), clique no link da sua versão do Visual Studio e baixe o SSDTSetup.exe referente ao seu idioma.  
  
