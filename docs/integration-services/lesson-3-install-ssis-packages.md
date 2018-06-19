---
title: 'Lição 3: instalar os pacotes SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f87066ce8b1f3bf28c904b3b8e225933d318fab
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403838"
---
# <a name="lesson-3-install-ssis-packages"></a>Lição 3: Instalar os pacotes SSIS
Na [Lição 2: Criar o pacote de implantação no SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md), você compilou um utilitário de implantação e criou o pacote de implantação que contém os itens para os quais é necessário instalar pacotes em outro computador. Você também verificou a lista de arquivos no pacote de implantação e examinou o conteúdo do arquivo de manifesto criado quando você compilou o utilitário de implantação.  
  
Nesta lição, você copiará o pacote de implantação para o computador de destino e executará o Assistente de Instalação de Pacotes para instalar os pacotes, as dependências dos pacotes e os arquivos auxiliares no computador. Os pacotes serão instalados no banco de dados **msdb**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os outros itens serão instalados no sistema de arquivos. Depois de concluir a instalação de pacote, você testará a implantação executando os pacotes do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usando o Execute o Utilitário de Pacotes.  
  
**Tempo estimado para concluir esta lição:** 30 minutos  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote de implantação](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [Etapa 2: Executando o Assistente de Instalação de Pacotes](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [Etapa 3: Testando os pacotes implantados](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiando o pacote de implantação](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
  
  
