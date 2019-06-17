---
title: Conectar a uma fonte de dados (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndatasource.f1
ms.assetid: 1e2b17e9-092b-4af1-8a58-c52b8fe10ff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c1114dd63b9082c6be7486ab5e576a6b8270485
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087337"
---
# <a name="connect-to-a-data-source-ssas"></a>Conectar com uma fonte de dados (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a criar uma nova conexão com várias fontes de dados, como bancos de dados relacionais, feeds de dados e arquivos. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador. Você também deve ter o provedor apropriado instalado no servidor de banco de dados de workspace. Para servidores de 32 bits (x86), provedores de 32 bits devem ser instalados. Para servidores de 64 bits (x64), provedores de 64 bits devem ser instalados.  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] é sempre executado em um processo de 32 bits, independentemente da arquitetura. Ao executar [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] em um computador de 64 bits, você deve estar consciente do seguinte ao instalar provedores de dados:  
  
-   Para provedores que dão suporte à instalação lado a lado de provedores de 32 bits e de 64 bits, você deve instalar ambos os provedores.  
  
-   Para o provedor ACE, você deve instalar a versão de 64 bits do provedor. Como o Office instala o provedor de ACE automaticamente, você não deve executar uma versão de 32 bits do Microsoft Office em um computador de 64 bits que hospeda o servidor de banco de dados de workspace.  
  
     O provedor ACE é usado para importar de arquivos de Texto, do Excel e do Access. Se o suporte a essas fontes de dados não for necessário, você poderá executar uma versão de 32 bits do Microsoft Office em um computador que executa um servidor de banco de dados de workspace de 64 bits.  
  
-   Para outros provedores que não dão suporte à instalação lado a lado de provedores de 32 bits e de 64 bits, instale o provedor de 32 bits. Se apenas computadores de 64 bits estiverem disponíveis, use um computador remoto com um provedor de 64 bits instalado como o servidor de banco de dados de workspace.  
  
  
