---
title: 'Lição 1: preparando-se para criar o pacote de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 11c76b725c8b4a076c49cf8e0742ca95475322fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092201"
---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>Lição 1: Preparando-se para criar o pacote de implantação
  Nesta lição, você criará as pastas de trabalho e as variáveis de ambiente que oferecem suporte ao tutorial, criará um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , adicionará vários pacotes e seus arquivos de suporte ao projeto e implementará configurações em pacotes.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implanta pacotes em uma base de projeto; portanto, como a primeira etapa na criação do pacote de implantação, você deve coletar todos os pacotes e dependências de pacotes em um único projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Normalmente é útil incluir outras informações com os pacotes implantados: por exemplo, você também adicionará ao projeto um arquivo Leiame, que fornece a documentação básica para esse grupo de pacotes.  
  
 Depois que você adicionar os pacotes e os arquivos, adicionará configurações aos pacotes que ainda não usam as configurações. As configurações atualizam as propriedades dos pacotes e os objetos do pacote em tempo de execução. Em uma lição posterior, você modificará os valores dessas configurações durante a implantação de pacotes para oferecer suporte aos pacotes no ambiente implantado.  
  
 Depois que você adicionar as configurações, deverá abrir os pacotes no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , a ferramenta gráfica do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para compilação de pacotes ETL, e examinar as propriedades e os elementos do pacote, assim como as configurações de pacote, para entender melhor os problemas que a implantação precisa resolver. Por exemplo, um dos pacotes extrai dados de arquivos de texto, portanto, o local dos arquivos de dados deve ser atualizado antes dos pacotes serem implantados com êxito.  
  
 **Tempo estimado para concluir esta lição:** 1 hora  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Criando pastas de trabalho e variáveis de ambiente](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [Etapa 2: Criando o projeto de implantação](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [Etapa 3: Adicionando pacotes e outros arquivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [Etapa 4: Adicionando configurações de pacote](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [Etapa 5: Testando os pacotes atualizados](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Criando pastas de trabalho e variáveis de ambiente](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
![Ícone do Integration Services (pequeno)](media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services** <br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
  
