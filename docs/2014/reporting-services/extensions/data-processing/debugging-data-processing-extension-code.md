---
title: Depurando o código de extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: 40
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 81bcc56583555627cac43ce350723109ac6f768d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118247"
---
# <a name="debugging-data-processing-extension-code"></a>Depurando o código de extensão de processamento de dados
  O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornece várias ferramentas de depuração que podem ajudar você a analisar o código de extensão de processamento de dados e localizar erros nele. A ferramenta mais adequada dependerá do que você está tentando realizar. Este exemplo usa o [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>Para depurar seu código de extensão de processamento de dados  
  
1.  Inicie o [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] e abra seu projeto de extensão de processamento de dados.  
  
2.  Crie o projeto e implante seu assembly de extensão de processamento de dados e o arquivo .pdb anexo ao Designer de Relatórios. Para obter mais informações sobre a implantação, consulte [Como implantar uma extensão de processamento de dados no Designer de Relatórios](deploying-a-data-processing-extension-to-report-designer.md).  
  
3.  Abra um novo Projeto de Relatório no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] enquanto deixa seu código de extensão de processamento de dados aberto em uma janela separada do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
4.  Navegue até a janela do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] que contém seu projeto de extensão de processamento de dados e defina alguns pontos de quebra em seu código.  
  
5.  Com a janela do projeto de extensão de processamento de dados ainda ativa, clique em **Anexar ao Processo** no menu **Depurar**.  
  
     A caixa de diálogo **Anexar ao Processo** será aberta.  
  
6.  Na lista de processos, selecione o processo devenv.exe que corresponde ao Projeto de Relatório e clique em **Anexar**.  
  
7.  Defina a fonte de dados do relatório usando a guia **Dados do Relatório** do Projeto de Relatório. Você provavelmente usará o Designer de Consulta genérico para executar uma consulta na fonte de dados personalizada. Isso deve chamar o depurador e executar o código correspondente a seus pontos de quebra.  
  
8.  Percorra seu código usando a tecla F11. Para obter mais informações sobre como usar o [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] para depuração, consulte a documentação do [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Implantando uma extensão de processamento de dados](deploying-a-data-processing-extension.md)   
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  