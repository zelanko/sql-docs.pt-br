---
title: 'Lição 3: Instalando pacotes | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
caps.latest.revision: 14
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2251360bfc69fd4e1846ace6a072ff537c6248e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287568"
---
# <a name="lesson-3-installing-packages"></a>Lição 3: Instalando pacotes
  Na [lição 2: Criando o pacote de implantação](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md), você compilou um utilitário de implantação e criou o pacote de implantação que contém os itens que você deve instalar pacotes em outro computador. Você também verificou a lista de arquivos no pacote de implantação e examinou o conteúdo do arquivo de manifesto criado quando você compilou o utilitário de implantação.  
  
 Nesta lição, você copiará o pacote de implantação para o computador de destino e executará o Assistente de Instalação de Pacotes para instalar os pacotes, as dependências dos pacotes e os arquivos auxiliares no computador. Os pacotes serão instalados no banco de dados **msdb**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os outros itens serão instalados no sistema de arquivos. Depois de concluir a instalação de pacote, você testará a implantação executando os pacotes do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usando o Execute o Utilitário de Pacotes.  
  
 **Tempo estimado para concluir esta lição:** 30 minutos  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote de implantação](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [Etapa 2: Executando o Assistente de Instalação de Pacotes](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [Etapa 3: Testando os pacotes implantados](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Copiando o pacote de implantação](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
![Ícone do Integration Services (pequeno)](media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services  **<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
