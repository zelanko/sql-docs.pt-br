---
title: Conectar a uma fonte de dados (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.conndatasource.f1
ms.assetid: 1e2b17e9-092b-4af1-8a58-c52b8fe10ff1
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f33af08d91f2c8e739c9295daed0ae47563ede51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012396"
---
# <a name="connect-to-a-data-source-ssas"></a>Conectar com uma fonte de dados (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a criar uma nova conexão com várias fontes de dados, como bancos de dados relacionais, feeds de dados e arquivos. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 Para conectar uma fonte de dados, você deve ter o provedor apropriado instalado no computador. Você também deve ter o provedor apropriado instalado no servidor de banco de dados de espaço de trabalho. Para servidores de 32 bits (x86), provedores de 32 bits devem ser instalados. Para servidores de 64 bits (x64), provedores de 64 bits devem ser instalados.  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] sempre é executado em um processo de 32 bits, independentemente da arquitetura. Ao executar [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] em um computador de 64 bits, você deve estar consciente do seguinte ao instalar provedores de dados:  
  
-   Para provedores que dão suporte à instalação lado a lado de provedores de 32 bits e de 64 bits, você deve instalar ambos os provedores.  
  
-   Para o provedor ACE, você deve instalar a versão de 64 bits do provedor. Como o Office instala o provedor de ACE automaticamente, você não deve executar uma versão de 32 bits do Microsoft Office em um computador de 64 bits que hospeda o servidor de banco de dados de espaço de trabalho.  
  
     O provedor ACE é usado para importar de arquivos de Texto, do Excel e do Access. Se o suporte a essas fontes de dados não for necessário, você poderá executar uma versão de 32 bits do Microsoft Office em um computador que executa um servidor de banco de dados de espaço de trabalho de 64 bits.  
  
-   Para outros provedores que não dão suporte à instalação lado a lado de provedores de 32 bits e de 64 bits, instale o provedor de 32 bits. Se apenas computadores de 64 bits estiverem disponíveis, use um computador remoto com um provedor de 64 bits instalado como o servidor de banco de dados de espaço de trabalho.  
  
  